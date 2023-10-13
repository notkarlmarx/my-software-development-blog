---
title: "Schone interfaces, simpele implementaties"
author: "Karl van Heijster"
date: 2023-10-13T08:28:39+02:00
draft: false
comments: true
tags: ["incrementele ontwikkeling", "leermoment", "mentaal model", "product backlog refinement", "representational state transfer (REST)", "samenwerking", "software ontwikkelen"]
summary: "Het dilemma was als volgt: ofwel de deadline missen met een \"goede\" oplossing (dat wil zeggen: een oplossing die de REST-standaard volgt), ofwel de deadline halen met een slechte (die een uitzondering introduceert in de opzet van onze API). Maar: dat is een vals dilemma."
---

Een tijd terug viel er tijdens een refinement een kwartje bij mij.


Mijn team en ik, we spraken over het implementeren van een algemene zoekfunctionaliteit aan onze back-end. Je moet weten: onze applicatie gebruikt drie databases, [SQL Server](https://www.microsoft.com/en-us/sql-server) voor [relationele data](https://en.wikipedia.org/wiki/Relational_database "'Relational database', Wikipedia"), [RavenDB](https://ravendb.net/) voor [niet-relationele data](https://en.wikipedia.org/wiki/Document-oriented_database "'Document-oriented database', Wikipedia"), en de [Azure Blob Storage](https://azure.microsoft.com/en-us/products/storage/blobs) voor [binaire data](https://en.wikipedia.org/wiki/Binary_data "'Binary data', Wikipedia"). Al die data hangt op de een of andere manier met elkaar samen. Binaire data is geassocieerd met niet-relationele data; niet-relationele entiteiten zijn altijd slechts ontsluitbaar in een relationele context.


"Gebruik de opslagmethode die het best bij de soort data past" klinkt als een intuïtief uitgangspunt. Maar de complexiteit die hij het volgen van dat mantra met zich meebrengt, neemt exponentieel toe met elke opslagmethode. (Het alternatief, alle data in één opslagmethode forceren, kent weer zijn eigen problemen.)


## Duur


Hoe dan ook, de details van die opzet doen er nu niet toe. Waar het om gaat is: we wilden een algemeen endpoint op onze [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer "'Representational state transfer', Wikipedia") [Web API](https://en.wikipedia.org/wiki/Web_API "'Web API', Wikipedia") definiëren om alle data te kunnen doorzoeken. Gedurende die refinement werden we het eens over het feit dat [Azure Elasticsearch](https://www.elastic.co/partners/microsoft-azure) een veelbelovende oplossingsrichting bood voor dit probleem.


Alleen: het was wel een betrekkelijk dure oplossing. We zouden onze code grondig onder handen moeten nemen. Elke keer als we elke soort data opsloegen, zouden we de indexen van Elasticsearch bij moeten werken. Dat betekende dat we op verschillende plekken extra code toe moesten voegen (daarmee het [Single-Responsibility Principe](/tags/single-responsibility-principe/ "Blogs met de tag 'single-responsibility principe'") schendend), of we zouden de code grondig moeten herstructureren om die indexen met een [decorator](https://refactoring.guru/design-patterns/decorator "'Decorator', Refactoring.guru") in één keer toe te kunnen voegen. Welke oplossingsrichting we ook kozen, we zouden de deadline die ons gesteld werd voor deze functionaliteit, sowieso niet halen.


## Specifiek


Ik vroeg door: waarom werd deze functionaliteit precies gewenst? -- Een algemene zoekfunctionaliteit stond al heel lang op het wensenlijstje, was het antwoord. -- Maar wat vormde de concrete aanleiding voor deze discussie, waarom hadden we het *nu* over het doorzoeken van de applicatie? (Ik was zojuist terug van vakantie, voegde ik toe, ik moest er nog even in komen.) 


Wat bleek: *op dit moment* bestond er een behoefte om op één (1) property van één (1) object te kunnen zoeken.


We hadden helemaal geen algemene zoekfunctionaliteit nodig. We hadden een heel specifieke zoekfunctionaliteit nodig. -- Althans, op dit moment.


Dus ik stelde voor: waarom definiëren we niet een nieuw endpoint voor dat ene object, met de mogelijkheid om op die ene property te zoeken? Dan hebben we geen Elasticsearch nodig, dan kunnen we ermee wegkomen om één (1) database te query'en -- en dat was dat. We zouden op korte termijn dit endpoint kunnen gebruiken om de onmiddellijke behoefte te bevredigen, en op de lange termijn zouden we over kunnen stappen op het algemene endpoint waarmee alle data doorzocht kon worden.


## Tegenwerpingen


Verschillende teamleden wierpen tegen dat dit soort tijdelijke oplossingen nooit tijdelijk blijken te zijn. De ervaring wijst uit dat er maar zelden ruimte kan worden gemaakt om dit soort technische schuld te vervangen. 


Bovendien, mijn voorstel kwam er op neer een enkel endpoint te definiëren dat afweek van de REST-standaard. Het zou een kwestie van tijd zijn voordat de volgende wens de volgende afwijking zou rechtvaardigen. Totdat er op een gegeven moment maar weinig RESTful zou zijn aan onze RESTful API.


## Dilemma


Het dilemma was als volgt: ofwel de deadline missen met een "goede" oplossing (dat wil zeggen: een oplossing die de REST-standaard volgt), ofwel de deadline halen met een slechte oplossing (die een uitzondering introduceert in de opzet van onze API).


Maar: dat is een vals dilemma. Na een tijd lang argumenten heen en weer gepingpongd te hebben, merkte een collega op dat we ook een API konden ontsluiten die de REST-standaard volgt, maar waarvan de implementatie op dit moment nog beperkt is. We zouden de contouren van een algemene zoekfunctionaliteit kunnen definiëren. Maar op dit moment hoefden we alleen nog resultaten terug te geven bij dat ene object met die ene property -- in alle andere gevallen zouden we een foutcode terug kunnen sturen.


Op het moment dat nieuwe (kortetermijn)behoeften rondom het kunnen doorzoeken van data zich aan zouden dienen, zouden we de implementatie steeds verder kunnen uitbreiden. De contouren die we op voorhand hadden gedefinieerd, zouden blijven staan -- het plaatje zouden we stap voor stap inkleuren.


## Incrementeel


Achteraf is het een voor de hand liggende suggestie. Software ontwikkelen is een [incrementeel](/tags/incrementele-ontwikkeling/ "Blogs met de tag 'incrementele ontwikkeling'") proces. Een ontwerpstrategie die stelt dat we alleen een snelle kortetermijnoplossing of een langzame langetermijnoplossing kunnen bouwen, doet daar geen recht aan. 


Het model dat zo'n strategie ons voorspiegelt, is te simpel. Het gaat uit van een monolitische *oplossing*, wat dat ook moge zijn. Maar de oplossing bestaat in dit geval uit twee delen: de interface en de implementatie.


Wanneer we interfaces definiëren, dan is het raadzaam om de langere termijn in gedachten te houden. (Natuurlijk kun je daar ook in doorschieten -- het gevaar van *over engineering* ligt altijd op de loer.) De implementaties van die interfaces hoeven zich slechts op de korte termijn te richten.


Als we onze interfaces schoon houden en onze implementaties simpel, dan zijn we in staat om toekomstbestendige oplossingsrichtingen uit te zetten die we op basis van onmiddellijke behoeften kunnen uitwerken. 
