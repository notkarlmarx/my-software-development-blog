---
title: "Zes andere dingen die ik leerde op Techorama"
author: "Karl van Heijster"
date: 2022-10-21T10:07:54+02:00
draft: true
comments: true
tags: ["end to end tests", "low code development", "performance", "proof of concept", "software architectuur"]
summary: "Een tijd geleden bezocht ik softwareconferentie Techorama in Utrecht. Vandaag pen ik kort neer welke inzichten ik de tweede dag opdeed."
---

Een tijd geleden bezocht ik softwareconferentie [Techorama](https://www.techorama.nl/) in Utrecht - ik schreef er [hier] (LINK) al eerder over. Vandaag pen ik kort neer welke inzichten ik de tweede dag opdeed.


## 1. Bewust gebruik van de Garbage Collector kan de performance van je applicatie verbeteren


[*Garbage collection*](https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals) is een intensieve operatie die impact kan hebben op de performance van je systeem. Voor systemen waarvan een hoge performance één van de primaire vereisten is, kan het zich lonen om na te gaan hoe de code met *garbage collection* omgaat.


De [Garbage Collector](https://learn.microsoft.com/en-us/dotnet/api/system.gc?view=net-6.0) deelt objecten die hij op wil ruimen onder water in in [drie generaties](https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals#generations): 0, 1 en 2. Objecten die meerdere rondes van *garbage collection* overleven, worden gepromoveerd naar een hogere generatie. Naarmate ze in een hogere generatie komen, probeert de Garbage Collector ze minder vaak op te ruimen.


Je kunt de performance van je applicatie verbeteren door je objecten zoveel mogelijk in Generatie 0 en 1 te houden, bijvoorbeeld door het gebruik van [valuetypes](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types). Als een object eenmaal in Generatie 2 zit, dan loont het zich om dat object daar te houden. Het opruimen van Generatie 2-objecten is zeer intensief. Je kunt hiervoor de [`ObjectPool`](https://learn.microsoft.com/en-us/aspnet/core/performance/objectpool?view=aspnetcore-6.0).


Een andere manier om de performance van de Garbage Collector te verbeteren, is middels de [configuratiesettings](https://learn.microsoft.com/en-us/dotnet/core/runtime-config/garbage-collector). Applicaties staan standaard op de Workstation-instellingen. Voor ASP.NET applicaties, is de Server-instelling doorgaans een betere instelling. (Documentatie [hier](https://learn.microsoft.com/en-us/dotnet/core/runtime-config/garbage-collector#workstation-vs-server).)


Twee dingen zijn belangrijk om daar bij op te merken. 1. Meestal is *garbage collection* niet het performanceprobleem in je applicatie. Performanceproblemen ontstaan meestal doordat er verschillende calls over het netwerk of naar de database worden gemaakt. 2. Voer daarom altijd benchmarks uit op je code om na te gaan waar het probleem zit - en of je "verbetering" daadwerkelijk een verbetering is. Als een extreem hoge performance essentieel is voor je applicatie, voeg dan altijd benchmarkinformatie toe aan je pull request.


*([Aaron Stannard](https://aaronstannard.com/) - [.Net systems programming learned the hard way](https://www.youtube.com/watch?v=lx39ih2eyeE))*


## 2. Een Proof of Concept is geslaagd als deze inzicht heeft gegeven


Een Proof of Concept (POC) is géén prototype of pilot, en al helemaal geen productiecode. Een POC is een manier om te identificeren of een technische oplossing zijn doel raakt, of het de juiste waarde levert - het is een manier om er zeker van te zijn dat je niet de verkeerde oplossing bouwt. Het is een onderdeel in een proces om geïnformeerde keuzes te kunnen maken.


In de volgorde van de vier P's die ik zojuist noemde, staat een op de tweede plek. Eerst doe je een prototype om de techniek te valideren, vervolgens doe je een POC om het businessdoel te valideren. Daarna draai je een pilot, en ten slotte rol je uit naar productie - met code die productierijp is. POC's gaan dus over businesswaarde. (Dit is een terminologisch punt. In de praktijk zie ik vaak dat POCs en prototypes omgedraaid worden gebruikt. Dat is geen probleem, als maar duidelijk is wat je wanneer valideert.)


Een POC heeft een duidelijk doel, en een afgebakende timebox - meestal twee weken. Als dat wat je wil valideren niet in twee weken past, hak de POC dan op in meerdere deel-POC's. En stel voor elk deel een duidelijk doel, dat haalbaar is binnen die twee weken. Voer de POC uit onder dezelfde omstandigheden als waarin je productiecode zou schrijven (bijvoorbeeld wat betreft security). Je wil er zo vroeg mogelijk achter komen of een bepaalde oplossing haalbaar is in een productiecontext.


Het doel van een POC is niet: bewijzen *dat* iets kan. Het doel is: valideren *of* iets kan. Een POC die aantoont dat de bedachte oplossing niet de juiste is, is een geslaagde POC. De POC heeft je namelijk in staat gesteld om na twee weken (!) te kunnen concluderen: hier moeten we niet mee doorgaan. - Zonder POC zou je daar in het slechtste geval pas achter komen als je code in productie draait. Het is dus allesbehalve zonde van de tijd.


Documenteer na de POC altijd de uitkomst en de dingen waar je tegenaan bent gelopen. Dit is van onmisbare waarde voor volgende POCs, en om te kunnen beoordelen of veranderde omstandigheden het de moeite waard maken om een idee nogmaals te willen valideren.


*([John Martin](https://www.linkedin.com/in/johnqmartin/) - How to run successful Proof of Concepts (POCs))*


## 3. Probeer Playwright eens uit als E2E testing framework


[Playwright](https://playwright.dev/) is een testing framework om webapplicaties mee te kunnen testen, vergelijkbaar met [Cypress](https://www.cypress.io/how-it-works/). Het is beschikbaar als [plugin](https://marketplace.visualstudio.com/items?itemName=ms-playwright.playwright) voor [Visual Studio Code](https://code.visualstudio.com/).


Eén van de meest veelbelovende features van deze tool is [Codegen](https://playwright.dev/docs/codegen-intro#running-codegen). Dit stelt je in staat om een (rudimentaire) test uit te schrijven, door simpelweg door een applicatie heen te klikken. Elke klik wordt omgezet in een stuk testcode, waardoor het schrijven van *E2E*-tests een eitje wordt.


In hoeverre Playwright zijn potentie in de praktijk waar maakt, durf ik niet te beoordelen - ik heb de tool nog niet zelf gebruikt. Maar de demo zag er veelbelovend uit, zoveel is zeker.


*([Debbie O'Brien](https://debbie.codes/) - [Testing web applications with Playwright](https://www.youtube.com/watch?v=dxbh0bl4It8))*


## 4. Wees je bewust van de beperkingen van *low code*-applicaties


Laat ik heel helder zijn: ik ga niet voor mijn lol naar praatjes over *low code*-applicaties op conferenties. Ik wou eigenlijk naar een praatje over code reviews, maar ik verwachtte daar eigenlijk weinig nieuws te horen. Dus bezocht ik een uiterst teleurstellend praatje over het [Microsoft Azure Well-Architected Framework](https://learn.microsoft.com/en-us/azure/architecture/framework/). Dat hield ik zo'n twintig minuten uit, waarna ik toch maar besloot naar de sessie van mijn eerste keus te gaan - die drie minuten later ten einde kwam.


Uit frustratie liep ik maar de volgende zaal in - net op tijd om een samenvatting te horen van alle beperkingen van *low code*-applicaties. Zulke applicaties zijn namelijk weinig flexibel, niet schaalbaar, niet performant, moeilijk testbaar en ongeschikt voor complexe *use cases*. (Collega's van me hebben die lessen overigens onlangs in de praktijk mogen leren - waarvoor mijn oprechte deelneming.)


Maar *low code*-applicaties zijn wel voor een heel ander doel geschikt, namelijk om een oplossing te valideren. - Sterker nog, ze zijn bij uitstek geschikt *voor niet-techneuten* om oplossingen te valideren. Hun *drag and drop*-interfaces maken het voor collega's uit de business aantrekkelijk om zelf een oplossing in elkaar te klikken in een poging hun werk te vereenvoudigen. Als eenmaal is bewezen dat de oplossing werkt, kunnen ze hiermee aankloppen bij hun IT-afdeling, die dit als input voor een robuuster oplossing kan gebruiken.


*Low code* heeft zo de potentie om programmeurs en mensen uit de business dichter bij elkaar te brengen. En dat kan ik alleen maar aanmoedigen.


*([Iona Varga](https://www.linkedin.com/in/iona-v-641487191/) - The intersection point of low-code vs pro-code projects with regards to return on investment)*


## 5. Laat transacties los in een gedistribueerde omgeving


Alles leuk en wel, maar een [transactie](https://en.wikipedia.org/wiki/Transaction_processing) over verschillende databases is eigenlijk gewoon niet te doen. In een gedistribueerde omgeving kan er zoveel misgaan tussen twee schrijfacties in, dat je je beter kunt voorbereiden op de inconsistenties die onvermijdelijk gaan plaatsvinden, dan met man en macht [ACID](https://en.wikipedia.org/wiki/ACID) over een hele keten van microservices af te dwingen.


Pak het liever zo aan: binnen de context van één [aggregaat](https://martinfowler.com/bliki/DDD_Aggregate.html) - één microservice - zijn je databasecalls transactioneel. Als je de grens van het aggregaat eenmaal voorbijgaat, dan zul je een andere oplossing moeten vinden. Een typische oplossing is: het gebruik van een [service bus](https://en.wikipedia.org/wiki/Enterprise_service_bus).


*[Jimmy Bogard](https://jimmybogard.com/) - Consistency and agreements in microservices)*


## 6. Bart de Smet is een absolute held


Niks aan toe te voegen verder.


*([Bart de Smet](https://www.linkedin.com/in/bartdesmet/) - Adding a new language feature in C# in 60 minutes)*
