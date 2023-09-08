---
title: "Drie vragen die elk pull request moet beantwoorden"
author: "Karl van Heijster"
date: 2023-09-08T08:13:59+02:00
draft: false
comments: true
tags: ["boeken", "code lezen", "code reviews", "pull requests"]
summary: "Schrijvers van *pull requests* zijn over het algemeen helemaal niet zo goed in het overbrengen van alle informatie die een lezer nodig heeft om deze goed te kunnen beoordelen. Want de meeste schrijvers weten überhaupt nauwelijks welke informatie er nodig is om dat te kunnen doen. In mijn beleving moet een PR antwoord geven op drie vragen."
---

[Mijn eerste code review](/blog/23/08/mijn-eerste-code-review/) ging gepaard met een gevoel van hulpeloosheid en ongemak. De herinnering staat me nog helder voor de geest -- maar niet omdat het nou zo'n heftige ervaring was. Eerder omdat ik dat gevoel nog heel vaak heb mogen beleven in mijn carrière als softwareontwikkelaar. 


Toen ik begon met professioneel software ontwikkelen, namen mijn team en ik aan dat dat code reviewen op een gegeven moment wel los zou lopen. Dat ik, naarmate ik meer code onder ogen had gehad, steeds makkelijker kon beoordelen of een *pull request* (PR) aan bepaalde kwaliteitsstandaarden voldeed of niet. (Waar die kwaliteitsstandaarden uit bestonden, daar hadden we allemaal hooguit een vaag idee van.)


## Geforceerd


