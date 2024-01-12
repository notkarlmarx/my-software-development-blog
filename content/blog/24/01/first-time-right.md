---
title: "First time right?"
author: "Karl van Heijster"
date: 2024-01-12T07:49:03+01:00
draft: false
comments: true
tags: ["agile ontwikkeling", "leren", "software ontwikkelaar (rol)", "tester (rol)", "verantwoordelijkheid"]
summary: "Na afloop van mijn praatje kreeg ik de vraag of ik geloof in het idee van *first time right*. Mijn antwoord was: \"Ik geloof niet dat er zoiets bestaat als *first time right*. Maar ik geloof wel in *first time een stuk beter dan we het nu doen*.\" Tijd om dat antwoord verder uit te werken, was er op dat moment niet. Maar de vraag bleef wel in mijn achterhoofd spoken. Is het mogelijk om een systeem in één keer goed te bouwen?"
---

Op het Najaarsevenement van [TestNet](https://www.testnet.org/) betoogde ik dat [testers een belangrijke rol hebben te spelen in het reviewen van code](/talks/waarom-testers-code-moeten-reviewen/ "'Waarom testers code moeten reviewen'"). Hun rol zou zich niet moeten beperken tot het controleren van het werk van de ontwikkelaars. Testers moeten niet in actie komen *nadat* de code is geschreven. Die manier van werken is [een erfenis van waterval](/blog/23/11/erfenissen-van-waterval/ "'Erfenissen van waterval'"), en (daarom) vreselijk inefficiënt bovendien.


In plaats daarvan zouden testers zich hard moeten maken voor het verhogen van het testbewustzijn bij hun teamgenoten. Wanneer ontwikkelaars tests als *first class citizens* van hun codebase gaan zien, dan is er geen aparte testfase achteraf meer nodig. De tester hoeft niet meer handmatig na te gaan of de ontwikkelaar zijn werk heeft gedaan. Hij kan dat van de code af lezen: de [tests documenteren het gedrag van het systeem](/blog/22/09/tests-als-documentatie/ "'Tests als documentatie'") (zie ook [deze blog](/blog/22/12/tests-zijn-specs/ "'Tests zijn specs'")).


## Verantwoordelijkheid


Hoe krijgen testers dat voor elkaar? [Ze zouden zich op kunnen werpen als code reviewer.](/blog/23/07/de-tester-als-code-reviewer/ "'De tester als code reviewer'") Of, beter nog: ze zouden kunnen [*pair programmen*](/tags/pair-programming/ "Blogs met de tag 'pair programming'") met de ontwikkelaars. Ze zouden de ontwikkelaars zo de zegeningen van [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) kunnen laten ervaren. En wanneer het team eenmaal doordrongen is van de meerwaarde van continue verificatie, zouden ze -- voordat er nog maar één regel code is geschreven! -- met een ontwikkelaar om tafel kunnen gaan zitten om te bespreken hoe deze zijn eigen werk het best kan testen.


Het is, als je het mij vraagt, niet de verantwoordelijkheid van de tester om te controleren of het systeem correct is geïmplementeerd. Dat is de verantwoordelijkheid van het hele team, het is de gedeelde verantwoordelijkheid van ontwikkelaar én tester (en businessanalist, UX-designer etc.). Alleen door met het hele team die verantwoordelijkheid te delen, kunnen we ervoor zorgen dat het juiste gebouwd wordt.


## Geloof ik in *first time right*?


Na afloop van mijn praatje kreeg ik de vraag of ik geloof in het idee van *first time right*. Mijn antwoord was: "Ik geloof niet dat er zoiets bestaat als *first time right*. Maar ik geloof wel in *first time een stuk beter dan we het nu doen*."


Tijd om dat antwoord verder uit te werken, was er op dat moment niet. Maar de vraag bleef wel in mijn achterhoofd spoken. Is het mogelijk om een systeem in één keer goed te bouwen? 


## Vermijdbare fouten


Het antwoord dat ik die avond gaf, bestond uit twee onderdelen. Laat ik met het tweede deel beginnen. We kunnen een systeem een stuk beter bouwen dan we nu doen. Dat betekent: op dit moment introduceren we fouten in het systeem die we eenvoudig kunnen vermijden. 


Veel van die fouten ontstaan door een gebrek aan communicatie. De ontwikkelaar heeft een bepaald idee van hoe het systeem moet functioneren, en dat idee wordt gereflecteerd in zijn implementatie. Een tester heeft ook een idee -- maar niet noodzakelijkerwijs hetzelfde idee! -- en dat idee wordt gereflecteerd in de tests die deze schrijft. De discrepantie tussen deze ideeën komt pas naar voren aan het eind van de ontwikkelcyclus: nadat de code op de testomgeving is uitgerold, en nadat de achteraf geschreven tests zijn gefaald.


Dit soort fouten kunnen worden voorkomen door beter samen te werken. Dat is precies waarom ik voorstel dat ontwikkelaars en testers samen optrekken. En het is waarom ik voorstel dat elke codewijziging gepaard moet gaan met bijbehorende geautomatiseerde tests. Tests maken aannames over de bedoelde werking van het systeem expliciet. Elke test is een gelegenheid om je af te vragen: is dit inderdaad wat ik wil dat het systeem doet? 


Dat is wat ik bedoel als ik zeg: *first time een stuk beter dan we het nu doen*.


## Mogelijkheid


Waarom geloof ik "slechts" in *first time beter*, en niet in *first time right*? Dat heeft wat te maken met de aard van ons werk als softwareontwikkelaar.


*First time right* impliceert de *mogelijkheid* van iets in één keer goed op kunnen leveren. En dat is alleen mogelijk -- op een duurzame, herhaalbare manier --, als we op voorhand de specificaties van een systeem helemaal goed kunnen krijgen. Alleen als je precies weet wat de gebruiker van een systeem verwacht, kun je het in één keer goed bouwen. Maar omdat te kunnen weten, moet ook de gebruiker precies weten wat 'ie van een systeem verwacht -- en dat blijkt in de praktijk... laten we zeggen: uitdagend.


Het is niet voor niets zo dat [Agile](/tags/agile-ontwikkeling/ "Blogs met de tag 'agile ontwikkeling'") methodologieën een [iteratieve](/tags/iteratieve-ontwikkeling/ "Blogs met de tag 'iteratieve ontwikkeling'") manier van softwareontwikkeling voorstellen. Het is onmogelijk om een volmaakt idee van een gewenste functionaliteit te formuleren vóórdat je die functionaliteit in de praktijk hebt gebruikt. En het is verdomd moeilijk om er een aardig idee van te formuleren.


Dit is geen gebrek van ons als softwareontwikkelaars. Het is niet zo, dat als we maar beter ons best hadden gedaan, we de eigenlijke wens boven water hadden kunnen krijgen. Alleen door een gebruiker bepaalde functionaliteit voor te schotelen en te zien hoe deze daarop reageert, komen we erachter wat diegene *echt* wilde hebben -- en niet slechts wat deze *dacht* te willen hebben.[^1]


## Ontdekken


Anders gezegd: ons werk is niet te bouwen wat er gevraagd wordt. Ons werk is ontdekken wat er gevraagd wordt -- en onze pogingen daar achter te komen naar die wens om te vormen.


Softwareontwikkeling lijkt minder op het bouwen van een huis en meer op iets als het schrijven van een tekst. Immers, schrijven is niets anders dan een probleem oplossen op papier.[^2] 


En een tekst schrijf je ook niet in één keer. Een tekst schrijf en herschrijf je, soms meerdere keren. (Of, wat ook mogelijk is: je verfijnt je begrip in een nieuwe blog!) Dat is hoe je erachter komt wat het probleem überhaupt is. -- En dat is al moeilijk genoeg, laat staan dat je eerste versie al de juiste oplossing bevat! 


[^1]: Nota bene: dit is geen excuus om niet je best te doen op voorhand een zo goed mogelijk idee van die wens op tafel te krijgen.

[^2]: Ik dank de formulering aan Pam Hurley, die dit zeer terechte punt maakte in [deze aflevering](https://open.spotify.com/episode/4wmFMbVumZa1LyDnr2a7Y0?si=44ee634f68ce43c6 "'Better Technical Writing for Everyone with Pam Hurley, PhD'") van [*Hanselminutes with Scott Hanselman*](https://open.spotify.com/show/4SrTUZr1s5C4SJmUxDIUDc?si=be6a588f9c4c4eae).
