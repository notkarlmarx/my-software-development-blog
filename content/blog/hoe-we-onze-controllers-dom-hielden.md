---
title: "Hoe we onze Controllers dom hielden"
author: "Karl van Heijster"
date: 2024-02-02T11:14:31+01:00
draft: true
comments: true
tags: ["exceptions", "refactoren", "software ontwikkelen", "web API's"]
summary: "Het is zaak je Controller-methods zo compact, zo \"dom\" mogelijk te houden. Valerio De Sanctis' *Building Web APIs with ASP.NET Core* deed me denken aan de verschillende manieren waarop mijn team dat de afgelopen jaren voor elkaar heeft proberen te krijgen. Want het dom houden van je Controllers -- zonder aan expressiviteit in te boeten -- is geen triviale zaak. Vandaag: hoe het niet moet."
---

Niet lang geleden las ik [*Building Web APIs with ASP.NET Core*](https://www.manning.com/books/building-web-apis-with-asp-net-core) van [Valerio De Sanctis](https://mvp.microsoft.com/en-US/mvp/profile/f42bd1d8-aa90-e811-813c-3863bb2bca60) (en schreef er een recensie over, [hier] (BLOG)). Een kritiekpunt die ik op De Sanctis' codevoorbeelden had, was dat hij teveel logica in zijn Controller methods stopte. Nu is dat in de context van een tutorial niet zo problematisch, maar het loont zich -- buiten die context dus -- denk ik wel om wat langer bij dit punt stil te staan.


Het is zaak je Controller-methods zo compact, zo "dom" mogelijk te houden. De Sanctis' boek deed me denken aan de verschillende manieren waarop mijn team dat de afgelopen jaren voor elkaar heeft proberen te krijgen. Want het dom houden van je Controllers -- zonder aan expressiviteit in te boeten -- is geen triviale zaak. 


Vandaag: hoe het niet moet.


## Een eenvoudig voorbeeld


Ik zal mijn weergave van de ontwikkeling van onze Controller-methods kaderen met een eenvoudig (en vereenvoudigd!) voorbeeld uit mijn dagelijkse praktijk: het ontsluiten van een toetsvragen, *items* in vakjargon, aan gebruikers van onze Web API.


Laten we -- niet onredelijkerwijs -- aannemen dat die *items* bestaan in een database. De Web API is, zou je kunnen stellen, een eenvoudig schilletje rondom die database. Dat zou er zo uit kunnen zien[^1]:


```cs
[Route("api/item")]
[ApiController]
public class ItemsController : ControllerBase
{
    private readonly IItemRepository _items;

    public ItemController(IItemRepository items)
    {
        _items = items;
    }

    [HttpGet("{id}")]
    public async Task<ActionResult<Item>> GetItem(int id)
    { 
        var item = await _items.GetByIdAsync(id);
        return Ok(item);
    }
}
```

Zeg nu zelf: veel dommer dan dit worden Controller-methods niet! We spreken onze database via de `IItemRepository` aan om een item op te halen met een bepaald id, en als we dat item hebben gevonden, geven we het resultaat aan de `Ok`-method. Deze wrapt het resultaat in een response met [statuscode 200](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200 "'200 OK', MDN web docs") om aan te geven dat de operatie geslaagd is.


Maar er is een probleem. Wat gebeurt er wanneer er geen item in de database correspondeert met het opgegeven `id`? In de huidige opzet, retourneren we dan nog steeds een response met statuscode 200, alleen zonder het daadwerkelijke item. Dat is verwarrend voor de gebruiker van de API: als de operatie geslaagd is, waarom heb ik dan geen resultaat?


Wat we zouden willen, is een andere response teruggeven, een met [statuscode 404](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404 "'404 Not Found', MDN web docs") om aan te geven dat de gevraagde *resource* niet gevonden kan worden:


```cs
[Route("api/item")]
[ApiController]
public class ItemsController : ControllerBase
{
    // ...

    [HttpGet("{id}")]
    public async Task<ActionResult<Item>> GetItem(int id)
    { 
        var item = await _items.GetByIdAsync(id);
        if (item is null)
        {
            return NotFound();
        }
        return Ok(item);
    }
}
```


Onze Controller-method is iets slimmer geworden. Hij maakt nu onderscheid tussen twee condities: success -- het item kon gevonden worden -- en mislukking -- niet gevonden. Is dat problematisch? Niet per se. Op zich is er niets mis met de implementatie zoals we die nu hebben staan. 


Maar als we onze Controller uitbreiden met andere methods, dan lopen we vrij snel tegen een irritatiepunt aan. Wanneer we items op naam willen op gaan vragen, of wanneer we nieuwe Controllers introduceren voor andere objecten, dan zullen we de logica om onderscheid te maken tussen beide condities steeds opnieuw moeten dupliceren. In elke method zullen we een `if`-statement terug gaan vinden: in geval van succes retourneren we `Ok`, en anders `NotFound`.


Dat irritatiepunt parkeren we voor nu; later kom ik daar op terug.


## Toegang


Eerst kijken we naar een volgende requirement van onze API: autorisatie. Niet elke gebruiker mag elk item zomaar zien. Pas als een gebruiker de juiste toegangsrechten heeft, zou de code het gevraagde item op moeten halen. Als die rechten niet aanwezig zijn, dan zou er een foutmelding terug moeten worden gegeven. Een naïeve implementatie van deze requirement zou er zo uit kunnen zien:


```cs
[Route("api/item")]
[ApiController]
public class ItemsController : ControllerBase
{
    private readonly IAccessManager _accessManager;
    private readonly IItemRepository _items;

    public ItemController(
        IAccessManager accessManager,
        IItemRepository items)
    {
        _accessManager = accessManager;
        _items = items;
    }

    [HttpGet("{id}")]
    public async Task<ActionResult<Item>> GetItem(int id)
    {
        if (!(await _accessManager.HasAccessToItemAsync(id, User)))
        {
            return Forbid();
        }
        
        var item = await _items.GetByIdAsync(id);
        if (item is null)
        {
            return NotFound();
        }
        return Ok(item);
    }
}
```


Voordat we het item op proberen te halen, controleren we op toegangsrechten via de `HasAccessToItemAsync` method.[^2]. Heeft de gebruiker de juiste rechten, dan wordt dezelfde code uitgevoerd als in onze eerdere implementatie. Maar heeft deze dat niet, dan retourneren we een reponse met [statuscode 403](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403 "'403 Forbidden', MDN web docs"), wat aangeeft dat de gebruiker geen toegang heeft tot de gevraagde resource.


## Abstractielaag


Opnieuw is onze Controller method een stukje slimmer geworden. Te slim zelfs. `GetItem` schendt het SRP. De method is zowel de ingang voor gebruikers van onze Web API én codificeert een *business rule*: een item is alleen op te vragen voor gebruikers die over de juiste rechten beschikken. We zullen na moeten denken over de introductie van een abstractielaag. 


Wat we moeten doen is de logica verplaatsen naar een class wiens enige verantwoordelijkheid het is om de logica te codificeren. Dat heeft tot gevolg dat de Controller als enige verantwoordelijkheid overhoudt bepaalde functionaliteit te ontsluiten voor gebruikers. Traditioneel losten we dit in ons team op met een service.[^3] Een -- opnieuw -- naïeve interfacedefinitie zou er als volgt uit kunnen zien: 


```cs
public interface IItemService 
{
    Task<Item> GetByIdAsync(int id, ClaimsPrincipal user);
}
```


Zo'n service zou onze Controller weer ouderwets dom maken:


```cs
[Route("api/item")]
[ApiController]
public class ItemsController : ControllerBase
{
    private readonly IItemService _itemService;

    public ItemController(IItemService itemService)
    {
        _itemService = itemService;
    }

    [HttpGet("{id}")]
    public async Task<ActionResult<Item>> GetItem(int id)
    {
        var item = await _itemService.GetByIdAsync(id, User);
        if (item is null)
        {
            return NotFound();
        }
        return Ok(item);
    }
}
```


## Probleem


Maar wanneer we de interface implementeren, lopen we tegen een probleem aan:


```cs
public class ItemService : IItemService
{
    private readonly IItemService _itemService;

    private readonly IAccessManager _accessManager;
    private readonly IItemRepository _items;

    public ItemService(
        IAccessManager accessManager,
        IItemRepository items)
    {
        _accessManager = accessManager;
        _items = items;
    }

    public async Task<Item> GetByIdAsync(
        int id, 
        ClaimsPrincipal user)
    {
        if (!(await _accessManager.HasAccessToItemAsync(id, user)))
        {
            // What do we do here?
        }
        
        return await _items.GetByIdAsync(id);
    }
}
```


Wat retourneren we wanneer de gebruiker niet de juiste toegangsrechten heeft om het item op te mogen halen? 


Een item teruggeven is geen optie -- er is immers geen item om aan de gebruiker terug te geven. We zouden `null` terug kunnen geven. Maar dan zou onze Controller het onderscheid niet meer kunnen maken tussen een item waar de gebruiker geen toegang toe heeft en een item dat niet bestaat. We zouden daarmee de bestaande functionaliteit wijzigen: zowel een verboden als niet gevonden item zouden in een statuscode 404 resulteren.


Welke opties staan er tot onze beschikking, gegeven het feit dat de `GetByIdAsync` een `Item` retourneert?


## Een oplossing


Dit is de oplossing waar we in eerste instantie (-- onthoud die frase!) voor kozen:


```cs
public class ItemService : IItemService
{
    // ...

    public async Task<Item> GetByIdAsync(
        int id, 
        ClaimsPrincipal user)
    {
        if (!(await _accessManager.HasAccessToItemAsync(id, user)))
        {
            throw new UnauthorizedException();
        }
        
        return await _items.GetByIdAsync(id);
    }
}
```


Als de gebruiker toegang heeft, dan retourneren we een `Item` (of `null`), en als de gebruiker geen toegang heeft, dan gooien we een [exception](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/exceptions/ "'Exceptions and Exception Handling', Microsoft documentatie") op. Maar daarmee zijn we er nog niet. Als we de `UnauthorizedException` niet opvangen, dan resulteert dat in een response met [statuscode 500](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/500 "'500 Internal Server Error', MDN web docs"), wat aangeeft dat er een fout op de server heeft plaatsgevonden. Dat is nog steeds niet het gedrag dat we willen.


We zouden de exception op kunnen vangen in de Controller method:


```cs
[Route("api/item")]
[ApiController]
public class ItemsController : ControllerBase
{
    // ...

    [HttpGet("{id}")]
    public async Task<ActionResult<Item>> GetItem(int id)
    {
        try
        {
            var item = await _itemService.GetByIdAsync(id, User);
            if (item is null)
            {
                return NotFound();
            }
            return Ok(item);
        }
        catch (UnauthorizedException)
        {
            return Forbid();
        }
    }
}
```


Maar dan zijn we weer terug bij af: onze Controller bevat meer logica dan we zouden willen. Bovendien zou deze oplossingsrichting ervoor zorgen dat we in al onze controllers dit soort constructies in zouden moeten bouwen: een onderhoudsnachtmerrie. De hoeveelheid codeduplicatie zou ons gauw boven het hoofd groeien.


## Middleware


Daarom besloten we het afvangen van exceptions te centraliseren in een stukje [middleware](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-8.0 "'ASP.NET Core Middleware', Microsoft documentatie") -- hier een vereenvoudigde implementatie:


```cs
public class ExceptionMiddleware
{
    private readonly RequestDelegate _next;

    public ExceptionMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (Exception ex)
        {
            await HandleException(ex);
        }
    }

    private async Task HandleException(
        HttpContext context, 
        Exception ex)
    {
        context.Response.ContentType = "text/plain";
        context.Response.StatusCode = DetermineStatusCode(ex);
        await context.Response.WriteAsync(ex.Message);
    }

    private static int DetermineStatusCode(Exception ex)
    {
        return ex switch
        {
            UnauthorizedException => (int)HttpStatusCode.Forbidden,
            // other exceptions here...
            _ => (int)HttpStatusCode.InternalServerError
        };
    }
}

```


Het enige dat ons nog rest is deze middleware te registreren in de `Configure` method van `Startup.cs` -- en klaar is kees.


## Duplicatie


Hoewel... klaar? Helemaal klaar waren we niet, want nu deze oplossing eenmaal stond, grepen we meteen de kans aan om de codeduplicatie waar ik het eerder over had aan te pakken. We pasten onze `ItemService` aan...


```cs
public class ItemService : IItemService
{
    // ...

    public async Task<Item> GetByIdAsync(
        int id, 
        ClaimsPrincipal user)
    {
        if (!(await _accessManager.HasAccessToItemAsync(id, user)))
        {
            throw new UnauthorizedException();
        }
        
        var result = await _items.GetByIdAsync(id);
        return result ?? throw new NotFoundException();
    }
}
```


...vingen die exception op in onze middleware...


```cs
public class ExceptionMiddleware
{
    // ...

    private static int DetermineStatusCode(Exception ex)
    {
        return ex switch
        {
            UnauthorizedException => (int)HttpStatusCode.Forbidden,
            NotFoundException => (int)HttpStatusCode.NotFound,
            // other exceptions here...
            _ => (int)HttpStatusCode.InternalServerError
        };
    }
}

```


...en konden onze Controller op die manier opnieuw weer een stukje dommer maken:


```cs
[Route("api/item")]
[ApiController]
public class ItemsController : ControllerBase
{
    // ...

    [HttpGet("{id}")]
    public async Task<ActionResult<Item>> GetItem(int id)
    {
        var item = await _itemService.GetByIdAsync(id, User);
        return Ok(item);
    }
}
```


## Resultaat


Het resultaat is: (1) een simpele Controller-method, ingebed in (2) een infrastructuur die het mogelijk maakt om in verschillende scenario's aan verschillende statuscodes terug te sturen.  


Is Kees dan nu echt klaar? Ja -- en nee. Ja, in de zin dat mijn team deze middleware een hele tijd heeft onderhouden en uitgebreid met allerhande andere exceptions. 


Maar onthoud dat ik zei dat we *in eerste instantie* voor deze oplossingsrichting hadden gekozen. Dus: nee. Nee, absoluut niet. Want er zitten verschillende problemen aan de code zoals die nu staat. 


-- Welke dat zijn, dat bewaar ik voor een volgende blog. Tot die tijd zou ik je willen vragen: wat vind jij van de gekozen oplossingsrichting? Wat zijn de voor- en nadelen? En hoe zou je het anders aan kunnen pakken?

 
[^1]: In dit codevoorbeeld gebruik ik een [repository](https://martinfowler.com/eaaCatalog/repository.html "'Repository' door Edward Hieatt and Rob Mee, Martin Fowler") om de details rondom het aanspreken van de database te abstraheren. Dat doe ik voornamelijk om het voorbeeld niet teveel te compliceren met allerlei code die vanuit het perspectief van de Web API niet relevant is. 

[^2]: De `IAccessManager` waar deze method onderdeel van is, is een stukje pseudocode bedoeld om de `ItemsController` te compliceren. Het verwijst niet naar een patroon dat we in onze daadwerkelijke codebase gebruiken.

[^3]: Maar van dit soort "horizontale" oplossingen zijn we niet lang geleden overgestapt naar een [*vertical slice architecture*](https://www.jimmybogard.com/vertical-slice-architecture/ "'Vertical Slice Architecture', Jimmy Bogard"). De details van die overstap zijn voor deze blog niet per se relevant; wellicht dat ik dit onderwerp in een toekomstige blog onder de loep neem.
