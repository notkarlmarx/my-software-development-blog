---
title: "Enkele gedachten over code reviews"
author: "Karl van Heijster"
date: 2024-11-01T10:14:03+01:00
draft: true
comments: true
tags: ["code reviews", "pair programming", "pull requests"]
summary: "De praktijk van *pull requests* is een *vertragingstactiek*. Dat is een teken dat er niet op vertrouwd kan worden dat de kwaliteit van nieuwe code structureel aan de gewenste kwaliteitsstandaarden voldoet. Zo bezien, zijn PR's een pleister op een wond die veel intensievere behandeling behoeft. "
---

Wat is een code review? -- Een code review is een inspectie van een deel van de broncode van een systeem. 


"Inspectie" klinkt formeel, en inderdaad doet de term "code review" veelal denken aan de praktijk van het goedkeuren van een [*pull request*](/tags/pull-requests/ "Blogs met de tag 'pull requests'") (PR). 


Een formele code review is omlijst met allerlei ceremonie: een programmeur doopt een set codewijzigingen tot *kandidaat*, hij maakt een PR aan, daar worden reviewers aan toegewezen, zij geven schriftelijk commentaar -- en hun oordeel is definitief. 


De reviewers zijn poortwachters. Zij besluiten of de codewijziging voldoet aan de voorwaarden om in de broncode te mogen worden opgenomen. Het is hun taak om ervoor te zorgen dat alleen de *juiste* codewijzigingen geaccepteerd worden. 


-- Dat roept de vraag op: wat zijn de voorwaarden waar code aan moet voldoen? Ironisch genoeg bestaat daar binnen een team niet altijd overeenstemming over.


{{< asterisk >}}


Natuurlijk is de formele code review niet het enige moment waarop we broncode inspecteren. Sterker nog, een groot deel van het werk van een programmeur bestaat uit het inspecteren van code. 


Code wordt vaker gelezen dan geschreven. En wanneer een programmeur code leest, vormt hij of zij daar een oordeel over. Soms is dat oordeel: goed. Meestal is het oordeel: slecht. 


Dat is geen steek naar de oorspronkelijke schrijver van de code -- niet per se. Meestal als programmeurs code lezen, doen ze dat met de bedoeling die te wijzigen. Vaak is de code niet voorbereid op zo'n wijziging. 


