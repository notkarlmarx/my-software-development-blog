---
title: "Schorseneren en software architectuur"
author: "Karl van Heijster"
date: 2021-10-11T07:39:41+02:00
draft: true
comments: true
tags: ["boeken", "functionele eigenschappen", "kwaliteitsattributen", "software architectuur", "software architect (rol)"]
summary: "Een ontwerper van een systeem - of dat nu een kok is of een softwarearchitect - dient niet alleen rekening te houden met de functionele eigenschappen van zijn componenten. *Smaak is niet alles!* Een lekker ingrediënt kan om allerlei redenen niet in een gerecht terechtkomen. De impact van het ingrediënt op de afwasser - niet onbelangrijk! - kan dusdanig zijn dat het verstandig is om toch maar een ander smaakje te kiezen."
---

Mijn vrouw maakte laatst aardappelen klaar met stoofvlees en schorseneren. - Schorseneren? 


Ja, schorseneren. Een [schorseneer](https://nl.wikipedia.org/wiki/Grote_schorseneer) is een wortel met een smaak die ergens tussen asperge, artisjok en bloemkool in zit. Ik had nog nooit schorseneren gehad, dus dat was een hele ervaring. Ik vond het niet vies, maar ik was er ook niet kapot van.


Schorseneren zijn een vergeten groente. Ze worden ook wel *keukenmeidenverdriet* of *huisvrouwenleed* genoemd, en dat is de eerste aanwijzing van waarom deze groente vergeten is. Bij het schillen van een schorseneer komt er een kleverige melksap vrij. Dat bracht mijn vrouw ertoe bracht om, op goed advies van het internet, voor het eerst in haar leven te koken met chirurgische handschoenen. Een hele ervaring, inderdaad!


Helaas had ik niet diezelfde luxe toen het mijn beurt was om af te wassen. Dat wat een werkje van een kwartiertje had moeten zijn, liep algauw uit tot een halfuur, omdat ik als een gek zat te schrobben op pannen, lepels en schilmesjes: als zat onder het kleverige schorsenerensap. Vanuit de keuken riep ik haar toe: "Ik heb heerlijk gegeten, lieverd, echt waar, maar vanuit afwassersperspectief hoef je dit wat mij betreft niet meer te maken."


## Gerechten, systemen


Waarom vertel ik dit verhaal? Omdat het me deed denken aan softwarearchitectuur. (Daarom mag er, vanaf nu, officieel een beroepsdeformatie bij me worden vastgesteld. Kom er maar in, dokter!)


We kunnen mijn vrouw zien als kok die met ingrediënten een gerecht samenstelt. Maar we zouden haar ook kunnen zien als een ontwerper (of architect) die met componenten een systeem samenstelt. Die componenten hebben functionele eigenschappen en kwaliteitsattributen[^1]. De functionele eigenschappen van zo'n ingrediënt-component wordt in dit geval gevormd door diens smaak en textuur. Kwaliteitsattributen zijn bijvoorbeeld de mate waarin het makkelijk te verkrijgen en te bereiden is. 


De componenten waar een systeem uit bestaat moeten niet *alleen* bepaalde functionaliteiten hebben. Ze moeten ook aan kwaliteitseisen voldoen, zoals schaalbaarheid, stabiliteit, gebruikersgemak of aanpasbaarheid, om er maar een paar te noemen. Een component kan functioneel precies doen wat verlangd wordt, maar omwille van kwaliteitsattributen toch van de hand gewezen worden.


Een ontwerper van een systeem - of dat nu een kok is of een softwarearchitect - dient niet alleen rekening te houden met de functionele eigenschappen van zijn componenten. *Smaak is niet alles!* Een lekker ingrediënt kan om allerlei redenen niet in een gerecht terechtkomen. De impact van het ingrediënt op de afwasser - niet onbelangrijk! - kan dusdanig zijn dat het verstandig is om toch maar een ander smaakje te kiezen. Geloof deze afwasser maar als 'ie zegt: aardappelen met stoofvlees en bloemkool zijn net zo lekker.


Een redelijk uitputtende lijst van kwaliteitsattributen is te vinden op - waar anders? - [Wikipedia](https://en.wikipedia.org/wiki/List_of_system_quality_attributes). Een prima inleiding in de materie is te vinden in [*Essential Software Architecture*](https://link.springer.com/book/10.1007/3-540-28714-0) van Ian Gorton. Over tactieken om enkele van de belangrijkste kwaliteitsattributen te waarborgen, zie [*Software Architecture in Practice*](https://www.pearson.com/us/higher-education/program/Bass-Software-Architecture-in-Practice-4th-Edition/PGM2920979.html) van Len Bass, Paul Clements en Rick Kazman.


[^1]: Deze worden ook wel "non-functionele eigenschappen" genoemd. Maar een strategisch ingestelde softwarearchitect kan op zijn klompen aanvoelen dat het makkelijker is om kwaliteitsattributen te verkopen aan stakeholders dan *non-functionals*, vandaar de naamswisseling.
