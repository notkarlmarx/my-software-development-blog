---
title: "Testen: een retrospectief in vijf fasen"
author: "Karl van Heijster"
date: 2024-03-01T07:42:41+01:00
draft: false
comments: true
tags: ["procesverbetering", "software ontwikkelen", "test-driven development", "testen", "teststrategie"]
summary: "Het leek me zinvol om te reflecteren op de ontwikkeling die mijn team en ik door hebben gemaakt op het gebied van testen. Want -- en dat is goed nieuws -- de manier waarop we het testen van onze software aanvliegen is radicaal veranderd sinds ik begon als ontwikkelaar."
---

Het leek me zinvol om te reflecteren op de ontwikkeling die mijn team en ik door hebben gemaakt op het gebied van testen. Want -- en dat is goed nieuws -- de manier waarop we het testen van onze software aanvliegen is radicaal veranderd sinds ik begon als ontwikkelaar.


Achteraf bespeur ik grofweg drie trends in onze teststrategie: (1) meer geautomatiseerd testen, (2) eerder testen en (3) meer samenwerking tussen ontwikkelaars en testers. Deze ontwikkelingen komen voort uit een veranderde opvatting van het doel van testen. Aanvankelijk zagen we testen als een controlemechanisme; gaandeweg is het steeds meer een ontwerpmiddel geworden.


Een retrospectief is altijd een idealisering -- de onderstaande geschiedenis ook. Ik zal de ontwikkeling van onze teststrategie indelen in verschillende fasen, waarin ik een paradigmatische manier van testen omschrijf.


Ik zal de fase scoren op schaalbaarheid, documentatiewaarde, lengte van de feedbackloop, het gevoel van zekerheid dat deze manier van testen oplevert, de impact op de codekwaliteit, en de onderhoudslast. Er zijn ongetwijfeld andere metrieken mogelijk, maar dit zijn er zes die me voor de hand liggend voorkomen.


## Fase #1: De tester test handmatig


|                     |              | 
| ------------------- | ------------ | 
| **Hoe testen?**     | Handmatig    |
| **Wanneer testen?** | Achteraf     |
| **Wie test er?**    | De tester(s) |
<br>


Toen ik begon met programmeren was testen iets wat de tester deed.


Testte ik dan helemaal niet? Dat ook weer niet: ik startte de applicatie op en klikte rond en als het deed wat ik verwachtte, dan was ik er tevreden over.


De tester deed hetzelfde, maar hij klikte ook op de andere knopjes.


### Regressietest


Het was geen proces dat goed schaalde. De twee weken vóór een nieuwe release -- we releasten eens in de zoveel maanden -- blokten we met het hele team: een regressietestsprint waarin we handmatig alle uitgeschreven testpaden doorklikten. 


Als we iets vonden, dan moesten we beslissen of we dat als *known issue* opvoerden, of dat we het risico namen de fout te fixen. (Elke fix bracht immers de mogelijkheid met zich mee van een nieuwe bug. Eigenlijk zou elke fix dus gepaard moeten gaan met een nieuwe regressietest, maar daarvoor was geen tijd.)


Dit is een teststrategie waar ik nooit meer naar terug wil.


### Score


|                         |   |
| ----------------------- | - |
| Schaalbaarheid          | ★ |
| Documentatie            | ★ |
| Lengte van feedbackloop | ★ |
| Gevoel van zekerheid    | ★ |
| Impact op codekwaliteit | ★ |
| Onderhoudslast          | ★ |


## Fase 2: De tester test (deels) geautomatiseerd


|                     |                                        | 
| ------------------- | -------------------------------------- | 
| **Hoe testen?**     | Deels handmatig, deels geautomatiseerd |
| **Wanneer testen?** | Achteraf                               |
| **Wie test er?**    | De tester(s)                           |
<br>


We kwamen tot de conclusie dat deze manier van testen niet houdbaar was. Dus deden we wat elk ontwikkelteam zou doen: we gingen op zoek naar manieren om al dit vreselijke handwerk te automatiseren.


Of liever gezegd: we gingen op zoek naar manieren waarop *de tester* al dit vreselijke handwerk zou kunnen automatiseren. Want de overtuiging dat testen iets is voor testers, bleef onaangeroerd -- voorlopig nog.


Het werk van de tester veranderde dus van het handmatig doorklikken van de applicatie naar het instrueren van een programma om de applicatie door te klikken. -- Ook de overtuiging dat de *user interface* de geijkte locus van het testwerk was, bleef overeind.


### Onderhoud


Deze automatiseringsslag bracht de duur van onze regressietest aanzienlijk naar beneden. Toen we op een dag binnen zes dagen klaar waren met onze regressietestsprint, vonden we dat we het heel goed gedaan hadden.


Maar het onderhouden van de testscripts was arbeidsintensief, en alle verantwoordelijkheid daarvoor lag bij de tester. Hij moest daarom elke keer opnieuw de afweging maken: automatiseer ik de tests voor deze functionaliteit of niet? Zo ja, dan winnen we aan zekerheid maar stapelt het testwerk zich op. Zo nee, dan blijft de werkvoorraad behapbaar, maar verliezen we de garantie op werkende software.


