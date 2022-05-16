---
title: "Testen via de voordeur"
author: "Karl van Heijster"
date: 2022-05-13T13:27:35+02:00
draft: true
comments: true
tags: ["integratietests", "refactoren", "test-driven development", "testen", "unit tests"]
summary: "Het ideaal van Test-Driven Development is dit: al coderend breid je je testsuite uit, zonder ooit één test te hoeven herschrijven. Het toevoegen van nieuwe functionaliteit gebeurt op zijn best binnen de kaders van een bestaande API. Op zijn slechtst leidt het tot uitbreidingen daarvan - meer niet. Er is, denk ik, een manier om dichter bij dat ideaal te komen. Dat ideaal bereik je door te testen via de voordeur. Dat houdt kort gezegd in dat je je logica idealiter test via dezelfde route als een gebruiker van je code. "
---

Onlangs had ik na een [Developer Meet-up](/blog/21/10/waarom-we-developer-meet-ups-organiseren/) een leuk gesprek over software testen. Althans, het was een leuk gesprek tot ik mijn collega vroeg naar zijn mening over [Test-Driven Development](/tags/test-driven-development/) (TDD). Zijn tot dan toe enthousiaste gezicht betrok onmiddellijk. "Nee," mopperde hij, "daar heb ik een bloedhekel aan. Ik denk terwijl ik codeer, ik kan niet van tevoren zo'n test schrijven, dan weet ik nog helemaal niet wat het moet zijn."


## Verandering


Ik begrijp waar die onvrede vandaan komt. Om testgedreven te ontwikkelen moet je op een andere manier leren nadenken over je code. TDD dwingt je om [eerst na te denken over de API van je code](/blog/22/05/nog-een-reden-om-testgedreven-te-ontwikkelen/), voordat je aan de implementatie begint. Voor veel ontwikkelaars werkt het echter andersom: ze laten de implementatie de API van hun classes vormen (of misschien wel: dicteren). 


Wie coderend nadenkt over de vorm van zijn code, kan onmogelijk die code [tegelijkertijd](/blog/22/03/agile-en-test-driven-development/) met de tests ontwikkelen. Want de code verandert nog continu - en de tests dus ook. En waarom zou je in hemelsnaam een reeks tests schrijven waarvan je nu al weet dat je ze straks toch weer moet refactoren om tegemoet te komen aan de nieuwe vorm van je code?


Dat is een bekend argument. Mijn leidinggevende gooit het ook elke keer in de strijd als ik me hardop afvraag waarom het zo moeilijk is voor ontwikkelaars om TDD te omarmen. Maar het argument veronderstelt dat je op voorhand niet kan weten wat de API van je te testen class gaat zijn - en daar ben ik niet van overtuigd.


## Ideaal


Het ideaal is dit: al coderend breid je je testsuite uit, zonder ooit één test te hoeven herschrijven. Het toevoegen van nieuwe functionaliteit gebeurt op zijn best binnen de kaders van een bestaande API. Op zijn slechtst leidt het tot uitbreidingen daarvan - meer niet. 


Er is, denk ik, een manier om dichter bij dat ideaal te komen. Dat ideaal bereik je door te testen via de voordeur.[^1] Dat houdt kort gezegd in dat je je logica idealiter test via dezelfde route als een gebruiker van je code. 


## Gebruiker


De vraag werpt zich dan op: wat een gebruiker van je code? Vaak ben je dat zelf, bijvoorbeeld als je een helper class schrijft die je in de rest van je applicatie gebruikt. Maar dat kan het juiste antwoord niet zijn, want mijn mopperende collega is ook een gebruiker van zijn eigen code en hij is mijlenver verwijderd van het ideaal.


