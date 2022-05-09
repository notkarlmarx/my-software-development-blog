---
title: "Nóg een reden om testgedreven te ontwikkelen"
author: "Karl van Heijster"
date: 2022-05-09T07:21:45+02:00
draft: false
comments: true
tags: ["boeken", "clean code", "intentie van code", "test-driven development", "testen"]
summary: "Als je mij zou vragen: *waarom zou je testgedreven ontwikkelen?* dan zou ik zeggen: *zodat je tests hebt*. Maar in *The Art of Agile Development* van James Shore vond ik een andere reden. Test-Driven Development dwingt je na te denken hoe het is een stuk code te *gebruiken*, in plaats van het te implementeren. Het vraagt je om helder te krijgen: hoe kan ik deze functionaliteit zo goed mogelijk ontsluiten, in plaats van: hoe kan ik deze functionalteit zo goed mogelijk bouwen?"
---

Als je mij zou vragen: *waarom zou je testgedreven ontwikkelen?* dan zou ik zeggen: *zodat je tests hebt*.


Dat antwoord is verwant met waarom sommige teams *mobile first* ontwikkelen. Dat doen ze niet per se omdat de meeste van hun gebruikers hun applicatie via een mobiel apparaat benaderen - al neemt het verkeer via zulke apparaten al jaren gestaag toe. Een goede reden om *mobile first* te ontwikkelen is *om de ondersteuning van mobiele apparaten te garanderen*. 


## Vergeten


Wie dat niet doet, blijkt halverwege het project namelijk nogal eens te zijn vergeten dat er ook nog zoiets als mobiele gebruikers bestaan. Het gevolg is dat een significant deel van de doelgroep zich ofwel moet behelpen met een op desktop gebaseerde applicatie, ofwel genoegen moet nemen met een mobiele variant die overduidelijk aan de laatste ontwikkelmem hing.


Met [Test-Driven Development](/tags/test-driven-development/) (TDD) werkt het ongeveer hetzelfde. Als je het nalaat, blijkt de testcoverage van je code halverwege het project plots ondermaats te zijn. Daarmee boor je jezelf die gemoedelijke refactorslag door de neus die de weg vrijbaande naar een volgende feature. Het aanpassen van de applicatie wordt een moeizaam proces, het design van de code begint te geuren en het aantal bugs blijft maar toenemen.


Goede geautomatiseerde tests zijn dé manier om je ontwikkelsnelheid over langere periode op peil te houden. TDD is dé manier om een goede testcoverage van je applicatie te garanderen. Daarom zou je aan de TDD moeten (hoe [moeilijk het ook is dat in je systeem te krijgen](/blog/22/04/een-test-per-keer/)!).


## Nóg een reden


In [*The Art of Agile Development*](https://www.oreilly.com/library/view/the-art-of/9780596527679/) van [James Shore](https://www.jamesshore.com/) vond ik een andere reden om aan TDD te doen. TDD dwingt je na te denken hoe het is een stuk code te *gebruiken*, in plaats van het te implementeren. Het vraagt je om helder te krijgen: hoe kan ik deze functionaliteit zo goed mogelijk ontsluiten, in plaats van: hoe kan ik deze functionalteit zo goed mogelijk bouwen?


Anders gezegd: het dwingt je éérst na te denken over de interface van je code, en pas daarna over haar implementatie.


Het is niet zo dat ontwikkelaars nooit op deze manier over code nadenken. Een goede ontwikkelaar denkt bewust na over de manier waarop bepaalde functionaliteit binnen het totale ontwerp van een applicatie past, en past zijn implementatie daarop aan. Maar ook goede ontwikkelaars hebben wel eens mindere dagen. En ik denk dat elke ontwikkelaar ten minste één keer (ik druk me voorzichtig uit) code heeft gelezen én geschreven waarvan de interface werd bepaald door de implementatie.


## Boodschap


Dat kan zich uiten in zogenaamde [*leaky abstractions*](https://en.wikipedia.org/wiki/Leaky_abstraction), interfaces die weggeven welke datastructuren en algoritmen er onder de motorkap worden gebruikt. - Maar dat is nog een peulenschil bij de interfaces van sommige *legacy* systemen. Deze bestaan uit handenvol methods die weinig met elkaar te maken lijken te hebben. Een class is in zulke systemen vaak een vergaarbak geworden van allerlei code die elkaar aanroept, maar naar buiten toe geen duidelijke boodschap communiceert.


En het laat zich raden waarom: er is nooit over die boodschap nagedacht, laat staan over de manier waarop ze gecommuniceerd wordt. Er is nagedacht over hoe de code in werkende staat te krijgen - en meer niet.


Maar als jij eerst een test schrijft, dan is er nog geen implementatie die de boodschap kan vertroebelen - er is alleen nog een boodschap. Op basis van die boodschap maak je een interface. Op basis van de test die de boodschap formaliseert, schrijf je een implementatie. - En op basis van het nieuwe inzicht dat elke test je in de code geeft, refactor je de implementatie. Waarbij je de interface over het algemeen met rust zou moeten kunnen laten, want daar heb je over nagedacht zonder je druk te maken om de implementatie.


TDD werpt zo een licht op dat wat een zuivere focus op implementatie vertroebelt. De intentie die je met code communiceert, is minstens zo belangrijk als dat wat de code daadwerkelijk doet. - Hoe vreselijk is het wanneer die twee niet in elkaars verlengde liggen! 