Dit is een teststrategie waar onze tester, stel ik me zo voor, nooit meer naar terug wil.


### Score


|                         |     |
| ----------------------- | --- |
| Schaalbaarheid          | ★★ |
| Documentatie            | ★★ |
| Lengte van feedbackloop | ★  |
| Gevoel van zekerheid    | ★★ |
| Impact op codekwaliteit | ★  |
| Onderhoudslast          | ★★ |


## Fase #3: De ontwikkelaars ontdekken het bestaan unittests


|                     |                                        | 
| ------------------- | -------------------------------------- | 
| **Hoe testen?**     | Deels handmatig, deels geautomatiseerd |
| **Wanneer testen?** | Achteraf                               |
| **Wie test er?**    | Testers & programmeurs                 |
<br>


Professioneel programmeren kan beter -- en ik weet niet of het begint bij tests, maar goed nadenken over je teststrategie is wel een vereiste voor een professioneel programmeur.


*Wie code schrijft is verantwoordelijk voor de kwaliteit van die code* -- waarbij "kwaliteit" in dit geval wordt opgevat in enge zin: de code doet wat het belooft te doen. Om de verantwoordelijkheid van een correcte werking te kunnen dragen, moet degene die code schrijft, ook tests schrijven voor die code.[^1]


Het was een hele klus om elke ontwikkelaar in het team zo ver te krijgen unittests te schrijven. Pas later werd me duidelijk waarom. We schrijven code, en als we merkten dat deze werkte zoals verwacht, dan schreven we een stuk of vijf, zes tests die vastleggen wat we hadden gedaan.


