---
title: "Zelfs de testpiramide is niet meer heilig!"
author: "Karl van Heijster"
date: 2022-07-04T07:47:43+02:00
draft: false
comments: true
tags: ["boeken", "domain-driven design", "domeinmodel", "end to end tests", "integratietests", "leermoment", "ontwerppatronen", "software architectuur", "test-driven development", "testen", "testpiramide", "teststrategie", "unit tests", "waarde"]
summary: "Ik ben altijd in de veronderstelling geweest dat mijn geautomatiseerde tests een piramidevormige verhouding tot elkaar zouden moeten hebben: aan de basis enorm veel unittests, in het midden een goede hoeveelheid integratietests, en aan de top een bescheiden aantal *end to end* (E2E) tests. Totdat ik *Learning Domain-Driven Design* van Vlad Khononov las. (Een aanrader, overigens!)"
---

Ik ben altijd in de veronderstelling geweest dat mijn geautomatiseerde tests deze verhouding tot elkaar zouden moeten hebben:


{{<figure src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/54/The_test_automation_pyramid.png/1024px-The_test_automation_pyramid.png" alt="testpiramide">}}


Jawel, de welbekende [testpiramide](https://martinfowler.com/articles/practical-test-pyramid.html). Met aan de basis enorm veel [unittests](/tags/unit-tests/), in het midden een goede hoeveelheid [integratietests](/tags/integratietests/), en aan de top een bescheiden aantal [*end to end* (E2E) tests](/tags/end-to-end-tests/).[^1]


## Feedback


Waarom deze opzet? Unittests zijn snel en testen geïsoleerde stukken code. Ze zijn dus makkelijk af te trappen om te controleren of je iets tijdens het ontwikkelen van je applicatie hebt gesloopt. Op die manier krijg je snelle feedback, zonder dat je [flow](/tags/the-zone/) er onder hoeft te lijden. 


Integratietests zijn al wat langzamer, waardoor ze minder geschikt zijn als continue metgezel tijdens het programmeren. En E2E-tests zijn zo langzaam, dat je ze eigenlijk alleen aftrapt wanneer je je codewijzigingen af meent te hebben gerond.


Alle drie de soorten tests hebben hun waarde, en horen daarom ook alle drie thuis in een goede testsuite. Maar de vuistregel luidde altijd: meer unittests dan integratietests, en meer integratietests dan E2E-tests.


## Drie domeinen, drie complexiteiten


Totdat ik [*Learning Domain-Driven Design*](https://www.oreilly.com/library/view/learning-domain-driven-design/9781098100124/) van [Vlad Khononov](https://vladikk.com/) las. (Een aanrader, overigens!)


In dat boek bespreekt Khononov enkele [architecturele ontwerppatronen](https://en.wikipedia.org/wiki/Architectural_pattern) die passen bij de drie soorten [strategische subdomeinen](/blog/22/06/de-ontdekking-van-strategische-subdomeinen/) die er in [Domain-Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design) (DDD) worden onderscheiden. Bij een generiek of ondersteunend domein hoort een relatief eenvoudige architecturele oplossing, zoals een [*Transaction script*](https://martinfowler.com/eaaCatalog/transactionScript.html) of [*Active record*](https://www.martinfowler.com/eaaCatalog/activeRecord.html). Bij een kerndomein is het verstandiger om complexere patronen te introduceren, zoals een ([*event sourced*](https://martinfowler.com/eaaDev/EventSourcing.html)) [*Domain model*](https://martinfowler.com/eaaCatalog/domainModel.html).


De reden daarvoor laat zich raden. Generieke en ondersteunende domeinen zijn doorgaans eenvoudiger dan kerndomeinen. Ze kennen minder complexe businesslogica en hoeven daarom niet zelf complex van aard te zijn.[^2] Software hoort zo complex te zijn als het de businessvraag vereist - en niet complexer. Wie een oplossingsdomein opbouwt dat complexer is dan het probleemdomein vereist, voegt de zo gevreesde [accidentele complexiteit](https://en.wikipedia.org/wiki/No_Silver_Bullet#Summary) toe aan een project. Het gevolg is dat je veel ontwikkeltijd verspilt aan software die relatief weinig waarde toevoegt.


## Testpiramides en testdiamanten


Wat heeft dit met de testpiramide te maken? Nou, niet elk architectureel patroon vraagt om dezelfde teststrategie. En ook dat heeft weer te maken met de complexiteit van de software.


Als je een complexe applicatie bouwt voor een complex businessvraagstuk, dan volgt daar haast automatisch uit dat er sprake is van veel businesslogica. En om die goed te kunnen testen, heb je veel unittests nodig. Anders gezegd: een rijk domeinmodel is bij uitstek geschikt om met unittests te valideren.


Maar als je een eenvoudige applicatie bouwt voor een eenvoudig businessvraagstuk, dan gaat die vlieger niet op. Een [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)-applicatie, opgebouwd volgens *Transaction script*-patroon, kent nauwelijks logica. Het is dan ook onlogisch om hier een gigantische hoeveelheid unittests voor te schrijven. Je hoeft alleen maar te valideren dat wat je erin stopt, ook in de database terechtkomt. Dat is bij uitstek iets wat met E2E-tests kan worden afgevangen. 


Dat betekent dus dat de testpiramide hier een andere vorm krijgt. Geheel tegen de conventionele wijsheid in, leveren E2E-tests in dit geval de meeste waarde, en unittest de minste. Het gevolg is dat de verhouding tussen de geautomatiseerde tests een piramidevorm aanneemt - maar dan omgekeerd! 


Een applicatie die volgens het *Active record*-patroon is gebouwd, houdt het midden tussen deze twee uitersten. De logica is hier verspreid over een service- en businesslogicalaag. Om dit af te testen, heb je vooral integratietests nodig. De testpiramide verandert hier dus in een testdiamant: veel integratietests, en een bescheiden hoeveelheid unit- en E2E-tests.


## Mijn eerste testgedreven stapjes


Khononovs subdomeinafhankelijke teststrategieën gaan in tegen alles wat ik intuïtief meende te weten. En toch had ik ongemerkt deze kennis al in de praktijk gebracht. Een tijd geleden, toen ik schreef over het principe van [testen via de voordeur](blog/22/06/testen-via-de-voordeur/), viel het me op dat je prima testgedreven kunt ontwikkelen door middel van integratietests. Sterker nog, [mijn eerste testgedreven stapjes](/blog/22/06/mijn-eerste-testgedreven-stapjes/) gingen nog wat verder: daarvoor schreef ik E2E-tests die het verwachte gedrag van een API beschreven.[^3]


De opzet van de applicatie verklaart waarom dat soort tests zo geschikt waren om die functionaliteit testgedreven te ontwikkelen. De back-end maakt gebruik van een *Transaction script* om de *resources* te valideren, en uiteindelijk te persisteren in de database.


Had ik gewerkt aan een complexer businessvraagstuk, waar meer logica bij komt kijken, dan had ik mijn eerste testgedreven stapjes op een heel andere manier gezet. Hadden de requirements me genoodzaakt een *Domain model* te gebruiken, dan had ik - waarschijnlijk intuïtief al - testgedreven ontwikkeld door middel van unittests.


## Zilveren kogel


De les is helder: er is geen zilveren kogel als het op software testen aankomt - net zoals er geen zilveren kogel is als het op software ontwikkelen aankomt, en die twee houden innig verband met elkaar. Welke teststrategie je het best kunt hanteren - vooral unit-, integratie of E2E-tests -, is afhankelijk van je softwarearchitectuur. 


Daarmee is wellicht nog een stukje van de puzzel ontdekt die verklaart waarom zoveel softwareontwikkelaars moeite hebben met [Test-Driven Development](https://en.wikipedia.org/wiki/Test-driven_development) (TDD). Ze nemen, met de testpiramide in het achterhoofd, aan dat ze hun applicatie door middel van unittests dienen te ontwikkelen. Wie een CRUD-applicatie middels unittests probeert te ontwikkelen, staat inderdaad een frustrerende ervaring te wachten. (Zie ook [deze blog](/blog/22/04/een-test-per-keer/).)


Maar TDD zegt niets of het *soort* tests dat je dient te schrijven om je code te schrijven. Je architectuur zegt daar wat over. De testpiramide is niet heilig.


[^1]: In de afbeelding worden mijn E2E-tests "UI" genoemd, maar dat is wat mij betreft een misleidende naam. Die suggereert namelijk dat alleen de User Interface wordt getest, wat onjuist is. De *hele applicatie* wordt getest *via* de UI. De nadruk van die tests ligt op het *hele applicatie*-gedeelte, niet op het *via*-gedeelte - vandaar mijn voorkeur voor "E2E" boven "UI".


[^2]: In de appendix van het boek vertelt Khononov overigens een interessante anekdote over wat er gebeurt wanneer je een ondersteunend domein voor een kerndomein aanziet. Laat ik het in één zin samenvatten: je hebt niet altijd overal microservices voor nodig!


[^3]: Dat statement is misschien wat controversieel. Je kunt je afvragen: waren het integratietests die mijn API aftestten, of E2E-tests? Het hangt van je definitie van het systeem af. Als je de back-end als één systeem ziet, dan zou je kunnen beargumenteren dat ik E2E-tests schreef: van de API *qua* UI tot de database. Als je de back-end als onderdeel ziet van een groter systeem, die ook de front-end omvat, dan gaat die definitie strikt genomen niet op - en waren mijn tests dus integratietests.
