---
title: "Drie feedbackloops die verbeteren met unit tests"
author: "Karl van Heijster"
date: 2023-10-06T08:27:19+02:00
draft: true
comments: true
tags: ["code reviews", "feedback", "test-driven development", "testen"]
summary: "Ik ben geneigd te zeggen: alles in het leven wordt beter met unit tests -- en dat toont hoe ver ik inmiddels van het padje ben geraakt. -- Maar op het gebied van softwareontwikkeling gaat die vlieger wel degelijk op. Toen ik voor het Najaarsevenement van TestNet op een rijtje begon uit te werken waarom testers code zouden moeten reviewen, stuitte ik op drie feedbackloops die geautomatiseerde tests kunnen versnellen."
---

Ik ben geneigd te zeggen: alles in het leven wordt beter met unit tests -- en dat toont hoe ver ik inmiddels van het padje ben geraakt.


Maar op het gebied van softwareontwikkeling gaat die vlieger wel degelijk op. Toen ik voor het [Najaarsevenement](https://www.testnet.org/evenement/entry/6515/?evenement=najaarsevenement) van [TestNet](https://www.testnet.org/) op een rijtje begon uit te werken [waarom testers code zouden moeten reviewen] (TALK) (zie ook [deze blog](/blog/23/07/de-tester-als-code-reviewer/ "'De tester als code reviewer'")), stuitte ik op drie feedbackloops die geautomatiseerde tests kunnen versnellen.


## Ontwikkelen


De eerste is de ontwikkelfeedbackloop. Tests kunnen als [vangnet](/blog/22/09/tests-als-vangnet/ "'Tests als vangnet'") dienen voor een ontwikkelaar. Ze geven tijdens de code directe terugkoppeling: ho, je laatste wijziging heeft dit deel van de code stukgemaakt! -- of juist: deze wijziging is oké, ga zo door!


Natuurlijk veronderstelt dit wel de aanwezigheid van tests voordat je de code gaat wijzigen. In een gezonde codebase is dat altijd het geval: er moeten sowieso tests zijn voor de functionaliteit die je niet aan het schrijven bent. Tests fungeren dan als vangnet dat je weerhoudt om onbedoeld de al bestaande functionaliteit te veranderen.


Maar tests kunnen ook dienen als vangnet voor de code die je *nu* schrijft. Uiteraard kan dat alleen als er ook tests zijn voor die code. Het kan alleen als je eerst een test schrijft, dan wat code, en dan weer een test, enzovoort en zo verder.


Het is niet zo dat tests je geen feedback geven over de werking van je code als je ze achteraf schrijft. Maar hun feedbackpotentie wordt het best gerealiseerd als je [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") praktiseert.


## Codereview


Tests kunnen ook de reviewfeedbackloop versnellen en verbeteren. Tests zijn een communicatiemiddel naar een codereviewer. Ze zeggen: dit is wat de code doet. (Zie ook [deze blog](/blog/23/09/drie-vragen-die-elk-pull-request-moet-beantwoorden/ "'Drie vragen die elk pull request moet beantwoorden'") en [deze talk](/talks/de-edele-kunst-van-het-pull-request/ "'De edele kunst van het pull request'").)


Dat is enorm waardevolle informatie voor een reviewer, want bij afwezigheid van tests mag (moet?) deze zich bij elke regel code afvragen: doet dit wat ik denk dat het doet? 


Dat slokt in potentie veel tijd op tijdens de review. Dat is waarom veel codereviewers deze vraag -- helaas! -- buiten beschouwing aan. Ze nemen aan dat de code werkt zoals bedoeld, zodat ze zich alleen op de implementatie hoeven te richten. 


Dat is een probleem, maar het wordt nog erger. Codereviewers zijn feilbaar en kunnen op basis van de implementatie de verkeerde conclusies trekken over de werking van de code. De code functioneel doorgronden op basis van implementatiedetails, is als proberen de werking van het menselijk lichaam te begrijpen door haar cellen te inspecteren.


Het doel van een codereview is niet om bugs te vinden, maar de potentie van een tweede set ogen om ze te spotten wordt wel tenietgedaan door een gebrek aan goede functionele documentatie in de vorm van tests.


## Tests


De derde feedbackloop is die van de tester. In veel teams fungeert de tester -- [een erfenis van de watervalmethode van softwareontwikkeling] (BLOG) -- als instantie die het wek van de ontwikkelaars controleert op functionele correctheid. Dat doen testers door het systeem op te starten en de aangeboden functionaliteit vervolgens zoveel mogelijk te misbruiken. (Met een beetje geluk automatiseren ze dat misbruik voor later.)


Hoe meer functionaliteit je aan een gebruiker aanbiedt, hoe meer manieren er bestaan om een systeem te misbruiken, hoe langer het testen duurt. Die complexiteit dwingt testers om pragmatisch te zijn: ze kunnen niet elke mogelijke combinatie van elke mogelijke invoer aftesten. Dan zou hun testwerk letterlijk een eeuwigheid duren. Ze moeten keuzes maken: *dit* test ik wel en *dat* test ik niet.


Stel dat testers weten dat bepaalde scenario's al gedekt zijn door unittests. In dat geval wordt de keuze des te eenvoudiger: *dat* (een al gedekt scenario) hoef ik in elk geval al niet meer na te gaan. Communicatie tussen de ontwikkelaar en tester over welke tests er al zijn geschreven, helpt de tester om sneller de testcases boven water te halen die nog niet gedekt zijn, en waar het systeem dus mogelijk op kan falen.


## Nooit klaar


Tests zijn niet alleen een verificatiemiddel. Ze bestaan niet om achteraf te bevestigen dat wij als ontwikkelaars ons werk goed hebben gedaan.


De eenvoudige reden daarvoor is dat er in zekere zin geen *achteraf* bestaat in softwareontwikkeling. Software is nooit klaar. (Of liever: bijna nooit klaar. Alleen systemen die worden uitgefaseerd, en daarom ook niet meer onderhouden, verdienen die kwalificatie.) Code is een levend iets: het verandert continu, zelfs wanneer een systeem in de onderhoudsfase terecht is gekomen.


Tests ondersteunen ons *tijdens* dat proces. -- En "ons" is een inclusieve term hier. Het omvat zowel ontwikkelaars als codereviewers en testers. Alles in het leven wordt beter met unittests, in elk geval wat die drie groepen aangaat.
