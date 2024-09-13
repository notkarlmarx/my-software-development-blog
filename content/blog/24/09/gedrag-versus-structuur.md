---
title: "Gedrag versus structuur"
author: "Karl van Heijster"
date: 2024-09-13T08:30:22+02:00
draft: false
comments: true
tags: ["boeken", "refactoren", "software ontwikkelen", "test-driven development", "waarde"]
summary: "Een systeem dat niet precies doet wat het moet doen, maar wel eenvoudig aan te passen is, is meer waard dan een systeem dat precies doet wat het moet doen maar slechts met grote moeite gewijzigd kan worden. Want het gedrag van een systeem *zal* veranderen, hoe dan ook. De wereld verandert, en daarmee de wensen van onze gebruikers en stakeholders. Het is onze taak als softwareontwikkelaars om daarop voorbereid te zijn, en een systeem te ontwikkelen dat daarop voorbereid is."
---

Wat is belangrijker: het gedrag van een systeem of haar structuur? [Robert "*uncle Bob*" Martin]((https://en.wikipedia.org/wiki/Robert_C._Martin)) is er in [*Clean Craftsmanship*](https://www.pearson.com/en-us/subject-catalog/p/clean-craftsmanship-disciplines-standards-and-ethics/P200000009529/9780136915713) heel duidelijk over: het onderhouden van de structuur van een codebase heeft voor ons ontwikkelaars voorrang op het wijzigen van het gedrag.


Daarmee zegt hij niet dat het gedrag van een systeem *on*belangrijk is. Immers, een perfect gestructureerd systeem dat geen enkel bruikbaar gedrag vertoont, is waardeloos. 


Maar: als we geconfronteerd worden met een gewenste gedragswijziging die ten koste gaat van de structuur van het systeem, dan is het onze eerste prioriteit om de structuur aan te passen zodat het nieuwe gedrag daar goed in past. Anders gezegd: het is onze taak om de software *soft* te houden. 


Een systeem dat niet precies doet wat het moet doen, maar wel eenvoudig aan te passen is, is meer waard dan een systeem dat precies doet wat het moet doen maar slechts met grote moeite gewijzigd kan worden. Want het gedrag van een systeem *zal* veranderen, hoe dan ook. De wereld verandert, en daarmee de wensen van onze gebruikers en stakeholders. Het is onze taak als softwareontwikkelaars om daarop voorbereid te zijn, en een systeem te ontwikkelen dat daarop voorbereid is.


## Test-Driven Development


Tegelijkertijd zegt Martin ook: ontwikkel je systeem aan de hand van [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD). Dat wil zeggen: schrijf eerst een falende test, laat deze vervolgens slagen, en refactor daarna je implementatie -- de welbekende *red*-*green*-*refactor*-cyclus. (Zie ook [deze blog](/blog/22/03/agile-en-test-driven-development/ "'Agile en Test-Driven Development'").)


Staat dit niet op gespannen voet met het idee dat structuur voorrang heeft op gedrag? Immers, wie TDD beoefent *begint* met het gedrag (*red* en *green*) en past *daarna* pas de structuur aan (*refactor*). Deze manier van werken lijkt dus gedrag voorrang te geven op structuur.


Maar dat is schijn, zegt Martin. Het geheim zit 'm in de *refactor*-fase. Ja, TDD begint met gedrag, maar dwingt daarna af te investeren in structuur *voordat er nieuw gedrag wordt toegevoegd*. Wie de cyclus van TDD netjes volgt, zorgt ervoor dat de structuur van de code altijd goed onderhouden is voordat er nieuw gedrag aan het systeem wordt toegevoegd.


## Rommel


Het is belangrijk om te begrijpen wat Martin hier *niet* zegt. Hij zegt niet dat refactoren de structuur van de code per se voorbereidt op de volgende gedragswijziging. 


Het is vaak zo dat je niet precies weet hoe de structuur van de code eruit zou moeten zien voordat de gedragswijziging is doorgevoerd. Collega's die met mij [pairen](/tags/pair-programming/ "Blogs met de tag 'pair programming'"), horen me regelmatig zeggen: "Ik ga dit eerst lelijk doen." Dan hack ik wat lompe code in elkaar om een falende test te doen slagen. Daarna vraag ik: "Oké, hoe maken we dit mooi?" Dan refactor ik de code zodat het nieuwe gedrag er mooi in past. Dit soort structuurwijzigingen vinden plaats nadat het gedrag is toegevoegd. 


Wat Martin zegt, is dat er pas nieuw gedrag wordt toegevoegd nadat de structuur is geoptimaliseerd voor het huidige gedrag. Dat stelt je in staat om, niet gehinderd door een rommelige structuur, verder te gaan met de volgende gedragswijziging.


Als je programmeren vergelijkt met koken, dan is refactoren het schoonhouden van het keukenblad na elke stap in het bereidingsproces. Wie tussen de stappen door de tijd neemt om op te ruimen, hoeft naarmate het proces vordert niet om een steeds grotere berg rommel heen te werken -- met alle ongemak en tijdverlies van dien. 


## Empirisch


De gedragswijziging gaat vooraf aan de structuurwijziging, maar de structuurwijziging is een noodzakelijke stap vóór de volgende gedragswijziging. 


Dat vertelt ons iets interessants over de verhouding tussen gedrag en structuur. Het gedrag komt eerst, omdat het gedrag de directe waarde levert voor de gebruikers en stakeholders. De structuur komt daarna -- omdat we niet op voorhand weten wat de beste structuur is om het gedrag te ondersteunen. 


Dat is waarom een *big design up front* slechts op papier een goed idee is. De werkelijkheid blijkt altijd weerbarstiger dan we op voorhand hadden durven dromen. Daarom is het beter om de werkelijkheid het ontwerp te laten dicteren, in plaats van de werkelijkheid te proberen te passen in de mal die we op voorhand gedefinieerd hebben. Structuur is, kortom, een empirische aangelegenheid.[^1]


## Tegenintuïtief


De spanning tussen het feit dat we structuur aan de ene kant belangrijker achten dan gedrag, terwijl we desondanks gedrag als beginpunt nemen in ons ontwerp, is ogenschijnlijk. Deze komt voort uit de aanname dat we de belangrijkste dingen het eerst (moeten) doen. Maar die aanname gaat niet op. Door het gedrag eerst te definiëren, kunnen we een betere inschatting maken van hoe de structuur eruit dient te zien. 


We bekommeren ons in TDD om de structuur *nadat* het gedrag is gedefinieerd, juist *omdat* de structuur belangrijker is. -- Softwareontwikkeling zit vol met zulke heerlijk tegenintuïtieve inzichten.


[^1]: De ondertitel van [Kent Becks](https://www.kentbeck.com/) [nieuwste boek](https://www.oreilly.com/library/view/tidy-first/9781098151232/ "Kent Beck, 'Tidy First?: A Personal Exercise in Empirical Software Design', O'Reilly Media, 2023") is niet voor niets *A Personal Exercise in Empirical Software Design*. 
