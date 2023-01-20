---
title: "Aantekeningen over requirements deel 2"
author: "Karl van Heijster"
date: 2023-01-06T12:10:25+01:00
draft: true
comments: true
tags: ["agile ontwikkeling", "boeken", "communicatie", "documentatie", "informatieanalyse", "requirements", "samenwerking"]
summary: "Het opstellen van de juiste requirements is één van de moeilijkste onderdelen van softwareontwikkeling. In een eerdere blog beschreef ik de eerste acht lessen die Karl Wiegers of dit onderwerp formuleerde in *Software Development Pearls*. In deze blog volgen de tweede acht."
---

Het opstellen van de juiste requirements is één van de moeilijkste onderdelen van softwareontwikkeling. In [een eerdere blog] (LINK) beschreef ik de eerste acht lessen die [Karl Wiegers](https://www.karlwiegers.com/) of dit onderwerp formuleerde in [*Software Development Pearls*](https://www.informit.com/store/software-development-pearls-lessons-from-fifty-years-9780137487776). In deze blog volgen de tweede acht.


**IX.**


Wie bepaalt wat de kwaliteit is van de requirements? Hun gebruikers, niet de makers. Vraag daarom feedback van verschillende gebruikersgroepen om te zien of de requirements voldoen aan de noodzakelijke kwaliteitskenmerken. Elke groep zal vanuit hun eigen perspectief naar de requirements kijken. Stakeholders uit de business beoordelen hen bijvoorbeeld vooral op de mate waarin ze tegemoet komen aan de behoeften van het bedrijf. Ontwikkelaars kijken of ze begrijpelijk zijn, en of ze überhaupt wel zijn te implementeren gegeven de beschikbare tijd en middelen. Testers gaan na of de requirements testbaar zijn, d.w.z.: scherp genoeg omschreven om er tests voor te kunnen schrijven.


Je zult nooit perfecte requirements schrijven. Gelukkig is dat ook niet het doel. De requirements moeten *goed genoeg* zijn. Ze moeten je in staat stellen om naar de volgende ontwikkelfase te gaan. 


Je kunt de informatie in requirements op verschillende manieren bekijken:


1. Het soort informatie (bijv. functioneeel vs. non-functioneel);

2. De breedte van de infromatie (bijv. een compleet overzicht vs. alleen de requirements met de hoogste prioriteit);

3. De diepte van de informatie (bijv. alleen *happy paths* vs. *happy* en *sad paths*).


Ontbrekende informatie in de requirements zal hoe dan ook worden opgevuld - bij voorkeur in gesprek met de relevante stakeholders, en anders via aannames die de ontwikkelaar tijdens het implementeren zal maken. De eerste is zoals voorgeschreven binnen de Agile manier van werken - de tweede is hoe het helaas nog te vaak in de praktijk gebeurt. Merk op dat aannames vaak "onzichtbaar" zijn voor degene die ze maakt. Pas wanneer een stakeholder feedback geeft op het opgeleverde product, valt het kwartje dat er aannames zijn gemaakt.


Neem, wanneer dat gebeurt, een stap terug en reflecteer: hoe heeft dit kunnen gebeuren, en hoe voorkomen we het in de toekomst? Welke aanname was hier de schuldige? Waar kwam die vandaan? Welke informatie ontbrak er in de requirements? Neem stappen om ervoor te zorgen dat die informatie de volgende keer wel aanwezig is.


Onthoud: het doel is niet om perfecte requirements te schrijven, maar om ze zodanig op te stellen dat de volgende fase van het ontwikkelproces zo efficiënt mogelijk van start kan gaan. Zowel aannames als het continu terug moeten gaan naar stakeholders voor verheldering, zijn een teken dat er iets mis is met het proces.


**X.**


Requirements worden niet "verzameld" - dat woord suggereert dat de requirements ergens rondslingeren, dat iemand ze maar op hoeft te pakken en er een strikje omheen hoeft te doen. 


Nee, requirements worden aan het licht gebracht, onttrokken of ontlokt aan stakeholders. Het vraagt tijd en inzet om de requirements op een juiste manier te formuleren - om nog maar te zwijgen van de tijd en moeite die het kost om de benodigde informatie te verzamelen om ze überhaupt te kunnen formuleren.


En dat is geen lineair proces. Het is niet zo dat je eerst de informatie verzamelt, en je dan concentreert op de juiste formulering. Dat is niet hoe communicatie werkt. Je begrip van de requirements is eerder cirkelvormig. Elk nieuw stukje informatie stelt je in staat om de requirements beter te formuleren, en elke formulering stelt je in staat om de informatie beter te verzamelen en te verwerken. Je begrip volgt de [hermeneutische cirkel](https://en.wikipedia.org/wiki/Hermeneutic_circle).


Merk op: als ik zeg dat requirements je in staat moeten stellen naar de volgende fase in het ontwikkelproces te gaan, dan doel ik niet per se op de programmeerfase. De volgende fase in het proces zou net zo goed kunnen zijn: nogmaals de requirements doornemen en verfijnen.


Gebruik verschillende technieken om requirements te onttrekken. Denk aan interviews - zowel individueel als in groepsverband -, workshops, vragenlijsten, observatie van het huidige werkproces, het analyseren van documentatie, en het bouwen en voorleggen van prototypes.


**XI.**


Communicatie is de sleutel tot een succelvol project. In het bijzonder: de communicatie tussen het ontwikkelteam en de gebruikers van het systeem. Zorg voor effectieve communicatiepaden tussen beide groepen.


Het gesprek tussen eindgebruikers en ontwikkelaars is tweerichtingsverkeer. Gebruikers bieden informatie aan aan het ontwikkelteam. Zij leveren de input aan op basis waarvan er ontwikkeld zal worden. Het team stelt op hun beurt verhelderingsvragen aan de eindgebruikers: bedoel je zus, of meer zo? Ook de ontwikkelde software - in alle stadia, dus in haar ruwe eerste vormen én als eindproduct - kan aan eindgebruikers getoond worden om een beter begrip te verkrijgen.


Noteer daarom altijd waar bepaalde informatie vandaan komt. Zo weet je, als er onduidelijkheden boven komen drijven, bij wie je aan moet kloppen voor een antwoord op je vragen.


**XII.**


Bij heel kleine projecten kunnen ontwikkelaars en eindgebruikers één op één met elkaar samenwerken. Naarmate het project groter wordt, wordt het belangrijker om een goede tussenpersoon te regelen, om het ontwikkelteam niet te overstelpen met (conflicterende?) informatie. Dat kunnen vertegenwoordigers zijn die uit de poule van eindgebruikers komen (ook wel *product champions* genoemd), een projectmanager of een [Product Owner](https://www.scrum.org/resources/what-is-a-product-owner), al dan niet in combinatie met een businessanalist. In sommige organisatie vervult de marketingafdeling deze rol: hun marktonderzoek stelt hen in staat om het ontwikkelteam de juiste richting in te sturen.


Hoe je die rol ook invult, stel jezelf altijd als doel te zorgen voor helder en continu tweerichtingsverkeer in de communicatie. Zonder feedback van gebruikers zul je nooit weten of je het juiste ontwikkelt of niet.


**XIII.**


Expliciete communicatie heeft de voorkeur boven impliciete. Neem niet aan dat je lezer wel zal snappen wat je bedoelt. Probeer ambiguïteiten zoveel mogelijk te vermijden. In het beste geval zullen ontwikkelaars een ambiguïteit opmerken en om verheldering vragen. In het slechtste geval nemen ze reflexief één interpretatie voor waarheid en aan en zullen ze die implementeren. Hopen dat het de juiste interpretatie was, is een twijfelachtige strategie.


Behandel, als opsteller van requirements, geïmpliceerde requirements als niet-bestaand. Voor zover deze geïmplementeerd zullen worden (spoiler alert: ze zullen niet geïmplementeerd worden), zullen ze toch niet overeenkomen met je verwachtingen. Waarom niet? Omdat ze niet gespecificeerd zijn! Over het algemeen zijn mensen - en ontwikkelaars in het bijzonder - behoorlijk slecht in het lezen van andermans gedachten. Zet daar dus niet op in. Als je niet expliciet hebt aangegeven dat iets een requirement is, dan zal degene die de software bouwt daar ook geen rekening mee houden.


Probeer zo precies en compleet mogelijk te zijn in het uitspellen van de requirements.


**XIV.**


Hoe meer zielen, hoe meer vreugd - en meer meningen. Hoe groter de groep, des te moeilijker is het om een productieve discussie te hebben. Het is moeilijk om mensen bij de les te houden, gesprekken ontsporen richting zijpaden die al dien niet overeenkomen met de stokpaardjes van een deel van de aanwezigen.


Houd focus in het gesprek, onder andere door het aantal aanwezigen zo klein mogelijk te houden. Nodig geen mensen uit "voor het geval dat". Als twee groepen gebruikers andere belangen hebben, houd dan twee workshops die zich elk focussen op die ene groep. Dat is beter te behappen dan een lange vergadering af te trappen waarin de helft van de groep zich de helft van de tijd verveelt, omdat het onderwerp voor hen niet interessant is.


Dat gezegd hebbende, natuurlijk verlies je informatie als je de groep klein en gefocust houdt. Wanneer je mensen met verschillende achtergronden bij elkaar zet, dan kan dat verrassende inzichten opleveren, die ze in hun eigen bubbel nooit zouden hebben opgedaan. De les is ook niet: zet nooit mensen uit diverse groepen bij elkaar. De les is: maak een bewuste afweging. Vraag je af: wat wil ik bereiken met deze discussie? - en selecteer de aanwezigen daar zorgvuldig op.


Je kunt mensen uit andere groepen ook op een andere manier bij een discussie betrekken. Maak de resultaten van een gefocuste workshop openbaar en vraag om commentaar en feedback. niet iedereen hoeft persoonlijk bij een meeting aanwezig te zijn om waardevolle input te kunnen leveren.


Welke vorm je ook kiest, tijdens sessies waarin je requirements verheldert, zullen er altijd conflicten ontstaan. Niet alle stakeholders hebben immers dezelfde belangen. Denk van tevoren na over hoe je die conflicten op gaat lossen. Wie heeft de volmacht om knopen door te hakken? Zorg ervoor dat alle aanwezigen akkoord zijn met het proces, om problemen achteraf te voorkomen.


Een goede facilitator vormt de sleutel tot een goede requirementsworkshop. Hij of zij houdt de discussie op het goede spoor. Dat wil zeggen: dat zowel de breedte (het aantal requirements) als de diepte (in hoeverre elke in detail wordt uitgewerkt) van de discussie binnen de perken blijft. Met name dat tweede wil nogal eens gebeuren wanneer je in gesprek bent met domeinexperts. Onthoud: het doel is om een gedeeld begrip te creëren dat het ontwikkelteam in staat stelt om een schatting te geven van de hoeveelheid werk, en te kunnen prioriteren. De details kunnen altijd later nog worden uitgewerkt, in bijvoorbeeld in individuele sessie.


Een goede facilitator zorgt ervoor dat iedereen in de groep wordt gehoord en zich ook gehoord voelt. Als iemand een suggestie doet die op dat moment niet relevant is, schrijf deze dan op. Geef aan dat jullie daar later nog op terug kunnen komen, en breng de discussie weer terug naar het onderwerp.


**XV.**


Prioriteer geen requirements op basis van wie het hardst schreeuwt - prioritering per decibel. Dat klinkt voor de hand liggend, maar blijkt in de praktijk vaak lastiger dan gedacht. Het is één van de vele redenen waarom ik blij dat ik geen PO ben.


Hoe belangrijk een stakeholder zijn of haar lievelingsfeature ook denkt te vinden, prioritering dient altijd plaats te vinden op basis van objectieve criteria. Denk aan: bedrijfsdoelen, de gebruikersdoelgroep, hoe vaak een feature gebruikt zal worden, het moeten voldoen aan bepaalde wetgeving, het leggen van een technische basis, en risico. Prioriteer op basis van een analyse waarin zulke factoren zijn opgenomen.


Verkoop nee aan luidruchtige stakeholders wier stokpaardjes op dit moment minder belangrijk zijn. Gebruik je analyse om uit te leggen waarom je tot die prioritering bent gekomen. En zorg dat je ook echt de volmacht hebt om die prioritering te bepalen.


**XVI.**


Veel softwareprojecten hebben last van [*scope creep*](https://en.wikipedia.org/wiki/Scope_creep). Vaak gebeurt dit omdat de scope van een project überhaupt niet is gedefinieerd. Zonder zo'n kader is het moeilijk om te beslissen of een nieuwe requirement binnen de scope valt of niet. Dit leidt tot frustratie en werkt prioritering per decibel in de hand. Zorg daarom altijd voor een expliciete formulering van de scope van een project, iteratie, increment of feature.


Maak aan de andere kant niet de fout om die initieel bepaalde scope in steen te beitelen. Het is nu eenmaal een feit des levens dat nieuwe requirements naar boven kunnen borrelen. Je oorspronkelijke analyse is nu eenmaal haast per definitie incompleet - gemaakt op basis van wat *op dat moment* bekend was. Een nieuwe requirement zou kunnen wijzen op een gat in die analyse. 


Het accepteren van een bepaalde hoeveelheid van verandering is goed, dat toont dat je leert. Maar wanneer het aantal veranderingen zich op blijft stapelen, dan toont dat dat de oorspronkelijke requirement onduidelijk was. Vage requirements zijn de belangrijkste bron van *scope creep*.


Wanneer een nieuwe requirement opborrelt, vraag je dan af: is het in scope? Er zijn drie mogelijke antwoorden:


1. Ja, de nieuwe requirement draagt bij aan ons huidige doel en moet worden toegevoegd aan de [Sprint Backlog](https://www.scrum.org/resources/what-is-a-sprint-backlog).

2. Nee, maar de nieuwe requirement past wel bij een ander doel en moet worden toegevoegd aan de [Product Backlog](https://www.scrum.org/resources/what-is-a-product-backlog), of dient geen enkel doel dat in scope is en moet in zijn geheel worden afgewezen.

3. Nee, maar het zou *eigenlijk* wel in scope moeten zijn.


In dat laatste geval pas je de scope aan. Maar pas op: als dit te vaak gebeurt, dan is dat een teken dat er meer aan de hand is. Dat betekent dat er ofwel een probleem bestaat met je manier van requirements aan het licht brengen, ofwel een probleem is met je prioritering.


## Meer in deze reeks


1. [Aantekeningen over requirements - deel 1] (LINK)

2. **Aantekeningen over requirements - deel 2**