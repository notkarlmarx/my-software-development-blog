---
title: "Horizontale of verticale PBI's?"
author: "Karl van Heijster"
date: 2021-10-25T08:09:26+02:00
draft: false
comments: true
tags: ["agile ontwikkeling", "incrementele ontwikkeling", "product backlog items", "productiviteit", "scrum", "software ontwikkelen", "sprint review", "waarde"]
summary: "Een risico van horizontaal ontwikkelen is dat je veel tijd besteedt aan de back-end, om er vervolgens bij de implementatie van de front-end achter te komen dat je iets over het hoofd hebt gezien. Met als gevolg dat je alsnog verticaal aan het ontwikkelen slaat. Dat is niet alleen irritant, het is ook ontzettend inefficiënt!"
---

Je kunt het ontwikkelen van software op een heleboel manieren oppakken. Maar één ding is onoverkomelijk: je zal de grote berg te verzetten werk moeten ophakken in kleinere stukken. Ook dat kan op een heleboel manieren. Je zou het werk bijvoorbeeld horizontaal kunnen ophakken of verticaal.


Laten we uitgaan van een applicatie met eenvoudige [CRUD](https://nl.wikipedia.org/wiki/CRUD)-functionaliteit, die bestaat uit een front- en een back-end. Ofwel je implementeert eerst de CRUD-functies aan de back-end, en dan aan de front end. Je hebt het werk dan horizontaal opgehakt. Ofwel je implementeert eerst de C aan de front- en de back-end, dan de R, dan de U en dan de D. Je hebt het werk dan verticaal opgehakt.


## De wet van Conway


Welke van de twee manieren is de beste? Dat hangt er natuurlijk (*natuurlijk!*) vanaf. Eén van de factoren die bepaalt of het verstandig is om je werk horizontaal of verticaal op te hakken, is de manier waarop teams zijn vormgegeven in de organisatie. Stel, er bestaat een team voor de front-end en een team voor de back-end. In dat geval ligt een horizontale werkwijze voor de hand. 


Je kunt je ook voorstellen dat er verschillende teams verantwoordelijk zijn voor één functionaliteit (of een handvol functionaliteiten). Dit zie je bijvoorbeeld bij de ontwikkeling van microservices. In dat geval ligt een verticale werkwijze voor de hand. 


Dit is een uitvloeisel van de [wet van Conway](https://en.wikipedia.org/wiki/Conway%27s_law). Deze stelt het ontwerp van een systeem een kopie zal zijn van de communicatiestructuren binnen de ontwerpende organisatie. Simpel gezegd: twee teams, twee subsystemen; vier teams, vier subsystemen, etc.. Het ligt voor de hand ligt om de PBI's op te hakken per subsysteem. Als de verdeling van de subsystemen horizontaal is, dan hak je het werk horizontaal op. Is de verdeling verticaal, dan doe je dat verticaal. 


## *Agile* ontwikkeling


Maar wat als er sprake is van één team dat verantwoordelijk is voor de hele applicatie? In dat geval gaan er inhoudelijke argumenten spelen. Ik neig dan naar verticaal ophakken.


De hoofdreden daarvoor is dat een verticale werkwijze het best past bij een [*agile*](https://nl.wikipedia.org/wiki/Agile-softwareontwikkeling) omgeving. Elke verticale *slice* software die je oplevert, levert immers onmiddellijk waarde. Het is voor een eindgebruiker onmiddellijk waardevol om objecten te kunnen aanmaken, zelfs al kan deze er op dit moment nog niets mee. (Aangenomen, natuurlijk, dat het lezen, updaten en verwijderen van deze objecten op korte termijn volgt!)


Een horizontale werkwijze associeer ik eerder met een [watervalmodel](https://nl.wikipedia.org/wiki/Watervalmethode). Het implementeren van volledige functionaliteit aan de back-end, levert voor een eindgebruiker in eerste instantie niets op. Pas als de volledige front-end ontwikkeld is, plukt deze daar de vruchten van. In plaats van incrementeel functionaliteit toe te voegen, krijgt de eindgebruiker in één klap het eindresultaat.


En gerelateerd hieraan: het levert leukere Sprint Reviews op. Je hebt immers elke keer een nieuwe *slice* functionaliteit te demo'en, in plaats van dat je moet verkopen dat je onder water echt heel hard bezig bent geweest.


## Afstemming


Mijn tweede reden is pragmatischer. Hoewel front- en back-end in principe los van elkaar zouden moeten kunnen bestaan, dient er wel afstemming tussen beide plaats te vinden. Wat is de snelste manier om te valideren of de twee goed op elkaar aansluiten? Door ze in samenspel op te pakken!


Een risico van horizontaal ontwikkelen is dat je veel tijd besteedt aan de back-end, om er vervolgens bij de implementatie van de front-end achter te komen dat je iets over het hoofd hebt gezien. Met als gevolg dat je alsnog verticaal aan het ontwikkelen slaat. Dat is niet alleen irritant, het is ook ontzettend inefficiënt!


## Reikwijdte


Een derde reden: verticaal ben je, ironisch genoeg, met minder dingen tegelijk bezig. 


Natuurlijk, op technisch vlak houd je je juist met meer zaken bezig, je gebruikt immers diversere technieken. Maar deze zijn, juist omdat ze door hun respectievelijke subsystemen afgebakend zijn, eenvoudig te scheiden in je hoofd. Je werkzaamheden aan de front- en back-end zullen daardoor heus niet zo eenvoudig door elkaar gaan lopen.


Aan de front-end is dat minder evident. Waarom werkt de *create*-functionaliteit nou niet? Wat het antwoord ook is, het probleem zit aan de voorkant. En elke fix voor die bug, kan impact hebben op de de *read* of *update*-functionaliteit - die *qua* horizontale *slice* jouw verantwoordelijkheid zijn. Dat maakt het makkelijk om kleine individuele problemen uit te laten groeien tot één groot gezamenlijk probleem. 


## Slaap


Ik leerde deze les onlangs op een harde manier, toen ik een paar nachten slecht geslapen had en de complexiteit van een handvol functionaliteiten me gauw boven het hoofd groeide. Met een vermoeide kop is het moeilijk om je op de C te richten, als je tegelijkertijd ziet dat de R nog niet werkt en de U foutmeldingen geeft.


Verticale PBI's hebben dus mijn voorkeur boven horizontale. Maar een goede nachtrust heeft mijn voorkeur boven beide.
