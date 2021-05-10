---
title: "Hoe Ik Mijn PBI's Opzet"
date: 2021-05-07T10:49:41+02:00
draft: true
comments: true
tags: []
summary: ""
---

Het is niemands favoriete klus: [Product Backlog Items](https://www.scrum.org/resources/what-is-a-product-backlog) (PBI's) aanmaken om de komende [Sprints](https://www.scrum.org/resources/what-is-a-sprint-in-scrum) op te kunnen pakken. En toch, het is een onderdeel van je werk als ontwikkelaar. En een belangrijk onderdeel ook, want zonder goed opgezette PBI's kan een team helemaal niets.


Hoewel, een team kan natuurlijk wel in het wilde weg gaan coderen, maar ik betwijfel of een opdrachtgever daar geld voor neer zou willen leggen. Nog los van de vermoeiende, chaotische situatie die het voor het team zelf creëert.


## Niet mijn probleem?


Er bestaan vast en zeker ontwikkelaars die menen dat het aanmaken van PBI's niet hun taak (c.q. probleem) is. Volgens deze ontwikkelaars is het aanmaken van PBI's de verantwoordelijkheid van bijvoorbeeld een business- of informatieanalist. 


Helemaal onjuist is die veronderstelling niet, want het *is* ook de taak van een analist om PBI's aan te maken. Maar daar volgt niet uit dat het niet óók de taak van de ontwikkelaar is om dat te doen. 


De aard van door ontwikkelaars geschreven PBI's zal doorgaans verschillen van die van de analist. Een analist zal doorgaans PBI's schrijven waarin nieuwe features functioneel uitgewerkt worden. Een ontwikkelaar zal vaker technische PBI's schrijven, bijvoorbeeld voor het wegwerken van technische schuld of het doorvoeren van een architecturele wijziging die nieuwe features mogelijk maakt.


Merk op dat een analist dit soort PBI's waarschijnlijk niet eens aan *kan* maken, omdat ze buiten zijn expertise en/of blikveld vallen.


Het is aan de analist om de gewenste features helder te verwoorden, maar het is aan de ontwikkelaar om ervoor te zorgen dat de code op een dusdanig niveau is dat die features ook ondersteund kunnen worden. Soms moet daar extra werk voor worden verzet. En wat dat werk precies inhoudt zal toch iemand uit moeten werken.


## Wel jouw probleem


De meeste ontwikkelaars vinden het helemaal niet leuk om PBI's te schrijven. Ze houden zich liever met code bezig. Helemaal verwonderlijk is dat ook niet. Als ze niets liever deden dan features uitwerken, dan waren ze wel analist geworden.


Maar het wordt een probleem wanneer ze hun PBI's daarom afraffelen. Ik denk dat veel ontwikkelaars heus wel weten dat het schrijven van PBI's onder hun takenpakket valt, maar dat ze die verantwoordelijkheid liever niet hebben. Wat dan gebeurt, is dat ze hun individuele verantwoordelijkheid af proberen te wentelen op het team als geheel, tot nadeel van iedereen. 


Zulke ontwikkelaars werken hun PBI's minimaal werken en slingeren deze vervolgens de Refinement in. Dit zorgt voor een moeizaam en inefficiënt verloop van de meeting. Moeizaam, omdat het team veel tijd kwijt is aan elk PBI. Inefficiënt, omdat zes, zeven, acht man met z'n allen het werk van één persoon doen. 


Denk je eens in hoeveel loonkosten je werkgever maakt wanneer je team dat ene PBI collectief uitwerkt dat je in je eentje in een halfuurtje voor had kunnen bereiden. Zou jij dat geld er zelf voor over hebben, als jij de baas zou zijn?


## Hoe ik mijn PBI's opzet


Neem de tijd voor je PBI's. Structureer ze zodanig dat je team je oplossing (én het probleem dat je oplost!) onmiddellijk in grote lijnen kan begrijpen. Dat stelt hen in staat om snel eventuele onduidelijkheden te identificeren.


Ik structureer mijn PBI's altijd volgens een vaste vorm:


> ### [Titel]
>
> #### Beschrijving
>
> *Als* [actor] *wil ik* [deze feature] *zodat* [deze waarde voor de business wordt toegevoegd].
>
> ##### Context
>
> [Een korte beschrijving van het probleem dat wordt ervaren.]
>
> ##### Oplossingsrichting
>
> [Een korte beschrijving van de manier waarop dat probleem wordt opgelost.]
>
> #### Acceptatiecriteria
>
> * [Eerste criterium]
> * [Tweede criterium]
> *  ...


Het voordeel van een vaste vorm is je niet elke keer het wiel opnieuw hoeft uit te vinden. Dat geldt zowel voor de schrijver als de lezer. 


Voor de schrijver snijdt een vaste structuur de mogelijkheid van een *writer's block* af. Doordat alle elementen van tevoren bekend zijn, kun je snel en efficiënt alle benodigde informatie ordenen. Bovendien kun je er, als je de structuur streng volgt, zeker van zijn niets te zijn vergeten. 


Ook lezers weten snel waar ze moeten kijken als ze bepaalde informatie nodig hebben. Dat vermindert het aantal (achteraf onnodig gebleken) verhelderingsvragen tijdens Refinements. Het valt hen ook sneller op als er informatie mist.


## De structuur


Laten we alle onderdelen kort nalopen.

- In de **titel** staat een kort weergegeven wat er gebouwd moet worden. Bijvoorbeeld: *Gebruiker kan inloggen met zijn Facebook-account*. Of: *Businesslogica uit UserRepository splitsen*.

- De **beschrijving** begint met de bekende formulering van een [*user story*](https://en.wikipedia.org/wiki/User_story). Veel ontwikkelaars laten deze achterwege, omdat dit meestal impliciet duidelijk wordt geacht. Maar of dat ook zo is...?

  Het voordeel van de *user story* expliciet maken zit 'm echter vooral in het laatste deel van de formule. Als je geen toegevoegde waarde voor de business kunt verzinnen voor je PBI, moet deze dan wel opgepakt worden? Wie help je met deze wijziging? Is dat ook wat je wil bereiken? Veel ontwikkelaars denken hier veel te weinig over na.

- In de **context** wordt met wat meer woorden uitgewerkt welk probleem je op wil lossen. Hier kun je ook kort uiteenzetten op welke processen het probleem en de te bouwen oplossing invloed heeft. Het is goed je hiervan bewust te zijn, omdat deze informatie jou of je teamleden tijdens een Refinement op het spoor kunnen zetten van een betere oplossing.

  Het weglaten van dit onderdeel heeft tot gevolg dat het PBI erg technisch van aard kan worden. Dat verlegt de focus van het kiezen van de beste oplossing voor het businessprobleem naar het kiezen van de "beste" technische implementatie. Die in een vacuum te presenteren en te bediscussiëren kan een demotiverende werking hebben op het team, omdat niet duidelijk is waarom je ontwikkelt wat je ontwikkelt.

- In de **oplossingsrichting** wordt in proza beschreven wat er - volgens de auteur - moet gebeuren om het probleem op te lossen. Dit lostrekken van de context heeft als doel ervoor te zorgen dat functionele en technische discussies niet door elkaar gaan lopen. Bovendien kan de oplossing makkelijk worden afgezet tegen het licht van de probleemstelling.

- De oplossingrichting wordt geformaliseerd in de vorm van **acceptatiecriteria** waar de code aan moet voldoen om deze als [*done*](https://www.scrum.org/resources/blog/getting-started-definition-done-dod) te kunnen kenmerken.


## De juiste oplossing


Ik zal niet beweren dat deze structuur de enige of zelfs de beste manier is om je PBI's mee op te zetten. Wat ik wel beweer, is dat ik in de loop der jaren heb gemerkt dat PBI's die deze onderdelen ontberen, het risico met zich meebrengen de efficiëntie van een Refinement ernstig naar beneden te halen. 


Of erger nog: ertoe leiden dat verkeerde oplossingen worden gebouwd. Terwijl je juist in het schrijven van een PBI de afstand van je code kan nemen die je in staat stelt het probleem scherp te krijgen. 


Het schrijven van PBI's is één van je taken als ontwikkelaar. En het is een belangrijke taak. Neem hem dus serieus.


Hoe bouw jij je PBI's op?
