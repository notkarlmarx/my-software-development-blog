---
title: "Scheid data ophalen van data manipuleren"
author: "Karl van Heijster"
date: 2022-08-08T10:43:03+02:00
draft: false
comments: true
tags: ["clean code", "refactoren", "single-responsibility principe", "testbaarheid", "testen"]
summary: "Het aantal refactoravonturen (met goede of slechte afloop) dat ik heb beleefd is, inmiddels al lang niet meer op één hand te tellen. In de loop der tijd is een terugkerend fenomeen me opgevallen: code waarin het ophalen van data niet wordt gescheiden van het manipuleren ervan. Laten we dat eens wat nader bekijken."
---

Begrijp me niet verkeerd, ik ben dol op het implementeren van nieuwe features. Maar als er één ding is waar mijn softwareontwikkelaarshartje sneller van gaat kloppen, dan is het 't opschonen van bestaande code: variabelen hernoemen, algoritmen vereenvoudigen, verantwoordelijkheden scheiden - oftewel: refactoren. Alles ondersteund door een goed testsuite, uiteraard!


## Het fenomeen


Het aantal refactoravonturen (met goede of slechte afloop) dat ik heb beleefd is, inmiddels al lang niet meer op één hand te tellen. In de loop der tijd is een terugkerend fenomeen me opgevallen: code waarin het ophalen van data niet wordt gescheiden van het manipuleren ervan. 


Denk je bijvoorbeeld een scenario in waarin er een lijst met *resources* wordt opgehaald uit de database. De individuele *resources* worden vervolgens in een `for each`-loop één voor één gemanipuleerd. Ze worden bijvoorbeeld gemapt naar een ander type, of dienen als input om een andere datastructuur op te bouwen. Vaak komt het in dat proces voor dat de data moet worden verrijkt met informatie uit andere bronnen. Dat kan voor alle data gelden, of voor data die aan bepaalde condities voldoet.


De volgende pseudocode geeft het idee aardig weer:


{{< gist dotkarl eb2b6cc84dd228200ecc277e88bfaded "GetAndMapSimultaneously.cs">}}


Het hoeft niemand die de titel van deze blog heeft gelezen, te verbazen dat ik geen voorstander ben van dit soort code. Hiermee geconfronteerd, slaat mijn hart een slag over. De linkerhelft duikt teleurgesteld ineen om dit soort structuren, de rechterhelft springt een gat in de lucht omdat ik weer aan het refactoren slaan mag.


## Het probleem


Maar laten we eerst een stapje terugzetten. Wat is het probleem van deze code?