("Vastleggen" is inderdaad het juiste woord. Je legt vast wat het gedrag is van de code die je hebt geschreven -- voor je collega's, zogezegd. Maar je legt het gedrag van de code ook vast in die zin dat je het vastpint: *dit* is wat de code moet doen. En wie daar vanaf wijkt, die heeft het bestaande contract gebroken.)


### Volgorde


Die volgorde maakt van tests een klus, iets "wat nu eenmaal moet". De pijn van onze ellendige regressietests lag nog vers genoeg in het geheugen om die klus te willen klaren.


Dat brengt een vraag aan het licht: gegeven dat er eerst wordt gebouwd en dan wordt getest, wat zegt dat over de functie van testen? -- De tests zijn een controlemiddel. Ze zijn als een checklist achteraf: "Heb ik ervoor gezorgd dat de code *dit* en *dat* en *dát* doet, voor ik 'm naar de main branch push?" En daarom *moeten* ze achteraf gebeuren.


"Eerst bouwen, dan testen" is de strategie die het team in tijden van regressietestsprints hanteerde. Die volgordelijkheid zit al ingebouwd in [het watervalmodel van softwareontwikkeling](/tags/waterval/ "Blogs met de tag 'waterval'"). Het is een diep gewortelde overtuiging waar voor veel ontwikkelaars moeilijk aan te tornen valt. 


### Score


|                         |      |
| ----------------------- | ---- |
| Schaalbaarheid          | ★★★ |
| Documentatie            | ★★★ |
| Lengte van feedbackloop | ★★★ |
| Gevoel van zekerheid    | ★★★ |
| Impact op codekwaliteit | ★★  |
| Onderhoudslast          | ★★★ |


## Fase #4: Test-Driven Development


|                     |                                 s| 
| ------------------- | ------------------------------- | 
| **Hoe testen?**     | Grotendeels geautomatiseerd     |
| **Wanneer testen?** | Tijdens ontwikkeling & achteraf |
| **Wie test er?**    | Testers & programmeurs          |
<br>


"Eerst bouwen, dan testen" is een voor de hand liggende strategie in de echte wereld. Maar de virtuele wereld gedraagt zich niet hetzelfde. Daar is het prima mogelijk een virtuele test te schrijven voor een stuk code dat nog niet bestaat.


Dat brengt ons bij [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD).


Ik kan daar duidelijk in zijn: TDD is geweldig, en iedereen die beweert dat dat niet zo is, die heeft het nog nooit geprobeerd -- niet echt, althans. Wie wil weten waarom TDD zo geweldig is, komt op dit blog uitgebreid aan zijn trekken. Ik heb onder andere geschreven over [TDD en Agile](/blog/22/03/agile-en-test-driven-development/ "'Agile en Test-Driven Development'"), [TDD en het Single-Responsibility Principe](/blog/22/04/een-test-per-keer/ "'Eén test per keer'"), [TDD in de context van *legacy code*](/blog/22/04/legacy-code-en-test-driven-development/ "'Legacy code en Test-Driven Development'"), [TDD en testscope](/blog/22/06/testen-via-de-voordeur/ "'Testen via de voordeur'") en [TDD als middel om aannames te expliciteren](/blog/23/04/wij-van-tdd-eend/ "'Wij van TDD-eend...'").


### Transformatief


De overgang van tests-achteraf naar TDD is transformatief. In deze fase moet een belangrijke aanname over het doel van testen eraan geloven: het idee van tests als controlemiddel. 


Wie voorafgaand aan het schrijven van een stuk code, een test definieert, stelt zichzelf een doel: code te schrijven die de test doet slagen. Natuurlijk vormt het aftrappen van de test een gelegenheid om te controleren of dat doel behaald is, maar dat is niet primair de bedoeling van de test. De bedoeling van de test is houvast bieden bij het schrijven van nieuwe code.


Anders dan de test-achteraf, geeft deze test je nieuwe informatie: of je code nu wél doet wat het moet doen. Daarom voelt het testen niet meer aan als een klus.


[Tests zijn een ontwerpmiddel](/blog/22/09/tests-als-ontwerpmiddel/ "'Tests als ontwerpmiddel'") geworden (zie ook [deze blog](/blog/22/05/nog-een-reden-om-testgedreven-te-ontwikkelen/ "'Nóg een reden om testgedreven te ontwikkelen'")).


-- Voor de ontwikkelaars, althans. Want terwijl ik steeds meer bedreven raakte in TDD, bleven onze testers hún tests achteraf uitvoeren. Deze manier van werken hebben we als team nog niet doorbroken[^2] -- dat is iets voor een volgende fase.


### Score


|                         |         |
| ----------------------- | ------- |
| Schaalbaarheid          | ★★★★  |
| Documentatie            | ★★★★  |
| Lengte van feedbackloop | ★★★★  |
| Gevoel van zekerheid    | ★★★★  |
| Impact op codekwaliteit | ★★★★★ |
| Onderhoudslast          | ★★★    |


## Fase #5: Een toekomstvisie


|                     |                                         | 
| ------------------- | --------------------------------------- | 
| **Hoe testen?**     | Volledig geautomatiseerd                |
| **Wanneer testen?** | Tijdens ontwikkeling                    |
| **Wie test er?**    | Testers & programmeurs in samenwerking  |
<br>


Wat volgt is speculatief -- voor mij althans, want ik twijfel er niet aan dat er teams bestaan die verder zijn dan het mijne als het op hun teststrategie aankomt. 


De vraag is deze: waarom testen testers de code van de ontwikkelaars eigenlijk nog achteraf, als deze hun code met hulp van tests geschreven hebben? Wat is de rol van een tester in een team waarin TDD de norm is?


Het antwoord kan niet zijn: ze schrijven dezelfde tests *nog* een keer om te controleren of de code wel écht doet wat de tests garanderen dat het doet. Dat is onnodig en inefficiënt. 


Dit komt me zinvoller over: de tester wordt een sparringpartner voor de ontwikkelaar. Tester en ontwikkelaar hebben -- vóór en tijdens de ontwikkeling -- discussies over het juiste gedrag van de code, en hoe dit het best in een test kan worden gevangen (zie ook [dit praatje](/talks/waarom-testers-code-moeten-reviewen/ "'Waarom testers code moeten reviewen'")).


De rol van de tester moet veranderen. Zijn taak moet niet langer zijn andermans werk te controleren. Zijn taak zou moeten zijn de ander in een zo vroeg mogelijk stadium te helpen bepaalde (onjuiste) aannames over het gewenste gedrag van het systeem aan het licht te brengen.  


### Niet of, maar wat


De [*Theory of constraints*](https://nl.wikipedia.org/wiki/Theory_of_constraints "'Theory of constraints', Wikipedia") stelt dat er in elk proces één grootste knelpunt is, en dat we dat knelpunt het eerst op moeten lossen. Toen ik begon met programmeren, waren dat bugs -- software die niet deed wat het behoorde te doen. Nu onze software dankzij TDD structureel een bepaald kwaliteitsniveau behaalt, wordt het tijd onze blik te richten op het volgende onderwerp waar de meeste winst te behalen valt: software bouwen die beter aansluit bij de wens van de eindgebruiker. 


De focus van testers komt minder te liggen op de vraag of het systeem doet wat het moet doen, en meer op de vraag wat het nu precies is dat het systeem moet doen. -- En dat is iets wat ik niet had durven vermoeden, toen ik jaren geleden samen met onze vaste tester zat te zuchten en steunen tijdens die regressietestsprints.


[^1]: Natuurlijk schreven wij ontwikkelaars in eerdere fasen ook heus wel eens een unittest -- bijvoorbeeld als we zelf vonden dat bepaalde logica erg complex was. Maar het bestaan van onze unittests was incidenteel, ongestructureerd. Zoals ik zei: het onderscheid in fasen is een idealisatie.


[^2]: Sterker nog, een deel van het team bevindt zich nog in fase #3. (Opnieuw: de fasen zijn een idealisatie.) Hoe ik hen zo ver krijg testgedreven te ontwikkelen, is een vraagstuk waar ik me al tijden het hoofd over breek (zie bijvoorbeeld [deze blog](/blog/23/04/tijdreis/ "'Tijdreis'")). 
