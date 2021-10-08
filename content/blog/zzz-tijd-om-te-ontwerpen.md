---
title: "Tijd om te ontwerpen"
author: "Karl van Heijster"
date: 2021-10-08T11:47:20+02:00
draft: true
comments: true
tags: []
summary: ""
---

Ik heb jarenlang als ontwikkelaar code kunnen kloppen zonder ooit maar één stroomdiagram te hoeven bekijken. Een grappig gegeven, want één van de eerste dingen die ik moest doen toen ik solliciteerde naar een traineeship als back end developer, was een cognitietaak waarbij ik steeds complexere stroomdiagrammen voor mijn neus kreeg. En om de indruk te wekken dat software ontwikkelen méér is dan alleen naar een scherm staren, moest ik dat doen in een ruimte behangen met foto's van lachende mensen die stroomdiagrammen op een whiteboard tekenen. 


De praktijk zag er anders uit: tekstuele beschrijvingen van features en een bak code waar je vervolgens zelf wijs uit mocht worden. Zeker als beginnend ontwikkelaar is dat een behoorlijke uitdaging. En hoewel mijn altijd geduldige collega's en de gestage toename van ervaring de pijn aanzienlijk verzachtten, bleef het af en toe sappelen om me door complexe codeproblemen heen te worstelen.


## Verademing


Totdat een collega een tijd terug een stroomdiagram tekende en ik uitriep: "Wat een verademing!" Het valt moeilijk te overschatten hoeveel je als ontwikkelaar hebt aan een visueel referentiepunt om je code aan te toetsen. (Uiteindelijk worstelde ik nog steeds met diverse complexe codeproblemen, maar dat meer te maken met de scope van mijn PBI dan met het diagram. Sterker nog, zonder diagram zou ik nu waarschijnlijk nog aan het worstelen zijn.)


Dat roept de vraag op: waarom doen we dit niet vaker? Trekken we met als softwareontwikkelaars niet eigenlijk veel te weinig tijd uit om onze oplossingen goed uit te denken én te tekenen, vóórdat we aan het coderen slaan?


## Tijd om te ontwerpen


Dit onderwerp kwam laatst naar boven tijdens een gesprek met mijn leidinggevende, en zijn antwoord op die laatste vraag was een volmondig "Ja!". Alle promotiefoto's ten spijt, het gemiddelde ontwikkelteam gaat niet voor een whiteboard staan om rechthoekjes met pijltjes aan elkaar te verbinden. Althans, mijn ervaring is dat niet. Dit is wat het gemiddelde ontwikkelteam doet: men begrijpt een probleem maar half, denkt op informele wijze een halfbakken oplossing uit en slaat aan het coderen.


Volgens mijn leidinggevende zou je 30 procent van een Sprint moeten besteden aan het ontwerpen van je oplossing. Waar hij dat getal vandaan haalde, geen idee, maar ik kan je verzekeren dat mijn team dat percentage niet haalt.


Dat wil zeggen: we halen dat percentage niet als we ontwerpen opvatten *als een van het coderen gescheiden bezigheid*. Want een oplossingsrichting wordt ontworpen, hoe dan ook, alleen in ons huidige ontwikkelstramien gebeurt dat tijdens de implementatie. De oplossing wordt ontworpen terwijl de code wordt geschreven.


## *Pantsen* en *plotten*