Code die verantwoordelijk is voor het ophalen én manipuleren van data, schendt het [*Single-Responsibility Principe*](https://en.wikipedia.org/wiki/Single-responsibility_principle) (SRP). Die code kent namelijk twee verantwoordelijkheden: (1) data ophalen, en (2) data manipuleren. 


Nu hoeft dat niet per se een probleem te zijn, zolang je de code nooit aan hoeft te passen. Maar wanneer dat wel gebeurt - en als je een verstokte refactorfanaat in je team hebt zoals ik, dan *gaat* het gebeuren -, leveren verknoopte verantwoordelijkheden allerlei moeilijkheden op. Het wordt bijvoorbeeld moeiijk om bepaalde functionaliteit naar aparte methods of classes te abstraheren. Die functionaliteit is immers verknoopt met andere verantwoordelijkheden. Een verhuizing zou betekenen: je verhuist ofwel alles, ofwel niets. Maar het hele idee van het abstraheren van bepaalde functionaliteit is nu eenmaal dat het om *bepaalde* functionaliteit gaat!


Om dat soort moeilijkheden verderop in de ontwikkeling van je code base te voorkomen, loont het zich eigenlijk altijd om code zo goed mogelijk te structureren naar het SRP. Maar hoe ver moet je daar in gaan? Want die twee verantwoordelijkheden van de code hierboven kunnen natuurlijk weer uiteenvallen in meerdere deelverantwoordelijkheden. Het ophalen van data kan in de bovenstaande code bijvoorbeeld worden uitgesplitst naar (1a) het ophalen van de `foos` en (1b) het ophalen van de `bars`. En het manipuleren van de data kent ook meerdere stappen: (2a) een nieuw type declareren, (2b) de properties mappen die voor alle objecten gelden, (2c) checken of een bepaalde conditie standhoudt, en (2d) de properties mappen die bij die conditie horen. 


## Wat is één verantwoordelijkheid?


Hoe strikt die deelverantwoordelijkheden gescheiden moeten worden, hangt van een aantal dingen af. Bijvoorbeeld van hun complexiteit. Om de code lees- en onderhoudbaar te houden, kan het zich lonen deze op verschillende plekken - methods, misschien zelfs classes - onder te brengen. 


Het kan ook afhangen van de mate waarin die deelverantwoordelijkheden los van elkaar moeten kunnen evolueren. Het is voor de hand liggend dat de manipulatie van data afzonderlijk moet kunnen worden aangepast van het ophalen ervan. Maar datzelfde kan niet per se gezegd worden van de manier waarop de data gemanipuleerd wordt. Het mappen van `foos` en `bars` naar `SomeType` is één actie. Die actie bestaat weliswaar uit deelstappen, maar die deelstappen hebben op zichzelf weinig betekenis. Ze zijn alleen zinvol binnen de context van het overkoepelende algoritme.


Oftewel, als het op het scheiden van de (a)'tjes en de (b)'tjes in de bovenstaande opsomming aankomt, mag je jezelf als ontwikkelaar best wat speelruimte gunnen. Datzelfde vind ik niet opgaan voor het scheiden van de (1)'tjes en de (2)'tjes. Het ophalen van data en het manipuleren ervan zijn mijns inziens zulke ver uit elkaar liggende verantwoordelijkheden, dat deze eigenlijk altijd gescheiden móeten worden.


## Testbaarheid (1)


Wellicht zijn deze overwegingen wat aan de theoretische kant. Ze bieden in elk geval weinig concrete handvaten. Wat complex is, is bijvoorbeeld afhankelijk van het vaardigheidsniveau van de programmeur. En welke deelverantwoordelijkheden bij elkaar horen en welke los van elkaar moeten kunnen evolueren, wil in de loop van een project wel eens overwacht veranderen. 


Een meer praktische leidraad is deze: code moet zodanig gescheiden worden, dat deze eenvoudig te testen is. Sterker nog, één van de belangrijkste redenen om het SRP te respecteren, is omdat dit makkelijk testbare code oplevert - makkelijker testbaar dan wanneer je het niet doet, in elk geval.


Ga maar na. Stel, je zou het algoritme willen testen die `foos` en `bars` mapt naar `SomeType`, zoals geschetst in de code hierboven. Op dit moment kun je die code niet testen zonder gebruik te maken van de `_repository` - wat dat ook moge zijn. Als dat een concrete implementatie is - *foei!* -, dan heb je een probleem. De code is dan namelijk niet in isolatie te testen. Het testen van het algoritme houdt automatisch ook het testen van de [Repository](https://dotnettutorials.net/lesson/repository-design-pattern-csharp/) in, en dat houdt het testen van de database in. 


Denk je eens in wat er allemaal voor nodig is om die tests aan de gang te krijgen! Je moet een database opzetten en inrichten en deze vullen met testdata, en dat allemaal vóórdat je kunt beginnen aan dat waar het je eigenlijk om gaat: het algoritme testen. Bovendien zal het je tests erg langzaam maken, waardoor je ontwikkelcyclus vertraagd zal worden. Elke keer als je de tests aftrapt, zul je even moeten wachten, wat je als ontwikkelaar uit je *flow* haalt, en je productiviteit vermindert.


## Testbaarheid (2)


Als `_repository` een interface is, kom je er een stuk makkelijker vanaf. Maar dan nog zul je een mock moeten specificeren die *the real deal* simuleert - en ook dat is niet niks. Je zal een mocking library zoals [*Moq*](https://moq.github.io/moq4/) of [*FakeItEasy*](https://fakeiteasy.github.io/) moeten gebruiken, en voor elke test moeten specificeren welk gedrag je van je gemockte `_repository` verwacht. (Over de nadelen van mocks schreef ik al eerder, [hier](/blog/22/02/de-leercurve-van-angulartests-beklimmen-deel-3/).)


Een test zou er met wat hulp van *FakeItEasy* bijvoorbeeld zou uit kunnen komen te zien:


{{< gist dotkarl eb2b6cc84dd228200ecc277e88bfaded "GetAndMapSimultaneouslyTest.cs">}}


Die test werkt, maar is verre van ideaal, natuurlijk. Het gebruik van mocks maakt de test broos. Bovendien vraagt deze opzet veel van de lezer. Door alle code in het `Arrange`-gedeelte van de test, is het moeilijk om in één oogopslag te zien wat de test precies doet. Een overdaad aan *low level*-informatie vertroebelt de intentie van de test.


## De scheiding


Het goede nieuws is: je *hoeft* je verantwoordelijkheden niet met elkaar te verknopen. In de meeste gevallen is het vrij eenvoudig om het ophalen van data te scheiden van het manipuleren ervan. Maar het vraagt wel wat bewustzijn van je als ontwikkelaar. De bovenstaande code kan bijvoorbeeld worden omgeschreven naar iets als dit:


{{< gist dotkarl eb2b6cc84dd228200ecc277e88bfaded "GetAndMapSeparated.cs">}}


De code om de data op te halen, is nu helemaal losgetrokken van de mappingcode. En je ziet: de code is er meteen een stuk eenvoudiger op geworden ook! De check op `SomeCondition` is uit het algoritme verdwenen, bijvoorbeeld. Dat komt doordat deze in wezen gekoppeld was aan de vraag of we de data op moesten halen of niet. Het `if`-statement kon worden omgeschreven naar een `Where`-clausule. 


Hierdoor hoeven we in het algoritme zelf alleen maar de corresponderende `bar` in de al opgehaalde lijst te vinden - of `null` terug te geven wanneer deze niet gevonden kan worden, waarmee we de property effectief niet setten.


## Testbaarheid (3)


Maar de voordelen eindigen nog niet daar. Onze aanvankelijke refactorslag heeft ons in staat gesteld om de `foreach`-loop te kunnen abstraheren naar een nieuwe method. Laten we 'm `ToSomeType` noemen:


{{< gist dotkarl eb2b6cc84dd228200ecc277e88bfaded "Map.cs">}}


Het mooie is nu: deze method valt in isolatie te testen. Het enige wat je moet doen, is wat `foos` en wat `bars` specificeren in je test, en deze meegeven aan die nieuwe method. De volgende test geeft een indruk:


{{< gist dotkarl eb2b6cc84dd228200ecc277e88bfaded "GetAndMapSeparatedTest.cs">}}


Nu weet ik niet hoe het met jou zit, maar als ik moest kiezen tussen een complete database opzetten, uitgebreide mockingcode schrijven, of wat objecten definiëren aan het begin van mijn test - nou, dan wist ik het wel! 


Daarom: scheid het ophalen van data van het manipuleren ervan. Je zal jezelf denkbaar zijn voor de moeite!
