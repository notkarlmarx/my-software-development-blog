---
title: "Legacy code en Test-Driven Development"
author: "Karl van Heijster"
date: 2022-03-18T10:52:06+01:00
draft: true
comments: true
tags: ["boeken", "leermoment", "legacy code", "software ontwikkelen", "test-driven development"]
summary: "TDD gaat over het toevoegen van nieuwe features - *per definitie*. Immers, wie tests toevoegt voor bestaande code is niet test-driven aan het developen. Maar de meeste ontwikkelaars werken helemaal niet aan *greenfield*-applicaties. Ze slepen zich dag na dag, week na week door het moeras dat we *legacy code* noemen. TDD lijkt te zijn weggelegd voor de *lucky few* onder ons die nieuwe applicaties mogen ontwikkelen. De rest van ons mag ploeteren in bestaande drek. Maar die conclusie gaat toch niet helemaal op."
---

# Gedachten naar aanleiding van *Learning Test-Driven Development* - Deel 4


*Onlangs las ik* [Learning Test-Driven Development](https://www.oreilly.com/library/view/learning-test-driven-development/9781098106461/) *van [Saleem Siddiqui](https://www.linkedin.com/in/ssiddiqui/). Ik zal met de deur in huis vallen: het boek is een aanrader. Zo erg zelfs, dat ik er wel vier blogs uit wist te persen! Vandaag: over TDD in de context van legacy code.*


Test-Driven Development (TDD) wordt doorgaans besproken binnen de context van [*greenfield*-projecten](https://en.wikipedia.org/wiki/Greenfield_project). Dat is voor de hand liggend, om twee redenen. De eerste is didactisch van aard: het stroomlijnt de uiteenzetting. Door uit te gaan van een leeg blad, voorkom je dat de bespreking wordt verward door allerlei vragen rondom de uitgangssituatie. 


De tweede is inhoudelijker. TDD gaat over het toevoegen van nieuwe features - *per definitie*. Immers, wie tests toevoegt voor bestaande code is niet test-driven aan het developen. De productiecode is in die situatie leidend, de tests volgen. Bestaande code lijkt geen plek te hebben binnen de praktijk van TDD.


## *Brownfield*


Maar de meeste ontwikkelaars werken helemaal niet aan *greenfield*-applicaties. (En als ze het doen, dan duurt het niet lang voordat die applicatie onvermijdelijk tot *brownfield* is gedegradeerd!) Ze slepen zich dag na dag, week na week door het moeras dat we *legacy code* noemen. TDD lijkt te zijn weggelegd voor de *lucky few* onder ons die nieuwe applicaties mogen ontwikkelen. De rest van ons mag ploeteren in bestaande drek.[^1]


Maar die conclusie gaat toch niet helemaal op. Ook in *legacy code* moeten nieuwe features toegevoegd worden. Hoe? [Michael Feathers](https://michaelfeathers.silvrback.com/) is daar gladhelder over in zijn klassieker [*Working Effectively with Legacy Code*](https://www.pearson.com/us/higher-education/program/Feathers-Working-Effectively-with-Legacy-Code/PGM254740.html): met TDD.


"Maar," hoor ik de gemiddelde ontwikkelaar al tegensputteren, "tests ontbreken juist veelal in *legacy code*, en ze toevoegen is praktisch onmogelijk!" En daar heeft die gemiddelde ontwikkelaar gelijk in. Feathers' boek gaat precies daarover. Sterker nog, hij definieert *legacy code* zelfs als code die niet wordt ondersteund door tests.[^2] De enige manier om ervoor te zorgen dat *legacy code* niet verder rot, is door tests toe te voegen - als niet voor de bestaande code, dan toch in elk geval voor de nieuwe functionaliteiten. En de beste manier om dat te doen, is via TDD.


## Duplicatie


Het is interessant om te zien hoe Feathers TDD karakteriseert, binnen die context van bestaande code. De eerste twee stappen zullen elke TDD'er bekend voorkomen: schrijf een falende test, en schrijf daarna zo simpel mogelijke code om ervoor te zorgen dat die slaagt. De derde stap omschrijft Feathers echter niet als refactoren, maar noemt hij "duplicatie verwijderen". (Wat overigens een vorm van refactoren is, daar niet van.)


Waarom? Omdat nieuwe features in een *legacy*-applicatie veelal bestaan uit variaties op bestaande functionaliteit. De snelste manier om je test te laten slagen zal in dit geval daarom ook niet per se bestaan uit het hard-coden van variabelen, maar door bestaande code te *ctrl-C & V'en*, en daarna licht aan te passen.


"Kopieer-en-plak?" hoor ik de gemiddelde ontwikkelaar uitroepen, "*quelle horreur!*" En ook daar heeft die gemiddelde ontwikkelaar gelijk in. Het regelmatig kopiëren en plakken van code is nu precies één van de redenen waarom *legacy code* zo vreselijk is om in te werken.


## Doelen


Maar dat is dus precies waarom TDD drie stappen kent, en niet twee. Het gekopieerde code dient een doel - nee, meerdere. Je zal je als ontwikkelaar hier doorheen moeten werken om je test te kunnen laten slagen. Dat is het eerste doel. 


Het tweede doel is je begrip van de bestaande code te vergroten *door* de nieuwe feature te implementeren. Dat is immers waarom het vaak zo frustrerend is om met *legacy code* te werken: de code is ondoorgrondelijk. Nou, als je klaar bent met de nieuwe feature dus niet meer.


Maar waarom dan gekopieerde code? Omdat dit je in staat stelt *veilig* de bestaande code te leren kennen. Je kunt de gekopieerde code vrijelijk aanpassen en kijken wat er gebeurt, zonder bang te hoeven zijn dat je bestaande - veelal ongeteste - functionaliteiten om te gooien. Dat is het derde doel.


Als de nieuwe feature eenmaal geïmplementeerd is, is je begrip van de bestaande code gegroeid. Dat stelt je in staat om met enige mate van zelfvertrouwen de bestaande code te refactoren en te integreren met het nieuwe deel. En dat zorgt er op zijn beurt misschien wel weer voor dat het makkelijker wordt om tests te kunnen schrijven voor de oorspronkelijke functionaliteit. - Waarmee het zijn status als *legacy code* verliest!


## Les


De les is belangrijk: het introduceren van nieuwe functionaliteit in *legacy code* hoeft niet tot grotere rot van een al rottende codebase te leiden. Integendeel, het is een kans om de oorspronkelijke code op te kunnen schonen. 


Met dien verstande, natuurlijk, dat dit geen eenvoudige klus is. Het vraagt tijd en inspanning van de ontwikkelaar - meer dan wanneer 'ie de nieuwe feature *quick and dirty* zou implementeren. Maar die tijd is allesbehalve verloren, want de testcoverage die het oplevert, stelt de ontwikkelaar in staat om de volgende feature des te sneller te implementeren.


Wat ik zeg is niets nieuws. Ontwikkelaars die zich regelmatig door *legacy code* heen moeten worstelen, weten ergens heus wel dat automatische tests de uitweg uit het moeras zijn. Maar ze weten vaak niet waar ze moeten beginnen. En precies daarom moeten ze *Working Effectively with Legacy Code* lezen. Wie weet, misschien inspireert het hen wel om eindelijk TDD te omarmen.


## Meer in deze reeks


1. [Agile en Test-Driven Development] (LINK)
2. [Eén test per keer] (LINK)
3. [*To polyglot or not to polyglot*] (LINK)
4. **Legacy code en Test-Driven Development**


[^1]: Misschien is dat [óók] (LINK_NAAR_DEEL_2) een reden waarom het zo moeilijk is om ontwikkelaars de praktijk van TDD eigen te maken. Ze hebben het gevoel dat het niets met hun dagelijkse werkzaamheden te maken heeft. 


[^2]: En die definitie heeft intuïtieve aantrekkingskracht voor iedereen die een *greenfield*-applicatie binnen de kortste keren heeft zien verbruinen! Voor een praktijkvoorbeeld: die keer dat we [de Angular-kant van onze applicatie dachten te kunnen ondersteunen met louter E2E-tests](/blog/22/01/de-leercurve-van-angulartests-beklimmen-deel-1/). 
