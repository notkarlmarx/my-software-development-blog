---
title: "Het probleem met cookbooks"
author: "Karl van Heijster"
date: 2022-02-21T07:29:57+01:00
draft: false
comments: true
tags: ["boeken", "leren", "SQL"]
summary: "Ik zeg het maar eerlijk, ik lees niet graag *cookbooks*. Dat ligt voor een deel aan mij, natuurlijk. Ik lees boeken namelijk het liefst van kaft tot kaft. En daar zijn cookbooks simpelweg niet voor bedoeld. Ze fungeren eerder als referentiemateriaal. Je hoort ze uit de kast te trekken wanneer je tegen een bepaald probleem aanloopt. Het probleem is: je hebt pas een goed idee wat erin staat als je het boek gelezen hebt. Hoe weet je anders waar je moet kijken?"
---

Ik ben een [degelijke afwasser](/blog/21/11/schorseneren-en-software-architectuur/), maar bepaald geen goede kok. Maar met een goed geschreven recept kan zelfs ik iets aardigs in elkaar flansen. - En dat is waarom er kookboeken bestaan.


Ook in de literatuur over softwareontwikkeling bestaat er zoiets als een kookboek. Onlangs las ik het [*C# Cookbook*](https://www.oreilly.com/library/view/c-cookbook/9781492093688/) van [Joe Mayo](https://github.com/JoeMayo) uit. En in de boekenkast heb ik ook een [*SQL Cookbook*](https://www.oreilly.com/library/view/sql-cookbook-2nd/9781492077435/) staan. Andere bekende voorbeelden in het genre zijn [*Patterns of Enterprise Application Software*](https://martinfowler.com/books/eaa.html) en [*Refactoring*](https://martinfowler.com/books/refactoring.html), beide van Martin Fowler. (De laatste scoorde een eervolle vermelding in [de beste boeken die ik vorig jaar las](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/).)


Ik zal zulke vakliteratuur in het vervolg met "*cookbooks*" aanduiden om ze te onderscheiden van hun culinaire tegenhanger.


## Problemen


Cookbooks en kookboeken hebben dezelfde functie. Ze bieden handvaten om problemen op te lossen.


In het geval van een kookboek is dat: je honger stillen. De variatie in recepten accommodeert de parameters waarbinnen dit dient te gebeuren. Denk aan het soort ingrediënten dat je tot je beschikking hebt, of de tijd die je hebt om te koken - of, natuurlijk, de smaak die je wil bewerkstelligen. 


Het overkoepelende probleem in het geval van een cookbook is, zou je kunnen stellen, je code op een duurzame manier in een werkende staat krijgen. De variatie in recepten komt voort uit de verschillende soorten problemen die je als ontwikkelaar tegen kan komen op weg naar dat doel. 


Ook de manier waarop kook- en cookbooks hun lezers in staat stellen problemen op te lossen, lijkt op elkaar. De boeken bieden recepten waarin stapsgewijs wordt beschreven wat je moet doen om het probleem tot een goed eind te brengen. Kookboeken mogen wat spaarzamer zijn in hun begeleidende tekst, maar cookbooks lichten daarnaast meestal toe waarom het recept in kwestie het probleem goed oplost.


Kookboeken stellen koks als ik in staat een alleraardigst gerecht te bereiden. En met hulp van een cookbook kan zelfs de klungeligste programmeur alleraardigste code schrijven.


## Leesplezier


Maar, ik zeg het maar eerlijk, graag lees ik zulke boeken niet. 


Dat ligt voor een deel aan mij, natuurlijk. Ik lees boeken namelijk het liefst van kaft tot kaft. En daar zijn cookbooks, net als kookboeken, simpelweg niet voor bedoeld. 


Ze fungeren eerder als referentiemateriaal. Je hoort ze uit de kast te trekken wanneer je tegen een bepaald probleem aanloopt. Je kijkt of jouw probleem erin staat, en zo ja, dan volg je het recept.


Het probleem is: je hebt pas een goed idee wat erin staat als je het boek gelezen hebt. Hoe weet je anders waar je moet kijken?


## Als..., dan...


Ik liep hier bijvoorbeeld tegenaan toen ik een als-dan-constructie in SQL wilde programmeren. De *use case* was behoorijk eenvoudig: als er al een rij met een bepaald ID in de database aanwezig was, update die rij dan. Zo niet, voeg een nieuwe rij toe.


Als een brave programmeur-kok haalde ik mijn *SQL Cookbook* uit de kast en begon met bladeren. Maar ik vond geen `IF` of `ELSE` - althans, niet in de context van mijn toch redelijk prozaïsche *use case*. Teleurgesteld legde ik het boek terug. 


Dus ik deed wat elke eenentwintigste-eeuwer in eerste instantie al gedaan zou hebben, en wendde me tot het internet. (Ik dichtte niet voor niets: ["Mijn beste vriend is / Google"](/blog/21/09/vijf-plus-een-haikus-over-software-ontwikkeling/)!) Binnen een minuut of twee was ik erachter dat wat ik zocht een [`MERGE`](https://www.sqlshack.com/understanding-the-sql-merge-statement/) heet. Ik pakte mijn cookbook er opnieuw bij - en ja hoor, daar stond 'ie: de oplossing voor mijn probleem. 


Maar het (luxe)probleem was dat ik al een oplossing had, namelijk de oplossing die ik zojuist van het internet had geplukt. En dat is dus exemplarisch voor mijn probleem met cookbooks. 


Vergeleken met het internet, is het doorzoeken van een cookbook een vervelende en vermoeiende klus. Eigenlijk zijn die boeken in twee gevallen pas goed te doorzoeken: (1) je weet de oplossing van het probleem al, maar dan biedt het boek maar weinig meerwaarde, of (2) je hebt ze al van kaft tot kaft gelezen, maar dat is nu precies waar ze niet voor gemaakt zijn!


## Voordelen


Betekent dat dat cookbooks overbodig zijn? Nee, zo ver wil ik nu ook weer niet gaan. 


Het voordeel van een cookbook is dat je redelijkerwijs kan aannemen de oplossing een goede is. Een hoofdstuk in een cookbook heeft immers een heel redactieproces doorgemaakt. Daarin onderscheidt het cookbook zich van de oplossing op het internet. Deze is misschien wel een stuk makkelijker te vinden, maar je hebt geen garantie dat de oplossing de beste is. 


(Aangenomen dat het cookbook niet verouderd is, natuurlijk. Dat is nog een probleem met cookbooks: in tegenstelling tot het internet zijn ze alleen te updaten door een nieuwe versie te kopen.)


Bovendien staat bij elk recept een motivatie geschreven. De antwoorden op [Stack Overflow](https://stackoverflow.com/), daarentegen, lossen je problemen misschien wel op, ze dragen niet altijd bij aan het begrip waarom dat het geval is.  


En een ontwikkelaar die begrijpt *waarom* een stuk code een probleem oplost, is een stuk waardevoller dan een ontwikkelaar die zijn applicatie in werkende staat heeft weten te rommelen. En als 'ie nou ook nog eens goed kan koken...
