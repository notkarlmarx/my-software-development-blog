---
title: "Hoe Technische Schuld Te Monitoren én Prioriteren"
author: "Karl van Heijster"
date: 2021-07-21T21:53:01+02:00
draft: true
comments: true
tags: []
summary: ""
---

Een applicatie gezond houden vergt een continue inzet. Het opbouwen van technische schuld gebeurt daarentegen helemaal vanzelf. Het is als ontwikkelaar dus niet alleen je taak om nieuwe features toe te voegen. Een belangrijk deel van je werk bestaat uit het tegengaan van coderot.


## Tooling


Gelukkig bestaan er een heleboel goede tools om de technische schuld van een applicatie te kunnen monitoren.


### SonarCloud


[SonarCloud](https://sonarcloud.io/) (het hippe cloud-broertje van [SonarQube](https://www.sonarqube.org/)) biedt bijvoorbeeld een mooi overzicht van allerhande bugs en [*code smells*](https://en.wikipedia.org/wiki/Code_smell) in je codebase. Daarnaast houdt de tooling een overzicht bij van alle security-sensitieve onderdelen van je applicatie, die je als ontwikkelteam kan beoordelen op hun ernst.


Belangrijker nog, je kunt SonarCloud [aansluiten op je build pipeline in Azure DevOps](https://sonarcloud.io/azure-devops), waardoor je als ontwikkelaar bij elke [*pull request*](https://docs.github.com/en/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) (PR) onmiddellijk feedback krijgt op de kwaliteit van je code. Dit is een fantastische service, waar mijn team afwisselend dankbaar en mopperend gebruik van maakt.


### NDepend


De analyse van SonarCloud bevindt zich echter voornamelijk op codeniveau, waardoor de tool minder geschikt is om architecturele rot in de code in kaart te brengen. Vanuit die invalshoek is [NDepend](https://www.ndepend.com/) een geschikter alternatief. Er bestaat een *stand alone*-applicatie van deze tool, maar in de rechtstreekse integratie in [Visual Studio](https://visualstudio.microsoft.com/) bewijst NDepend haar grootste toegevoegde waarde.


Met name het [*class dependency diagram*](https://www.ndepend.com/docs/class-dependency-diagram) heeft mij en mijn team al meermaals gered van ongemerkte [circulaire afhankelijkheden](https://en.wikipedia.org/wiki/Circular_dependency). Ook het op verschillende niveaus [in beeld kunnen brengen van de complexiteit van je codebase](https://www.ndepend.com/docs/treemap-visualization-of-code-metrics) is een waardevolle feature bij het oppakken van grootschalige refactorslagen.


## Mensenwerk


Software ontwikkelen is echter mensenwerk. En hoe goed de tooling tegenwoordig ook is, ze is niet meer dan een hulpmiddel voor ontwikkelaars om grip te krijgen op een codebase. De beste manier om technische schuld in beeld te krijgen, is dan ook niet door allerhande tools op je code los te laten, maar *door erover te praten met je collega's*.


Precies om deze reden heeft ons team een tweewekelijks overleg opgezet waarin de ontwikkelaars hun inzichten in de code met elkaar delen. Dat kunnen zaken zijn die je tijdens het coderen tegenkwam - bijvoorbeeld een stuk code dat complexer is dan zou moeten -, of een vraag die tijdens een [code review](https://en.wikipedia.org/wiki/Code_review) opkwam, maar niet kritiek genoeg was om een PR tegen te houden.


We noemen dit overleg het *Team Alignment*. Het doel van het overleg is immers om als ontwikkelaars op één lijn te komen wat betreft de pijnpunten van onze code. (Maar eigenlijk werd de naam vooral gekozen als parodie op de diverse teamoverstijden *alignment*-overleggen waar onze lead developer elke week met tegenzin aanschoof.)


## Het proces


Het Team Alignment kent min of meer een vast proces:


- Gedurende de Sprint is elke ontwikkelaar vrij om punten op de Alignment-agenda te plaatsen. Zo'n punt bestaat uit drie onderdelen: een titel, een korte omschrijving, en de naam van degene die het punt heeft ingebracht. Diegene neemt tijdens het overleg het voortouw in het beschrijven van het probleem.


- Als we bijeenkomen, gaan we eerst na of er agendapunten zijn die, naar inschatting van de ontwikkelaars, op dit moment hoge prioriteit hebben. Die punten bespreken we het eerst. De overige punten worden op volgorde besproken waarop ze op de agenda zijn gezet. Het bespreken van elk agendapunt zou niet langer dan vijf à tien minuten mogen duren.


  Merk op dat het voor kan komen dat het Alignments op de planning staan zonder agendapunten. Dit is op zich niet problematisch. Het team komt dan bijeen om te zien of er spontaan nog punten boven komen drijven. Zo niet, dan vervalt het overleg eenvoudigweg. 


- De bespreking van elk agendapunt kent twee mogelijke uitkomsten. (1) Het punt is (op dit moment) niet belangrijk genoeg. In dat geval gaan we door naar het volgende punt. (2) Het team concludeert dat er actie moet worden uitgezet op het punt. In dat geval wordt er een [ontwikkelaar](/blog/21/06/schrijf-pbis-en-doe-het-goed) aangewezen die een [Product Backlog Item (PBI)](https://www.scrum.org/resources/what-is-a-product-backlog) aanmaakt waarin [het probleem en de oplossingsrichting verder worden uitgewerkt](/blog/21/06/hoe-ik-mijn-pbis-opzet/). Zo'n PBI komt dan ter sprake in de volgende [Refinement](https://www.scrum.org/resources/blog/product-backlog-refinement-explained-13).


  (Onze Scrum Master had laatst overigens een goede suggestie. Gezien de punten technisch van aard zijn en alle ontwikkelaars bij elkaar zitten, zou de actie ook op dat moment ingeschat kunnen worden en kan het PBI er later bij geschreven worden. Stel dat tijdens het uitwerken van het PBI alsnog blijkt dat er nieuwe inzichten zijn, dan kan deze alsnog tijdens de Refinement worden behandeld.

  
  Het voordeel van die aanpak is dat het Refinements wat minder stroperig maakt (en dat is [altijd welkom](/blog/21/05/het-doel-van-deze-sprint-is-niet-om-code-te-schrijven)!). Het nadeel is dat het de niet-ontwikkelaars in het team, zoals de Product Owner (PO), wat meer in het duister laat rondom de technische schuld van de applicatie.) 


## Technische schuld monitoren...


Het voordeel van een Team Alignment is allereerst simpelweg dat technische schuld in beeld wordt gebracht én er acties worden uitgezet om deze in te dammen. Dat klinkt voor de hand liggend, maar is allesbehalve vanzelfsprekend. Te vaak komt het voor dat ontwikkelteams rücksichtlos features toevoegen aan een applicatie, om er na een jaar achter te komen dat hun applicatie een ononderhoudbaar zooitje is geworden.


De reden daarvoor is dat het moeilijk is om de business case te maken voor het wegwerken van technische schuld. Stakeholders zullen vrijwel altijd nieuwe features prioriteren boven onderhoud. Het gevolg is dat het wegwerken van technische schuld pas een prioriteit wordt als het te laat is.


## ...én prioriteren


Het tweede, minder in het oog springende voordeel van een Team Alignment houdt precies daar mee verband. Het overleg stelt het team in staat om technische schuld te *prioriteren*. Dat gebeurt op twee manieren. 


Ten eerste toont het team middels een structureel overleg dat het waarde hecht aan het aanpakken van technische schuld. Het opvoeren van PBI's om die schuld weg te werken, is een teken aan de PO: *wij als team vinden dat dit moet gebeuren.* 


Ten tweede stelt de onderlinge communicatie het team in staat om de noodzaak van hun PBI's te verdedigen. Doordat elke ontwikkelaar aan het eind van elk agendapunt overtuigd is van de redenen waarom er actie moet worden uitgezet, kan er een front gevormd worden wanneer de PBI's dreigen te worden gedeprioriteeerd. Met een heel team tegenover zich, wordt het moeilijker voor de PO om deze PBI's terzijde te schuiven.


Eén van de grootste uitdagingen van technische schuld is de business case maken voor het oplossen ervan. Om dat voor elkaar te kunnen krijgen, is het essentieel dat je als ontwikkelteam goed uit kan leggen waar de problemen in de code zitten en hoe ze opgelost kunnen worden. Een Team Alignment is een daar een uitstekend middel voor.


Hoe gaat jouw team om met de aanpak van technische schuld?
