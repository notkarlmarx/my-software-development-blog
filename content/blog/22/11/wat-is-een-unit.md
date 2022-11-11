---
title: "Wat is een unit?"
author: "Karl van Heijster"
date: 2022-11-11T08:16:07+01:00
draft: false
comments: true
tags: ["mocks", "testen", "teststrategie", "unit tests"]
summary: "Een tijd geleden presenteerde ik enkele ideeën over testen aan mijn collega's. Toen ik aankwam bij het gedeelte waarin ik stelde je het best via de voordeur kunt testen, stelde een collega apodictisch: \"Een unittest test een openbare method op een class. Elke afhankelijkheid op die class moet je mocken.\" Dat is een manier om er naar te kijken, zeker. Het is de zogenaamde *mockist* strategie, ook wel bekend als de Londense school van unittesten. De vraag waar ik me op wil richten is: waar komt de aantrekkingskracht van deze strategie dan vandaan? Ik geloof dat deze voortkomt een bepaalde interpretatie van wat een unittest is of moet zijn. Meer specifiek: wat de *unit* in unittest is of moet zijn."
---

Een tijd geleden presenteerde ik enkele ideeën over testen aan mijn collega's. Toen ik aankwam bij het gedeelte waarin ik stelde je het best [via de voordeur](/blog/22/06/testen-via-de-voordeur/) kunt testen (zie ook [deze blog](/blog/22/09/tests-als-vangnet/)), stelde een collega apodictisch: "Een unittest test een openbare method op een class. Elke afhankelijkheid op die class moet je mocken."


