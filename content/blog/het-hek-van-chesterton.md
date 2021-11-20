---
title: "Het hek van Chesterton"
author: "Karl van Heijster"
date: 2021-11-20T10:03:59+01:00
draft: true
comments: true
tags: ["boeken", "filosofie", "hek van Chesterton", "verandering"]
summary: "Ik ben niet vies van het refactoren van code die ik onduidelijk vind, of zelfs van weggooien van (meestal dode) code. Dat is een goede eigenschap wanneer je het met beleid doet en een slechte als het uit louter enthousiasme voorkomt. De eerste resulteert in helderder en eenvoudiger code, de tweede in buggy software. Waar zit hem precies het onderscheid in? Het antwoord vond ik in *Software Engineering at Google* in het hoofdstuk over kennisdeling."
---

Ik ben niet vies van het refactoren van code die ik onduidelijk vind, of zelfs van weggooien van (meestal dode) code. Dat is een goede eigenschap wanneer je het met beleid doet en een slechte als het uit louter enthousiasme voorkomt. De eerste resulteert in helderder en eenvoudiger code, de tweede in buggy software.


## Context


Waar zit hem precies het onderscheid in? Het antwoord vond ik in [*Software Engineering at Google*](https://www.oreilly.com/library/view/building-secure-and/9781492083115/) in het hoofdstuk over kennisdeling. Auteurs [Nina Chen](https://www.linkedin.com/in/ninabikes/) en [Mark Barolak](https://www.linkedin.com/in/mbarolak/) halen het volgende citaat van [G.K. Chersterton](https://en.wikipedia.org/wiki/G._K._Chesterton) aan.


> Bij het hervormen, en niet vervormen, van dingen geldt er een eenvoudig principe; een principe dat vast en zeker een paradox zal worden genoemd. Stel, er bestaat er een bepaald instituut of een bepaalde wet; laten we, voor de eenvoud, een hek of poort als voorbeeld nemen, die over een weg is geplaatst. Het meer moderne type hervormer stapt er opgewekt op af en zegt: "Ik zie de toegevoegde waarde hier niet van; laten we het weghalen." Waarop het meer intelligente type hervormer er goed aan doet te antwoorden: "Als je de toegevoegde waarde er niet van ziet, dan laat ik je het absoluut niet weghalen. Neem wat afstand en denk na. Pas wanneer je terugkomt en me kunt vertellen waarom het er staat, dan sta ik je toe het weg te halen of niet."[^1]


Pas wanneer je de gedachtegang achter een bepaald stuk code hebt doorgrondt, kun je goed en wel beslissen of de code adequaat is voor het doel. Of juist nodeloos complex, of verouderd, of eenvoudigweg overbodig. Die kennis is essentieel om de keuze te maken: laat ik dit staan, pas ik het aan, of gooi ik het weg?


De kwaliteit van code wordt voor een groot deel bepaald door context. Complexe code is een zonde in eenvoudige contexten, maar noodzakelijk in ingewikkelde. En omgekeerd geldt precies hetzelfde.


## Het beestje


Ik geloof niet dat ik een slechte softwareontwikkelaar ben, maar ik zal onmiddellijk bekennen dat ik me vaak zat eerder als Chestertons moderne hervormer gedraag, dan het meer intelligente type. Waarom?


Voor een deel zal het in de aard van het beestje zitten. Ik heb het dan over mijn karakter, maar ook de menselijke aard *an sich*. Wie geen enkele contextuele kennis heeft, weet heel goed dat hij niet zomaar moet handelen. 


Maar wat als je een beetje contextuele informatie hebt? Mensen overschatten hun kennis van zaken in zulke gevallen enorm. Dat is zo, omdat ze nog niet weten wat ze niet weten. Geen wonder dat ze het niet in hun overwegingen meenemen. Dit [Dunning-krugereffect](https://nl.wikipedia.org/wiki/Dunning-krugereffect) heeft heel wat frustrerende debugsessies veroorzaakt.


## Het vak


Maar voor een ander deel zit het denk ik ook in de aard van ons vak. Software heet niet voor niets *soft*: het is makkelijk te wijzigen - of dat zou het in elk geval moeten zijn - en daardoor heerst de verwachting dat dit ook gebeurt. Er bestaat een druk van buitenaf om snel te handelen, zonder alle noodzakelijke context tot je te kunnen nemen.


Sterker nog, zulke gedrag wordt in het vak zelfs gevierd en aangemoedigd. [Mark Zuckerberg](https://nl.wikipedia.org/wiki/Mark_Zuckerberg) zei niet voor niets [*move fast and break things*](https://en.wikipedia.org/wiki/Move_fast_and_break_things). [Het succes van Facebook, Google en Amazon](https://www.panmacmillan.com/authors/jonathan-taplin/move-fast-and-break-things/9781509847709) lijkt nu juist het gevolg van de antithese van het hek van Chesterton te zijn! 


## Zachtheid


Betekent dat dat het hek van Chesterton een achterhaald idee is? Ik denk het niet. Het is niet voor niets zo dat ik het idee leer kennen uit een boek over softwareontwikkeling bij Google.


Chestertons voorbeeld is geladen met vooronderstellingen die niet opgaan voor softwareontwkkelaars. De keuze om een hek weg te halen, met alle gevolgen van dien, is kostbaar. Zulke keuzes moeten weloverwogen genomen worden, want eenmaal genomen zijn ze moeilijk terug te draaien. 


Maar de keuze om code te wijzigen, met alle gevolgen van dien, is relatief goedkoop. De zachtheid van software stelt ons in staat om snel dingen te breken, zeker. Maar het stelt ons ook in staat de gebroken code snel terug te draaien, te inspecteren en te repareren. 


## Middel


De gevolgen hiervan zijn moeilijk te overschatten. Het breken van code kan in worden gezet *als middel om context te vergaren*. Gebroken code wijst ons relatief goedkoop op de toegevoegde waarde van de oorspronkelijke implementatie. De aard van software stelt ons in staat om *move fast and break things* te verenigen met het hek van Chesterton. 


Zijn we daarom vrij om ons als Chestertons moderne hervormers te gedragen, en kunnen we het intelligenter type vaarwel zeggen? Zo ver wil ik niet gaan. Voordat we die conclusie kunnen trekken, zou je toch echt eerst de gedachtegang achter Chestertons hek moeten hebben doorgrond.


[^1]: De vertaling is van mijn hand.