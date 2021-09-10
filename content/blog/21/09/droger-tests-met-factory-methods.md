---
title: "Droger tests met factory methods"
author: "Karl van Heijster"
date: 2021-09-10T06:55:36+02:00
draft: false
comments: true
tags: ["clean code", "DRY", "ontwerppatronen", "testen", "unit tests"]
summary: "Ga eens voor jezelf na: hoe instantieer je objecten in je unit tests? Introduceer je veel codeduplicatie over tests heen? Wat zegt dit over je houding tegenover testcode? Is die houding hetzelfde als die tegenover productiecode?"
---

Valt je iets op aan deze tests?


{{< gist dotkarl 864e6132c8b41e97feb97bcde73d4298 "DryUnitTests00.cs">}}


Oké, afgezien van het feit dat ze nogal triviale code testen. En dat de naamgeving (bewust) weinig inhoudelijk is. En dat ik geen gebruik maak van de Microsofts [Assert-class](https://docs.microsoft.com/en-us/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert?view=visualstudiosdk-2019), maar van het (fantastische!) [Fluent Assertions](https://fluentassertions.com/), wat valt je op aan deze tests?


Ik denk dat de meeste mensen hier drie keurig volgens het boekje opgezette unit tests zien. En weet je wat het is: die mensen hebben gelijk, want het *zijn* keurig volgens het boekje opgezette unit tests.


Toch roept deze code irritatie bij mij op. Dat is omdat deze testsuite één van de meest basale principes van softwareontwikkeling schendt: [*DRY*](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), oftewel: *don't repeat yourself*.


Zie je wat ik bedoel?


## Wat is het probleem?


Je zou kunnen stellen dat de bovenstaande vorm van duplicatie redelijk goedaardig is. Wie waarschuwt voor de gevaren van codeduplicatie, heeft meestal de duplicatie van complete stukken logica in het achterhoofd. Dit heeft tot gevolg dat bepaalde kennis verspreid wordt over de codebase. Elke keer als die kennis verouderd raakt, moet de ontwikkelaar de codebase afspeuren naar de diverse plekken waar deze aangepast dient te worden.


Het is waar: het steeds opnieuw instantiëren van nieuwe objecten in een test is minder kritiek dan dat. Maar het is minstens even irritant. Wat gebeurt er bijvoorbeeld, wanneer je de constructor van `SystemUnderTest` aanpast? Dan moet je elke test aanpassen waarin dit object wordt geïnstantieerd. Het schenden van *DRY* leidt tot een toename van *test fragility*.


Dat is een probleem dat toeneemt naarmate je je codebase uitgebreider test. Het werpt een drempel op de goede gewoonte te ontwikkelen je code grondig te testen.


## Waarom doen we dit?


Neem nu even afstand van de bovenstaande code en ga voor jezelf na: schrijf ik mijn tests op dezelfde manier? Dat wil zeggen: instantieer ik in elke method op dezelfde manier dezelfde objecten? 


Begrijp me niet verkeerd, het is niet erg als je dat doet. Ik deed lang genoeg precies hetzelfde. De vraag is alleen: waarom?


Ik kan twee antwoorden op die vraag bedenken. Het eerste is betrekkelijk neutraal, het tweede cynisch. 


## Een neutraal antwoord


Het eerste antwoord is dat dit de manier waarop de meeste mensen het schrijven van unit tests krijgen aangeleerd. Niet voor niets karakteriseerde ik de bovenstaande unit tests als "keurig volgens het boekje." 


Zulke voorbeeldtests worden meestal geschreven in de context van demo-applicaties. Om die reden behoeven ze geen onderhoud, en wordt gedurende het leerproces nooit duidelijk welke nadelen er zitten aan de geïntroduceerde codeduplicatie. 


Wanneer de ontwikkelaar-in-opleiding vervolgens in het werkveld aan de slag gaat, is het leed al geschied. De ontwikkelaar-in-het-werkveld voegt nieuwe tests toe zoals hij of zij dit geleerd heeft, en bij elke nieuwe test wordt de boodschap versterkt: *dit is hoe unit tests eruit horen te zien.*


## Een cynisch antwoord


Het cynischer antwoord is dat veel softwareontwikkelaars weinig waarde hechten aan testcode. Of, minder scherp gesteld: minder waarde hechten aan testcode dan aan productiecode.


In zekere zin snap ik die houding ook wel. Productiecode voegt functionaliteiten toe die businesswaarde levert. Testcode doet dat niet. Softwareontwikkelaars die weinig of minder waarde hechten aan testcode, verabsoluteren het doel om businesswaarde te leveren tot het enige doel van coderen.


Maar als testcode niet als doel heeft businesswaarde te leveren, welk doel heeft het dan? *Testcode heeft als doel de werking van de productiecode te verifiëren.* Of, preciezer: de werking van de productiecode te *blijven* verifiëren. Want één van de belangrijkste redenen om een goede test coverage te hebben, is om regressiebugs te vinden. 


Natuurlijk, je kunt erover steggelen of dat doel op hetzelfde niveau staat als het doel van productiecode. Maar dat tests een waardevol doel vervullen, is mijns inziens onomstotelijk.


## Een cynische ontwikkelaar?


De meest extreme verpersoonlijking van het idee dat unit tests weinig waarde hebben, is die van een softwareontwikkelaar die nooit unit tests schrijft. Zulke ontwikkelaars menen dat ze betaald worden om businesswaarde te leveren in de vorm van toegevoegde functionaliteit, en meer ook niet. Klaarblijkelijk menen ze niet betaald te worden om na te gaan of die toegevoegde functionaliteiten ook (blijven) werken zoals bedoeld.


Gelukkig vormen deze ontwikkelaars een uitstervend ras. Maar ze bestaan - en je wil ze niet als collega hebben.


Het gros van de softwareontwikkelaars dicht ik echter niet zulke cynische motieven toe. Het feit dat zij testcode minder waarderen dan productiecode, komt denk ik eerder voort uit het feit dat ze het *leuker* vinden om de laatste te schrijven dan de eerste. En dat begrijp ik wel. Het is een uitdaging om zo schone, efficiënt mogelijke businesslogica te schrijven. Vergeleken daarbij bestaan unit tests voornamelijk uit saaie *plumbing code*.


De ironie is natuurlijk: wie unit tests keurig volgens het boekje schrijft, precies dát doet: saaie *plumbing code* schrijven. 


## Wat te doen?


Een softwareontwikkelaar die de codekwaliteit van unit tests net zo serieus neemt als die van productiecode, vindt net zulke uitdaging in het schrijven van de eerste als in het schrijven van de laatste.


Nu zal ik niet beweren een expert te zijn in het zo efficiënt mogelijk opzetten van unit tests. Het vinden van betere manieren is voor mij nog altijd een bijna dagelijkse uitdaging. Maar er zijn enkele heel eenvoudige technieken om het soort codeduplicatie zoals hierboven beschreven, te voorkomen. De aller-, aller-, allereenvoudigste daarvan is het gebruik van statische *factory methods*:


{{< gist dotkarl 864e6132c8b41e97feb97bcde73d4298 "DryUnitTests01.cs">}}


Als de constructor van `SystemUnderTest` wordt aangepast, dan hoeft dat nog maar op één plek te gebeuren. En als verschillende tests altijd dezelfde afhankelijkheid verwachten, dan kan deze worden toegevoegd aan de *factory method*, in plaats van de *Arrange*-sectie van diverse tests uit te hoeven breiden met extra informatie. Het abstraheren van zulke informatie naar helpers met een desciptieve naam, zorgt ervoor dat je test goed leesbaar blijft.


De factory methods zijn natuurlijk nog maar stap 1. Naarmate de codebase uitgebreider wordt, loont het zich om deze te verzamelen in zogenaamde [*ObjectMothers*](https://martinfowler.com/bliki/ObjectMother.html). Dat zijn factory classes die speciaal voor testdoeleinden geschreven worden. Zulke classes combineren DRY met het [Single-Responsibility Principe](https://en.wikipedia.org/wiki/Single-responsibility_principle). Ze wijzen de verantwoordelijkheid van het creëren van nieuwe objecten toe aan één plek.


Een andere methode om codeduplicatie te voorkomen en de lees- en onderhoudbaarheid van je tests te vergroten, is door gebruik te maken van [Test Data Builders](http://natpryce.com/articles/000714.html). Dat is een patroon dat al langer op mijn verlanglijstje staat om toe te passen in onze testcode, maar waar ik tot mijn grote spijt nog steeds niet aan toegekomen ben. Wellicht in een volgende blog...?


Hoe kijk jij naar de verhouding tussen productiecode en testcode? En wat doe je om de onderhoudbaarheid van je testcode te vergroten?
