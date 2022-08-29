---
title: "Over afwas en software"
author: "Karl van Heijster"
date: 2022-08-29T12:31:09+02:00
draft: true
comments: true
tags: ["beroepsdeformatie", "refactoren"]
summary: "Afwassen is net als software ontwikkelen. Althans, ik probeer mijn afwas net zo aan te pakken zoals ik mijn software het liefst ontwikkel. Het fundamentele idee wordt kernachtig verwoord door Kent Beck in de volgende quote: \"*For each desired change, make the change easy (warning: this may be hard), then make the easy change.*\""
---

Mijn vrouw en ik zitten heel anders in elkaar. Neem nu bijvoorbeeld de manier waarop we afwassen.


Als mijn vrouw gaat afwassen, dan pakt ze een schuursponsje. Ze doet daar wat afwasmiddel op, zet de kraan aan en begint met afwassen.


Als ik ga afwassen, dan verplaats ik eerst al het vuile eetgerei naar de linkerkant van de gootsteen. Dan pak ik een schuursponsje, doe daar wat afwasmiddel op, zet de kraan aan en begin me afwassen.


## Beter


Nu ben ik de laatste die zal beweren dat de ene manier beter is dan de andere ~~want mijn vrouw leest mee en als ik te hoog van de toren blaas, dan mag ik tot in de lengte der dagen afwassen~~. Maar naar mijn persoonlijke, uiterst subjectieve en nauwelijks gefundeerde mening, is mijn strategie beter.


Als mijn vrouw begint af te wassen, dan loopt ze binnen de kortste keren aan tegen het feit dat ze nergens plek heeft om de schone borden neer te kunnen zetten. Ze heeft de keus: ruimte maken of beginnen met afdrogen. Hoe dan ook, het houdt een onderbreking van haar huidige werkzaamheden in.


Dat is een probleem waar ik niet tegenaan loop. Doordat ik alle afwas naar de linkerkant van de gootsteen heb geplaatst, heb ik per definitie het rechtergedeelte vrij. Welke uitdagingen ik tijdens het afwassen ook tegenkom (zie bijvoorbeeld [deze blog](/blog/21/11/schorseneren-en-software-architectuur/)), ruimtegebrek is er in elk geval niet een van.


## Makkelijke verandering


Waarom vertel ik dit verhaal? Omdat afwassen net is als software ontwikkelen. Althans, ik probeer mijn afwas net zo aan te pakken zoals ik mijn software het liefst ontwikkel. Het fundamentele idee wordt kernachtig verwoord door [Kent Beck](https://www.kentbeck.com/) in de volgende quote:


> For each desired change, make the change easy, then make the easy change.[^1]


Afwassen terwijl het volledige keukenblad is bezaaid met vuile borden, is een moeilijke wijziging. Je moet immers constant afwisselen tussen afwassen, afdrogen en borden verplaatsen. 


Om die taak te vergemakkelijken, is het verstandig om je eerst bezig te houden met de plaatsing van de vuile borden op het keukenblad. Als dat probleem eenmaal is opgelost, is het een stuk eenvoudiger om af te wassen. Dan is 't een kwestie van de borden verplaatsen van de linkerkant van het keukenblad, via de gootsteen, naar de rechterkant.


## Refactoren


In softwaretaal zou je kunnen zeggen: het verplaatsen van de vaat is een refactorslag. Het daadwerkelijk schoonmaken van de borden is het implementeren van een feature.


Soms - vaak - nee, meestal is het verstandig om éérst je code te refactoren, voordat je een nieuwe feature implementeert. Die refactorslag is bedoeld om de code voor te bereiden op de komende functionaliteit. Eérst pas je de code aan, zodat deze makkelijk een bepaalde kant op uit te breiden is. Daarna breid je de functionaliteit uit - die bepaalde kant op.


Merk op dat het implementeren van de nieuwe feature eenvoudig hoort te zijn, maar dat de refactorslag dat niet per se is. De code in een juiste staat krijgen om de volgende feature te kunnen implementeren, is juist het moeilijke gedeelte.


En die moeilijkheid zit 'm op twee gebieden. Ten eerste kan het inhoudelijk moeilijk zijn om de code aan te passen. Anders gezegd: soms moet je veel code omschrijven om iets nieuws mogelijk te kunnen maken. Dat is in zekere zin de minst interessante moeilijkheid.


## Moeilijker


Het tweede gebied is subtieler. Veel ontwikkelaars zijn zich ofwel niet bewust van de zinvolheid van een voorbereidende refactorslag, ofwel ze voelen zich niet zeker genoeg om deze te ondernemen met ongeduldige stakeholders in hun kielzog. In hun beleving is elke minuut die ze niet besteden aan het toevoegen van nieuwe features, een verloren moment. Of, wat minder gechargeerd: refactoren voegt in hun beleving geen waarde toe zoals features dat wel doen.


Het is waar: de waarde die een refactorslag toevoegt, is van een heel andere aard dan die van een nieuwe feature. De waarde van de laatste is onmiddellijk voelbaar voor de business. De waarde van de eerste zit 'm in het feit dat deze de consistentie waarborgt van het proces van businesswaarde leveren. En hoewel dat minstens zo waardevol is als businesswaarde, is deze een stuk moeilijker naar stakeholders te communiceren.


De denkstap is daarom snel gemaakt dat zo'n refactorslag niet voldoende waarde heeft om te ondernemen. Dat hoeft overigens geen expliciete overtuiging te zijn van de ontwikkelaar in kwestie. Het kan een gevoel zijn, ongedifferentieerd en onuitgesproken. Dat gevoel is, denk ik, de reden waarom de ontwikkeling van veel softwareprojecten na verloop van tijd steeds stroperiger verloopt. 


En het is de reden waarom mijn vrouw pertinent weigert om éérst de vaat te verplaatsen, voordat ze aan het afwassen slaat. Niet dat daar iets mis mee is. Maar ik vind mijn manier wel de betere.


[^1]: Klik [hier](https://twitter.com/kentbeck/status/250733358307500032/) voor de oorspronkelijke Tweet.
