---
title: "Ik loste het op met een monad"
author: "Karl van Heijster"
date: 2024-08-02T08:26:33+02:00
draft: true
comments: true
tags: []
summary: "Een soort van *monad*. Denk ik."
---

-- Een soort van *monad*. Denk ik. (Zie ook [deze blog](/blog/22/12/wat-is-een-monad/ "'Wat is een monad?'"))


Laatst lag onze [Redis](https://redis.io/) cache eruit. Niet lang, en 'm een schop geven was voldoende om 'm weer aan de praat te krijgen, maar toch: hij lag eruit. En we deden toen een interessante ontdekking als team: als de cache eruit lag, dan kon je niet alleen niet meer de gecachte data ophalen, dan kon je bepaalde data überhaupt niet meer ophalen.


Wat was nu het geval: de cache gooide een [exception](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/exceptions/ "'Exceptions and Exception Handling', Microsoft documentatie") op -- en dus kreeg de eindgebruiker een foutmelding voor z'n neus, in plaats van de gevraagde data.


## Decorator


Maar dat is onzin, natuurlijk, want we *hebben* die data heus wel. We hebben 'm alleen niet in de cache. We vonden: of de gebruiker de data op kan halen of niet, mag niet afhankelijk zijn van het feit dat de cache in de lucht is. Als de cache eruit ligt, dan zou je de data uit de originele bron moeten krijgen -- klaar.


Dus ik schreef een [decorator](https://refactoring.guru/design-patterns/decorator "'Decorator', Refactoring.Guru") -- en verwachtte het probleem daarmee te hebben opgelost:


```cs
public class ResilientCacheDecorator<T>(
    ICache<T> decoree,
    ILogger<ICache<T>> logger) 
    : ICache<T>
    {
        public async Task<Option<T>> Get(string key)
        {
            try
            {
                return await decoree.Get(key);
            }
            catch (Exception ex)
            {
                logger.LogError(ex, "Cache error!");
                return None;
            }
        }

        // ...
    }
```

En dit loste het probleem ook daadwerkelijk op -- in *bijna* alle gevallen. Want een oplettende collega wees me gedurende de [code review](/tags/code-reviews/ "Blogs met de tag 'code reviews'") gelukkig op een uitzondering: de code waarmee we de gegevens van de gebruikers in ons systeem ophaalden.


## Kunststukje


Deze code was een waar kunststukje -- als in: moderne kunst; als in: onooglijk lelijk, nodeloos complex en mateloos interessant. 


De flow van de code was als volgt. 


(1) Kijk of er wordt verzocht om gebruikers op te halen die niet in de cache zitten. (2) Zo ja, kijk dan of deze gebruikers in onze SQL-tabel van historische gebruikers zitten.[^1] (3) Zo ja, voeg ze toe aan de cache. 


-- Hebben we nu alle gebruikers gevonden? (4) Zo nee, dan zetten we grof geschut in: (4a) haal alle (*alle!*) gebruikers op uit [Microsoft Entra](https://www.microsoft.com/nl-nl/security/business/microsoft-entra?market=nl) en voeg ze toe aan de cache. O, en als je dan toch bezig bent, (4b) haal dan alle (nogmaals: *alle!*) gebruikers op uit de SQL-tabel van historische gebruikers en voeg ze toe aan de cache. 


-- (5) Als er dan alsnog niet-gevonden gebruikers zijn, voeg ze dan toe aan de cache als niet-gevonden gebruikers. (6) Haal de gevraagde gebruikers op uit de cache.


Het zal de oplettende lezer opgevallen zijn dat als de cache eruit ligt, het onmogelijk wordt om gegevens van gebruikers op te vragen.


Hoe kan code als deze ontstaan? Misschien was de flow voor de schrijver van de code volslagen logisch. Waarschijnlijk was de flow voor de reviewer van de code zo ondoorgrondelijk dat deze het op een gegeven moment uit wanhoop opgegeven heeft. Maar zeker is dat er feature op feature bovenop een oorspronkelijk onschuldige ontwerpfout is gebouwd, met een dampend bord spaghetti tot gevolg.


## Datatransformatie


Het is duidelijk: deze code moest gerefactord worden. De vraag was alleen: hoe?[^2]


Laat ik een andere vraag stellen: met wat voor soort probleem hebben we hier te maken?[^3] Het is duidelijk dat de oorspronkelijke schrijver van de code het zag als een *control flow* probleem: zijn code stond vol met `if`-statements die aangaven dat er in het ene geval *zus* moest gebeuren en in het andere geval *zo*.


Maar al [mijn gefilosofeer over functioneel programmeren](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'") heeft mijn hersenen inmiddels dusdanig aangetast dat ik dit soort opgaven veeleer als datatransformatieproblemen ben gaan zien. (Zie ook [deze blog](/blog/24/05/functioneel-denken-een-praktijkvoorbeeld/ "'Functioneel denken: een praktijkvoorbeeld'").) De datatransformatie is in dit geval: het transformeren van een lijst ID's naar een lijst met gebruikersinformatie -- in dit geval, met drie databronnen in het midden.


Dit was hoe ik de flow zag.


(1) Haal de gevraagde gebruikers op uit de cache. (2) Als niet alle gevraagde gebruikers daar gevonden kunnen worden, haal ze dan op uit [Microsoft Entra](https://www.microsoft.com/nl-nl/security/business/microsoft-entra?market=nl). (3) Als ze daar niet allemaal gevonden kunnen worden (bijvoorbeeld omdat ze niet meer voor ons werken), haal ze dan op uit een SQL-tabel van historische gebruikers van onze applicatie. (4) Als ze daar niet gevonden kunnen worden, behandel hen dan als niet-gevonden gebruikers. (5) Voeg alle gebruikers die niet in de cache zaten, toe aan de cache. (6) Retourneer de opgevraagde gebruikers.


De signatuur (zie [deze blog](/blog/22/07/wat-zijn-eerlijke-functies/ "'Wat zijn eerlijke functies?'")) van het geheel is en blijft `int[] -> UserInformation[]`. Maar om de datatransformaties van de tussenstappen mogelijk te maken, had ik een ander object nodig: een object waarin ik bijhield (1) welke gebruikers er nog niet gevonden waren, (2) welke gebruikers er al wel gevonden waren, en (3) welke gebruikers ik toe moest voegen aan de cache. Oftewel:


```cs
public record GetUserInformationDto(
    int[] MissingUsers, 
    UserInformation[] FoundUsers, 
    UserInformation[] UsersToAddToCache);
```


Gedurende elke tussenstap moest ik dit object updaten (of liever gezegd, omdat het een [*immutable*](/tags/immutability/ "Blogs met de tag 'immutability'") [record](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record "'Records (C# reference)', Microsoft documentatie") betreft, een nieuw record instantiëren met de juiste informatie) naar de op dat moment relevante stand van zaken.


## Eerste poging


Mijn eerste poging zag er als volgt uit:


```cs
private async Task<UserInformation[]> GetUserInformations(
    int[] userIds)
{
    var dto = new UserInformationDto(userIds, [], []);
    var fromCache = await GetCachedUsers(dto);
    if (!fromCache.MissingUsers.Any())
    {
        return fromCache.FoundUsers;
    }

    var fromEntra = await GetEntraUsers(fromCache);
    if (!fromEntra.MissingUsers.Any())
    {
        await AddUsersToCacheAsync(fromEntra.UsersToAddToCache);
        return fromEntra.FoundUsers;
    }

    var fromHistoric = await GetHistoricUsers(fromEntra);
    if (!fromHistoric.MissingUsers.Any())
    {
        await AddUsersToCacheAsync(fromHistoric.UsersToAddToCache);
        return fromHistoric.FoundUsers;
    }

    var unknownUsers = fromHistoric.MissingUsers
        .Select(CreateUnkownUser);
    var addToCache = fromHistoric.UsersToAddToCache
        .Union(unknownUsers);
    await AddUsersToCacheAsync(addToCache);
    return fromHistoric.FoundUsers.Union(unknownUsers).ToArray();
}
```


Is dit mooie code? Absoluut niet. Maar het werkte wel, en het was makkelijk leesbaar, van boven naar beneden. De code is één op één een weergave van de flow zoals ik die hierboven heb beschreven. Dus het was nu in elk geval helder welke stappen er werden ondernomen.


Wat er natuurlijk aan scheelt, is die vreselijke codeduplicatie. Hoe daarmee om te gaan? -- Het antwoord schoot me te binnen onder de douche, en de hele zweterige nacht zat ik me te verkneukelen om het te verwachten resultaat.


## `Bind`


Het terugkerend patroon is: als er nog ontbrekende gebruikers zijn, doe dan *x*, waarbij *x* is "kijk in de cache", "kijk in Entra" etc.; en zo niet, retourneer het resultaat (al dan niet nadat je de cache hebt bijgewerkt als [*side effect*](https://en.wikipedia.org/wiki/Side_effect_(computer_science) "'Side effect (computer science)', Wikipedia")).


Oftewel: we hebben een object met daarin de huidige stand van zaken -- welke gebruikers er nog niet gevonden zijn, welke wel, en gebruikers die we straks toe moeten voegen aan de cache. We hebben een functie die we uit willen voeren op de inhoud van dat object -- een transformatie van de niet-gevonden gebruikers naar eventueel gevonden-gebruikers. En als we dat eenmaal hebben gedaan, willen we het object bijwerken als gevolg van die transformatie.


Dat klinkt als `Bind` -- en dit was mijn implementatie[^4] (-- let niet op die `addFoundUsersToCache`, daar kom ik zo dadelijk nog op terug):


```cs
public static async Task<GetUserInformationDto> Bind(
    this GetUserInformationDto dto,
    Func<int[], Task<UserInformation[]>> findUsers,
    bool addFoundUsersToCache = true)
{
    if (dto.MissingUsers.Any())
    {
        var foundUsers = await findUsers(dto.MissingUsers);
        return dto.Update(foundUsers, addFoundUsersToCache);
    }
    return dto;
}
```


De `Update`-[*extension method*](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods "'Extension Methods (C# Programming Guide)', Microsoft documentatie") "verheft" het resultaat van `findUsers` naar een `GetUserInformationDto`, en zag er als volgt uit:


```cs
private static GetUserInformationDto Update(
    this GetUserInformationDto request,
    UserInformation[] foundUsers,
    bool addFoundUsersToCache)
{
    var totalFound = request.FoundUsers
        .Union(foundUsers)
        .ToArray();
    var missingUsers = request.MissingUsers
        .Except(totalFound.Select(u => u.Id));
    var usersToAddToCache = addFoundUsersToCache
        ? request.UsersToAddToCache
            .Union(foundUsers.Except(request.FoundUsers))
        : request.UsersToAddToCache;
    return new GetUserInformationDto(
        totalFound, 
        missingUsers, 
        usersToAddToCache);
}
```


## Tweede poging


Deze methods stelden met in staat mijn eerste poging als volgt te herschrijven:


```cs
private async Task<UserInformation[]> GetUserInformations(
    int[] userIds)
{
    var result = await new GetUserInformationDto(userIds, [], [])
        .Bind(GetCachedUsers, addFoundUsersToCache: false)
        .Bind(GetEntraUsers)
        .Bind(GetHistoricUsers)
        .Bind(CreateUnknownUsers)
        .Do(AddUsersToCacheAsync);
    return result.FoundUsers;
}
```


Dan kunnen we het nu eindelijk over (soort van, denk ik) [*monads*](/tags/monads/ "Blogs met de tag 'monads'") hebben. -- Wat ik me onder de douche besefte is: die `GetUserInformationDto` die ik had gedefinieerd, dat is een doosje waar ik de tussenliggende resultaten van mijn pogingen in kon bewaren. 


Het is een object dat op een hoger abstractieniveau leeft dan de input (`int[]`) of uiteindelijke output (`UserInformation[]`). En het moet daarom mogelijk zijn om die inputs en outputs te "verheffen" naar dat hogere niveau, en de resultaten aan elkaar te knopen. -- Is het *formeel* bezien een *monad*? Nee, volgens mij niet. Maar de denkwijze is hetzelfde.


Het resultaat is een eenvoudige *pipeline* (zie ook [deze blog](SEMANTISCHE_BUGS)) die op [declaratieve wijze](/tags/declaratief-programmeren/ "Blogs met de tag 'declaratief programmeren'") aangeeft *wat* er allemaal gebeurt, en voor de lezer abstraheert *hoe* dat gebeurt.


`Do`, ten slotte, is een functie om *side effects* mee te bewerkstelligen.


```cs
public static async Task<GetUserInformationDto> Do(
    this Task<GetUserInformationDto> dto,
    Func<IEnumerable<UserInformation>, Task> addToCache)
{
    var awaited = await dto;
    if (awaited.UsersToAddToCache.Any())
    {
        await addToCache(awaited.UsersToAddToCache);
    }
    return awaited;
}
```


## Pijnpunt


Het moge duidelijk zijn: ik was behoorlijk in mijn nopjes met mijn oplossingsrichting. Maar helemaal zonder pijnpunten is 'ie ook niet. De grootste doorn in mijn oog is de parameter `addFoundUsersToCache` -- een [*flag argument*](https://martinfowler.com/bliki/FlagArgument.html "'Flag Argument', Martin Fowler"), en over het algemeen een [*code smell*](https://refactoring.guru/refactoring/smells "'Code Smells', Refactoring.Guru").


Die parameter komt voort omdat er twee soorten opzoekacties zijn: ofwel er wordt in de cache gezocht (en in geval van succes hoeft deze natuurlijk niet te worden bijgewerkt), ofwel niet (en in dat geval moet de cache wel worden bijgewerkt). De *flag* was de eenvoudigste, maar niet per se de mooiste, manier om onderscheid tussen die twee scenario's te maken.


Een alternatieve oplossing zou zijn om een tweede object te definiëren, `GetUserInformationFromCacheDto`. Deze zou geen property `UsersToAddToCache` hebben, en de `Bind` zou deze transformeren naar een `GetUserInformationDto`. Maar die oplossing leverde meer code op zonder de boel echt te verhelderen, dus die route heb ik niet gevolgd.


## Experiment


Zoals altijd is de vraag: was dit de beste manier om dit probleem op te lossen? (Zie ook [deze blog](/blog/24/02/callback-hell/ "'Callback hell'").) En zoals altijd is het antwoord: ik weet het niet. Ik weet niet of mijn van huis uit objectgeoriënteerde collega's dit nu een beter leesbare oplossing vinden dan een meer idiomatische "C#-achtige" implementatie. 


Maar wat ik wel weet, is dat het een verdomd leuk codeerexperiment was. En dat is toch ook wat waard?


[^1]: Deze tabel gebruiken we om auditing van onze data mogelijk te maken. Het is voor privacyminnende (ex-)medewerkers mogelijk om te verzoeken hieruit verwijderd te worden.

[^2]: Een andere vraag is: wanneer? (Vgl. [Kent Beck](https://www.kentbeck.com/), [*Tidy First?*](https://www.oreilly.com/library/view/tidy-first/9781098151232/ "Kent Beck, 'Tidy First?: A Personal Exercise in Empirical Software Design', O'Reilly Media, 2023") -- al is "*tidying*" voor deze casus waarschijnlijk een te zwakke uitdrukking!) In dit geval refactorde ik achteraf. Mijn eerste oplossing bestond uit het wrappen van het geheel in een [`try-catch`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/exception-handling-statements "'Exception-handling statements - throw, try-catch, try-finally, and try-catch-finally', Microsoft documentatie"). De wetenschap dat het oorspronkelijk probleem daarmee opgelost was, gaf me de ruimte in mijn hoofd om rustig te kunnen refactoren.

[^3]: Opnieuw ontleen ik inspiratie uit [dit praatje](https://www.youtube.com/watch?v=NMPeAW2RWdc "Refactoring Is Not Just Clickbait - Kevlin Henney - NDC London 2023") (zie ook [deze](REFACTORING_ALS_COMMUNICATIEMIDDEL) en [deze blog](REFACTORING_EN_HANNAH_ARENDT)) van [Kevlin Henney](http://kevlin.tel/).

[^4]: Omdat ik werk met [asynchrone functies](https://learn.microsoft.com/en-us/dotnet/csharp/asynchronous-programming/ "'Asynchronous programming with async and await', Microsoft documentatie"), definieerde ik daarnaast een variant op `Bind` die met een `Task<GetUserInformationDto>` werkt. Het enige wat die doet, is de task *awaiten*, en daarna de bovenstaande aanroepen. Zie de implementatie van `Do` verderop.