Maar ondanks dat ik steeds meer ervaring opdeed met de syntax van [C#](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/ "'C# programming guide', Microsoft documentatie") (en noodgedwongen ook van [Visual Basic](https://learn.microsoft.com/en-us/dotnet/visual-basic/ "'Visual Basic documentation', Microsoft documentatie")), en ondanks dat ik de codebase steeds beter wist te doorgronden, en ondanks dat ik me de principes van softwareontwikkeling steeds meer eigen maakte -- kwam het, net als die eerste keer, nog steeds voor dat ik PR's goedkeurde zonder dat ik nu echt een mening had over de code. Keer op keer op keer.


Dat gevoel van ongemak dat ik bij mijn eerste code review ervaarde, heb ik nog heel vaak mogen ervaren. Het is het gevoel geforceerd te zijn een oordeel te vellen over iets wat je niet goed kunt beoordelen. Wat blijkt: het vermogen om code te reviewen is niet iets wat je vanzelf wel ontwikkelt naarmate je langer als softwareontwikkelaar bezig bent. 


## Code lezen


Eén van de redenen daarvoor, is dat we als vakgebied nauwelijks aandacht besteden aan het lezen van code. Dat is een punt dat [Felienne Hermans](https://www.felienne.com/) maakt in [*The Programmer's Brain*](https://www.manning.com/books/the-programmers-brain "Felienne Hermans - 'The Programmer's Brain', uitgeverij Manning") (en in [deze video](https://www.youtube.com/watch?v=58LeSsn_nSQ "How to Read Complex Code • Felienne Hermans • YOW! 2021")). Ik schreef er in de context van PR's al eerder over, [hier](/blog/22/08/hoe-review-je-eigenlijk-code/ "'Hoe review je eigenlijk code?'") en [hier](/blog/22/09/test-driven-code-reviews/ "'Test-Driven Code Reviews'").


Anders dan een blog of tijdschriftartikel of roman is code niet iets wat je van boven naar beneden leest. Code verwijst op regel 1 naar een ander stuk code op regel 298. De code op regel 298 maakt gebruik van code die is gedefinieerd op een heel andere plek in de codebase. Die code maakt op zijn beurt weer gebruik van code uit *third party libraries* -- class- en methodnamen, en eventueel enige documentatie, zijn onze enige manieren om chocola van die code te kunnen maken.


Ook code is een tekst, en lezen is een proces van het opbouwen van een mentaal model op basis van de tekst. Maar hoe dat model tot stand komt verschilt aanzienlijk in het geval van een blog of een PR. -- Probeer het eens: kun je verwoorden hoe je begrip van een stuk code tot stand komt? 


## Drie vragen


Er is nog een reden waarom zoveel programmeurs blijven worstelen met code reviews. Schrijvers van PR's zijn over het algemeen helemaal niet zo goed in het overbrengen van alle informatie die een lezer nodig heeft om deze goed te kunnen beoordelen. (Zie ook [deze blog](/blog/22/10/pull-requests-als-documentatie/ "'Pull requests als documentatie'").)


Want de meeste schrijvers weten überhaupt nauwelijks welke informatie er nodig is om dat te kunnen doen. In mijn beleving moet een PR antwoord geven op drie vragen:


1. Waarom bestaat dit PR überhaupt?
2. Wat doet de code concreet? 
3. Hoe doet de code dat?


Pas als een codereviewer deze vragen kan beantwoorden, kan deze beoordelen of de wijziging de codebase verbetert of niet. (En dat is het belangrijkste doel van elke codewijziging, zie [deze blog](/blog/22/10/pull-requests-als-documentatie/ "'Pull requests als documentatie'").)


## Drie antwoorden


Programmeurs hebben -- begrijpelijkerwijs -- een *bias* richting code. Ze zijn daarom geneigd om de antwoorden op die vragen in code te willen vangen. Dat is waarom zoveel ontwikkelaars graag roepen dat [code zichzelf moet documenteren](/blog/21/12/goede-code-documenteert-zichzelf-niet/ "'Goede code documenteert zichzelf (niet)'").


Maar niet alle informatie is even geschikt om in code uit te drukken. Hoewel een PR op alle drie van de bovenstaande vragen antwoord moet geven, volgt daar niet uit dat die antwoorden allemaal in de (productie)code terecht moeten komen.


1. Waarom een PR überhaupt bestaat, kun je het best kwijt in diens metadata: de titel en omschrijving. Vaak blijft deze informatie impliciet -- het is onderdeel van de [*tribal knowledge*](https://en.wikipedia.org/wiki/Tribal_knowledge "'Tribal knowledge', Wikipedia") van een team. Maar het expliciet maken van het bestaansrecht van een codewijziging is een uitstekende lakmoesproef. Als dit niet lukt, moet je je afvragen of de wijziging wel de moeite waard is.

2. Wat de code concreet doet, kan het best worden vastgelegd middels geautomatiseerde tests. Het doel is de lezer te *vertellen* wat de code doet, niet de lezer dat zelf uit te laten vogelen. Ik heb hier veelvuldig over geschreven (en [gesproken](/talks/altijd-up-to-date-documentatie-met-maximaal-descriptieve-tests/ "'Altijd up to date documentatie met maximaal descriptieve tests'")), onder andere [hier](blog/22/09/tests-als-documentatie/ "'Tests als documentatie'"), [hier](/blog/22/12/tests-zijn-specs/ "'Tests zijn specs'") en [hier](/blog/23/02/waarom-dry-waarom-damp/ "'Waarom DRY? Waarom DAMP?'").

3. Hoe de code dat doet, is de daadwerkelijke implementatie -- de code zelf. 


## Belangrijk


Het is geen toeval dat de laatste vraag de vraag naar de code zelf is. Het is een belangrijke vraag, maar -- nota bene -- de minst belangrijke van de drie. Code is een implementatiedetail -- het *hoe* dat een noodzakelijk kwaad is om een bepaalde *wat* te bereiken. 


Niet voor niets wordt gezegt dat code een *liability* is en geen *asset* (zie ook [deze blog](/blog/21/08/moet-je-dit-willen-testen/ "'Moet je dit willen testen?'")). Een probleem hoeft niet per se met code opgelost te worden. Sommige doelen kun je net zo goed, of misschien zelfs beter, bereiken zonder er één regel code voor te schrijven.


Ook dat kan een conclusie zijn van een PR -- al trek je die natuurlijk liever een veel vroeger stadium. Maar waak voor de [*sunk cost fallacy*](https://en.wikipedia.org/wiki/Sunk_cost "'Sunk cost', Wikipedia"): het grootste deel van de kosten van code bevinden zich in de onderhoudsfase, niet in de ontwikkelfase. (Zie ook [deze blog](/blog/21/12/zonde-om-weg-te-gooien/ "'Zonde om weg te gooien?'").) De goedkoopste code is code die je niet hoeft te onderhouden -- en de enige code die je niet hoeft te onderhouden is *geen code*.


-- Misschien is "code review" wel helemaal het verkeerde woord, bedenk ik nu. Zou "solution review" niet een betere term zijn?
