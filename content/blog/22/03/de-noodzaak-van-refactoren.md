---
title: "De noodzaak van refactoren"
author: "Karl van Heijster"
date: 2022-03-04T07:54:30+01:00
draft: false
comments: true
tags: ["agile ontwikkeling", "communicatie", "documentatie", "informatieanalyse", "refactoren", "sprint review", "stakeholders", "waarde"]
summary: "Ons team heeft een stakeholder wiens gezicht vertrekt, elke keer als we tijdens een Sprint Review aangeven tijd te hebben gestoken in het refactoren van onze applicatie. In zijn beleving is refactoren een verspilling van je tijd. Als we meer tijd hadden genomen om de wensen van onze gebruikers grondig te analyseren, redeneert hij, dan had zo'n dure, inefficiënte refactorslag kunnen worden voorkomen. Als ik iemand zo hoor redeneren, dan vertrekt míjn gezicht."
---

Ons team heeft een stakeholder wiens gezicht vertrekt, elke keer als we tijdens een Sprint Review aangeven tijd te hebben gestoken in het refactoren van onze applicatie. 


In zijn beleving is refactoren een verspilling van je tijd. Niet omdat hij niet gelooft dat een refactorslag de codekwaliteit van een applicatie verbetert, maar omdat hij vindt dat het een teken is dat je je applicatie in eerste instantie niet goed op hebt gezet. Als we meer tijd hadden genomen om de wensen van onze gebruikers grondig te analyseren, redeneert hij, dan had zo'n dure, inefficiënte refactorslag kunnen worden voorkomen.


Als ik iemand zo hoor redeneren, dan vertrekt míjn gezicht.


## Waterval


Refactoren is geen teken van inefficiëntie. Constant, meedogenloos refactoren is een essentieel onderdeel van de [filosofie achter Agile ontwikkeling](/blog/21/11/agile-zijn-niet-agile-doen/). Als softwareontwikkelaar vind ik het verbazingwekkend dat er - 20 jaar na de introductie van Agile, in een tijdperk waarin deze stijl van ontwikkelen zo mainstream is als maar kan - nog steeds stakeholders bestaan die dit niet inzien. 


(Maar dan herinner ik me weer: niet elke stakeholder zit zo diep in het softwareontwikkelwereldje als een ontwikkelaar, natuurlijk!)


Het idee dat je refactoring kunt voorkomen met gedegen analyse, is gebaseerd op wensdenken, op een papieren werkelijkheid. Want op papier is het eenvoudig, inderdaad. Stap 1: Je verzamelt de *requirements* voor je software-oplossing. Stap 2: je werkt deze uit in gedegen documenten. Stap 3: je programmeert de oplossing op basis van deze documenten. Stap 4: via tests verifieer je de werking van het systeem. Stap 5: blije gebruikers.


Het is de intuïtieve aantrekkingskracht van het [watervalmodel](https://nl.wikipedia.org/wiki/Watervalmethode) dat ervoor zorgde dat het het dominante ontwikkelparadigma kon worden in de jaren '80 en '90. 


## Informatie verzamelen


Maar dit model steunt op een onjuist aanname, namelijk dat je alle relevante informatie kunt verzamelen vóórdat je aan het programmeren slaat.


Ga maar na: wanneer weet je het best of een bepaalde oplossing werkbaar is? Vóórdat je onderzoek hebt gedaan? Nee, natuurlijk niet! Je moet eerst analyse verrichten. - Goed, die geef ik je. Je verricht analyse. Weet je nu alles wat je moet weten om een goede oplossing te bouwen? - Nee, je moet die analyse eerst uitwerken in een document, waarin de uitkomst van die analyse eenduidig beschreven staat.


Prima, dat doe je. En nu? Weet je nu alles wat je moet weten? - Nee: tijdens het programmeren zullen er onvermijdelijk vragen naar boven komen waar je geen rekening mee had gehouden. 


Nota bene, de vooronderstelling van het watervalmodel valt op dit punt al in duigen. Maar we zijn er nog niet.


Je voert wat verdere analyse uit tijdens het programmeren om de problemen waar je tegenaan liep, op te kunnen lossen. Weet je nu voldoende? - Nee, want zodra de tester aan de slag gaat, leer je van een heleboel scenario's waar je tijdens het programmeren geen rekening had gehouden. Die verwerk je. Gelukkig heb je nu alle relevante informatie eindelijk tot je beschikking, toch? 


\- Nee! Want zodra je je software aan een eindgebruiker presenteert, ontdek je dat deze op een compleet andere manier naar je oplossing aankijkt. Dit is de eigenlijke lakmoesproef: pas als een eindgebruiker met de software aan de slag gaat, kom je erachter of de informatie op basis waarvan je een oplossing hebt bedacht, ook maar enigszins volledig was.


## Nooit klaar


De implicaties van deze observatie zijn niet te overdrijven. Het betekent dat *software nooit klaar is*. Immers: elke codewijziging levert feedback op van eindgebruikers, die (potentieel) leidt tot tot nieuwe codewijzigingen, die weer nieuwe feedback opleveren.


We refactoren niet omdat we hebben gekort op de analysefase[^1], we refactoren omdat we - per definitie! - nu een beter begrip hebben van wat onze code moet doen dan hiervóór.


En dit is het belangrijke punt: we hebben een beter begrip dan hiervóór, precies omdat we een eindgebruiker een stuk code hebben gepresenteerd waarvan we weten dat het niet perfect is. Die code was een middel om feedback te verkrijgen. 


Feedback, nota bene, die bruikbaarder is dan alle eenduige requirements in het oorspronkelijke analysedocument bij elkaar. Want het beeld van de eindgebruiker van hoe de oplossing eruit hoort te zien, is veranderd nu deze van een enigszins werkende oplossing heeft mogen proeven.


En ten tweede - dit is wat mij betreft het doorslaggevende punt waarop Agile het watervalmodel ver achter zich laat -, die enigszins werkende code heeft onmiddellijk businesswaarde geleverd. Niet per se enorme waarde - de oplossing is immers incompleet, gedeeltelijk onjuist, een ruwe versie -, maar waarde niettemin. Met deze versie van de code is een eindgebruiker al gedeeltelijk geholpen in zijn of haar probleem.


## Wat zie je?


Dat is precies waarom het zo vervelend is voor ons ontwikkelaars, als onze stakeholder zijn gezicht vertrekt als we enthousiast over onze refactorslag vertellen. Hij heeft alleen maar oog voor de vermeende inefficiëntie van die bezigheid. 


Maar hij heeft geen oog voor het feit dat onze ongerefactorde code al waarde leverde. Waarde die zijn gedroomde analysedocument niet zou hebben gehad. 


En hij heeft geen oog voor het feit dat we, getuige de refactorslag, een beter begrip hebben ontwikkeld van het probleem en de oplossing. Een begrip dat, nogmaals, zijn analysedocument ons niet had kunnen geven.


...schreef hij, met een vertrokken gezicht. Maar 't klaaguurtje is nu voorbij. [Oogjes dicht en snaveltjes toe](https://youtu.be/1c84T7KT-xs).


[^1]: Hoewel we óók soms korten op de analysefase. Ontwikkelaars zijn ook maar mensen, en soms doen we dingen waarvan we achteraf zeggen: dat hadden we inderdaad beter aan moeten pakken.
