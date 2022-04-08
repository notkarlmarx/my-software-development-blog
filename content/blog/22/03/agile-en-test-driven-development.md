---
title: "Agile en Test-Driven Development"
author: "Karl van Heijster"
date: 2022-03-25T08:32:31+01:00
draft: false
comments: true
tags: ["agile ontwikkeling", "boeken", "leermoment", "refactoren", "test-driven development", "testen", "unit tests"]
summary: "De meeste ontwikkelaars (waaronder ondergetekende!) schrijven als volgt code. Ze bekijken de specificaties en beginnen vervolgens te klungelen. Dat duurt een tijd, totdat ze iets hebben wat werkt. Of dat zo is, verifiëren ze middels handmatige tests. Pas als de code werkt als bedoeld, schrijft men - als het goed is! - een reeks geautomatiseerde tests. Het is een hardnekkig misverstand dat TDD deze praktijk van software schrijven omdraait: eerst de geautomatiseerde tests (meervoud!) schrijven, en dan pas de productiecode. De werkelijkheid ligt wat genuanceerder."
---

# Gedachten naar aanleiding van *Learning Test-Driven Development* - Deel 1


*Onlangs las ik* [Learning Test-Driven Development](https://www.oreilly.com/library/view/learning-test-driven-development/9781098106461/) *van [Saleem Siddiqui](https://www.linkedin.com/in/ssiddiqui/). Ik zal met de deur in huis vallen: het boek is een aanrader. Zo erg zelfs, dat ik er wel vier blogs uit wist te persen! Vandaag: over de overeenkomsten tussen Agile en TDD.*


## Wat is TDD?


De meeste ontwikkelaars (waaronder ondergetekende!) schrijven als volgt code. Ze bekijken de specificaties en beginnen vervolgens te klungelen. Dat duurt een tijd, totdat ze iets hebben wat werkt. Of dat zo is, verifiëren ze middels handmatige tests. Pas als de code werkt als bedoeld, schrijft men - als het goed is! - een reeks geautomatiseerde tests.


Het is een hardnekkig misverstand dat TDD deze praktijk van software schrijven omdraait: eerst de geautomatiseerde tests (meervoud!) schrijven, en dan pas de productiecode. De werkelijkheid ligt wat genuanceerder. 


Het proces van TDD valt uiteen in drie fasen. In de literatuur worden deze aangeduid als *red-green-refactor*-cyclus.


1. *Red*. De ontwikkelaar schrijft een test (enkelvoud!) die faalt.


2. *Green*. De ontwikkelaar schrijft genoeg code om de falende test te laten slagen - en niet meer dan dat.


3. *Refactor*. De ontwikkelaar schoont zijn code op. De eenvoudigst mogelijke code om een test te laten slagen voldoet namelijk maar zelden aan *best practices*. Ze bevat bijvoorbeeld hardgecodeerde variabelen of bevat codeduplicatie of schendt de SOLID-principes.


Een testgedreven ontwikkelaar schrijft dus *afwisselend* tests en productiecode. Eerst een test, dan wat productiecode (gevolgd door wat opschoning), dan weer een nieuwe test. De tests zijn een zich langzaam uitbreidend vangnet die het mogelijk maken steeds een klein beetje meer productiecode te schrijven zonder regressiebugs te introduceren.


## Inefficiënt?


Als klungelende ontwikkelaar (geen veroordeling! - nogmaals: ik ben er zelf ook een) zou je kunnen denken: waarom zou je, test voor test, continu je code willen refactoren? Waarom zou je niet eerst alle unit tests schrijven en dan de code in één keer goed neerzetten? 


Is het niet gruwelijk inefficiënt om eerst zo eenvoudig mogelijke code voor die ene feature (c.q. test) te schrijven, wetende dat ik die daarna toch overhoop mag halen om de volgende feature te kunnen implementeren (c.q. test te laten slagen)?


Dit is geen onterecht vraag. Als we aannemen dat de uitkomst van beide methoden dezelfde is, dan loont het zich te overwegen welke van de twee het doeltreffendst zal zijn. 


## Opleveren


Op dit gebied vertoont TDD een interessante parallel met de Agile manier van software ontwikkelen. Wie Agile ontwikkelt, levert elke feature één voor één op. Het idee daarachter is niet dat deze manier van software oppakken (en ophakken) per se sneller is - ook dat is een veelvoorkomend misverstand. Het idee is dat je sneller *uit kan leveren* naar je klant. 


Ga maar na: je kunt één keer twee maanden doen over twee features, en het hele pakket dan opleveren - of één maand doen over één feature, deze opleveren, en de maand erop de volgende feature opleveren. De totale doorlooptijd is hetzelfde, maar in het tweede geval heb je één maand langer waarde geleverd dan in het eerste geval.


Het mooie van TDD is dat je op een Agile manier kunt ontwikkelen met de zekerheid dat datgene wat je oplevert, ook daadwerkelijk doet wat het moet doen. Je hebt immers voor die ene feature een stel tests geschreven.


Nu wordt ook duidelijk waarom je de tests per feature schrijft, en niet allemaal tegelijk. Het is heel simpel: deze aanpak stelt je in staat om op te leveren. 


Natuurlijk, als je tests had geschreven voor features die nog niet geïmplementeerd zijn, dan kun je *in principe* ook opleveren. Je hebt dan alleen een stel tests die niet slagen - en waarvan je weet dat ze ook niet horen te slagen. Dat is een strategie, maar het is een riskante. Door op deze manier met tests om te gaan, verliest de *test suite* haar waarde als signaalfunctie voor de ontwikkelaar.


## Test voor test, feature voor feature


Er is nog een tweede parallel tussen TDD en Agile - eentje die samenhangt, misschien zelfs wel voortvloeit uit de eerste. Om dat concreet te maken, loont het zich te kijken naar de manier waarop *Learning Test-Driven Development* is opgebouwd.


Het boek is geschreven rondom één centraal probleem, namelijk het schrijven van een programma dat het mogelijk maakt om geld in meerdere munteenheden te beheren. Siddiqui begint met de volgende handvol operaties die het programma aan moet kunnen:


> 1. $5 * 2 = $10
>
> 2. €10 * 2 = €20
>
> 3. ₩4002 / 4 = ₩1000,5
>
> 4. $5 + €10 = $17[^1]
>
> 5. $1 + ₩1100 = ₩2200[^1]


Het programma moet dus, van boven naar beneden, de volgende features ondersteunen: 1. dollars kunnen vermenigvuldigen; 2. diverse munteenheden kunnen vermenigvuldigen; 3. diverse munteenheden kunnen delen (inclusief ondersteuning van breuken); 4. dollars en euro's bij elkaar op kunnen tellen; 5. diverse munteenheden van verschillende soorten 
bij elkaar op kunnen tellen.


Je raadt het al: elke feature krijgt zijn eigen test - aanvankelijk rood, dan groen, gevolgd door een refactorslag. Siddiqui loodst je als lezer test voor test, feature voor feature door dit probleem. Elke keer bouw je zowel de *test suite* als de productiecode een stapje verder uit.


## Feedback


Na elke geslaagde test - of liever: na elke refactorslag na elke geslaagde test - heb je de kans om te pauzeren en te kijken hoe je applicatie ervoor staat. Het is een ideaal moment om de ontwikkeling van je applicatie tegen het licht te houden. En naar die feedback kun je handelen door je prioritering aanpassen.


Dit toont zich ook in de manier waarop Siddiquis lijst van features zich in de loop van het boek ontwikkelt. Aan het eind van hoofdstuk twee van het boek, ziet de lijst er bijvoorbeeld als volgt uit:


> 1. ~~$5 * 2 = $10~~
>
> 2. ~~€10 * 2 = €20~~
>
> 3. ~~₩4002 / 4 = ₩1000,5~~
>
> 4. $5 + €10 = $17
>
> 5. $1 + ₩1100 = ₩2200
>
> 6. Remove redundant `Money` multiplication tests


En aan het eind van hoofdstuk vier:


> 1. ~~$5 * 2 = $10~~
>
> 2. ~~€10 * 2 = €20~~
>
> 3. ~~₩4002 / 4 = ₩1000,5~~
>
> 4. ~~$5 + $10 = $15~~
>
> 5. Separate test code from production code
>
> 6. Remove redundant `Money` multiplication tests
>
> 4. $5 + €10 = $17
>
> 7. $1 + ₩1100 = ₩2200


Enfin, het hoeft geen verrassing te heten dat de featurelijst er aan het eind van het boek helemaal anders uitziet dan aan het begin.


Het schrijven van één test per keer, stelt je in staat om makkelijk met de prioriteiten te schuiven - precies zoals we dat vanuit het Agile ontwikkelparadigma gewend zijn. En dat zonder last te hebben van het gewicht van eerder geschreven falende tests.


## Conclusie


In [*Clean Agile*](https://www.vanduurenmedia.nl/EAN/9789463562393/Clean_Agile_Nederlandse_editie) noemt [Robert C. Martin](http://cleancoder.com/products) TDD een essentiële praktijk om Agile te kunnen ontwikkelen.[^2] Dat is een observatie die ik, na het lezen van *Learning Test-Driven Development*, kan onderschrijven. Agile en TDD vullen elkaar perfect aan, zoveel zelfs dat het lijkt alsof ze aan dezelfde bron zijn ontsproten. Beide gaan uit van stapsgewijze ontwikkeling, wat het mogelijk - en eenvoudig! - maakt om met prioriteiten te kunnen schuiven.


Toch is TDD geen wijdverbreide praktijk in de wereld van softwareontwikkeling - althans niet in dezelfde mate als Agile. Waarom? Daarover gaat het volgende deel in deze reeks.


## Meer in deze reeks


1. **Agile en Test-Driven Development**
2. [Eén test per keer](/blog/22/04/een-test-per-keer/)
3. [*To polyglot or not to polyglot*](/blog/22/04/to-polyglot-or-not-to-polyglot/)
4. Legacy code en Test-Driven Development [binnenkort]


[^1]: Siddiqui neemt, om het voorbeeld simpel te houden, aan dat wisselkoersen niet veranderen. De wisselkoers dollar-euro vast staat op 1.2; die van dollar-won op 1100.


[^2]: *Fun fact*: precies deze observatie zette me ertoe aan Siddiquis boek te gaan lezen. Mijn recensie van *Clean Agile* is [hier](/blog/21/11/agile-zijn-niet-agile-doen/) te lezen.
