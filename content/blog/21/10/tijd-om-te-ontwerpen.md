---
title: "Tijd om te ontwerpen"
author: "Karl van Heijster"
date: 2021-10-29T08:06:11+02:00
draft: false
comments: true
tags: ["diagrammen", "documentatie", "productiviteit", "software ontwikkelen", "waarde"]
summary: "Ik heb jarenlang als ontwikkelaar code kunnen kloppen zonder ooit maar één stroomdiagram te hoeven bekijken. Een grappig gegeven, want één van de eerste dingen die ik moest doen toen ik solliciteerde naar een traineeship als back end developer, was een cognitietaak waarbij ik steeds complexere stroomdiagrammen voor mijn neus kreeg. En om de indruk te wekken dat software ontwikkelen méér is dan alleen naar een scherm staren, moest ik dat doen in een ruimte behangen met foto's van mensen die lachend naar whiteboards staan te wijzen. "
---

Ik heb jarenlang als ontwikkelaar code kunnen kloppen zonder ooit maar één stroomdiagram te hoeven bekijken. Een grappig gegeven, want één van de eerste dingen die ik moest doen toen ik solliciteerde naar een traineeship als back end developer, was een cognitietaak waarbij ik steeds complexere stroomdiagrammen voor mijn neus kreeg. En om de indruk te wekken dat software ontwikkelen méér is dan alleen naar een scherm staren, moest ik dat doen in een ruimte behangen met foto's van mensen die lachend naar whiteboards staan te wijzen. 


De praktijk zag er anders uit: tekstuele beschrijvingen van features en een bak code waar je vervolgens zelf wijs uit mocht worden. Zeker als beginnend ontwikkelaar is dat een behoorlijke uitdaging. En hoewel mijn altijd geduldige collega's en de gestage toename van ervaring de pijn aanzienlijk verzachtten, bleef het af en toe sappelen om me door complexe codeproblemen heen te worstelen.


## Verademing


Totdat een collega een tijd terug een stroomdiagram tekende en ik uitriep: "Wat een verademing!" Het valt moeilijk te overschatten hoeveel je als ontwikkelaar hebt aan een visueel referentiepunt om je code aan te toetsen. (Uiteindelijk worstelde ik nog steeds met diverse complexe codeproblemen, maar dat meer te maken met de scope van mijn PBI dan met het diagram. Sterker nog, zonder diagram zou ik nu waarschijnlijk nog aan het worstelen zijn.)


Dat roept de vraag op: waarom doen we dit niet vaker, stroom- of architectuurdiagrammetjes tekenen? Trekken we als softwareontwikkelaars niet eigenlijk veel te weinig tijd uit om onze oplossingen goed uit te werken, vóórdat we aan het coderen slaan?


## Tijd om te ontwerpen


Dit onderwerp kwam laatst naar boven tijdens een gesprek met mijn leidinggevende, en zijn antwoord op die laatste vraag was een volmondig "Ja!". Alle promotiefoto's ten spijt, het gemiddelde ontwikkelteam gaat niet voor een whiteboard staan om rechthoekjes met pijltjes aan elkaar te verbinden. Althans, mijn ervaring is dat niet. Dit is wat het gemiddelde ontwikkelteam doet: men hoort een probleem aan, kiest op informele wijze een oplossingsrichting uit en slaat aan het coderen.


Volgens mijn leidinggevende zou je 30 procent van een Sprint moeten besteden aan het ontwerpen van je oplossing. Waar hij dat getal vandaan haalde, geen idee, maar ik kan je verzekeren dat mijn team dat percentage niet haalt.


Dat wil zeggen: we halen dat percentage niet als we ontwerpen opvatten *als een van het coderen gescheiden bezigheid*. Want een oplossingsrichting wordt ontworpen, hoe dan ook, alleen in ons huidige ontwikkelstramien gebeurt dat te vaak nog tijdens de implementatie. De oplossing wordt ontworpen terwijl de code wordt geschreven.


## *Pantsen* en *plotten*


