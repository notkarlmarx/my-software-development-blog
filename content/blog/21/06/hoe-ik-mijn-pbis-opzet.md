---
title: "Hoe Ik Mijn PBI's Opzet"
date: 2021-06-28T08:45:22+02:00
draft: false
comments: true
tags: ["product backlog items", "scrum"]
summary: "Immitatie is de hoogste vorm van vlijerij, zegt men wel. En inderdaad, toen ik laatst zag dat onze stagiaire de structuur van mijn PBI's had overgenomen, kon ik mezelf een gevoel van trots niet ontzeggen. Misschien is het een goed idee om uiteen te zetten hoe ik mijn PBI's opzet en waarom."
---

Immitatie is de hoogste vorm van vlijerij, zegt men wel. En inderdaad, toen ik laatst zag dat onze [stagiaire](/blog/21/06/niet-zo-bijzonder/) de structuur van mijn PBI's had overgenomen, kon ik mezelf een gevoel van trots niet ontzeggen. Misschien is het een goed idee om uiteen te zetten hoe ik mijn PBI's opzet en waarom.


## Een vaste vorm


Ik structureer mijn PBI's vrijwel altijd volgens een vaste vorm. Het voordeel van een vaste vorm is je niet elke keer het wiel opnieuw hoeft uit te vinden. Dat geldt zowel voor de schrijver als de lezer. 


Voor de schrijver snijdt een vaste structuur de mogelijkheid van een *writer's block* af. Doordat alle elementen van tevoren bekend zijn, kun je snel en efficiënt alle benodigde informatie ordenen. Bovendien kun je er, als je de structuur streng volgt, zeker van zijn niets te zijn vergeten. 


Ook lezers weten snel waar ze moeten kijken als ze bepaalde informatie nodig hebben. Dat vermindert het aantal (achteraf onnodig gebleken) verhelderingsvragen tijdens Refinements. Het valt hen ook sneller op als er informatie mist.


## De structuur


Mijn PBI's hebben de volgende structuur (waarbij de zinsdelen tussen rechte haken ("[" en "]") placeholders zijn):


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


Laten we alle onderdelen kort nalopen.

- In de **titel** staat een kort weergegeven wat er gebouwd moet worden. Een functioneel voorbeeld: *Gebruiker kan inloggen met zijn Facebook-account*. En een technische: *Businesslogica uit UserRepository halen*.

- De **beschrijving** begint met de bekende formulering van een [*user story*](https://en.wikipedia.org/wiki/User_story). Veel ontwikkelaars laten deze achterwege, omdat dit meestal impliciet duidelijk wordt geacht. Soms is dat zo, maar minstens zo vaak ook niet. Ik kan hier kort over zijn: de waarde van deze zin invullen weegt altijd op tegen de tijd die daarvoor nodig is. 

  Het voordeel van de *user story* expliciet maken zit 'm echter vooral in het laatste deel van de formule. Als je geen toegevoegde waarde voor de business kunt verzinnen voor je PBI, moet deze dan wel opgepakt worden? Wie help je met deze wijziging? Is dat ook wat je wil bereiken? Veel ontwikkelaars denken hier veel te weinig over na.

- In de **context** wordt met wat meer woorden uitgewerkt welk probleem je op wil lossen. Hier kun je ook kort uiteenzetten op welke processen het probleem (en de te bouwen oplossing) invloed heeft. Het is goed je hiervan bewust te zijn, omdat deze informatie jou of je teamleden tijdens een Refinement op het spoor kunnen zetten van een betere oplossing.

  Het weglaten van dit onderdeel heeft tot gevolg dat het PBI erg technisch van aard kan worden. Dat verlegt de focus van het kiezen van de beste oplossing voor het businessprobleem naar het kiezen van de "beste" technische implementatie. Die in een vacuüm te presenteren en te bediscussiëren kan een demotiverende werking hebben op het team, omdat niet duidelijk is waarom je ontwikkelt wat je ontwikkelt.

- In de **oplossingsrichting** wordt in proza beschreven wat er - volgens de auteur - moet gebeuren om het probleem op te lossen. Dit lostrekken van de context heeft als doel ervoor te zorgen dat functionele en technische discussies niet door elkaar gaan lopen. 

  Bovendien kan de oplossing makkelijk worden beoordeeld tegen het licht van de probleemstelling. Is er een betere oplossing mogelijk? Dan is in één oogopslag duidelijk waar en hoe het PBI aangepast moet worden. 

- De oplossingrichting wordt geformaliseerd in de vorm van **acceptatiecriteria** waar de code aan moet voldoen om deze als [*done*](https://www.scrum.org/resources/blog/getting-started-definition-done-dod) te kunnen kenmerken.


## De juiste oplossing


Deze structuur zorgt ervoor dat het team de door jou bedachte oplossing én het probleem dat je daarmee oplost (!) in één oogopslag kan begrijpen, in elk geval in grote lijnen. Dat stelt hen in staat om snel eventuele onduidelijkheden te identificeren.


Ik zal niet beweren dat deze structuur de enige of zelfs de beste manier is om je PBI's mee op te zetten. Wat ik wel beweer, is dat ik in de loop der jaren heb gemerkt dat PBI's die deze onderdelen missen, het risico met zich meebrengen de efficiëntie van een Refinement ernstig naar beneden te halen. 


Of erger nog: ertoe leiden dat verkeerde oplossingen worden gebouwd. Terwijl je juist in het schrijven van een PBI de afstand van je code kan nemen die je in staat stelt het probleem scherp te krijgen. 


Precies daarom is het schrijven van PBI's zo'n belangrijke taak [voor een ontwikkelaar](/blog/21/06/schrijf-pbis-en-doe-het-goed/). Neem hem dus serieus.


Hoe bouw jij je PBI's op?
