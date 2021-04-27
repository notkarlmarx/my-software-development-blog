---
title: "Enums, Switch Statements en SOLID - Deel 3"
date: 2021-04-23T18:20:48+02:00
draft: true
comments: true
tags: ["clean code", "dependency inversion principe", "enums", "refactoren", "single-responsibility principe", "SOLID", "switch statements"]
---

# Het *Dependency inversion* principe


[Vorige week](/blog/enums-switch-statements-en-solid-2) refactorde ik [een stuk code](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V01/ClaimsHelper.cs) om meer in lijn te zijn met het [*Single-Responsiblity* principe](https://en.wikipedia.org/wiki/Single-responsibility_principle). 


Ik abstraheerde logica die oorspronkelijk in onderstaande switch-statement zat, naar aparte classes. Dat zorgde ervoor dat de oorspronkelijke class een reden minder had om gewijzigd te worden (of drie drie redenen minder, afhankelijk van hoe je het bekijkt). Anders gezegd: door code te verhuizen, bracht ik het aantal verantwoordelijkheden van de oorspronkelijke class terug. 


Het resultaat was een stapje in de richting van beter leesbare en onderhoudbare code.


{{< gist notkarlmarx 8d1b1346a9b21306e5f128fbd5602fec "ClaimsHelperV02.cs">}}


De logica in `GetClaimsForUser()` bevat echter nog veel repetitie en is afhankelijk van de concrete implementatie van de classes die we aanroepen. Om dat probleem aan te pakken, kunnen we gebruik maken van een ander SOLID-principe: het *Dependency inversion* principe.


## Het kan me niet schelen *hoe* je het doet, *als* je het maar doet


...uitleg...


## Drie classes, één abstractie


Als je de code snippet bekijkt waar deze blog-post mee begon, valt je dan iets op aan de drie methods die we aan hebben gemaakt? 


In wezen doen ze alle drie hetzelfde, namelijk: de claim teruggeven die bij de `Permission` hoort. Dit is een functie van alle drie de methods die de concrete implementatie overstijgt. We zijn op een [abstractie](https://en.wikipedia.org/wiki/Abstraction_(computer_science)) gestuit. Dat gedrag kunnen we vangen in een [interface](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface):


{{< gist notkarlmarx bedb39a5b877fd1fdbc9508e745e8b4f "IGetClaim.cs">}}


Onze eerder geschetste `ReadClaimProvider` hoeven we maar minimaal aan te passen om aan deze interface te kunnen voldoen:


{{< gist notkarlmarx bedb39a5b877fd1fdbc9508e745e8b4f "ReadClaimProvider.cs">}}


Nu we tegen een interface aan kunnen programmeren, hoeft de `ClaimsHelper` niet meer te weten van concrete methods die de claim van elk individueel recht teruggaven. Hij hoeft alleen maar te weten dat hij met een class te maken heeft die `IGetClaim` implementeert en daar de method `GetClaim()` van aan te roepen.


De `ClaimsHelper` komt er nu als volgt uit te zien:


{{< gist notkarlmarx bedb39a5b877fd1fdbc9508e745e8b4f "ClaimsHelper.cs">}}


Zoals je ziet, is `GetClaimsForUser()` een stuk opgeschoond. Omdat we niet meer afhankelijk zijn van concrete implementaties, hebben we het oorspronkelijke switch-statement uit de method kunnen abstraheren naar zijn eigen helpermethod met een [switch-expressie](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/switch-expression). 


De oorspronkelijke method hoeft zich alleen nog maar te bekommeren om het verkrijgen van de claim, niet meer om alle concrete manieren waarop die claims verkregen worden. Ook vanuit het perspectief van het *Single-responsibility* principe is er vooruitgang geboekt: alweer een verantwoordelijkheid minder!


## *What's next?*


Maar helemaal zijn we er nog niet. De `ClaimsHelper` heeft via `GetClaimProvider()` op dit moment nog weet van de concrete implementaties die er van `IGetClaim` bestaan. Hij moet ook wel, lijkt het, want hoe kan `GetClaimsForUser()` ooit de juiste claims aan de rechten van de gebruiker koppelen? Dat bekijken we volgende week. 


Wie tot die tijd graag zelf wil experimenteren, kan de code [via GitHub](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V02/ClaimsHelper.cs) binnenhalen.


## Meer in deze reeks

...