In [schrijversjargon](https://thewritepractice.com/plotters-pantsers/) heet dat *pantsen*: beginnen met schrijven en kijken waar je uitkomt. Het tegenovergestelde daarvan is *plotten*: op voorhand in grote lijnen uittekenen wat je wil vertellen en dit vervolgens inkleuren.


Beide hebben zo hun eigen voor- en nadelen. Het voordeel van plotten is houvast. De structuur die je op voorhand hebt uitgedacht leidt als het ware je hand tijdens het schrijven. Het nadeel is dat een rigide plan creativiteit kan doodslaan. Dat is nu juist het voordeel van pantsen. Je bent vrij om te doen wat je wil, en dat kan tot onverwachte nieuwe inzichten leiden. Met het risico dat je doodlopende wegen inslaat, natuurlijk, dat is het nadeel.


Ik zal (en kan) geen uitspraken doen over de gehele ontwikkelpopulatie. Maar te oordelen aan het gebrek aan diagrammen, denk ik te mogen stellen dat mijn team en ik reflexief meer naar *pantsen* neigen dan naar *plotten*. 


## Een plek, een tijd


Doen we onszelf daarmee tekort? Het ontwikkelen van software leent zich, anders dan creatief schrijven, eerder voor *plotten* dan voor *pantsen*. Het verschil tussen beide is namelijk dat de uitkomst bij de eerste op voorhand vastligt. Een auteur is vrij om een boek te schrijven over elk mogelijk onderwerp, maar een softwareontwikkelaar moet opleveren wat de klantbehoefte het best bevredigt.


Daarmee is niet gezegd dat er geen plek en tijd is voor *pantsen*. Soms is een gevraagde wijziging zo klein dat het onnodig is om een aparte ontwerpstap in te bouwen. En soms heeft een ontwikkelaar voldoende begrip van het probleem én de oplossing, dat deze met vertrouwen aan het coderen kan slaan. 


Maar vaak zijn wijzigingen aanzienlijk en is het moeilijk om zonder hulpmiddelen de architecturele implicaties van bepaalde beslissingen te overzien. In dat geval moeten er moeilijke keuzes worden gemaakt, keuzes waar het team als geheel iets van moet (willen) vinden. Dat is eigenlijk het moment om aan het tekenen te slaan.


## Obstakels


Waarom gebeurt dit niet? Eén van de redenen is dat ontwikkelaars het leuker vinden om te programmeren dan te tekenen. Ze schrijven liever code, en dus laten ze het ontwerpen maar zitten. Dit was de reden die mijn leidinggevende aandroeg als bron van het kwaad. En ergens herken ik mezelf en mijn omgeving wel in die karakterisering, dus zijn analyse is niet helemaal onterecht.


(Maar de werkelijkheid is denk ik toch iets complexer dan dat. Veel ontwikkelaars zijn zo bedreven in het schrijven van code dat ze nadenken over het ontwerp *door* te coderen. Het is echter de vraag of dit de efficiëntste manier is om tot een goede oplossing te komen.)


Een tweede reden zou kunnen zijn dat ontwikkelaars het gevoel hebben onproductief te zijn als ze geen code schrijven. Rationeel bezien weten ze misschien wel dat dat gevoel niet terecht is, maar toch is het moeilijk om van je af te schudden. Scrum dicteert immers dat er elke Sprint een [potentieel uitleverbaar increment](https://www.scruminc.com/potentially-shippable-product/) wordt opgeleverd, en daar is code voor nodig. 


Een derde reden zou kunnen zijn dat ontwikkelaars helemaal niet zo goed zijn in uit uittekenen van oplossingen. Als programmeurs zijn we de hele dag met code in de weer, dat is wat we goed kunnen. Architectuur- en stroomdiagrammen tekenen is, hoewel verwant aan coderen, een heel andere vaardigheid. En mensen zijn nu eenmaal geneigd om dingen uit de weg te gaan die ze niet zo goed kunnen. Ze besteden liever aandacht aan de dingen waar ze goed in zijn, want daardoor voelen ze zich competent.


Maar je kunt je afvragen: is een ontwikkelaar die nooit een diagram tekent wel echt competent in zijn vakgebied, code schrijven?


## Valideren


Het is niet onterecht om te stellen dat mijn team en ik nog genoeg groeimogelijkheden hebben als het gaat om het ontwerpen van oplossingen, los van de implementatie. Gelukkig voelen we dit op onze klompen aan, en zijn er stappen gezet om hier meer tijd voor vrij te maken. 


Want alle obstakels ten spijt, is het voor iedereen zonneklaar dat je een ontwerp beter aan het begin van een ontwikkelcyclus kunt valideren dan aan het eind. Wie weet, misschien presenteren we binnenkort wel stroomdiagrammen aan elkaar zonder dat iemand uit hoeft te roepen: "Wat een verademing!" 
