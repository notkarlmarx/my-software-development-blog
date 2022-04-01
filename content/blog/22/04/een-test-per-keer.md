---
title: "Eén test per keer"
author: "Karl van Heijster"
date: 2022-04-01T08:06:10+02:00
draft: false
comments: true
tags: ["boeken", "leren", "software ontwikkelen", "test-driven development", "testen", "verandering"]
summary: "Ik hou niet van programmeerboeken die van me vragen dat ik onder het lezen code schrijf. Daar kan zo'n boek niks aan doen, ik houd er nu eenmaal van om een boekje op de bank te lezen, ver weg van mijn laptop. Voor één boek maak ik een uitzondering, en dat is *Learning Test-Driven Development* van Saleem Siddiqui. Dat boek draait namelijk niet om het eindproduct, de code. Het draait om het proces."
---

# Gedachten naar aanleiding van *Learning Test-Driven Development* - Deel 2


*Onlangs las ik* [Learning Test-Driven Development](https://www.oreilly.com/library/view/learning-test-driven-development/9781098106461/) *van [Saleem Siddiqui](https://www.linkedin.com/in/ssiddiqui/). Ik zal met de deur in huis vallen: het boek is een aanrader. Zo erg zelfs, dat ik er wel vier blogs uit wist te persen! Vandaag: over de discipline die TDD vraagt van jou als ontwikkelaar.*


Ik hou niet van programmeerboeken die van me vragen dat ik onder het lezen code schrijf. Daar kan zo'n boek niks aan doen, ik houd er nu eenmaal van om een boekje op de bank te lezen, ver weg van mijn laptop. Voor één boek maak ik een uitzondering, en dat is *Learning Test-Driven Development*.


Dat boek draait namelijk niet om het eindproduct, de code. Het draait om het proces. Test-Driven Development (TDD) is een vaardigheid, een manier van denken en doen die uiteindelijk in je vingers moet gaan zitten. TDD moet zich als het ware als vanzelfsprekend manifesteren wanneer je een programmeertaak op gaat pakken. En dat is iets wat je niet kunt leren door te lezen, dat is iets wat je moet doen.


## Focus


Waarom zeg ik dat? Omdat de theorie van TDD eenvoudig is. Het is niets meer dan het volgen van een simpel stappenplan: schrijf een test (*red*), zorg dat de test slaagt (*green*), en ruim je code op (*refactor*).[^1] De praktijk is moeilijker - veel moeilijker.


TDD is een oefening in terughoudendheid - of nee: in focus. Wie op z'n TDD's software ontwikkelt, zegt expliciet tegen zichzelf: ik ga nu eerst *deze* taak oppakken, en pas daarna *die* taak. *Deze* taak kan het schrijven van een test zijn, of de code implementeren om die te laten slagen, of je code opschonen. Maar het is in elk geval *niet*: alvast de volgende feature implementeren of handige code schrijven "voor straks".


## Denken als code


Je zou kunnen zeggen: TDD is een oefening in denken zoals je code denkt. Je code doet één ding tegelijkertijd. (Ik hoor je denken: en multithreaded code dan? Daarop zou ik willen antwoorden: elke thread doet één ding tegelijkertijd.) Als je programma een regel code uitvoert, dan voert het die regel code uit. Het is niet bezig vooruit te kijken hoe de volgende regel eruit ziet en wat ervoor nodig is om die succesvol te tackelen.


Mensen in het algemeen, en softwareontwikkelaars in het bijzonder, zitten wat minder rechtlijnig in elkaar. Dat is deels onze kracht: het vermogen naar de toekomst te kijken stelt ons in staat rampen te voorkomen. Sterker nog, een aanzienlijk deel van onze taak als softwareontwikkelaar bestaat uit het voorzien van toekomstige problemen en onze code daarop voorbereiden. Wie dat niet doet, schrijft code die zijn nut verliest zodra er maar één kleine aanpassing nodig is.


Maar het kan ook onze zwakte zijn. Door naar de toekomst te kijken - de nabije toekomst, de verre toekomst en zelfs de toekomst die nooit zal komen - lopen we het risico het overzicht te verliezen. We zijn met teveel zaken tegelijkertijd bezig, wat ervoor zorgt dat we code schrijven die vijftien dingen half doet, in plaats van één ding goed.


TDD is een techniek die die situatie tracht te voorkomen.


## *Single responsibility*


TDD legt een ontwikkelaar een [*single responsibility*](/tags/single-responsibility-principe/) op: een test schrijven, een test laten slagen, of je code opruimen - *en niets anders*. Dat betekent niet dat je als softwareontwikkelaar niet meerdere verantwoordelijkheden hebt, het betekent dat je er *nu op dit moment* maar één hebt. Zodra je die hebt afgerond, richt je je op de volgende, niet eerder.


Het is makkelijk om onder het TDD'en terug te glijden in oude gewoonten. Dat doe je bijvoorbeeld als je tegen jezelf zegt: ik zet deze method of class alvast wat generieker op dan nodig is, want ik weet dat ik 'm voor de volgende feature toch aan moet passen. TDD vraagt je om dat te laten. 


TDD vraagt je, ironisch genoeg, precies datgene af te leren wat je normaliter een goede softwareontwikkelaars maakt - opdat je een betere softwareontwikkelaar wordt.


## Discipline


Dat vraagt discipline van een ontwikkelaar, en ik denk dat dat één van de redenen is waarom het zo moeilijk is om ontwikkelaars zover te krijgen TDD te omarmen. Het voelt inefficiënt om code te schrijven waarvan je nu al weet dat deze in de (nabije?) toekomst niet meer zal voldoen. We schrijven liever code die wat generieker is opgezet, zodat we de volgende *use case* er zó in kunnen schuiven.


(Uiteraard negeren we daarbij in ons hoofd alle bugs die we veroorzaken met die werkwijze. Want in ons hoofd introduceren we geen bugs in onze code. - Is dat soms waarom sommige ontwikkelaars ook liever geen tests schrijven?)


Precies om die reden is het zo belangrijk dat *Learning Test-Driven Development* een boek is dat van je vraagt om mee te coderen naarmate je verder leest. Dat is een oefening in het aanleren van een nieuwe gewoonte - en daarbij het afleren van een oude. Je een vaardigheid eigen maken vereist actie - gedisciplineerde actie. En dat begint bij iets kleins als het overtikken van een stukje JavaScript - en dan op de testknop te rammen.


## Meer in deze reeks


1. [Agile en Test-Driven Development](/blog/22/03/agile-en-test-driven-development/)
2. **Eén test per keer**
3. *To polyglot or not to polyglot* [binnenkort]
4. Legacy code en Test-Driven Development [binnenkort]


[^1]: Zie ook deel 1 in deze reeks: [*Agile en Test-Driven Development*](/blog/22/03/agile-en-test-driven-development/)
