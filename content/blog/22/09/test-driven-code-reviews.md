---
title: "Test-driven code reviews"
author: "Karl van Heijster"
date: 2022-09-09T07:58:39+02:00
draft: false
comments: true
tags: ["code reviews", "testen"]
summary: "Door een alfabetisch toeval presenteert Azure DevOps elk *pull request* van mijn team in deze volgorde: eerst de front-end, dan de back-end - de API, de businesslogica, de datatoegang en het model - en ten slotte te tests. Onlangs stelde ik de vraag hoe je eigenlijk code reviewt - en waar je het best kunt beginnen bij zo'n beoordeling. Ik heb er een tijdje op zitten broeden, en ik denk dat ik eruit ben."
---

Door een alfabetisch toeval presenteert [Azure DevOps](https://azure.microsoft.com/nl-nl/services/devops/) elk *pull request* (PR) van mijn team in deze volgorde: eerst de front-end, dan de back-end - de API, de businesslogica, de datatoegang en het model - en ten slotte te tests.


Onlangs stelde ik de vraag [hoe je eigenlijk code reviewt](/blog/22/08/hoe-review-je-eigenlijk-code/) - en waar je het best kunt beginnen bij zo'n beoordeling. Ik heb er een tijdje op zitten broeden, en ik denk dat ik eruit ben.


(In wat volgt, heb ik het alleen over fikse PR's, die meerdere lagen van het systeem raken. Kleine PR's - die één of een handvol files raken -, kunnen uiteraard eenvoudig in andere volgorde worden afgelopen.)


## 1. De tests


Waar begin je je code review? Wat denk je van deze: *bij de tests*.


Waarom de tests? Omdat de tests fungeren als *low level*-documentatie van wat de code beoogt te doen. De tests geven je als code reviewer als het ware de context waartegen je de implementatie kunt beoordelen.


Let op de volgende zaken: zijn de tests makkelijk te begrijpen? Is de naamgeving helder en eenduidig? Bevatten de tests geen overbodige informatie? Abstraheren de tests geen relevante informatie? - Kortweg: heb ik na het lezen van de tests een goed idee van het verantwoordelijkheden van de code?


Vraag jezelf ook af: zijn de tests compleet? Wordt alleen het *happy path* getest, of heeft de ontwikkelaar zich ook afgevraagd wat er gebeurt bij afwijkende inputs? Wat als je *hier* een `null` meegeeft? Wat als je *daar* een negatief getal invoert? - Bedenk: tests bewijzen niet dat de code vrij is van bugs, hun functie is te signaleren wanneer dat wél het geval is. Hoe completer de tests, hoe zekerder je kunt zijn over de kwaliteit van de code.


Wat als een PR geen tests bevat? Dan zou dat een goede reden kunnen zijn om de wijziging in zijn geheel te blokkeren. Hoe kun je er als reviewer immers zeker van zijn dat de code doet wat het beoogt, als je collega daar geen bewijs van levert?[^1]


## 2. Het model (of: de API)


Wanneer je de tests voldoende hebt bekeken, kun je je richten op wijzigingen in het model. Het gaat in dit geval om wijzigingen in interfaces, toegevoegde DTO's, gewijzigde properties op domeinobjecten - dat soort dingen.


Bekijk deze wijzigingen los van de context waarin ze gebruikt worden, en vraag je af: kan ik op basis van deze informatie een begrip vormen van het doel van deze code? - Kijk nog niet naar de plekken waar het model gebruikt wordt! (Afgezien van de tests, natuurlijk.) Kijk niet naar de implementatie van de methods! 


Kun je op basis van de naamgeving afleiden wat de functie van de code is? Passen de properties en methods bij de classnamen? Staat alles op de plek waar je het zou verwachten?


Het doel van dit deel is vaststellen: is deze code begrijpelijk ontworpen? Staat alles op de juiste plek? Zou ik als ontwikkelaar op een intuïtieve manier deze code kunnen gebruiken? 


Vraag jezelf af: wat is de uitdrukkingskracht van de code? Elke ontwikkelaar kan op basis van de implementatie nagaan wat de code feitelijk doet. Maar goede code bespaart ontwikkelaars die moeite. Dus: is dit goede code of gewoon... code?


## 3. Implementatie


Pas als je voor jezelf hebt genoteerd wat je denkt dat de code doet, ga je naar de implementatie kijken. Komt deze overeen met wat je verwacht had?


Zo nee, waarom niet? Houd de naamgeving nogmaals tegen het licht. Wat is de bron van de verwarring? Wat waren je aannames? Waren die terecht? Kun je, nu je de implementatie hebt gezien, een betere naam bedenken?


Zo ja, kijk dan of er mogelijkheden tot verbetering zijn. Kan een bepaald algoritme efficiënter? Zou een bepaald stuk logica eigenlijk geabstraheerd moeten worden naar een aparte class? Waarom wordt hier een [`List`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1) gebruikt en geen [`IEnumerable`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerable)? [*Implementing Effective Code Reviews*](https://link.springer.com/book/10.1007/978-1-4842-6162-0) van [Giuliana Carullo](https://www.linkedin.com/in/giucar/) biedt een uitstekend, handzaam overzicht van alle dingen waar je op kunt letten in deze fase van de code review.


Merk op dat deze exercitie is wat ontwikkelaars gewoonlijk onder code reviews verstaan. Bij mij komt deze stap pas aan het eind van de rit. Mijn reden daarvoor is eenvoudig: dit deel van de codebase kan - en moet! - morgen totaal op de schop gaan. 


In een goed functionerend team wordt code constant gerefactord door ontwikkelaars die gezamenlijk eigenaarschap voelen voor de code waar ze verantwoordelijk voor zijn. In zekere zin is de implementatie het minst belangrijke deel van coderen. Als je code helder is opgezet en ondersteund wordt door een goede testsuite, zal de implementatie nooit lang overleven.


Begrijp me niet verkeerd, dit is absoluut geen excuus om niet goed naar de implementatie te kijken. Het is niet zo dat de implementatie onbelangrijk is - maar het is wel zo dat tests en ontwerp belangrijker zijn. Het gros van de tijd die je aan een code review besteedt zou dan ook daar naartoe moeten gaan. 


## Van buiten naar binnen


Ik noem deze manier van code beoordeelen *Test-Driven Code Reviews*.


Dat is een vreselijke naam, natuurlijk, die vooral bedoeld is om op de goede naam van [Test-Driven Development](/tags/test-driven-development/) (TDD) mee te liften, dat geef ik eerlijk toe. Een belangrijk verschil is bijvoorbeeld dat je bij TDD afwisselend met de tests en de implementatie bezighoudt. Bij TDCR bekijk je eerst de tests, en pas later de implementatie. Je werkt van buiten naar binnen toe, als het ware.


Waarom dan toch die naam? 


Tests zijn - zowel voor ontwikkelaars als voor code reviewers - vaak een ondergeschoven kindje. En dat is zonde. Want heldere, goed leesbare tests zijn van onschatbare waarde bij het diagnosticeren van bugs. Hoe eenvoudiger de tests te begrijpen zijn, hoe makkelijker het is om de de oorzaak van een probleem te achterhalen. Complexe, moeilijk leesbare tests signaleren daarentegen hooguit dát er iets mis is met de code (of erger: met de test zelf!), en laten het aan de ontwikkelaar om erachter te komen wát er aan scheelt.


Goede tests (met de nadruk op "goede"!) zijn belangrijker dan veel ontwikkelaars zullen erkennen. Buiten het feit dat ze je als reviewer op weg helpen om het PR in kwestie te begrijpen, verdienen ze extra aandacht om de kwaliteit van de codebase als geheel op peil te houden. 


Ze verdienen een bijzondere plek in het proces van code reviewen. Ze verdienen het om als eerst tegen het licht te worden gehouden.


[^1]: Een uitzondering op deze regel zijn zuivere refactor-PR's, oftewel: PR's waarin er geen nieuwe functionaliteit wordt toegevoegd. En dan uiteraard alleen in de veronderstelling dat er al een goede testsuite voor dit stuk code bestaat!  