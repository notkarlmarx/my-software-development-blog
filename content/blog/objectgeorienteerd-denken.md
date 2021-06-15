---
title: "Objectgeoriënteerd Denken"
author: "Karl van Heijster"
date: 2021-05-28T12:37:05+02:00
draft: true
comments: true
tags: ["boeken", "leermoment", "objectgeoriënteerd programmeren", "procedureel programmeren"]
summary: "Onlangs las ik *The Object-Oriented Thought Process* van Matt Weisfeld (vijfde editie). Waarom lees ik, ruim vier jaar na mijn eerste regels C#, een inleiding in objectgeoriënteerd programmeren? Nou..."
---

Onlangs las ik [*The Object-Oriented Thought Process*](https://www.oreilly.com/library/view/the-object-oriented-thought/9780135182130/) van Matt Weisfeld (vijfde (!) editie). Waarom lees ik, ruim vier jaar na mijn eerste regels C#, een inleiding in objectgeoriënteerd programmeren?


## Procedurele versus objectgeoriënteerde code


Nou, het viel me op dat onze codebase hier en daar behoorlijk procedureel aandoet. Dat fenomeen uit zich met name in de [services](https://martinfowler.com/eaaCatalog/serviceLayer.html) en aanverwante helpers in onze [domeinlaag](https://docs.microsoft.com/en-us/windows/win32/cossdk/using-a-three-tier-architecture-model). (Waarom helpers, los van het procedurele aspect, geen goed idee zijn, zette ik al [eerder](/blog/21/04/neem-afscheid-van-helpers) uiteen.) Het is de taak van die classes om datgene wat vanuit de front-end naar de back-end wordt verstuurd, te transformeren waar nodig en door te geven aan de data access-laag. 


Zo lang de transformatielogica minimaal is, is het verleidelijk om deze in een helpermethod in dezelfde class te houden. Verleidelijk en begrijpelijk, maar bepaald niet objectgeoriënteerd. Deze gewoonte leidt tot procedurele code die zich eenvoudig van boven naar beneden laat lezen.


Op zich is daar niets mis mee. [Procedureeel programmeren](https://nl.wikipedia.org/wiki/Imperatief_programmeren) is een valide paradigma, net als [objectgeoriënteerd programmeren](https://nl.wikipedia.org/wiki/Objectgeori%C3%ABnteerd). Weisfeld benadrukt dan ook dat die twee stijlen elkaar niet uitsluiten: je bent niet een procedurele  *of* een objectgeoriënteerde programmeur. Integendeel, de stijlen vullen elkaar aan, en een goede programmeur beheerst beide.


Maar toch bezorgt het me jeuk. Dat zal deels een smaakdingetje zijn. Maar een ander deel van me meent dat die code beter moet kunnen, en dat het team hier kansen laat liggen.


## Handvaten


In Weisfelds boek hoopte ik wat handvaten te vinden om de procedurele elementen in onze code te kunnen refactoren tot objecten, met alle voordelen van dien. Het was met name de titel die me die kant op stuurde. Ik wilde het objectgeoriënteerde gedachteproces internaliseren, of liever: de woorden vinden voor datgene wat ik waarschijnlijk al jaren onbewust doe.


Het beoogde publiek van het boek bestaat uit procedurele programmeurs die zich objectgeoriënteerde concepten eigen wil maken. Het grootste gedeelte van *The Object-Oriented Thought Process* is daarom gewijd aan het uitleggen van concepten als [*encapsulatie*](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)), [*inheritance*](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)), [*polymorfisme*](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)) en [*compositie*](https://en.wikipedia.org/wiki/Object_composition). De voorbeelden die Weisfeld daarvoor gebruikt, zijn ontleend aan het dagelijks leven: stel dat je een hond of een auto objectgeoriënteerd uit zou moeten programmeren, hoe zou dat er dan uitzien?


Dat ik van huis uit een objectgeoriënteerde programmeur ben, was desondanks dat geen belemmering om van het boek te leren. Opvallend genoeg zijn het niet de vier bovengenoemde concepten die mij de uitweg wezen uit de onze procedurele services. Wat me op het juiste spoor zette, is een gedachtegang die het hele boek door zo nadrukkelijk op de voorgrond aanwezig is, dat je hem haast over het hoofd zou zien: *het gaat om objecten*.


## Een verzameling helpermethods, of...?


De crux zit hem in het feit dat een helper (of een verzameling helpers) geen object is. Althans, geen vastomlijnd object. Het is een verzameling methods die haast per toeval is ontstaan. En dat zorgt ervoor dat je het design van die class geen best practices honoreert.


Een voorbeeld. Eén van de operaties in onze services, behelsde het zoeken naar een bepaald [item](https://www.imsglobal.org/spec/qti/v3p0/guide#h.w7rp6is7v7fd) in onze database. De logica die hierbij komt kijken, was verspreid over enkele private methods in de service. De benodigde informatie werd aan elke method middels een parameter meegegeven. Dit is een schoolvoorbeeld van procedurele code.


Ik kon al deze methods in één klap naar een static class verplaatsen, zonder de code te breken. Ik had dit de `ItemHelper` kunnen noemen en kunnen menen dat mijn werk er dan op zat.


## Wat is dit voor object?


De objectgeoriënteerde denkstap zit hem in het feit dat ik me nu afvroeg wat voor *object* ik zojuist geschapen had. Ik besloot: een `ItemSearcher`. En omdat die class in vrijwel elke method dezelfde informatie gebruikte, kon ik dat statische wel van de class afhalen, en daar instance variables van maken.


Deze strategie betaalde zich onmiddellijk uit. Middels compositie kon ik deze class ook uitbreiden met diverse `SearchStrategies`, al naar gelang de zoekcriteria. Het maakte de code leesbaarder, meer uitgesplitst, beter testbaar, en... mooier. Gewoon: mooier. (Zoals ik zei: het is deels een smaakdingetje.)


Daarom lees ik, ruim vier jaar na mijn eerste regels C#, een inleiding in objectgeoriënteerd programmeren.