Dit zou een antwoord kunnen zijn: iemand buiten het team. Als je een enterprise applicatie ontwikkelt, dan is dat iemand van de business, en als je een [NuGet](https://www.nuget.org/) package ontwikkelt, dan is dat een andere ontwikkelaar die je code gebruikt.


## Haalbaar


Maar de lat die je met dat antwoord legt, is wel erg hoog. Is testen via de voordeur altijd haalbaar? Het idee lijkt bijvoorbeeld te impliceren dat ik de back-end zou moeten testen door via de front-end op een knop te klikken. - En dan hebben we het rijk van de unittest toch ruimschoots verlaten! 


Volgens mij kun je hier best pragmatisch in zijn. Als we uitgaan van een systeem met een front- en een back-end (of is het: twee systemen, een front- en een back-end?), dan kunnen we het punt waarop de eerste met de laatste communiceert redelijkerwijs als voordeur beschouwen. Testen via de voordeur betekent in dat geval veelal: testen via de Web API.[^2]


## Afstand


Door op deze manier te testen, geef je jezelf als ontwikkelaar een ruime afstand van de implementatiedetails van je code. Je definieert een input en een output - maar hoe de code dat onder water afhandelt, is voor jou om het even. Of elk request nu in één lange method wordt verwerkt, of dat je gebruik van een rijk [domeinmodel](https://en.wikipedia.org/wiki/Domain_model) dat diverse verantwoordelijkheden delegeert, is voor een eindgebruiker van je code om het even. Het enige waar die wat om geeft, is dat een bepaald request gepaard gaat met een bepaalde response.


En het voordeel is dat je via de voordeur zeker weet dat de uitkomsten van je test reflectief zijn voor de ervaringen van een gebruiker van je code. Ga je dichter op het metaal zitten met je tests - en schrijf je unittests op basis van een specifieke implementatie -, dan loop je het risico scenario's te testen die in de praktijk nooit voor kunnen komen. Dat is zonde - al helemaal als je op basis daarvan onterecht meent te mogen concluderen dat de eindgebruiker van bugs vrijgewaard zal blijven!


## Integratietests


Een vraag werpt zich op: ben je hier niet eigenlijk integratietests aan het schrijven, en geen unittests? Het antwoord is: misschien wel, inderdaad. 


De vraag is hoe erg dat is. Ook op het vlak van TDD hoef je niet dogmatisch te zijn. Als het logisch is om een deel van je applicatie middels unittests te ontwikkelen - een stuk logica in de kern van je domeinmodel, bijvoorbeeld -, doe het dan alsjeblieft via unittests. Maar als het om relatief eenvoudige CRUD-operaties gaat, is het dan per se nodig om elke laag in isolatie testgedreven te ontwikkelen, of kun je het met integratietests af?


Hoewel ik testen via de voordeur niet expliciet in ons gesprek noemde, zal mijn collega me dit punt denk ik wel gunnen. Hij vertelde enthousiast over een stuk code dat hij gerefactord had, waarbij de bestaande unittests vrijwel onmiddellijk sneuvelden, maar de integratietests glansrijk overeind bleven staan. De unittests testten de implementatie, de integratietests de API.


## Resistent


Natuurlijk wil ik daar niet mee zeggen dat unittests geen waarde hebben - integendeel, ik ben wel [de laatste die dat zou willen beweren](/blog/21/04/zeg-het-met-een-vraag/)! 


Maar het is goed om je je te beseffen dat unittests vaak implementatiedetails testen. Ze testen via de achterdeur, ze zitten dicht op het metaal. Daardoor blijken ze broos bij refactorslagen. Dat is wat een oké test van een goede test onderscheidt: de mate waarin ze resistent blijken bij refactoring.


De les is daarom: schrijf de soort tests die het mogelijk maken om een publieke[^3] interface te definiëren. De concrete implementatie van die interface zou voor je tests om het even moeten zijn. Daardoor heb je als ontwikkelaar maximale ruimte om te refactoren in een poging aan de eisen van de interface tegemoet te komen. 


Je test legt vast wat die eisen zijn - de in- en output: de voordeur -, niet hoe je eraan voldoet - de achterdeur.


[^1]: Ik meen de term te hebben ontleend uit één van de hoofdstukken over testen uit [*Software Engineering at Google*](https://www.oreilly.com/library/view/software-engineering-at/9781492082781/). Maar ik kan de referentie niet vinden, dus het zou goed kunnen dat mijn geheugen me bedriegt. Het zou ook goed kunnen dat ik de term van [Dennis Doomen](https://www.continuousimprover.com/) heb, die jaren geleden een soortgelijk idee uiteenzette tijdens een sessie op [dotNed Saturday](https://dotnedsaturday.nl/).


[^2]: Nota bene, dit is precies wat ik deed gedurende [mijn eerste testgedreven stapjes] (LINK)!


[^3]: Merk op dat ik hier haast ongemerkt opnieuw een taal hanteer die veronderstelt dat er een gebruiker van de code is die geen weet heeft of moet willen hebben van de implementatie!
