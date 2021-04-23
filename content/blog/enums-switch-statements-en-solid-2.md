---
title: "Enums, Switch Statements en SOLID - Deel 2"
date: 2021-04-23T13:49:53+02:00
draft: true
comments: true
tags: ["clean code", "enums", "single-responsibility principe", "SOLID", "switch statements", "refactoren"]
---

# Het *Single-Responsibility* principe


[Vorige week](/blog/enums-switch-statements-en-solid-1) liet ik een stuk code zien dat op verschillende manieren de SOLID-principes schond. Deze week gaan we een eerste stap zetten deze code te refactoren om hem wat makkelijker onderhoudbaar te maken. 


We beginnen ons SOLID-avontuur met de S van [*Single-Responsiblity* principe](https://en.wikipedia.org/wiki/Single-responsibility_principle) (SRP). Het SRP stelt dat een software-entiteit moet maar één reden hebben om te worden aangepast, of, met andere woorden, precies één verantwoordelijkheid hebben.


Dit is in zekere zin zowel het eenvoudigste als het belangrijkste principe om in je dagelijkse ontwikkelpraktijk te integreren. 


(Ik stel me graag voor dat dit ook de reden is waarom hij helemaal vooraan staat in de afkorting, maar de waarheid ligt waarschijnlijk bij het feit dat "LOSID" of "DILOS" een stuk minder pakkend is. "DISOL" klinkt wel weer cool, maar helaas niet erg duurzaam.)


## Hoe minder verantwoordelijkheid, hoe beter


Waarom is het SRP zo belangrijk? Omdat code die meerdere verantwoordelijkheden tegelijk heeft, ontzettend snel ontzettend moeilijk wordt om te volgen. 


Je kunt je ook wel voorstellen waarom. Probeer eens van duizend in stappen van drie terug te tellen naar nul. Probeer dat nu eens terwijl je een pen balanceert op het puntje van je vinger. Probeer dat nu eens terwijl je een afspraak probeert te maken bij de tandarts.


Al die taken zijn op zichzelf genomen niet bijzonder complex. Maar allemaal tegelijkertijd zijn ze onmogelijk uit te voeren.


Wie veel dingen tegelijkertijd probeert te doen, legt een grote cognitieve last op zichzelf om verschillende ballen tegelijkertijd in de lucht te houden. Het is moeilijk die last te blijven dragen. Op een gegeven moment laat je een bal vallen. Wie teveel tegelijk doet, zal onherroepelijk fouten maken.


Met code is het niet anders. Wie code schrijft (of leest, of debugt, of refactort...) die veel tegelijk doet, zal dingen over het hoofd zien en bugs introduceren. En alsof dat nog niet vervelend genoeg is, maakt de complexe aard van zulke code het moeilijk om de bug op te sporen.


## SRP bij hoog en bij laag


Een tweede reden waarom het zo belangrijk het SRP te internaliseren, is dat het op vrijwel alle abstractieniveaus kan worden toegepast. In de definitie wordt niet voor niets van het generieke "software-entiteit" gesproken. 


Methods zouden maar één verantwoordelijkheid moeten hebben. Datzelfde geldt voor classes. En je zou hetzelfde ook kunnen stellen voor modules. De traditionele verdeling van software in [drie lagen](https://en.wikipedia.org/wiki/Multitier_architecture#Three-tier_architecture) - user interface, businesslogica en datatoegang - is een toepassing van het SRP op [architectureel](https://en.wikipedia.org/wiki/Software_architecture) niveau. Zelfs voor complete applicaties geldt: liever een die één probleem goed oplost, dan een die een heleboel problemen half oplost.


Natuurlijk hebben al die entiteiten niet één verantwoordelijkheid op hetzelfde niveau. Een goed geschreven method is alleen verantwoordelijk voor zoiets simpels als het optellen van twee getallen. Een class voor het [encapsuleren](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) van alle eenvoudige rekenkundige operaties (waaronder de genoemde method). Een module voor het herbergen van rekenkundige operaties in het algemeen. En zo verder, enzovoort.


Wie het SRP serieus neemt, schrijft code die makkelijk te begrijpen is en logisch gegroepeerd is.


## De code


Dus: welke verantwoordelijkheden kunnen we allemaal in deze code onderscheiden?


{{< gist notkarlmarx c8d96422d63e6cd7165e19a4fb243886 "ClaimsHelper.cs">}}


De verantwoordelijkheid van de class als geheel beperkt zich tot één ding: het teruggeven van een string-representatie (claims) van de rechten (`Permissions`) van de gebruiker (`User`). Dat is alvast goed nieuws: de class hoeft dus niet in tweeën te worden gesplitst omdat deze twee verschillende verantwoordelijkheden herbergt.


Het probleem is echter dat de class ook maar één method kent: `GetClaimsForUser()`. Om te zien welke verantwoordelijkheden deze method heeft, is het verstandig om na te gaan onder welke omstandigheden deze aangepast zou moeten worden.


* De inleidende tekst moet worden gewijzigd.
* Eén of meerdere nieuwe rechten moeten worden toegevoegd aan de enum, of juist een verwijderd.
* De claim van één of meerdere van de rechten moet worden veranderd.


Kun je nog meer redenen bedenken waarom de method aangepast zou moeten worden?


## Een stap in de goede richting


Laten we met het laatste punt beginnen. Het is de verantwoordelijkheid van `GetClaimsForUser()` de claim ergens vandaan te halen. De inhoud van een claim is dat niet. Deze kan dus geabstraheerd worden naar een aparte method.


We zouden een nieuwe method kunnen schrijven met daarin opnieuw een switch-statement, maar daarmee zouden we het probleem alleen maar verplaatsen. Beter zou zijn om de logica voor het ophalen van de claim voor elke `Permission` in een aparte method te plaatsen. Op die manier kun je er zeker van zijn dat die ene method alleen maar aangepast hoeft te worden als de claim van die ene specifieke `Permission` wijzigt.


De code komt er dus als volgt uit te zien (voor de leesbaarheid heb ik irrelevante zaken als de [class-declaratie](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes#declaring-classes) weggelaten):


{{< gist notkarlmarx 8d1b1346a9b21306e5f128fbd5602fec "ClaimsHelper.cs">}}


## *What's next?*


We hebben een stap in de goede richting gezet, maar de winst is bescheiden. `GetClaimsForUser()` hoeft niet meer aangepast te worden wanneer één of meerdere claims moeten worden aangepast, maar de class als geheel nog wel. 


Er moet dus een manier gezocht worden om de `ClaimsHelper` te isoleren deze wijziging. Hoe? Dat bespreken we volgende week. Voor wie tot die tijd graag zelf wil experimenteren, kan de code [via GitHub](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V01/ClaimsHelper.cs) binnenhalen.


## Meer in deze reeks

1. [Inleiding en SOLID principes](/blog/enums-switch-statements-en-solid-1)
2. **Het *Single-Responsibility* principe**