Dat is een manier om er naar te kijken, zeker. Het is de zogenaamde *mockist* strategie, ook wel bekend als de [Londense school van unittesten](https://medium.com/@adrianbooth/test-driven-development-wars-detroit-vs-london-classicist-vs-mockist-9956c78ae95f). 


## Snel problemen vinden


Het voordeel van die strategie is dat het gedrag tot in extreme mate isoleert. Als een bepaalde functionaliteit omvalt, dan kun je er zeker van zijn dat er maar één test faalt. De rest van de tests is immers via de mocks afgeschermd van eventuele fouten in andere classes. Het idee daar achter is dat je op die manier eenvoudig kunt pinpointen waar het probleem zich bevindt. En dat versnelt je ontwikkelsnelheid - zo is de theorie.


De praktijk is geloof ik weerbarstiger. Het schrijven van mocks is een extreem arbeidsintensieve bezigheid - niet alleen omdat mocks schrijven tijd kost, maar ook omdat ze aangepast moeten worden als het gedrag wijzigt van de classes die ze vertegenwoordigen. Het is bovendien foutgevoelig, want de schrijver van de mock zou immers zomaar het verkeerde gedrag kunnen implementeren. (Zie ook [deze blog](/blog/22/02/de-leercurve-van-angulartests-beklimmen-deel-3/).)


Het is ten zeerste de vraag of de extra tijd die je als ontwikkelaar moet steken in het schrijven en onderhouden van mocks, opweegt tegen de snelheid waarmee je de oorzaak van bugs kunt vinden. Ik ben niet van die redenering overtuigd, in elk geval.


Bovendien valt dit probleem op een andere manier af te vangen. Een goede suite aan unittests is razendsnel. In het ideale geval trap je constant je tests af tijdens het programmeren. Bij [Test-Driven Development](/tags/test-driven-development/) is dit zelfs in het proces ingebouwd. En *tools* als [NCrunch](https://www.ncrunch.net/) nemen deze handeling zelfs voor je over. Het pinpointen van de fout wordt zo triviaal: de fout zit 'm altijd in je laatste wijziging.


## Aantrekkingskracht


Lang verhaal kort: ik ben er geen fan van, van de Londense school. - Maar het staat mijn collega natuurlijk vrij van mening te verschillen. De vraag waar ik me op wil richten is: waar komt de aantrekkingskracht van deze strategie dan vandaan?


Ik geloof dat deze voortkomt een bepaalde interpretatie van wat een unittest is of moet zijn. Meer specifiek: wat de *unit* in unittest is of moet zijn.


Een unittest is een test die één eenheid test. Mijn vermoeden[^1] is dat de Londense school in het algemeen, en mijn collega in het bijzonder, die eenheid opvatten als een eenheid code. Concreet: een publieke method op een class (en eventueel de daarbij geassocieerde private methods).


Als je een eenheid zó opvat, dan is het logisch dat je dat stuk code probeert te isoleren met mocks. Je wil immers alléén die regels code testen - en niet meer. Vanuit dit perspectief bezien, is elke unittest die niet volgens de Londense school is opgezet eigenlijk een integratietest. Een test die méér dan alleen dat ene stukje code aanroept, test immers meer dan alleen die eenheid.


## Eenheid van gedrag


Maar het is geen vanzelfsprekendheid dat de *unit* in een unittest naar een eenheid code verwijst. Je zou een *unit* ook op kunnen vatten als een eenheid van *gedrag*.


Een voorbeeld kan dat hopelijk verhelderen. (Zie ook [deze blog](/blog/22/09/tests-als-vangnet/).) Mijn team ontwikkelt een applicatie die onder andere als functionaliteit heeft om een toetsvraag, zoals gedefinieerd in ons model, om te zetten naar de [QTI-standaard](http://www.imsproject.org/spec/qti/v3p0/impl#introduction), een uitwisselingsstandaard voor toetsen en toetsvragen. Een toetsvraag bestaat uit meerdere onderdelen - een inleidende tekst, een afbeelding, de vraag, de antwoordmogelijkheden etc. -, en deze moeten allemaal individueel worden omgezet naar hun QTI-representatie. 


Als we deze functionaliteit testen, dan testen we de code die de inleidende tekst (of de afbeelding of de vraag of de antwoordmogelijkheden) naar QTI omzet niet in isolatie. Merk op dat ik hier spreek van "de code" - dat is het relevante deel!


## Eenheid en veelheid


We testen die deelfunctionaliteiten altijd als onderdeel van een volledige toetsvraag. Dat wil zeggen: we nemen een toetsvraag met een inleiding, zetten die om naar QTI, en controleren daarna of de inleiding correct is omgezet. Hetzelfde doen we voor de afbeelding, de vraag, de antwoordmogelijkheden etc..


Deze tests roepen voor een groot deel dezelfde code aan. Alle code die verantwoordelijk is voor de toetsvraag in het geheel is immers hetzelfde. 


Maar code aanroepen is niet hetzelfde als code *testen*. Welke code we testen, blijkt uit de inputs en de outputs. De input van de test is een toetsvraag met inleiding (of afbeelding etc.); alle ceremonie daaromheen is voor de test irrelevant. De output van de test is een stukje QTI waarin we die inleiding (of afbeelding etc.) terug zien komen; alle eveneens gegenereerde QTI laten we voor de test buiten beschouwing. 


Zo kunnen we toch één eenheid testen - een eenheid van gedrag -, terwijl we een veelheid aan classes aanroepen om dat gedrag te bewerkstelligen. 


## Wat is een unit?


De *unit* in unittest verwijst naar het enkele stukje gedrag dat je test, eh, test. De *unit* is een logische deelfunctionaliteit waar je test zich op focust. Het verwijst *niet* naar het enkele stukje code dat je test. 


Het is geen probleem om een heleboel regels code aan te roepen om één stukje gedrag te testen. Integendeel, dit geeft je juist zekerheid dat het systeem als geheel werkt zoals bedoeld.


Dat gezegd hebbend, natuurlijk staat het iedereen vrij om zoveel mocks te schrijven als diegene wil. Maar mijn advies zou zijn om ze te bewaren voor functionaliteit die om de een of andere reden niet rechtstreeks getest *kan* worden - en voor de rest van je tests *the real deal* te gebruiken. 


[^1] En ik spreek van een vermoeden, omdat ik ruiterlijk toe durf te geven dat ik in het vervolg van dit verhaal vanuit mijn onderbuik ga spreken.
