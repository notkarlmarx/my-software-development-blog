---
title: "Wat zegt deze test?"
author: "Karl van Heijster"
date: 2024-06-28T10:11:35+02:00
draft: true
comments: true
tags: []
summary: "\"Wat zegt deze test?\" -- Het meest voor de hand liggende antwoord is natuurlijk: wat de code doet. Maar dat is slechts wat een test *expliciet* zegt, de informatie die een test *inhoudelijk* overbrengt. Dat is niet het enige wat het zegt -- verre van."
---

"Wat zegt deze test?" -- Het meest voor de hand liggende antwoord is natuurlijk: wat de code doet. Of, preciezer: *gegeven* deze omstandigheid, *wanneer* deze code wordt uitgevoerd, *dan* zal dat dit tot gevolg hebben. (Wat je overigens ook uitstekend in de naamgeving van een test terug kunt laten komen, zie [deze blog](/blog/22/09/tests-als-documentatie/ "'Tests als documentatie'").)


Tests zijn uitvoerbare requirementsspecificaties (zie ook [deze blog](/blog/22/12/tests-zijn-specs/ "'Tests zijn specs'")). In tests is vastgelegd wat de [requirements](https://www.karlvanheijster.com/tags/requirements/ "Blogs met de tag 'requirements'") van een systeem zijn -- en ze gaan na of het systeem inderdaad aan die requirements voldoet.


Tests zijn een vorm van [documentatie](/tags/documentatie/ "Blogs met de tag 'documentatie'") -- en een verdomd handige vorm daarvan, want het is de enige vorm van documentatie die onmiddellijk een signaal geeft wanneer ze verouderd is.


## Belangrijk


Maar dat is slechts wat een test *expliciet* zegt, de informatie die een test *inhoudelijk* overbrengt. Dat is niet het enige wat het zegt -- verre van.


"Wat zegt deze test?" -- Een test zegt: deze code is belangrijk. Immers: niet alle onderdelen van een systeem zijn deel van de requirements ervan -- niet alle onderdelen zouden er deel van *moeten* zijn. Niet elk deel van de code is het waard om gedocumenteerd te worden.


Sommige delen van de code zijn implementatiedetails -- *slechts* implementatiedetails. Sterker nog, het overgrote deel van een codebase bestaat uit implementatiedetails. Die code brengt een bepaald gedrag tot stand. Maar *hoe* ze dat gedrag tot stand brengen, is oninteressant. (Dat wil zeggen: voor een gebruiker van de code. Voor iemand die een codebase probeert te doorgronden, bijvoorbeeld om hem aan te passen, kan het daarentegen razendinteressant zijn!) 


Implementatiedetails hoeven niet in tests gevat te worden. Reserveer tests voor de belangrijke delen van de code. (Ik behandel dit punt uitgebreid in [deze](/talks/altijd-up-to-date-documentatie-met-maximaal-descriptieve-tests/ "'Altijd up to date documentatie met maximaal descriptieve tests'") en [deze talk](/talks/de-edele-kunst-van-het-pull-request/ "'De edele kunst van het pull request'").)


## Veranderen


Maar wat zijn dan die belangrijke delen? -- Dat zijn de interfaces, de API's. Het zijn de delen van de code die een bepaalde functionaliteit ontsluiten -- voor de eindgebruikers, of voor andere delen van de code (in het geval van herbruikbare componenten).


Het zijn de stabiele delen van de code, de delen die niet eenvoudig kunnen worden aangepast omdat andere delen van de code erop rekenen. Ze vertrouwen op (de integriteit van) het contract dat in de interface is gespecificeerd.


"Wat zegt deze test?" -- De test zegt: dit deel van de code mag *niet* veranderen. Of liever: niet *zomaar* veranderen. Want een wijziging in dit deel van de code signaleert een wijziging in requirements, of heeft (in het geval van herbruikbare componenten) een grote impact op de codebase. 


Tests fixeren een deel van de codebase. (Ik ontleen de formulering aan [dit praatje](https://www.youtube.com/watch?v=fsvRXOADWnw "'Fixing Design with Tests - Michael Feathers, R7K Research & Conveyance | Craft Conference, 2023'") van [Michael Feathers](https://michaelfeathers.silvrback.com/).)


## Refactoren


De andere kant van die munt is: de delen van de code die niet direct getest worden, de implementatiedetails, die mogen *wel* veranderen. Sterker nog, ze *moeten* regelmatig veranderen om nieuwe functionaliteit mogelijk te maken.


[Refactoren](/tags/refactoren/ "Blogs met de tag 'refactoren'") is niet iets wat je plant, waar je een Sprint (of twee, of drie) voor reserveert. Wanneer teams refactorings plannen, dan is dat een teken dat ze ofwel hun plicht hebben verzuimd de codebase te onderhouden terwijl ze nieuwe features toevoegen, of een teken dat ze hun code niet onder controle hebben.[^1] Het is een teken dat ze niet hebben begrepen dat het hun taak was hun software *soft* te houden.


Eén van de belangrijkste redenen om tests te hebben, is te om te kunnen refactoren -- om de structuur aan te kunnen passen zodat er nieuwe functionaliteit kan worden gevoegd *zonder* dat je daarbij regressiebugs introduceert.


## Zorg


"Wat zegt deze test?" -- Dus ook: aan deze codebase wordt [zorg](/tags/zorg/ "Blogs met de tag 'zorg'") besteed. De ontwikkelaars die aan deze code werken willen hun werk veilig en efficiënt kunnen doen. 


Of liever: de afwezigheid van een test, zegt dat er *onvoldoende* zorg aan de codebase wordt besteed. Het zegt misschien dat het team een bepaald volwassenheidsniveau nog niet heeft bereikt, of heeft toegegeven aan druk om een feature snel naar productie te brengen. Het zegt: wij als team staan niet in voor de kwaliteit van ons werk -- niet voor dit deel althans.


Maar dat dit volgt uit de afwezigheid van tests, maakt niet *per se* dat de aanwezigheid van tests voldoende zorg signaleert. Niet elke testsuite is gelijk geschapen. Het is niet ongewoon om te zien dat de ergste [technische schuld](/tags/technische-schuld/ "Blogs met de tag 'technische schuld'") in een codebase zich bevindt in de testsuite -- nota bene hét instrument om technische schuld mee te beteugelen. 


Wat zegt zo'n testsuite? -- Dat de ontwikkelaars tests als tweederangsburgers zien. En dat zegt opnieuw: we staan niet in voor de kwaliteit van ons werk.


## Kwaliteit


Ik heb, tijdens het [spreken](/public-speaking/) over het belang van goede tests (met name [hier](/talks/altijd-up-to-date-documentatie-met-maximaal-descriptieve-tests/ "'Altijd up to date documentatie met maximaal descriptieve tests'"), [hier](/talks/waarom-testers-code-moeten-reviewen/ "'Waarom testers code moeten reviewen'") en [hier](/talks/testen-een-filosofisch-retrospectief/ "'Testen: Een filosofisch retrospectief'")), wel eens het vermoeden opgeworpen dat je de kwaliteit van een codebase af kunt lezen van de kwaliteit van de tests. En het verband is voor de hand liggend: als de tests een teken van kwaliteitsbewustzijn zijn, en als de tests zelf van hoge kwaliteit zijn, dan signaleert dat een kwaliteitsbewustzijn in het kwadraat.


Maar zelfs al is de "echte" code, de productiecode, niet in een geweldige staat, dan zorgen tests ervoor dat die gedegradeerde status van de codebase niet lang aan hoeft te houden -- precies omdat ze ontwikkelaars in staat stellen hun code veilig te refactoren.


En dat is waarom *ontwikkelaars* [verantwoordelijk](/tags/verantwoordelijkheid/ "Blogs met de tag 'verantwoordelijkheid'") moeten zijn voor het onderhouden van de tests, niet *de tester* of -- God verhoede -- een apart QA-team. Een van ontwikkelaars losgetrokken testsuite zegt: deze organisatie heeft softwareontwikkeling niet begrepen.


[^1]: Maar het loont zich niet dogmatisch te zijn op dit punt. In sommige gevallen, bijvoorbeeld bij grootscheepse architectuurwijzigingen, is het verstandig om de refactoring apart op de backlog te definiëren -- *naast* het gebruikelijke werk. Het punt is: wanneer een refactoring *alle* tijd opslokt in een Sprint, dan is er in een eerder stadium iets misgegaan.
