---
title: "Enums, Switch Statements en SOLID - Deel 3"
date: 2021-05-14T08:42:31+02:00
draft: false
comments: true
tags: ["clean code", "dependency inversion principe", "enums", "refactoren", "single-responsibility principe", "SOLID", "switch statements"]
summary: "Vorige week refactorde ik een switch statement rondom een enum aan de hand van het *Single-Responsibility* principe. Deze week zetten we onze refactorslag voort aan de hand van de D in SOLID: het *Dependency inversion* principe. Tijd om de interfaces van stal te halen!"
---

# Het *Dependency inversion* principe


[Vorige week](/blog/21-05-07-enums-switch-statements-en-solid-2) refactorde ik [een stuk code](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V01/ClaimsHelper.cs) om meer in lijn te zijn met het [*Single-Responsiblity* principe](https://en.wikipedia.org/wiki/Single-responsibility_principle). 


Ik abstraheerde logica die oorspronkelijk in onderstaande switch-statement zat, naar aparte classes. Dat zorgde ervoor dat de oorspronkelijke class een reden minder had om gewijzigd te worden (of drie drie redenen minder, afhankelijk van hoe je het bekijkt). Anders gezegd: door code te verhuizen, bracht ik het aantal verantwoordelijkheden van de oorspronkelijke class terug. 


Het resultaat was een stapje in de richting van beter leesbare en onderhoudbare code.


{{< gist notkarlmarx 8d1b1346a9b21306e5f128fbd5602fec "ClaimsHelperV02.cs">}}


De logica in `GetClaimsForUser()` bevat echter nog veel repetitie en is afhankelijk van de concrete implementatie van de classes die we aanroepen. Om dat probleem aan te pakken, kunnen we gebruik maken van een ander SOLID-principe: het *Dependency inversion* principe.


## Het kan me niet schelen *hoe* je het doet, *als* je het maar doet


Dit principe stelt twee dingen. 


1. Modules op een hoger abstractieniveau moeten onafhankelijk zijn van modules op een lager abstractieniveau. Beide moeten afhankelijk zijn van abstracties, zoals interfaces of baseclasses. 

2. Abstracties moeten onafhankelijk zijn van details. Het is juist andersom: details, in de vorm van concrete implementaties, moeten afhankelijk zijn van abstracties.


(Deze [karakterisering](https://linux.ime.usp.br/~joaomm/mac499/arquivos/referencias/oodmetrics.pdf) van het *Dependency inversion* principe is afkomstig van softwareguru [Robert "Uncle Bob" Martin](http://cleancoder.com/products), wiens [boeken ik van harte aanraad](/blog/21-05-03-de-beste-boeken-over-software-ontwikkeling-die-ik-in-2020-las). Maar ik zal niet liegen: voor deze blog baseer ik me gewoon op de [Wikipediapagina](https://en.wikipedia.org/wiki/Dependency_inversion_principle).)


Dit zijn veel woorden om te zeggen: programmeer tegen een interface aan en niet tegen een concrete class. De reden daarvoor is simpel: als je tegen een interface aan programmeert, kun je de concrete implementatie aanpassen zonder de aanroepende code te hoeven wijzigen.


Hoe verhoudt dit principe zich tot de code hierboven? We kunnen de `ClaimsHelper` zien als een module op hoger abstractieniveau, en de `Read`-, `Write`- en `DeleteClaimProvider` als modules op een lager abstractieniveau. Het probleem wordt dan meteen duidelijk: de eerste heeft nu een afhankelijkheid van de laatste drie.


## Drie classes, één abstractie


Als je de code snippet bekijkt waar deze blog-post mee begon, valt je dan iets op aan de drie methods die we aan hebben gemaakt? 


In wezen doen ze alle drie hetzelfde, namelijk: de claim teruggeven die bij de permission hoort. Dit is een functie van alle drie de methods die de concrete implementatie overstijgt. We zijn op een [abstractie](https://en.wikipedia.org/wiki/Abstraction_(computer_science)) gestuit. Dat gedrag kunnen we vangen in een [interface](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface):


{{< gist notkarlmarx bedb39a5b877fd1fdbc9508e745e8b4f "IProvideClaims.cs">}}


Onze eerder geschetste `ReadClaimProvider` hoeven we maar minimaal aan te passen om aan deze interface te kunnen voldoen:


{{< gist notkarlmarx bedb39a5b877fd1fdbc9508e745e8b4f "ReadClaimProvider.cs">}}


Nu we tegen een interface aan kunnen programmeren, hoeft de `ClaimsHelper` niet meer te weten van concrete methods die de claim van elke individuele permission teruggaven. Hij hoeft alleen maar te weten dat hij met een class te maken heeft die `IProvideClaims` implementeert en daar de method `GetClaim()` van aan te roepen.


De `ClaimsHelper` komt er nu als volgt uit te zien:


{{< gist notkarlmarx bedb39a5b877fd1fdbc9508e745e8b4f "ClaimsHelper.cs">}}


Zoals je ziet, is `GetClaimsForUser()` een stuk opgeschoond. Omdat we niet meer afhankelijk zijn van concrete implementaties, hebben we het oorspronkelijke switch-statement uit de method kunnen abstraheren naar zijn eigen helpermethod met een [switch-expressie](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/switch-expression). 


De oorspronkelijke method hoeft zich alleen nog maar te bekommeren om het verkrijgen van de claim, niet meer om alle concrete manieren waarop die claims verkregen worden. Ook vanuit het perspectief van het *Single-Responsibility* principe is er vooruitgang geboekt: alweer een verantwoordelijkheid minder!


## *What's next?*


Maar helemaal zijn we er nog niet. De `ClaimsHelper` heeft via `GetClaimProvider()` op dit moment nog weet van de concrete implementaties die er van `IGetClaim` bestaan. Hij moet ook wel, lijkt het, want hoe kan `GetClaimsForUser()` ooit de juiste claims aan de rechten van de gebruiker koppelen? Dat bekijken we volgende week. 


Wie tot die tijd graag zelf wil experimenteren, kan de code [via GitHub](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V02/ClaimsHelper.cs) binnenhalen.


## Meer in deze reeks

1. [De casus](/blog/21-04-30-enums-switch-statements-en-solid-1)
2. [Het *Single-Responsibility* principe](/blog/21-05-07-enums-switch-statements-en-solid-2)
3. **Het *Dependency inversion* principe**
4. [Het *Open-closed* principe](/blog/21-05-21-enums-switch-statements-en-solid-4)
5. SOLID en performance (binnenkort)
6. Conclusie (binnenkort)
