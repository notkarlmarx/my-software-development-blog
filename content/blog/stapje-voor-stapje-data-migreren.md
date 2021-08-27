---
title: "Stapje voor stapje data migreren"
author: "Karl van Heijster"
date: 2021-08-27T10:11:37+02:00
draft: true
comments: true
tags: ["databases", "datamigratie", "leermoment", "NoSQL", "open source", "procesverbetering", "proof of concept", "software ontwikkelen", "testen"]
summary: "Als er één constante is in softwareontwikkelland, dan is het wel dat software constant verandert. Nieuwe inzichten noodzaken ontwikkelaars om hun code aan te passen om bepaalde *use cases* beter te kunnen ondersteunen. Soms betekent dat dat er een aanpassing moet plaatsvinden in je model. Hoe ga daarbij om met data die is opgeslagen volgens het verouderd model?"
---

Als er één constante is in softwareontwikkelland, dan is het wel dat software constant verandert. Nieuwe inzichten noodzaken ontwikkelaars om hun code aan te passen om bepaalde [*use cases*](https://nl.wikipedia.org/wiki/Usecase) beter te kunnen ondersteunen. Soms betekent dat dat bepaalde [algoritmen](https://nl.wikipedia.org/wiki/Algoritme) moeten worden vervangen, andere keren betekent dat dat er een aanpassing moet plaatsvinden in het model waar de algoritmen gebruik van maken.


## Modelwijzigingen


Die laatste situatie kan problemen opleveren. De meeste applicaties maken gebruik van data die is opgeslagen in een [database](https://nl.wikipedia.org/wiki/Database). Hoe ga je bij modelwijzigingen om met data die is opgeslagen volgens een inmiddels verouderd model?


Er zijn twee opties: ofwel je beschouwt alle oude data als verloren, ofwel je vindt een manier om de verouderde data om te zetten naar het nieuwe model. De eerste optie is in de meeste gevallen onaanvaardbaar. Uitzonderingen zijn: privéprojecten of applicaties die zich nog in een pilotfase bevinden.


In alle andere gevallen zal er een [datamigratie](https://en.wikipedia.org/wiki/Data_migration) plaats moeten vinden. Ook hier bestaan twee smaken in: ofwel je migreert alle data in één keer - de zogenaamde *big bang* -, ofwel je doet dat stapje voor stapje.


## *Big bang*


Mijn team heeft jarenlang van dat eerste smaakje mogen proeven in onze *legacy*-applicatie. We hadden een aparte tool ontwikkeld die gebruik maakte van de applicatiecode om de database te benaderen. In die tool gaven we aan welke eigenschappen sinds de modelwijziging waren veranderd. Vervolgens drukten we op een knop, en - *tada!* - de data was weer *up to date*.


Deze oplossingsrichting is relatief eenvoudig, maar niet zonder nadelen. Ten eerste speelt er een coördinatievraagstuk. Wanneer je de nieuwe code uitrolt zonder het migratiescript op de productieomgeving te draaien, wordt de applicatie onbruikbaar. Andersom geldt dat, als je geen boze gebruikers wil, je het migratiescript niet kunt draaien zonder de nieuwe code uit te rollen.


Dit maakte een uitrol een heikel punt, dat goede afstemming vergt met gebruikers. Je kunt niet elke nieuwe wijziging zomaar meer doorzetten naar je productieomgeving. Als gevolg daarvan hopen codewijzigingen zich op. Wanneer er dan een bug wordt ontdekt, valt moeilijk na te gaan in welke codewijziging deze erin is geslopen.


Een tweede probleem is [schaalbaarheid](https://en.wikipedia.org/wiki/Scalability). In de loop der jaren was de database van onze applicatie enorm gegroeid. Hierdoor was de migratie geen kwestie van seconden meer, zoals op onze ontwikkellaptops, maar minuten. Als er halverwege de migratie een probleem ontstond, dan was onze data in corrupte staat geraakt en moest de boel terug worden gedraaid. Vervolgens begon het proces weer van voren af aan.


Dit is het soort ervaringen waar horrorverhalen uit worden geboren.


## *Proof of concept*


Met deze ervaringen in het achterhoofd, besloot het team te onderzoeken of het tweede smaakje misschien niet een aantrekkelijker optie was. 


Twee factoren speelden daarbij in ons voordeel. (1) Onze nieuwe applicatie maakt gebruik van [RavenDB](https://ravendb.net/), een [NoSQL-database](https://nl.wikipedia.org/wiki/NoSQL) die [objecten](https://en.wikipedia.org/wiki/Object_(computer_science)) opslaat in [JSON](https://nl.wikipedia.org/wiki/JSON)-formaat. (2) Er bestaat [*open source*](https://nl.wikipedia.org/wiki/Open_source) tooling in de vorm van [Migrations.Json.Net](https://github.com/Weingartner/Migrations.Json.Net), die één of meerdere migratiescripts uit kan voeren bij het [serialiseren](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/serialization) of deserialiseren van JSON naar objecten.


Tijdens de [*proof of concept*](https://en.wikipedia.org/wiki/Proof_of_concept) (POC) waarin we deze technieken met elkaar combineerden, deden we de volgende inzichten op:


- **Het werkt!** Het is mogelijk om *on the fly* nieuwe [*properties*](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties) aan een object toe te voegen, of bestaande *properties* te wijzigen, wanneer deze opgehaald worden uit onze database. De oude data wordt omgezet naar het nieuwe model *wanneer dat nodig is*, niet wanneer het ontwikkelteam dat forceert.

- **Deze functionaliteit laat zich niet integratietesten.** Ik had een test geschreven waarin ik met wat trucage een verouderd object opsloeg in RavenDB, om te zien of ik hem als geüpdate object terug zou krijgen, maar dat vond de database niet zo leuk. Binnen de POC bleef dit ongemak echter beperkt: de functionaliteit liet zich net zo goed handmatig bewijzen. 
  
  Maar voor de daadwerkelijke implementatie van deze techniek is het wel belangrijk om deze beperking in het achterhoofd te houden. Het haalt een stukje zekerheid weg voor de ontwikkelaar wiens taak het is de migratie te schrijven, en legt extra daarnaast verantwoordelijkheid bij de tester neer.

- **Pas op voor botsende *properties*.** RavenDB kent zijn eigen [versioneringssysteem](https://ravendb.net/docs/article-page/5.2/csharp/server/extensions/revisions), waar we als ontwikkelaarteam dankbaar gebruik van maken. Onze objecten kennen dan ook een *Version*-*property* waarmee we de versie van een object naar de eindgebruiker communiceren. Migrations.Json.Net veronderstelt echter ook een *Version*-*property* om te kunnen bepalen welke migratiescripts er allemaal uitgevoerd dienen te worden. Een object dat op versie 3 zit, zal de migraties uit moeten voeren om van versie 1 naar 2 naar 3 te gaan. 

  Zoals te verwachten valt, is dat een verwarrende situatie voor beide tools. Om hiermee om te kunnen gaan, moet het team deze ambiguïteit oplossen. Dat kan ofwel door onze eigen *Version* om te zetten naar een andere naam, ofwel door een *pull request* te doen op Migrations.Json.Net om de naam van die property configurabel te maken. Merk op dat het gebruik van Migrations.Json.Net niet de geschikte kandidaat is om dit voor elkaar te krijgen, hiervoor moet een migratiescript oude stijl worden geschreven.


## Stapje voor stapje


Door verouderde data stapje voor stapje te migreren naar een nieuw model, worden de nadelen van onze oorspronkelijke oplossingsrichting verholpen. De modelwijziging en migratiecode worden tegelijkertijd uitgerold en vergen vervolgens geen handmatige actie meer van het ontwikkelteam. Het coördinatieprobleem is dus van de baan. 


Hetzelfde geldt voor de schaalbaarheidsproblematiek. Het kritieke moment waarop alle data moest worden gemigreerd, is uitgesmeerd over een veelvoud aan niet-kritieke momenten. In tegenstelling tot de bulkmigratie, kan de migratie van individuele objecten snel en pijnloos gebeuren.


Bovendien is de oplossing eenvoudig te bouwen door gebruik te maken van onze bestaande tooling in combinatie met *open source*-software.


Kleven er dan helemaal geen nadelen aan deze oplossingsrichting? Ongetwijfeld wel. Maar daar zullen we in de loop van de tijd pas achter komen, stapje voor stapje. En dan zal ik ongetwijfeld een blog schrijven over de zegeningen van *big bang*-datamigraties.
