---
title: "Blijven we dit ondersteunen?"
author: "Karl van Heijster"
date: 2021-10-29T10:13:34+02:00
draft: true
comments: true
tags: ["legacy code", "stakeholders", "technische schuld", "waarde"]
summary: "Onze *legacy*-applicatie focust zich op de constructie van toetsen, niet op de afname. Om de afnameomgeving te kunnen bekijken, heeft de applicatie een integratiepunt met een externe tool. Maar de laatste tijd levert die functionaliteit alleen maar frustratie op. Problemen met de externe tool worden op onze applicatie geschoven, en het gedrag met de geïntegreerde versie is bij een grote load inconsistent met die van de externe tool. De klachten over de integratie vreten tijd van het ontwikkelteam, en zorgen bovendien voor frustraties over en weer naar de stakeholders."
---

Moet je een bepaalde feature tot in de eeuwigheid blijven ondersteunen? Nu ja, de vraag stellen is hem beantwoorden, misschien. Laat ik uiteenzetten waarom ik 'm stel.


## Constructie en afname


Met hulp van onze *legacy*-applicatie kunnen gebruikers een toets samenstellen. Die toets zal uiteindelijk in een digitale omgeving afgenomen moeten worden. Om te kunnen controleren dat de toetsvragen er zo uitzien als bedoeld, is het belangrijk om de toets in die uiteindelijke omgeving te kunnen bekijken, en desgewenst aan te passen.


Onze applicatie focust zich op de constructie van toetsen, niet op de afname. Om de afnameomgeving te kunnen bekijken, heeft de applicatie een integratiepunt met een externe tool. Met een eenvoudige muisklik wordt de afnameomgeving vanuit onze applicatie geopend en kan de controle beginnen.


## Extraatje


Onze gebruikers zouden de tool in principe ook los van de applicatie kunnen gebruiken. Maar de integratie scheelt hen enkele muisklikken. Het bespaart hen de moeite van het exporteren van de toets uit ons systeem en het importeren ervan in het externe systeem. Deze optie is lang, lang geleden ingebouwd, oorspronkelijk als een extraatje, een manier om het gebruikersgemak wat te verhogen. 


Maar de laatste tijd levert dat extraatje eigenlijk alleen maar frustratie op. Problemen met de externe tool worden op onze applicatie geschoven, en het gedrag met de geïntegreerde versie is bij een grote load inconsistent met die van de externe tool. De klachten over de integratie vreten tijd van het ontwikkelteam, en zorgen bovendien voor frustraties over en weer naar de stakeholders.


En dat terwijl heel duidelijk is aangegeven dat het team zich niet meer met dit soort problemen bezig zal houden. Sinds anderhalf jaar is onze *legacy*-applicatie officieel tot *legacy* bestempeld. Dat wil zeggen: we leveren geen nieuwe features op, we fixen geen *known issues*, we komen alleen nog in actie voor bedrijfskritische wijzigingen die op geen enkele andere manier af te vangen zijn.


## Urgentie


Te oordelen naar het aantal mailtjes met hoge urgentie[^1] naar onze Product Owner, is deze boodschap blijkbaar niet helemaal aangekomen. Sommige stakeholders willen dat we de boel fixen. 


Dit ondanks het team - en zij ook, zeggen ze althans! - liever tijd steekt in het ontwikkelen van onze nieuwe applicatie om de *legacy*-code te kunnen vervangen. En ondanks het feit dat de externe tool, met wat extra muisklikken, los van onze *legacy*-applicatie te gebruiken is.


Moeten we dat integratiepunt wel blijven handhaven, nu het, voor ons en de gebruikers, alleen maar frustratie oplevert en weinig meerwaarde levert? Nu ja, de vraag stellen is hem beantwoorden, misschien. Wat denk jij?


[^1]: Wat me doet denken aan deze quote van Dwight D. Eisenhower: *"I have two kinds of problems, the urgent and the important. The urgent are not important, and the important are never urgent."* Aan de hand van de [Eisenhower-methode](https://nl.wikipedia.org/wiki/Eisenhower-methode) zou ik denk ik wel weten hoe ik die mailtjes zou classificeren.
