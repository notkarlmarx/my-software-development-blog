---
title: "Hoe we onze controllers dom houden"
author: "Karl van Heijster"
date: 2024-02-16T11:30:46+01:00
draft: true
comments: true
tags: ["eerlijke functies", "exceptions", "functioneel programmeren", "refactoren", "software ontwikkelen", "web API's"]
summary: "Onlangs schreef ik over Controllers en de manier waarop mijn team ervoor zorgde dat er zo min mogelijk logica in die dingen terechtkwam. Onze opzet had impact op de manier waarop we onze logica structureerden. Het betekende dat de methods in onze services exceptions op moesten gooien zodra deze van het succespad afwijkten. Je kunt je vraagtekens hebben bij deze oplossingsrichting -- en die kregen we uiteindelijk ook."
---

Onlangs schreef ik over [Controllers](https://learn.microsoft.com/en-us/aspnet/core/web-api/ "'Create web APIs with ASP.NET Core', Microsoft documentatie") en [de manier waarop mijn team ervoor zorgde dat er zo min mogelijk logica in die dingen terechtkwam] (BLOG). Lang verhaal kort: in de Controller method zelf handelden we alleen de succesconditie af; de verantwoordelijkheid foutcondities af te handelen delegeerden we naar een een stukje [middleware](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-8.0 "'ASP.NET Core Middleware', Microsoft documentatie"). Zo maakten we het voor onszelf mogelijk om verschillende [statuscodes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes "'List of HTTP status codes', Wikipedia") terug te geven in verschillende scenario's.


Deze opzet had impact op de manier waarop we onze logica structureerden. Het betekende dat de methods in onze services [exceptions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/exceptions/ "'Exceptions and Exception Handling', Microsoft documentatie") op moesten gooien zodra deze van het succespad afwijkten. Exceptions werden een integraal onderdeel van onze [*control flow*](https://en.wikipedia.org/wiki/Control_flow "'Control flow', Wikipedia").


## Vraagtekens


Je kunt je vraagtekens hebben bij deze oplossingsrichting -- en die kregen we uiteindelijk ook. Er zijn verschillende problemen met het gebruik van exceptions voor de afhandeling van businesslogica. 


Eén zo'n probleem is de [performanceimpact van het gebruik van exceptions](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/exceptions-and-performance "'Exceptions and Performance', Microsoft documentatie"). Maar ik zal eerlijk zijn: dit is wat mij betreft niet een doorslaggevend argument om van het gebruik van exceptions af te stappen. Hoewel het routinematig gebruik van exceptions een negatieve impact heeft op de performance, vormen exceptions in mijn ervaring maar zelden de bottleneck voor de snelheid van een systeem.


## Semantisch


Dit is een interessanter vraagstuk: zijn exceptions semantisch bezien het juiste middel om afwijkingen van het succespad mee uit te programmeren? Communiceren deze de juiste intentie? In het voorbeeld dat ik in [mijn vorige blog] (BLOG) uitwerkte, gebruikten we exceptions om te signaleren dat de gebruiker geen toegang had tot een resource, of dat een resource niet gevonden kon worden. 


```cs
public async Task<Item> GetByIdAsync(
    int id, 
    ClaimsPrincipal user)
{
    if (!(await _accessManager.HasAccessToItemAsync(id, user)))
    {
        throw new UnauthorizedException();
    }
    
    var item = await _items.GetByIdAsync(id);
    return item ?? throw new NotFoundException();
}
```


Vraag jezelf af: zijn deze scenario's inderdaad uitzonderlijk, *exceptioneel*? Horen foutcondities als geen toegang hebben of een resource niet kunnen vinden bij de "normale" flow van een systeem? -- Het klinkt als een gewetensvraag: is falen een geaccepteerde mogelijkheid of niet?


## Over exceptions


Het loont zich om te reflecteren op wat de structuur van exceptions ons vertellen over de scenario's waarin ze toepasselijk zijn. Exceptions onderbreken de normale flow van een programma. De meeste code valt van boven naar beneden te lezen, als een verhaal: eerst gebeurt er dit, dan gebeurt er dat. Maar op het punt dat er een exception wordt opgegooid, doen de regels daar onder er niet meer toe. Wie wil weten hoe het verhaal afloopt, moet naar een heel andere bladzijde bladeren, zogezegd.


Exceptions coderen (*pun intended*) hun exceptionele status dus niet alleen in hun naam, maar ook in hun gedrag, en in de reactie die ze van de lezer van de code vragen. (Voor meer bespiegelingen over de communicatieve eigenschappen van code, zie [deze blog](/blog/24/01/symmetrische-en-asymmetrische-overerving/ "'Symmetrische en asymmetrische overerving'").)


Als we beslissen dat deze scenario's inderdaad uitzonderlijk zijn, dan kunnen we de implementatie laten zoals deze is. Maar dat is niet de beslissing die we als team namen. Nee, het is niet uitzonderlijk dat een bepaalde gebruiker geen toegang heeft tot een bepaald Item; niet elke gebruiker mag immers elk Item bekijken. En het is evenmin uitzonderlijk dat een databasequery met een bepaald `id` geen resultaat oplevert; het kan nu eenmaal zo zijn dat er geen record met dat `id` bestaat. Exceptions zijn semantisch dus niet het juiste middel voor wat we willen bereiken.


## Leesbaarheid


Bovendien, hun gedrag heeft -- dit is het derde probleem -- impact op de leesbaarheid van de code. Exceptions maken het gedrag van een method ondoorzichtig. Het is moeilijk om aannames te doen over de gevolgen die een bepaalde method call kan hebben. Je zal als lezer de context waarin de method method wordt aangeroepen, moeten inspecteren om erachter te komen wat die aanroep voor allemaal gevolgen voor gevolgen kan hebben.


Dat geldt in het bijzonder voor de code waar ik [mijn vorige blog] (BLOG) mee eindigde:


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


Deze code lijkt eenvoudig: je roept iets aan, je krijgt een antwoord terug, en je wrapt dat resultaat in een response met [statuscode 200](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200 "'200 OK', MDN web docs"). Maar schijn bedriegt. Want de aangeroepen method kan óók een exception opgooien -- twee zelfs, en dat kan resulteren in een [403](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403 "'403 Forbidden', MDN web docs") of [404](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404 "'404 Not Found', MDN web docs"). Maar om te begrijpen hoe en waarom, moet de lezer heel wat meer context hebben dan deze code allen.


## (On)eerlijk


De bovenstaande method is -- in het jargon van [functioneel programmeren](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'") -- niet [eerlijk](/blog/22/07/wat-zijn-eerlijke-functies/ "'Wat zijn eerlijke functies?'"). (Zie ook [deze blog](/blog/23/01/eerlijke-domeinmodellen/ "'Eerlijke domeinmodellen'").) Een eerlijke functie is transparant wat ze doet: gegeven input *x* retourneert deze ouput *y* -- en meer niet.


Kunnen we deze method zodanig herschrijven dat deze eerlijk is? Ja: we zouden de verschillende scenario's die plaats kunnen vinden -- succes, geen toegang, of niet gevonden -- kunnen vastleggen in object van hoger abstractieniveau. Laten we deze `QueryResult` noemen. Een naïeve implementatie zou er als volgt uit kunnen zien:


```cs
public class QueryResult
{
    public Item Value { get; set; }
    public bool AccessDenied { get; set; }
    public bool NotFound { get; set; };
}
```


De implementatie van `GetByIdAsync` zou er zo uit kunnen zien:


```cs
public async Task<QueryResult> GetByIdAsync(
    int id, 
    ClaimsPrincipal user)
{
    if (!(await _accessManager.HasAccessToItemAsync(id, user)))
    {
        return new QueryResult { AccessDenied = true };
    }
    
    var item = await _items.GetByIdAsync(id);
    return item is not null 
        ? new QueryResult { Value = item }
        : new QueryResult { NotFound = true };
}
```


Ook onze Controller method behoeft wat aanpassing -- maar daar kom ik later op terug. Eerst wil ik reflecteren op de winst die we geboekt hebben. 


Merk op dat we middels het `QueryResult`-object communiceren dat het *niet* uitzonderlijk is dat een gebruiker geen toegang heeft tot een bepaald Item, of dat een Item niet kan worden gevonden. En dat heeft direct impact op de leesbaarheid van de code. We zouden ons kunnen beperken tot het lezen van de signatuur van de functie -- `GetItemByIdasync: (int, ClaimsPrincipal) -> QueryResult` -- om erachter te komen wat deze doet. We hoeven niet langer de functie zelf te inspecteren om te zien of we niet voor nare verrassingen worden gesteld.


## Problemen


Maar dat betekent niet dat onze oplossing niet voor verbetering vatbaar is. Stel je een naïeve (of vergeetachtige, of slordige) programmeur voor die de code als volgt schrijft:


```cs
// ...
var item = await _items.GetByIdAsync(id);
return item new QueryResult { Value = item };
```


Zo'n programmeur zou onbedoeld een statuscode 200 teruggeven, terwijl deze eigenlijk een 404 bedoelde te retourneren. Een fout zit in een klein hoekje -- maar de gevolgen zijn er niet minder groot om.


En dat is niet het enige probleem. De huidige implementatie weerhoudt een programmeur er bijvoorbeeld niet van iets als het volgende te doen:


```cs
public async Task<QueryResult> GetByIdAsync(
    int id, 
    ClaimsPrincipal user)
{
    var result = new QueryResult();
    if (!(await _accessManager.HasAccessToItemAsync(id, user)))
    {
        result.AccessDenied = true;
    }
    
    var item = await _items.GetByIdAsync(id);
    if (item is null)
    {
        result.NotFound = true;
    } 
    result.Value = item;
    return result;
}
```


Er zijn twee problemen met deze code. Ten eerste is deze inefficiënt. Ook als de gebruiker geen toegang heeft tot het Item, wordt er een poging gedaan deze uit de database op te halen. Ten tweede geeft deze aanleiding tot mogelijke verwarring. Deze code kan bijvoorbeeld leiden tot een situatie waarin zowel `AccessDenied` als `NotFound` op `true` zijn geset. Wat voor statuscode moet er in dat geval geretourneerd worden, een 403 of een 404?


Natuurlijk, het is mogelijk om hier afspraken voor te maken binnen het team. We zouden er extra alert op kunnen zijn tijdens [code reviews](/tags/code-reviews/ "Blogs met de tag 'code reviews'"), bijvoorbeeld. Maar daarmee leggen we de verantwoordelijkheid voor het voorkomen van fouten zuiver en alleen bij de programmeurs. Dat is een risicovolle beslissing. 


## Fouten voorkomen


Beter zou zijn als we de code zo zouden schrijven, dat het voor de programmeurs onmogelijk wordt om deze klasse van fouten nog te maken. Gelukkig blijkt dit relatief eenvoudig.


Het eerste probleem kunnen we oplossing door te erkennen dat `NotFound` eigenlijk een afgeleide eigenschap is. De waarde van deze property is volledig afhankelijk van de waarde van `Value`. Met het expliciet setten van deze property hoeven we een gebruiker van dit object daarom niet lastig te vallen:


```cs
public class QueryResult
{
    public Item Value { get; set; }
    public bool AccessDenied { get; set; }
    public bool NotFound => Value is null;
}
```


Dit maakt het onmogelijk voor een ontwikkelaar om te vergeten `NotFound` de juiste waarde mee te geven wanneer het Item niet gevonden kan worden.


(Een alternatieve oplossing zou zijn om het type van `Value` te veranderen van `Item` naar `Option<Item>`. -- Sterker nog, deze variant heeft mijn voorkeur, en dat is inderdaad de manier waarop we het in onze eigen codebase hebben geprogrammeerd. -- Maar voor onze huidige uiteenzetting is dit implementatiedetail niet van belang. Voor meer over Options, zie [deze](/blog/22/07/wat-zijn-eerlijke-functies/ "'Wat zijn eerlijke functies?'") en [deze blog](/blog/22/08/spelen-met-options/ "'Spelen met Options'").)


## Beperken


Om het tweede probleem op te kunnen lossen, moeten we ervoor kunnen zorgen dat we een `QueryResult` kunnen instantiëren waarin ofwel `AccessDenied` ofwel `NotFound` op `true` is geset, maar niet allebei. We moeten de gebruiker van deze class dus beperken in zijn mogelijkheden de waarden van deze properties handmatig aan te passen. Dat doen we door dit te controleren via [factory methods](https://en.wikipedia.org/wiki/Factory_method_pattern "'Factory method pattern', Wikipedia"):


```cs
public class QueryResult
{
    public Item Value { get; private set; }
    public bool AccessDenied { get; private set; }
    public bool NotFound => Value is null;

    private QueryResult() { }

    public static QueryResult Value(Item value) => 
        new() { Value = value };
    public static QueryResult AccessDenied() => 
        new() { AccessDenied = true };
}
```


Het is nu nog maar op één manier mogelijk om dit object op een correcte manier te gebruiken in `GetById`:


```cs
public async Task<QueryResult> GetByIdAsync(
    int id, 
    ClaimsPrincipal user)
{
    if (!(await _accessManager.HasAccessToItemAsync(id, user)))
    {
        return QueryResult.AccessDenied();
    }
    
    var item = await _items.GetByIdAsync(id);
    return QueryResult.Value(item);
}
```


## Controller


Dan kunnen we nu eindelijk terugkeren naar onze Controller. Deze moesten we nog aanpassen om met `QueryResult` om te kunnen gaan. Een naïeve implementatie zou er zo uit kunnen zien: 


```cs
[Route("api/item")]
[ApiController]
public class ItemsController : ControllerBase
{
    // ...

    [HttpGet("{id}")]
    public async Task<ActionResult<Item>> GetItem(int id)
    {
        var result = await _itemService.GetByIdAsync(id, User);
        if (result.AccessDenied)
        {
            return Forbid(); 
        }
        if (result.NotFound)
        {
            return NotFound();
        }
        return Ok(result.Value);
    }
}
```


Maar zijn we hier niet mee terug bij af? Zit er nu niet veel te veel logica in onze Controller? Het antwoord is: ja. 


Maar we hebben nu de mogelijkheidsvoorwaarden geschapen om onze Controller methods te standaardiseren. Als we `QueryResult` omschrijven naar `QueryResult<T>`, waarbij `T` in dit specifieke geval voor `Item` staat, kunnen we dit object hergebruiken voor andere objecten in onze applicatie. Die zouden we uniform af kunnen handelen door de bovenstaande logica naar een [extension method](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods "'Extension Methods (C# Programming Guide)', Microsoft documentatie") te verplaatsen:


```cs
public static QueryResultExtensions
{
    public static ActionResult ToActionResult<T>(
        this QueryResult<T> queryResult)
    {
        if (queryResult.AccessDenied)
        {
            return new ForbidResult();
        }
        if (queryResult.NotFound)
        {
            return new NotFoundResult();
        }
        return new OkObjectResult(queryResult.Value);
    }
}
```


## Eenvoudig


Onze Controller zou er daarna ouderwets eenvoudig uit komen te zien:


```cs
[Route("api/item")]
[ApiController]
public class ItemsController : ControllerBase
{
    // ...

    [HttpGet("{id}")]
    public async Task<ActionResult<Item>> GetItem(int id)
    {
        var result = await _itemService.GetByIdAsync(id, User);
        return result.ToActionResult();
    }
}
```


In twee regels code (plus de code in `QueryResult<T>` en diens extension method) hebben we onszelf de mogelijkheid gegeven om verschillende statuscodes terug te geven in verschillende scenario's zonder in te leveren op leesbaarheid dankzij een onnavolgbare *control flow*.


En dat is dus hoe we onze Controllers dom houden. -- In elk geval, totdat we een betere manier hebben gevonden.
