---
title: "Evolutionaire datamigratie met FluentMigrator"
author: "Karl van Heijster"
date: 2021-10-22T08:15:24+02:00
draft: false
comments: true
tags: ["databases", "datamigratie", "open source", "procesverbetering", "refactoren", "SQL"]
summary: "In het kort komt evolutionair databasedesign hier op neer. Stel, een ontwikkelaar maakt een wijziging in de code die een databasewijziging impliceert. In dat geval is het aan dezelfde ontwikkelaar om een migratiescript te schrijven die de codewijziging mogelijk maakt, en deze bij de codewijziging in te checken. De databasewijziging is onderdeel van de codewijziging, als het ware. En terecht, want zonder de databasewijziging is het niet mogelijk om de gewijzigde code te runnen."
---

Een tijd geleden schreef ik hoe mijn team met [Migrations.Json.Net](https://github.com/Weingartner/Migrations.Json.Net) de ongestructureerde data in onze [NoSQL-database](https://nl.wikipedia.org/wiki/NoSQL) [stapje voor stapje migreert](/blog/21/09/stapje-voor-stapje-data-migreren/), elke keer wanneer een object opgehaald wordt. Maar dat is nog niet het einde van het verhaal. Omdat we softwareontwikkelaars zijn en ons leven dus graag zo moeilijk mogelijk maken, hebben we niet alleen een NoSQL-, maar ook een [SQL-database](https://nl.wikipedia.org/wiki/SQL). Waarom? Voor onze gestructureerde data, natuurlijk!


## Strategie


Voor deze soort data is het ons helaas niet gegund om dezelfde tooling te gebruiken. Erg verwonderlijk is dat natuurlijk niet, SQL is immers geen [JSON](https://nl.wikipedia.org/wiki/JSON). Maar de verschillen gaan dieper dan de tooling alleen. Het is ons zelfs niet gegund om dezelfde *strategie* te gebruiken als voor onze ongestructureerde data. Omdat de data in een SQL database volgens een bepaald [schema](https://nl.wikipedia.org/wiki/Databaseschema) moet zijn opgeslagen, kunnen we de data per definitie niet inconsistent opslaan.


(Helemáál waar is dat overigens niet. Voor een subset van databasewijzigingen zouden we met deze strategie weg kunnen komen. Elke keer als er sprake is van toegevoegde properties op een object, zouden we een *nullable* kolom toe kunnen voegen, die gevuld wordt zodra een object wordt opgehaald. Hiermee is echter het gros van de wijzigingen niet afgevangen. Bovendien zouden we in zulke gevallen vaak uit de voeten kunnen met *default* waarden, waarmee inconsistente opslag voorkomen wordt.)


## FluentMigrator (1)


Het team heeft naar verschillende alternatieven gekeken om met deze situatie om te gaan. De keuze is uiteindelijk gevallen op [FluentMigrator](https://nl.wikipedia.org/wiki/Databaseschema), een *open source* project dat databasemigraties faciliteert.


Ik zal niet schrijven over dat wat een ontwikkelaar moet doen om een migratie voor elkaar te krijgen, dat staat uitstekend beschreven in FluentMigrators [documentatie](https://fluentmigrator.github.io/).



## Codewijzigingen


Waar ik het over wil hebben, is het idee dat achter deze tooling schuilgaat. Dit idee ben ik namelijk jaren geleden al eens tegengekomen, toen ik een onderzoekje deed naar de mogelijkheid van databasemigraties in onze *legacy*-applicatie. Ik stuitte toen op [deze blog](https://martinfowler.com/articles/evodb.html) van [Pramod Sadalage](http://www.sadalage.com/) en [Martin Fowler](https://martinfowler.com/).


In het kort komt de migratiestrategie hier op neer. Stel, een ontwikkelaar maakt een wijziging in de code die een databasewijziging impliceert. In dat geval is het aan dezelfde ontwikkelaar om een migratiescript te schrijven die de codewijziging mogelijk maakt, en deze bij de codewijziging in te checken. De databasewijziging is onderdeel van de codewijziging, als het ware. En terecht, want zonder de databasewijziging is het niet mogelijk om de gewijzigde code te runnen.


## Volgorde


Het ding met databasewijzigingen is dat ze in een bepaalde volgorde plaats moeten vinden. Om het overzicht te kunnen bewaren in de veelheid aan migratiescripts die in de loop van de tijd zullen ontstaan, zullen deze van een nummer voorzien moeten worden. Dat kan een oplopend nummer zijn of een datum. Door de scripts in de juiste volgorde uit te voeren, verandert de database stap voor stap richting haar uiteindelijke vorm.


Niet voor niets noemden Sadalage en Fowler dit *evolutionary database design*. Met migratiescripts wordt het mogelijk om databases in kleine stapjes aan een nieuwe context aan te passen.


## FluentMigrator (2)


Bijhouden welke migratiescripts al zijn uitgevoerd, en deze handmatig uitvoeren, is arbeidsintensief en foutgevoelig. (En dat was een tijd lang onze werkwijze, dus ik kan het weten!) 


Dit is waar FluentMigrator om de hoek komt kijken. Deze tooling stelt de ontwikkelaar in staat om in een [*fluent interface*](https://en.wikipedia.org/wiki/Fluent_interface) migratiescripts in C# te schrijven en deze, wanneer nodig, automatisch uit te laten voeren wanneer de applicatie opgestart wordt.


## Databases refactoren


In de eerste edtie van [*Refactoring*](https://refactoring.com/) noemde Fowler databasewijzigingen nog een pijnpunt in de praktijk van het omwerken van code. Dankzij ideeën als evolutionair databasedesign en tooling als FluentMigrator is dat pijnpunt inmiddels weggemasseerd. 


Dit is één van de leukste dingen aan softwareontwikkeling: je kunt er vanuit gaan dat een goed idee op een gegeven moment altijd wel door iemand geautomatiseerd zal worden. En dat bespaart je als ontwikkelaar tijd en energie, die je vervolgens kan steken in het automatiseren van hopelijk even goede ideeën. 
