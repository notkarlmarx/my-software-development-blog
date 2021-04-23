---
title: "Enums, Switch Statements en SOLID - Deel 3"
date: 2021-04-23T18:20:48+02:00
draft: true
comments: true
tags: ["clean code", "dependency inversion principe", "enums", "single-responsibility principe", "SOLID", "switch statements", "refactoren"]
---

# Het *Dependency inversion* principe


[Vorige week](/blog/enums-switch-statements-en-solid-1) refactorde ik [een stuk code](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V01/ClaimsHelper.cs) om meer in lijn te zijn met het [*Single-Responsiblity* principe](https://en.wikipedia.org/wiki/Single-responsibility_principle). 


Ik abstraheerde logica die oorspronkelijk in onderstaande switch-statement zat, naar aparte methods. Dat zorgde ervoor dat de oorspronkelijke method een reden minder had om gewijzigd te worden (of drie drie redenen minder, afhankelijk van hoe je het bekijkt). Anders gezegd: door code te verhuizen naar aparte methods, bracht ik het aantal verantwoordelijkheden van de oorspronkelijke method terug. 


Het resultaat was een stapje in de richting van beter leesbare en onderhoudbare code.


{{< gist notkarlmarx 8d1b1346a9b21306e5f128fbd5602fec "ClaimsHelper.cs">}}


Maar hoewel de oorspronkelijke method nu minder verantwoordelijkheden had, kon dit niet gezegd worden voor de class. Deze bevindt zich in zekere zin op hetzelfde niveau als vorige week. Elke keer als een claim voor een bepaald recht (`Permission`) wordt aangepast moeten we onze `ClaimsHelper` aanpassen.


Zou het niet fijn zijn als we deze wijzigingen door konden voeren zonder dat we de `ClaimsHelper` aan hoeven te passen?


## Drie classes...


De opdracht lijkt duidelijk: de code die nu in de methods `GetReadClaim()`, `GetWriteClaim()` en `GetDeleteClaim()` zit, moet de `ClaimsHelper` uit. We kunnen voor alle drie een aparte class aanmaken met hun respectievelijke methods. De class voor leesrechten zou er bijvoorbeeld als volgt uit kunnen zien:


{{< gist notkarlmarx 9d8b1caf8ffff8de065db008ed423305 "GetReadClaim.cs">}}


Dit is opnieuw een stap in de goede richting. Elke keer als de inhoud van een claim wordt aangepast, hoeft die wijziging alleen maar doorgevoerd te worden in de bijbehorende class. 


Maar helemaal weg is het probleem nog niet. Het hart van `GetClaimsForUser()` wordt nog steeds gevormd door de `Permissions`-enum. Elke keer als deze wordt aangepast, zal die method een foutmelding gaan geven. 


## ...één abstractie


Onze opdracht is nu van dat vervelende switch-statement af zien te komen. Het was deze opdracht die [in eerste instantie mijn interesse in deze class wekte](/blog/enums-switch-statements-en-solid-1). Hoe vliegen we dit aan?


Gelukkig zijn we al vrij dicht bij de oplossing. Als je de code snippet bekijkt waar deze blog-post mee begon, valt je dan iets op aan de drie methods die we aan hebben gemaakt? 


In wezen doen ze alle drie hetzelfde, namelijk: de claim teruggeven die bij de `Permission` hoort. Dit is een functie van alle drie de methods die de concrete implementatie overstijgt. We zijn op een abstractie gestuit. Dat gedrag kunnen we vangen in een interface:


{{< gist notkarlmarx bedb39a5b877fd1fdbc9508e745e8b4f "IGetClaim.cs">}}


Onze eerder geschetste `GetReadClaim` hoeven we maar minimaal aan te passen om aan deze interface te kunnen voldoen:


{{< gist notkarlmarx 6ad02f71ae563e2a665badcd988d1d4f "GetReadClaim.cs">}}


Nu we tegen een interface aan kunnen programmeren, hoeft de `ClaimsHelper` niet meer te weten van de `Permissions`-enum. Hij hoeft alleen maar te weten dat hij met een class te maken heeft die `IGetClaim` implementeert en daar de method `GetClaim()` van aan te roepen.


Maar hoe weet de `ClaimsHelper` welke implementatie hij wanneer aan moet roepen? Dit is een uitstekende vraag, en mijn antwoord daarop is voorlopig nog een beetje valsspelen. Ik ga het probleem van de `ClaimsHelper` voor nu namelijk even parkeren in een ondersteunende method die ik de `GetClaim()` noem.


## Een tussenstand


De `ClaimsHelper` komt er nu als volgt uit te zien:


{{< gist notkarlmarx 8cc39148d7b0165c9ad9d58399b7f640 "ClaimsHelper.cs">}}
