---
title: "Wat betekent het tests te schrijven?"
author: "Karl van Heijster"
date: 2024-11-08T08:47:13+01:00
draft: true
comments: true
tags: ["software ontwikkelaar (rol)", "sprint retrospective", "testen", "verantwoordelijkheid"]
summary: "Het is een terugkerend thema in onze Retrospectives: testcapaciteit -- en dan natuurlijk vooral het gebrek eraan. Het komt regelmatig voor dat verschillende *pull requests* een tijd lang open blijven staan, wachtend op iemand die de testautomatiseringsscripts aan de codewijziging toevoegt."
---

Het is een terugkerend thema in onze [Retrospectives](/tags/sprint-retrospective/ "Blogs met de tag 'sprint retrospective'"): testcapaciteit -- en dan natuurlijk vooral het gebrek eraan. (Ik schreef er eerder over, [hier](/blog/24/05/waarom-testen-testers/ "'Waarom testen testers?'").) Het komt regelmatig voor dat verschillende [*pull requests*](/tags/pull-requests/ "Blogs met de tag 'pull requests'") (PR's) een tijd lang open blijven staan, wachtend op iemand die de testautomatiseringsscripts aan de codewijziging toevoegt.


De bron van het probleem is bekend. Het rekensommetje is simpel: we hebben zes ontwikkelaars in het team en één tester, en die ene tester kan onmogelijk alle tests schrijven voor het werk wat de ontwikkelaars opleveren.


De situatie is niet altijd zo geweest. Ooit hadden we twee testers in het team (en één ontwikkelaar minder), waarvan er één full-time werd ingezet om [Cypress](https://www.cypress.io/)-tests te schrijven voor onze front-end. Het hoeft dan ook niet te verbazen dat met name onze front-endontwikkelaar in Retrospectives met nostalgie terugdenkt aan de goede oude tijd dat het gebrek aan testcapaciteit geen *bottleneck* vormde om zijn PR's er doorheen te loodsen.


## De ontwikkelaar hoort tests te schrijven


Mijn antwoord op zulke mijmeringen is altijd hetzelfde: de ontwikkelaar hoort de tests te schrijven. (Zie onder andere [deze](/blog/23/09/drie-vragen-die-elk-pull-request-moet-beantwoorden/ "'Drie vragen die elk pull request moet beantwoorden'") en [deze blog](/blog/24/07/goede-code-is-geteste-code/ "'Goede code is geteste code'").) Het is de taak van de ontwikkelaar om middels een geautomatiseerde testsuite te bewijzen dat ze zijn code doet wat het moet doen. En dat geldt niet alleen voor [unit](/tags/unit-tests/ "Blogs met de tag 'unit tests'")- en [integratietests](/tags/integratietests/ "Blogs met de tag 'integratietests'"),[^1] maar óók voor [*end-to-end*-tests](/tags/end-to-end-tests/ "Blogs met de tag 'end to end tests'") -- in Cypress.


Zijn antwoord op mijn tegenargument is altijd hetzelfde: je hebt een tweede set ogen nodig om de blinde vlekken in je eigen testcoverage te zien. Een tester kijkt anders naar een stuk functionaliteit dan een ontwikkelaar -- en wie het testen overlaat aan de ontwikkelaar zal daarom [bugs](/tags/bugs/ "Blogs met de tag 'bugs'") over het hoofd zien.


Hoewel ik die stelling [eerder](/blog/24/05/waarom-testen-testers/ "'Waarom testen testers?'") al genuanceerde, ben ik het daar niet mee oneens. Twee zien meer dan één, en al helemaal wanneer één van die twee een professional is die getraind is in het formuleren van *edge cases*. Het is inderdaad een goed idee om de tester te betrekken bij het schrijven van testsscenario's.


## Wat betekent het tests te schrijven?


Tijdens onze laatste Retrospective realiseerde ik me plots waar de bron van ons meningsverschil in bestond: een andere opvatting van wat het betekent om tests te *schrijven*.


Wanneer ik zeg: "ontwikkelaars moeten tests schrijven," dan bedoel ik: "ontwikkelaars moeten test*code* schrijven." Duurzaam software ontwikkelen is als dubbel boekhouden. Elke gedraging in de code dient tweemaal te worden vastgelegd: één keer in de productiecode en één keer in de testcode. (De metafoor ontleen ik aan [Robert Martins](https://en.wikipedia.org/wiki/Robert_C._Martin) [*Clean Craftsmanship*](https://www.pearson.com/en-us/subject-catalog/p/clean-craftsmanship-disciplines-standards-and-ethics/P200000009529/9780136915713); zie [deze blog](/blog/24/07/goede-code-is-geteste-code/ "'Goede code is geteste code'").)


Wat mijn collega echter leek te horen, is: "ontwikkelaars moeten test*scenario's* schrijven." Welnu, ik ben inderdaad van mening dat het de taak van een goede ontwikkelaar is om na te denken over testscenario's. Maar ik ook ben de eerste die toegeeft dat het zeker geen kwaad kan om daar de hulp van de tester bij in te roepen. De tester is immers de expert in het bedenken van testscenario's -- je zou wel gek zijn daar *geen* gebruik van te maken.


## Automatiseren


Je zou mijn standpunt als volgt kunnen karakteriseren: het is de taak van de ontwikkelaar om testscenario's te *automatiseren*. Ga maar na: automatiseren is de kerntaak van een ontwikkelaar. Het is wat wij dag in dag uit doen -- zowel voor onszelf als voor onze opdrachtgevers. 


Automatiseren is *niet* de kerntaak van een tester. De kerntaak van de tester is om zoveel mogelijk manieren te vinden om het systeem te breken. (Hoe minder manieren hij vindt, hoe beter wij ons werk hebben gedaan.)


En als hij een manier heeft gevonden om het systeem te breken, dan doen wij er goed aan die manier te automatiseren alvorens we het defect repareren, zodat we er zeker van kunnen zijn dat het niet opnieuw op zal treden.


Het is natuurlijk niet *verboden* voor een tester om zijn eigen testscenario's te automatiseren. Maar wanneer deze taak het grootste deel van de tijd van de tester gaat beslaan, is er sprake van een problematische werkverdeling. 


Het is de kerntaak van de tester om testscenario's te bedenken en uit te werken. Het schrijven en onderhouden van testcode is de verantwoordelijkheid van de ontwikkelaar. 


## Van strategie wisselen


Daarmee wil ik niet suggereren dat ik niet snap waar mijn collega vandaan komt. Hij heeft mogen proeven van de luxe zijn eigen *end-to-end*-tests niet te hoeven schrijven, zodat hij zich kon concentreren op dat wat hij leuk vindt en waar hij ook goed in is. Het is niet meer dan menselijk dat hij met nostalgie aan die tijd terugdenkt.


Maar wanneer verschillende PR's open blijven staan, wachtend op iemand die Cypress-tests ervoor gaat schrijven, heeft het geen zin om te pleiten voor een tweede tester -- niet op korte termijn, in elk geval. Het is in dat geval beter van strategie te wisselen. En dat betekent in dit geval: de verantwoordelijkheid voor het schrijven (i.e. *automatiseren*) van tests op je te nemen. 


Het is beter één *feature* helemaal af te maken dan er tien half af te hebben. 


[^1]: Gelukkig hoef ik mijn collega dáár niet op aan te spreken: de testcoverage van zijn [Angulartests](/blog/22/02/de-leercurve-van-angulartests-beklimmen-deel-2/ "'De leercurve van Angulartests beklimmen - deel 2: Van integratie- naar unit tests'") is zonder uitzondering uitmuntend.
