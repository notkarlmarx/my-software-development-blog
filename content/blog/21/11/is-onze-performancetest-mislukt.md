---
title: "Is onze performancetest mislukt?"
author: "Karl van Heijster"
date: 2021-11-15T07:41:17+01:00
draft: false
comments: true
tags: ["leermoment", "performance", "procesverbetering", "software ontwikkelen", "testen"]
summary: "Het doel van de performancetest was niet om aan te tonen dat onze applicatie de load aankon. Het doel was om *erachter te komen* of onze applicatie de load aankon. Nu weten we het antwoord: nee. Men zegt niet voor niets: *meten is weten*, en niet: *meten is slagen*."
---

We hebben onze applicatie onlangs geperformancetest. Het was een hele happening.


Op dit moment - we zitten nog altijd in iets wat je een pilot-fase zou kunnen noemen - ondersteunen we nog maar een handvol gebruikers. Maar onze applicatie is bedoeld om een dertien jaar oude *legacy*-applicatie te vervangen, dus het blijft niet bij dat aantal. Bovendien komt er nog een lieve dot externe gebruikers bij, doordat het systeem vanuit een andere invalshoek is opgezet dan die *legacy*-applicatie.


Of we dat eigenlijk wel aankunnen? Nou, daar is die performancetest dus voor.


## Opzet


We hadden onszelf het volgende doel gesteld: de applicatie moet 600 gelijktijdige gebruikers aankunnen zonder vertraging. Om een productie-omgeving te simuleren, hebben we de databases van onze acceptatie-omgeving volgepomp met zo'n 250.000 objecten. Daarna lieten we, via een externe partij, een paar honderd gebruikers op onze applicatie los.


Tijdens het vullen van de databases merkten we al dat bepaalde functionaliteiten tot bottlenecks leidden. Dat was zowel goed als slecht nieuws. Goed, omdat we daar tijdig actie op konden ondernemen door die functionaliteiten vóór de test de verwijderen. Slecht, omdat er al vertraging optrad bij één gebruiker, laat staan bij 600!


## Uitkomst


Mijn vrouw en ik waren jarig toen de performancetest werd uitgevoerd, dus we sliepen die dag uit. De gang van zaken heb ik uit de tweede hand. 


Honderd gelijktijdige gebruikers kon onze applicatie prima aan, bij 130 begon 'ie te haperen. Mijn collega's hebben zich in de rondte geprogrammeerd om de performance nog op te krikken. Ze hebben als een bezetene foutmeldingen lopen duiden, limieten in [Azure](https://azure.microsoft.com/nl-nl/) omhoog gegooid en lopen schelden op teruglopende grafieken.


Bij 300 gelijktijdige gebruikers was het feestje voorbij. - 300, dat is dus de helft van de door ons beoogde 600. Is dat een teleurstellend resultaat? Mja. Een deel van mijn collega's baalde er enorm van. "De test is mislukt," concludeerden ze mistroostig.


Zelf zag ik dat toch anders. 


## Realistisch


Ten eerste: was het realistisch om ons doel op 600 gelijktijdige gebruikers te zetten? Ik heb daar mijn twijfels bij. Toen we [de resultaten presenteerden tijdens de Sprint Review](/blog/21/11/slecht-nieuws-en-sprint-reviews/), zei mijn leidinggevende: "600 *gelijktijdige* gebruikers? Dat zou heel indrukwekkend zijn, als jullie applicatie dat zou halen." 


Hij lichtte toe voor de minder technisch onderlegde stakeholders: "Je moet dat niet lezen alsof er op dat moment 600 mensen het systeem tegelijkertijd gebruiken. Je moet dat lezen alsof 600 mensen op precies dezelfde seconde inloggen. Het is eerder alsof er 6000 mensen tegelijkertijd in het systeem werken."


Er zijn, voor zover ik weet althans, geen plannen om 6000 gebruikers op onze applicatie aan te sluiten. Voorlopig zitten we dus nog wel even goed.


## Meten is weten


Belangrijker nog, en dit is het tweede punt: een meting die resultaten oplevert *kan niet mislukken*. Natuurlijk, de resultaten kunnen tegenvallen ten opzichte van wat je gehoopt had. Maar het doel van een meting is om inzicht te geven in het feitelijk gedrag, niet om de gestelde doelen te halen.[^1]


Anders gezegd: het doel van de performancetest was niet om aan te tonen dat onze applicatie de load aankon. Het doel was om *erachter te komen* of onze applicatie de load aankon. Nu weten we het antwoord: nee. Men zegt niet voor niets: *meten is weten*, en niet: *meten is slagen*.


## Inzicht


Maar belangrijker dan dat antwoord, is het inzicht dat deze test ons verschaft in de pijnpunten in onze applicatie. Op een gegeven moment begon de applicatie foutmeldingen op te gooien die verband houden met de door ons gebruikte [NoSQL-database](https://nl.wikipedia.org/wiki/NoSQL), [RavenDB](https://ravendb.net/). Tegelijkertijd zagen we dat de database op zichzelf niet enorm hard stond te draaien. Blijkbaar is de manier waarop we naar deze database query'en bepaald niet optimaal.


De performancetest heeft het team inzicht verschaft in de manier waarop de applicatie werkt. Een inzicht, bovendien, dat we nooit hadden kunnen verkrijgen op onze developerlaptops, waar de database slechts een handvol objecten kent en er één gebruiker is. 


## Onderzoeksproject


De test heeft zo de weg vrij gemaakt voor een nieuw onderzoeksproject: als je de performance op wil krikken, kijk dan *daar*. Het komende [Team Alignment](/blog/21/09/hoe-technische-schuld-te-monitoren-en-prioriteren/) hebben we wat code om kritisch tegen het licht te houden. We zullen [PBI's moeten aanmaken](/blog/21/06/schrijf-pbis-en-doe-het-goed/) om de pijnpunten die uit de performancetest naar voren kwamen systematisch aan te pakken.


Tegelijkertijd kunnen de resultaten van de afgelopen test fungeren als *baseline* om te valideren of onze wijzigingen daadwerkelijk de performance verbeteren. Dat geldt voor wijzigingen die direct voortkomen uit (analyses naar aanleiding van) deze performancetest, maar ook voor nieuwe functionaliteit. De meting stelt ons in staat om te beoordelen of we vóór of achteruit gaan, en biedt daarmee duurzaam waarde.


De enige mislukte test, is een test waar je niets van leert. Is onze performancetest mislukt? Allesbehalve. 


[^1]: Om dezelfde reden kan een Sprint in Scrum nooit mislukken. Als de beoogde *velocity* niet wordt gehaald, dan is dat jammer - zeker! - voor de gebruiker. Maar vanuit het oogpunt van de Product Owner is er winst geboekt: er is een nieuw en beter inzicht gekomen in de snelheid van het team.
