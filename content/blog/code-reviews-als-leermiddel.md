---
title: "Code reviews als leermiddel"
author: "Karl van Heijster"
date: 2021-11-26T10:12:42+01:00
draft: true
comments: true
tags: ["code reviews", "communicatie", "empathie", "intentie van code", "leermoment", "samenwerking"]
summary: "Toen ik begon als softwareontwikkelaar, was ik eerlijk gezegd een beetje bang voor code reviews. Inmiddels zijn de rollen omgedraaid, en zijn mijn collega's banger voor mijn code reviews dan ik voor die van hen. Feit is dat ik een stuk scheutiger ben met mijn opmerkingen dan mijn collega's. Toch denk ik dat er in mijn feitelijke commentaar maar weinig is om bang voor te zijn. Ik zie code reviews namelijk niet als middel en moment om kritiek te geven op andermans code. Of liever: *niet alleen* als middel en moment om kritiek te geven."
---

Toen ik begon als softwareontwikkelaar, was ik eerlijk gezegd een beetje bang voor [code reviews](https://en.wikipedia.org/wiki/Code_review). Ik was bang dat ik stomme fouten maakte waar mijn meer ervaren collega's me zuchtend op zouden wijzen. En als ik hun code na moest lopen, was ik bang dat ik overduidelijke bugs over het hoofd zou zien, en daarmee aan zou tonen dat ik eigenlijk helemaal niet kon programmeren.


Want toen ik begon als softwareontwikkelaar, kon ik ook eigenlijk helemaal niet programmeren. Nu ja, dat is misschien te stellig. Ik kon nauwelijks programmeren, laten we het daar op houden. Ik had een cursus van acht weken gevolgd en werd in het wild losgelaten. Ik had nog niet het zelfvertrouwen om me daar vrij in te bewegen.


## Kritiek


Inmiddels zijn de rollen omgedraaid, en zijn mijn collega's banger voor mijn code reviews dan ik voor die van hen. Soms vraag ik me af of ik niet inderdaad teveel commentaar op elk klein dingetje heb, wanneer ik een pull request naloop. Feit is dat ik een stuk scheutiger ben met mijn opmerkingen dan mijn collega's.


Of ze daar altijd even blij mee zijn, durf ik niet te zeggen. Toch denk ik dat er in mijn feitelijke commentaar maar weinig is om bang voor te zijn. Ik zie code reviews namelijk niet als middel en moment om kritiek te geven op andermans code. 


Of liever: *niet alleen* als middel en moment om kritiek te geven. Soms is kritiek gewenst of zelfs noodzakelijk, natuurlijk. Bijvoorbeeld wanneer een collega een probleem oplost op een manier die efficiënter kan. Of wanneer code teveel verantwoordelijkheden heeft. Maar mijn collega's zijn gewaardeerde en doorgewinterde softwareontwikkelaars, dus kritiek - *dit kan beter!* - beslaat maar een klein deel van mijn totale commentaar.


## Hardop nadenken


Een groot deel van mijn opmerkingen zou je kunnen classificeren onder de categorie *hardop nadenken*. Dan zeg ik dingen als: "Hier zie ik dat je *x* doet, maar op basis van de code eromheen zou ik verwachten dat je het à la *y* zou oplossen. Waarom heb je hiervoor gekozen?" Of: "Je doet hier eerst *x* en dan *y*, is er een bewuste reden waarom je voor die volgorde hebt gekozen?" En soms, wanneer de code precies doet wat ik zou verwachten, zeg ik alleen maar: "Netjes!"


Zulke opmerkingen hebben niet tot doel mijn collega te bewegen de code te wijzigen. Met de code op zichzelf hoeft niets mis te zijn. Vaak hebben mijn collega's een goede reden om te doen wat ze hebben gedaan. Ze hebben soms uren met een probleem geworsteld, en kunnen goed uitleggen waarom een ogenschijnlijk simpeler oplossing niet afdoende is. 


In dat geval hebben de opmerkingen gediend als middel om gedeeld begrip te kweken in het waarom van de code. Dat begrip wordt dan onderdeel van de [*tribal knowledge*](https://en.wikipedia.org/wiki/Tribal_knowledge) van het team.


Soms heeft zo'n opmerking alsnog een codewijziging tot gevolg, niet in de zin dat een oplossingsrichting wordt aangepast, maar dat het waarom van een oplossing wat explicieter in de code wordt geformuleerd. Dit kan in de vorm van codecommentaar zijn, maar nog liever zie ik dat die kennis wordt vastgelegd met scherpere naamgeving van functies en variabelen.


## Twee manieren


Meer nog dan moment van kritiek, zie ik code reviews liever als leermiddel. Die functie wordt op twee manieren vervuld, afhankelijk van het gekozen perspectief.


Ten eerste is het een middel voor mij, de reviewer, om te leren hoe mijn collega's problemen oplossen, en waarom ze dat doen zoals ze dat doen. Door hardop na te denken en te vragen naar het waarom van de code, leer ik de rationale achter bepaalde oplossingsrichtingen kennen. 


Ten tweede is het een middel voor mijn collega's, de auteurs, om te leren hoe iemand die het relevante probleem nog niet helemaal heeft doordacht, de oplossing ervaart. Door hardop na te denken, leren zij van mij welke dingen nog niet duidelijk zijn op het moment dat een andere ontwikkelaar de code voor het eerst ziet.


Want dat is uiteindelijk het ideaal van elke code, dat een ander het leest en alleen maar hoeft te denken: *ja, dat is logisch*. En het ideaal van elke code review? Dat je de opmerking van de ander leest en alleen maar hoeft te denken: *ja, ik zie waarom je dat zegt*.
