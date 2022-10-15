---
title: "Zes dingen die ik leerde op Techorama"
author: "Karl van Heijster"
date: 2022-10-14T13:57:56+02:00
draft: true
comments: true
tags: ["communicatie", "conferenties", "domain-driven design", "legacy code", "leren", "LINQ", "open source", "software architectuur"]
summary: "Een tijd geleden bezocht ik softwareconferentie Techorama in Utrecht. Ik hoorde een boel nieuwe ideeën, werd gesterkt in enkele van mijn al bestaande overtuigingen, en uitgedaagd sommige ingesleten gewoonten te herzien. Uit mijn stapel aantekeningen destilleer ik zes inzichten die ik alleen al de eerste dag opdeed."
---

Een tijd geleden bezocht ik softwareconferentie [Techorama](https://www.techorama.nl/) in Utrecht. Ik hoorde een boel nieuwe ideeën, werd gesterkt in enkele van mijn al bestaande overtuigingen, en uitgedaagd sommige ingesleten gewoonten te herzien. Uit mijn stapel aantekeningen destilleer ik zes inzichten die ik alleen al de eerste dag opdeed.


## 1. Open source software is niet gratis 


Open source software is *niet* gratis. Of liever gezegd: open source software is gratis in dezelfde zin dat gratis puppy's gratis zijn.


Als je gebruik maakt van open source code, dan helpt je dat om snel nieuwe features te ontwikkelen. Maar wat gebeurt er als laterna blijkt dat die code niet precies een *use case* ondersteunt die je applicatie nodig heeft? Of erger nog, wat als de onderhouder van die code besluit ermee op te houden? 


In dat geval valt de verantwoordelijkheid van het onderhoud van die code op jouw schouders. Een gratis puppy kost misschien niets om aan te schaffen, maar hij is net zo duur om in leven te houden als alle andere puppy's - en hij verdient net zoveel zorg en aandacht.


Je hebt een ethische verplichting om de open source code te onderhouden die je gebruikt. Dat hoeft niet per se door code te schrijven voor het project in kwestie. Actief zijn in de gemeenschap rondom het project betekent vaak al heel veel voor de onderhouders.


*([Rockford Lothka](https://lhotka.net/) - A career with open source)*


## 2. Hoe implementeer je DDD in een *legacy* omgeving?


Het is niet aan te raden *legacy* softwaresystemen van de grond af aan opnieuw te bouwen. Natuurlijk, op deze manier ben je in één klap van je technische schuld af - maar ook van alle features die het systeem je bood. Je gooit de baby met het badwater weg. Dit is een betere oplossing: behoud het oude systeem en bouw er nieuwe systemen omheen dat langzaam maar zeker steeds meer functionaliteiten ervan overneemt. Pas Domain-Driven Design (DDD) toe voor die nieuwe systemen.


Het meervoud (system*en*) is van belang hier. *Legacy* systemen zijn vaak monolieten wier model meerdere [*bounded contexts*](https://www.martinfowler.com/bliki/BoundedContext.html) beslaat - dat is precies één van de redenen waarom ze zo ononderhoudbaar zijn geworden. Elke *bounded context* moet in zijn eigen model worden ondergebracht, en mag niet direct interacteren met de modellen uit andere *bounded contexts*.


(Nota bene, onder "systeem" versta ik: alle code die behoort tot één *bounded context*. Dat kunnen aparte services zijn - één microservice per *bounded context* (zie ook [deze blog](/blog/21/08/domain-driven-design-en-ludwig-wittgenstein/)) -, maar dat hoeft niet per se. Verschillende contexten zouden in theorie in één .NET-solution kunnen leven, als ze maar gescheiden van elkaar zijn.)


[Eric Evans](https://www.domainlanguage.com/) heeft gratis beschikbaar boekje geschreven over DDD binnen de context van [*legacy* software: *Getting started with DDD when surrounded by legacy systems*](https://www.domainlanguage.com/wp-content/uploads/2016/04/GettingStartedWithDDDWhenSurroundedByLegacySystemsV1.pdf).


*([Kenny Baas-Schwegler](https://baasie.com/) - [Domain-Driven Design heuristics for dealing with legacy software](https://speakerdeck.com/baasie/domain-driven-design-heuristics-for-dealing-with-legacy-software-at-techorama-2022))*



## 3. Er valt nog veel meer uit LINQ te halen 


[LINQ](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/) is een fantastisch middel om [declaratieve code](https://en.wikipedia.org/wiki/Declarative_programming) te schrijven - dat wisten we al. Maar de uitdrukkingsvaardigheid van LINQ reikt ook maar zo ver. Wees dus niet bang om de `Func<T, bool`-parameters om te schrijven naar functies met heldere namen.


Meer nog, wees niet bang om je eigen LINQ-operators toe te voegen als daar behoefte aan is. Maar vóórdat je dat doet, check even of een project als [MoreLINQ](https://github.com/morelinq/MoreLINQ) je niet voor is geweest.


Gebruik [LINQPad](https://www.linqpad.net/) als je wat met deze feature wil spelen - bijvoorbeeld om wat *[lunchtime](https://markheath.net/post/lunchtime-linq-challenge) [LINQ](https://markheath.net/post/lunchtime-linq-challenge-2) [challenges](https://markheath.net/post/linq-challenge-3)* op te lossen.


*([Mark Heath](https://markheath.net/) - [HyperLINQ: Take your LINQ skills to the next level](https://speakerdeck.com/markheath/hyperlinq-taking-your-linq-skills-to-the-next-level))*


## 4. Leren is ook afleren


Leren bestaat zowel uit nieuwe dingen aanleren als oude gewoonten afleren. Een beginnend programmeur schrijft eenvoudige code - toegespitst op één *use case*. Een ervaren programmeur schrijft complexe code - voorbereid om uit te breiden naar tal van verwachte *use cases*. Een expert schrijft opnieuw eenvoudige code - toegespitst op één *use case*.


Het inzicht dat daar achter ligt, is dat code niet het product is dat je als ontwikkelaar oplevert. Je levert waarde voor de business - code is slechts het middel waarmee je dat doet. De waarde ligt niet in de code, de waarde ligt in waar die code mensen toe in staat stelt.


De kosten liggen daarentegen wel bij de code. Hoe complexer de code, hoe hoger het onderhoud. Een expert is in staat de afweging te maken: weegt deze complexiteit, wegen deze kosten op tegen de waarde die ik voor de business lever? - Het antwoord is meestal: nee.


In de [objectgeoriënteerde](/tags/objectgeoriënteerd-programmeren/) wereld is een verschuiving merkbaar naar steeds [functioneler](/tags/functioneel-programmeren/) opgezette code. Die komt voort uit het verlangen (opnieuw) eenvoudige code te schrijven. [Monadisch](https://en.wikipedia.org/wiki/Monad_(functional_programming)) opgezette code is [eerlijk](/blog/22/07/wat-zijn-eerlijke-functies/) op een manier die typische objectgeoriënteerde code dat niet is. 


Ook de praktijk van [Test-Driven Development](/tags/test-driven-development/) leidt tot het schrijven van eenvoudiger code. Wie zijn [tests als ontwerpmiddel](/blog/22/09/tests-als-ontwerpmiddel/) gebruikt, vervuilt zijn code niet met lekkende abstracties. 


*([Sander Hoogendoorn](https://sanderhoogendoorn.com/) - [The zen of programming: A personal journey towards writing beautiful code](https://sanderhoogendoorn.com/the-zen-of-programming/))*


## 5. Communicatie is contextueel tweerichtingsverkeer


Communicatie vindt nooit in isolatie plaats. Al onze concepten vinden hun betekenis in een bepaalde context. Eén en hetzelfde woord kan verschillende dingen betekenen in verschillende contexten. Ken dus de context van je gesprekspartner - verken diens context, als dat nog niet het geval is. Alleen zo kun je ervoor zorgen dat je boodschap overkomt.


Communicatie is immers meer dan alleen informatie naar de ander zenden. Communicatie is het overbrengen van informatie die de kennis en overtuigingen van de ander beïnvloedt. Het is daarom altijd tweerichtingsverkeer. Jouw verbale en nonverbale gedrag brengen een reactie teweeg, en die reactie doet op zijn beurt hetzelfde bij jou. Het is een iteratief proces waarin twee of meer sprekers zich continu aanpassen aan elkaar.


De beïnvloede kennis en overtuigingen bevinden zich soms op expliciet niveau, soms op impliciet niveau. De eerste soort kan geverbaliseerd worden. De tweede soort is moeilijk in woorden uit te drukken. Het is een gevoel, dat je hooguit per analogie of nonverbaal uit kunt drukken. Soms kom je tijdens een code review bijvoorbeeld code tegen waar je slechts met één kreet op kunt reageren: "Brwaargh!" Geef die impliciete kennis de tijd om haar woorden te vinden. Even iets anders doen - een nachtje slapen, desnoods -, kan de sleutel zijn tot de oplossing van dit communiatieprobleem.


Verschillende contexten en impliciete kennis kunnen tot conflict leiden. Er zijn verschillende dingen die je kunt doen om uit deze situatie te raken. Actief luisteren, bijvoorbeeld (zie ook [deze blog](/blog/22/03/luisteren-sammenvatten-en-doorvragen/)). Of je cognitieve empathie oefenen: sommige mensen zien de wereld *oprecht* anders, en denken er daarom op een andere manier over na. Of aannemen dat je ernaast zit. Of, God verhoede, aannemen dat de ander gelijk heeft!


*([Arthur Doler](https://arthurdoler.com/) - [Getting your point accross: The psychology of communication](https://speakerdeck.com/arthurdoler/getting-your-point-across-the-psychology-of-communication))*


## 6. Baseer de communicatiestructuur in je code patronen in de echte wereld


Het aanroepen van publieke methods op verschillende deelsystemen binnen een monoliet zijn wezenlijk anders dan het aanroepen van een openbaar *endpoint* op een microservice. Wie zich onvoldoende bewust is van dat onderscheid, knutselt een prachtig microserviceslandschap in elkaar met de performance van een bejaarde luiaard.


Communicatie over het netwerk moet geleid worden door een helder achterliggend idee. Het loont zich om hiervoor naar de echte wereld te kijken. Dit levert het [mentale model](/tags/mentaal-model/) om de communicatiestructuur te begrijpen. Hoe verlopen de communicatiestructuren binnen verschillende soorten restaurants, bijvoorbeeld? 


Neem nu een foodtruck. Bemand door één persoon, zou je dit als een monoliet kunnen zien. Een bestelling (request) wordt aangenomen, het voedsel bereid (sequentieel uitvoeren van code) en vervolgens aan de klant overhandigd (response). 


Een eenvoudig microserviceslandschap zou je kunnen vergelijken met een foodtruck die door meerdere personen wordt bemand. Een bestelling (request) wordt aangenomen, op een papiertje geschreven en de klant wordt gevraagd om even te wachten (response). De man of vrouw achter de toonbank geeft het papiertje door aan degene die het voedsel bereid (een event wordt opgegooid) en kan zich op de volgende klant richten. Het is een *real life* implementatie van wat in softwareland een [*routing slip*](https://learn.microsoft.com/en-us/biztalk/esb-toolkit/message-routing-patterns#routing-slip) wordt genoemd.


Naarmate de complexiteit van de communicatiestructuren toeneemt, nemen de patronen toe in complexiteit. De communicatiestructuren in een fastfoodrestaurant als McDonalds kun je modelleren aan de hand van het [*choreography*-patroon](https://learn.microsoft.com/en-us/azure/architecture/patterns/choreography), die in een traditioneel restaurant met een chefkok hebben meer weg van [*orchestration*](https://medium.com/gbtech/orchestration-pattern-3d8f5abc3be3).


(*[Jimmy Bogard](https://jimmybogard.com/) - [Effective microservice communication and conversation patterns](https://www.youtube.com/watch?v=aHsVsbo_VOE)*)