Dat kan frustrerend zijn, maar is ook terecht. Immers: [*you ain't gonna need it*](/tags/yagni/ "Blogs met de tag 'YAGNI'"). Speculeren over toekomstige wijzigingen levert negen van de tien keer nodeloos complexe code op.


De tiende keer levert het code op die voorbereid is op de *verkeerde* wijziging.


Bovendien, er zijn veel meer manieren om slechte code te schrijven dan goede (en programmeurs zijn vaak sterk geopinieerd in hun oordeel, soms op het onredelijke af -- en ik ben niet zonder zonde).


{{< asterisk >}}


Maar is zo'n informele inspectie een *code review*? Niet in de traditionele zin van het woord. Doorgaans reserveren we die term voor *nieuwe* code.


We willen nieuwe code inspecteren voordat we deze toelaten in de codebase. Dat is een terechte wens. We willen dat de nieuwe code in lijn is met onze kwaliteitsstandaarden, dat deze past in het geheel. En dat willen we nagaan *voordat* we ertoe veroordeeld zijn die code te onderhouden.


Nieuwe code introduceert een risico: dat het gedrag van de bestaande code onder deze wijziging zal lijden. We *weten* hoe de oude code functioneert. Voordat we nieuwe code accepteren, willen we zeker weten dat deze de integriteit van het systeem niet aantast.


{{< asterisk >}}


Maar de aanname dat onze oude code *functioneert* is niet altijd gegrond. Sommige codewijzigingen ontlenen hun bestaansrecht aan het oplossen van problemen in de oude code. Het zijn precies die soort wijzigingen die we proberen te voorkomen door code reviews te doen.


Een code review is een moment waarop het team zich afvraagt: is dit *inderdaad* de kant die we op willen met onze code?


{{< asterisk >}}


Een probleem van het PR-model is dat het deze vraag uitstelt tot het moment dat de wijziging (in de ogen van de *schrijver* van de code) uitgewerkt en voltooid is. Het is frustrerend erachter te komen dat je oplossingsrichting niet de juiste blijkt te zijn *nadat* je al het werk hebt gedaan om deze te implementeren.


PR's zijn een middel dat ervoor zorgt dat ontwikkelaars niet direct met elkaar hoeven te praten -- met alle negatieve gevolgen van dien.


Een mogelijke oplossing voor dit probleem bestaat erin het probleem volledig uit te kauwen met het hele team tijdens [Refinements](/tags/product-backlog-refinement/ "Blogs met de tag 'product backlog refinement'"). Maar het *volledig* specificeren van een oplossingsrichting is even veel werk als het daadwerkelijk schrijven van de code -- en reduceert het schrijven van code tot louter een mechanisch proces van vertalen. 


[*Pair programming*](/tags/pair-programming/ "Blogs met de tag 'pair programming'") biedt een andere oplossing. Binnen dit model wordt de vraag niet achteraf of vooraf gesteld, maar *doorlopend*. (Zie ook [deze blog](/blog/23/01/wel-code-reviews-geen-pull-requests/ "'Wel code reviews, geen pull requests'").) De code review is voor samenwerkende ontwikkelaars geen aparte stap in het proces, maar ingebed in de manier van ontwikkelen zelf. 


*Pair programming* doet voor code reviews wat [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) deed voor het schrijven van tests.


{{< asterisk >}}


Het doel van PR's is om wijzigingen tegen te houden totdat het team overeenstemming heeft bereikt over de kwaliteit van de oplossing. 


Maar: wie is "het team" hier? Het team als geheel? -- Nee, ik heb nog nooit gezien dat elk teamlid zijn zegening moest geven voor een stuk code gedurende een formele code review.


Klaarblijkelijk is er een afgevaardigde die voor het hele team kan spreken. -- Wie?


Is het soms: degene die het meest vertrouwd is met het deel van de code dat zal wijzigen? -- Maar dat zou erop kunnen wijzen dat er geen sprake is van gedeeld eigenaarschap over de code. De reviewer is dan heer en meester over *zijn* deel, de (hopelijk verlichte) dictator die bepaalt welke soorten code er onder zijn bewind mag bestaan.


Soms is het antwoord: de *lead developer* of senior ontwikkelaar(s). Maar dat veronderstelt dat code reviews voornamelijk bestaan om junioren ervan te weerhouden fouten te maken.


{{< asterisk >}}


De praktijk van PR's is een *vertragingstactiek*. Dat is een teken dat er niet op vertrouwd kan worden dat de kwaliteit van nieuwe code structureel aan de gewenste kwaliteitsstandaarden voldoet. Zo bezien, zijn PR's een pleister op een wond die veel intensievere behandeling behoeft. 


{{< asterisk >}}


Je zou het ook om kunnen draaien: laat junioren code reviewen. Zulke reviews hebben een ander doel: valideren of de code begrijpelijk is voor niet-experts. (-- Opnieuw: wat zijn de voorwaarden waar code aan moet voldoen?)


En wanneer die code *niet* begrijpelijk is, duidt dat op de noodzaak van een interventie. Soms is dat: de code moet gewijzigd worden. Maar dit kan ook: de code moet uitgelegd of toegelicht worden. 


Code reviews zijn ook een manier om kennis te delen. Wanneer je junioren code laat reviewen, laat je hen kennismaken met nieuwe programmeertechnieken of domeinconcepten.


{{< asterisk >}}


Code reviews dienen er niet alleen toe de kwaliteit van de code te verbeteren, maar ook de kwaliteit van het team.
