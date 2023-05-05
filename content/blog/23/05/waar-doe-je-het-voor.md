---
title: "Waar doe je het voor?"
author: "Karl van Heijster"
date: 2023-05-05T08:49:03+02:00
draft: false
comments: true
tags: ["bloggen", "clean code", "documentatie", "luie programmeur", "refactoren", "test-driven development", "testen", "verantwoordelijkheid", "werkplezier"]
summary: "Een luie programmeur grijpt alles aan om zijn eigen werk makkelijker te maken (met uitzondering van het besparen op kwaliteit - daar is een andere term voor: een *slechte programmeur*). En makkelijker maken betekent meestal: automatiseren. Want waarom zou je zelf het werk doen, als een machine het ook voor je kan doen?"
---

Een tijd terug gaf ik een presentatie bij usergroup [*Nimma.Codes*](https://www.meetup.com/nimma-codes-meetup-group/events/287692035/) - en met veel plezier.[^1] Wat blijkt: als je af en toe een grapje maakt, dan kun je mensen best drie kwartier wakker houden met gezemel over tests en documentatie.


Maar daar wil ik het niet over hebben. Ik wil het hebben over een gesprek dat ik had voor aanvang van de presentatie, met front-end developer [Bram Doppen](https://www.linkedin.com/in/bramdoppen/), op dat moment een gloedjenieuwe aanwinst voor de organisatie van *Nimma.Codes*. We spraken over zijn werk als interactiedesigner en hoe hij plezier haalde uit het verzinnen van oplossingen waar eindgebruikers écht wat aan hebben. 


We hadden het ook over waar *ik* plezier uit haal, en ik kwam erachter dat mijn motieven een stuk minder hoogdravend zijn. 


Ik hou ervan mijn eigen werk zo makkelijk mogelijk te maken.


## Makkelijker


Dat is waarom ik blogs schrijf over [tests als documentatie](/blog/22/09/tests-als-documentatie/), bijvoorbeeld. Of [*pull requests* als documentatie](/blog/22/10/pull-requests-als-documentatie/). Of [documentatie als documentatie](/blog/22/09/collegiale-documentatie/). Als er is opgeschreven waarom iets op een bepaalde manier is opgezet, dan bespaart me dat het denkwerk dat opnieuw uit te vogelen.


Dat is waarom ik schrijf over [*clean code*](/tags/clean-code/) in het algemeen, en [Test-Driven Development](/tags/test-driven-development/) en [refactoren](/tags/refactoren/) in het bijzonder. Als ik, [met tests als stevig vangnet](/blog/22/09/tests-als-vangnet/), een codebase steeds een klein beetje op kan schonen, dan heb ik de volgende feature des te sneller af.


En het is ook [waarom ik überhaupt blogs schrijf](/blog/21/08/vijf-voordelen-van-bloggen/). Elke blog is een oefening in het redeneren over code - en de manier waarop we code schrijven. Hoe beter ik erover kan redeneren, hoe makkelijker het wordt om fouten te herkennen en te voorkomen. En - dat is het fijne aan geschreven tekst -, ik hoef al die lessen niet eens te onthouden.


(Op [FutureTech](https://futuretech.nl/) in Utrecht, woonde ik een hartstikke leuke sessie bij over de verschillende manieren waarop [ChatGPT](https://chat.openai.com/auth/login) je als ontwikkelaar kan ondersteunen. Maar toen werd gesuggereerd dat je AI ook kunt gebruiken om blogs te schrijven, voelde ik een haast fysieke weerstand bij me opkomen. Het hele idee van bloggen is - als je het mij vraagt althans - nu juist dat je voor jezelf helderheid creëert over het onderwerp waar je over schrijft. AI kan de output wel vervangen, maar niet het verkrijgen van een beter begrip.)


## Lui


Het constant willen vereenvoudigen van je eigen werk heeft een sterke link met het idee van de *luie programmeur*. Een luie programmeur grijpt alles aan om zijn eigen werk makkelijker te maken (met uitzondering van het besparen op kwaliteit - daar is een andere term voor: een *slechte programmeur*). En makkelijker maken betekent meestal: automatiseren. Want waarom zou je zelf het werk doen, als een machine het ook voor je kan doen?


Unittests zijn een automatisering van alle handelingen die ervoor nodig zijn om het systeem in een bepaalde staat te brengen, een actie uit te voeren en te checken of dat het juiste resultaat had. Gerefactorde code is een automatisering van een nieuw inzicht dat je op hebt gedaan over de code - in de code zelf, nota bene. En schriftelijke documentatie is een automatisering van kennisoverdracht. In plaats van die overdracht elke keer opnieuw *face to face* te doen, kun je alle relevante informatie één keer vastleggen en iemand in het vervolg daar naar verwijzen. 


De term "luie programmeur" is bewust prikkelend, natuurlijk. Want het automatiseren van sommige taken kan een enorme inspanning vragen. In hun inspanning om hun eigen werk makkelijker te maken, kunnen luie programmeurs zich dus absoluut geen luiheid veroorloven.


## Verbeteren


Je hebt eigenlijk twee soorten luiheid, bedenk ik nu. 


Destructieve luiheid is je verantwoordelijkheid verzaken. Het is het testen achterwege laten omdat je die bugfix snel naar productie wil brengen - [met alle gevolgen van dien](/blog/22/10/de-fix-die-productie-om-zeep-hielp/).


Constructieve luiheid is iets heel anders. Wie constructief lui is, neemt wél de verantwoordelijkheid op zich om te verbeteren - maar is ook van mening dat dat op termijn niet tot extra werklast mag leiden. Het is unittest na unittest na unittest schrijven - omdat je weet: als die er eenmaal zijn, dan breng ik alle inspanning die ervoor nodig is om te erachter te komen of de applicatie werkt, terug tot één druk op de knop.


Ja, weet je, daar doe ik het wel voor. 


Als ik eerlijk ben, zijn blije eindgebruikers voor mij eerder bijvangst. Maar van die bijvangst worden teamgenoten die meer op Bram lijken dan weer blij, en dat is ook wat waard. 


Waar doe jij het voor?


[^1]: [Marlou de Ridder](https://nl.linkedin.com/in/marlou-de-ridder-54733010b) van [Rootnet](https://www.rootnet.nl/) - waar de Meet-up plaatsvond - schreef er nog [een leuke blog](https://www.rootnet.nl/blogs/meetups/nimma-codes/) over. Op [mijn eigen LinkedIn](https://www.linkedin.com/in/karl-van-heijster-833503aa/) was ik wat spaarzamer met mijn woorden: ["Het was leuk!"](https://www.linkedin.com/posts/karl-van-heijster-833503aa_hoe-test-%C3%A9n-documenteer-je-een-systeem-in-activity-7037375109216526336-Es9r?utm_source=share&utm_medium=member_desktop)