In [schrijversjargon](https://thewritepractice.com/plotters-pantsers/) heet dat *pantsen*: beginnen met schrijven en kijken waar je uitkomt. Het tegenovergestelde daarvan is *plotten*: op voorhand in grote lijnen uittekenen wat je wil vertellen en dit vervolgens uitschrijven.


Beide hebben zo hun eigen voor- en nadelen. Het voordeel van plotten is houvast. De structuur die je op voorhand hebt uitgedacht leidt als het ware je hand tijdens het schrijven. Het nadeel is dat een rigide plan creativiteit kan doodslaan. Dat is nu juist het voordeel van pantsen. Je bent vrij om te doen wat je wil, en dat kan tot onverwachte nieuwe inzichten leiden. Met het risico dat je doodlopende wegen inslaat, natuurlijk, dat is het nadeel.


Ik zal (en kan) geen uitspraken doen over de gehele ontwikkelpopulatie. Maar te oordelen aan het gebrek aan stroomdiagrammen, denk ik te mogen stellen dat mijn team en ik reflexief meer *pantser* zijn dan *plotter*. 


## Een plek, een tijd


Het is de vraag of we onszelf daarmee tekort doen. Want software ontwikkelen leent zich, anders dan creatief schrijven, eerder voor *plotten* dan voor *pantsen*. Het verschil tussen beide is namelijk dat de uitkomst bij de eerste op voorhand vastligt. Een auteur is vrij om een boek te schrijven over elk mogelijk onderwerp, maar een softwareontwikkelaar moet opleveren wat de klant vraagt.


Daarmee is niet gezegd dat er geen plek en tijd is voor *pantsen*. Soms is een gevraagde wijziging zo klein dat het onnodig is om een aparte ontwerpstap in te bouwen. En soms heeft een ontwikkelaar voldoende begrip van het probleem én de oplossing, dat deze met vertrouwen aan het coderen kan slaan. Maar vaak zijn wijzigingen aanzienlijk, en is het moeilijk om de architecturele implicaties van bepaalde beslissingen te overzien. 


In dat geval moeten er moeilijke keuzes worden gemaakt, keuzes waar het team als geheel iets van moet (willen) vinden.


...


Wat doe je in zo'n geval? In de praktijk gebeurt het nog te vaak dat de ontwikkelaar (ikzelf niet uitgezonderd!) op eigen houtje een oplossing bedenkt en implementeert. Met een steeds grotere berg technische schuld tot gevolg. Nu is mijn team redelijk bedreven in het [monitoren van technische schuld](/blog/21/09/hoe-technische-schuld-te-monitoren-en-prioriteren/), maar toch, ideaal is het niet.


Dit zou eigenlijk moeten gebeuren: de ontwikkelaar overziet de architecturele problemen van de wijziging en neemt afstand van zijn ontwikkelomgeving. Hij pakt er pen en papier bij (al dan niet digitaal) en begint een oplossing te tekenen. Als hij er redelijkerwijs op kan vertrouwen dat zijn oplossing duurzaam is, dan begint hij met coderen. Als hij twijfelt, klopt hij aan bij de rest van het team om zijn *ontwerp* te valideren.


(Een alternatief zou zijn: de ontwikkelaar roept het team bij elkaar om te brainstormen over de oplossingsrichting en slaat dán aan het tekenen.)


Waarom gebeurt dit niet? Eén van de redenen is dat ontwikkelaars het leuker vinden om te programmeren dan te tekenen. Ze schrijven liever code dan dat ze diep nadenken, en dus laten ze het nadenken maar zitten. Dit was de reden die mijn leidinggevende aandroeg als bron van het kwaad. En niet helemaal onterecht.


Een tweede reden zou kunnen zijn dat ontwikkelaars het gevoel hebben onproductief te zijn als ze geen code schrijven. Rationeel bezien weten ze misschien wel dat dat gevoel niet terecht is, maar toch is het moeilijk om van je af te schudden. Scrum dicteert immers dat er elke Sprint een potentieel uitleverbaar increment wordt opgeleverd, en daar is code voor nodig. 


Een derde reden zou kunnen zijn dat ontwikkelaars helemaal niet zo goed zijn in uit uittekenen van oplossingen. Als programmeurs zijn we de hele dag met code in de weer, dat is wat we goed kunnen. Stroomdiagrammen tekenen is, hoewel verwant aan coderen, een heel andere vaardigheid. En mensen zijn nu eenmaal geneigd om dingen uit de weg te gaan die ze niet zo goed kunnen. Ze besteden liever aandacht aan de dingen waar ze goed in zijn, want daardoor voelen ze zich competent.


Maar is een ontwikkelaar die nooit een stroomdiagram tekent wel echt competent in zijn vakgebied, code schrijven?


Waar het om gaat is: zo snel mogelijk valideren dat je op de goede weg zit. Dat kan aan het eind van je ontwikkelcyclus, bij de code review, maar het kan ook aan het begin. Maar dan moet je daar wel tijd voor vrijmaken.


Zeg, zo'n 30% van je Sprint.
