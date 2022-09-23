---
title: "De fix die productie om zeep hielp"
author: "Karl van Heijster"
date: 2022-09-23T10:49:15+02:00
draft: true
comments: true
tags: ["falen", "leermoment", "productieverstoring", "software ontwikkelen", "test-driven development", "testen", "verantwoordelijkheid"]
summary: "\"De fix staat op productie,\" meldden we trots. \"Het bleek te liggen aan wat validatielogica die in dit specifieke scenario wat te streng bleek - enfin, een technisch verhaal, dat hoef je niet te weten. Het enige wat je hoeft te weten is: we hebben weer eens geweldig werk geleverd, bedankjes worden gewaardeerd maar zijn niet noodzakelijk.\" En we leefden nog lang en gelukkig. Een halfuur lang. Want toen kregen we een berichtje: \"Help! Ik kan nu *geen enkel item* meer inzien!\""
---

Mijn team en ik, wij ontwikkelen geen software waar mensenlevens vanaf hangen. - Goddank! Want als het aan ons zou liggen, dan zouden er doden vallen.


Nee, de software die wij ontwikkelen heeft een iets bescheidener doel: het kunnen construeren van toetsen. Dat begint met het construeren van toetsvragen ([*items*](http://www.imsproject.org/spec/qti/v3p0/impl#h.77l136x98r3) in vakjargon, uitgesproken als: "ie-tem").


Onze gebruikers kunnen items construeren in een prachtige [WYSIWYG](https://nl.wikipedia.org/wiki/Wysiwyg)-editor. Meer nog: ze kunnen die items rondsturen naar hun collega's, die daar feedback op mogen geven.


## Een leeg scherm


Die editor en die feedbackfunctionaliteit werkt natuurlijk als een zonnetje - totdat 'ie niet meer werkt. Onlangs ontvingen we een bericht van een eindgebruiker: "Help! Als ik een item open, dan krijg ik een leeg scherm te zien!"


"Geen probleem," zeiden we. En daarna zeiden we: "Of ja, wel een probleem natuurlijk. Maar we bedoelen: we zitten er bovenop. We kijken ernaar. We gaan het fixen, geen zorgen."


"Ja, graag! Want we hebben over twee dagen een belangrijke vergadering, en als niemand zijn items kan openen, dan loopt het hele proces in de soep. Als in: dan halen we de deadline niet. Als in: dan hebben we een heleboel boze mensen aan de lijn." "Als in: dat is het eind van dit bedrijf?" "Nee. Maar veel scheelt het niet."


Enfin, er zat druk op, dat is wat ik bedoel te zeggen.


## De fix


De oorzaak van de bug bleek gelukkig vrij snel gevonden. Het probleem bleek te liggen bij items die rond waren gestuurd naar collega's en daarna weer terug waren genomen. We maakten een item aan, stuurde 'm naar onze testcollega's, namen 'm terug: en ja hoor, het werkte weer als een zonnetje.


We rolden uit naar de testomgeving, de acceptatieomgeving, en - huppa! - in één soepele beweging door naar de productieomgeving.


"De fix staat op productie," meldden we trots. "Het bleek te liggen aan wat validatielogica die in dit specifieke scenario wat te streng bleek - enfin, een technisch verhaal, dat hoef je niet te weten. Het enige wat je hoeft te weten is: we hebben weer eens geweldig werk geleverd, bedankjes worden gewaardeerd maar zijn niet noodzakelijk."


En we leefden nog lang en gelukkig.


## Foutmeldingen


Een halfuur lang. Want toen kregen we een berichtje: "Help! Ik kan nu *geen enkel item* meer inzien!"


Koortsachtig doken we opnieuw in de code. De foutmeldingen die we - wij nu ook! - terugkregen waren cryptisch: iets over items die niet bestonden. Maar als we in onze database keken, dan zagen we de items in kwestie daar toch echt wel staan! Wat was er in hemelsnaam aan de hand?


Na een hoop gedebug ging er een lichtje op bij een ontwikkelaar. De code werkte als je één item naar je collega's stuurde - maar wat als feedback vroeg op meerdere toetsvragen in één keer? - Daar had zijn fix geen rekening mee gehouden! En daar hadden hij en onze tester in hun handmatige tests geen rekening mee gehouden. Maar onze eindgebruikers, die deden niet anders!


Ik paste de validatiecode aan zodat deze opnieuw meerdere items aankon - en ik zette de boel ongetest door naar de testomgeving, want als rechtgeaarde softwareontwikkelaar heb ik een uiterst beperkte capaciteit om van fouten te leren.


Maar ik had geluk: mijn collega had gelijk, de bug in onze fix (onze "fix") zat op precies die plek. Onze tester zorgde er ditmaal wel voor dat hij daar zeker van was.


En we leefden nog enige tijd in relatieve onzekerheid, maar toen de fix eenmaal op productie was uitgerold en ook onze eindgebruikers weer items zagen, waren we best wel gelukkig.


## De tests


Ondertussen schreef ik een stuk of wat integratietests die het scenario in kwestie afdekten, opdat dit - althans: *deze* bug - nooit meer opnieuw voor zou komen.


Maar eigenlijk is dat precies verkeerd om, natuurlijk. Ik heb op deze blog regelmatig geschreven over [Test-Driven Development](/tags/test-driven-development/) (TDD) - en al die kennis ging het raam uit zodra onze eindgebruikers in paniek met hun handen begonnen te wapperen.


TDD wordt meestal besproken in de context van het ontwikkelen van nieuwe features - maar volgens mij is de praktijk *bij uitstek* geschikt voor het fixen van dit soort productieproblemen.


Ga maar na. We wisten wanneer het probleem optrad - wanneer je een item op probeerde te halen. We wisten onder welke omstandigheden het misging - wanneer deze naar collega's was rondgestuurd. En we wisten wat het verwachte gedrag was - *dat je gewoon je item kon zien!* 


We hadden respectievelijk de *Act*, *Arrange* en de *Assert* in handen. En toch fixten we de bug zonder ook maar één geautomatiseerde test te schrijven (sterker nog, in tweede instantie, drukte de boel door zonder zelfs maar een handmatige test uit te voeren!) - en hielpen we productie om zeep. Kortstondig misschien, zeker, maar gedurende een uur konden onze gebruikers helemaal niks meer.


Ik heb in [een eerdere blog] (LINK) [Robert Martin](http://cleancoder.com/products) geciteerd, die stelt dat TDD een voorwaarde is voor professionaliteit in dit vak. Nou, laat ik me voorzichtig uitdrukken: het optreden van mijn team - en mij in het bijzonder - had zeker professioneler gekund.


## De les


De les van dit verhaal is er één die de meeste ontwikkelaars volgens mij wel kennen - maar waar maar zelden naar geleefd wordt: als je een bug fixt, zorg dan dat je een test hebt die die fix valideert. - Nee, zorg dat je méérdere tests hebt die die fix valideren.


De crux is natuurlijk: heel veel meer moeite dan handmatig testen is het niet. In beide gevallen doe je hetzelfde - in het ene geval met muisklikken, en in het andere geval met code. 


Het voordeel van de codemanier is niet alleen dat je een specifiek scenario nu voor eens en voor altijd aftest. Het in dit geval nog veel relevanter voordeel is dat het opschrijven van wat je doet je dwingt om na te denken over de scenario's die je *niet* test.


Hadden we productie niet om zeep geholpen was we deze bug met tests gevalideerd hadden? Laten we hopen erachter te komen, de volgende keer als een eindgebruiker twee dagen voor een belangrijke vergadering in paniek bij ons aanklopt!
