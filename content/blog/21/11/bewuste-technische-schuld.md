---
title: "Bewuste technische schuld"
author: "Karl van Heijster"
date: 2021-11-22T07:50:11+01:00
draft: false
comments: true
tags: ["agile ontwikkeling", "communicatie", "incrementele ontwikkeling", "iteratieve ontwikkeling", "professionaliteit", "software ontwikkelaar (rol)", "stakeholders", "technische schuld", "waarde"]
summary: "Is technische schuld erg? Niet per se, zolang de keuze voor technische schuld maar een *bewuste* is. Als het team duidelijk maakt dat de oplossingsrichting technische schuld met zich meebrengt *en afdwingt dat er op middellange termijn tijd wordt vrijgemaakt om die op te ruimen*, hoeft die schuld geen probleem op te leveren. Integendeel: dankzij die schuld zijn we in staat om op korte termijn - vóór de deadline - waarde te leveren."
---

Ik heb geen idee hoeveel zekerheden er bestaan in het leven van een softwareontwikkelaar, maar één ervan is: je zult technische schuld opbouwen. De vraag is of dat erg is. Het antwoord daarop is: *it depends*.


Mijn team is op dit moment bezig met het ondersteunen van een nieuwe gebruikersgroep in onze applicatie. Deze groep heeft bepaalde functionaliteit nodig die nog niet voorhanden is - en ze hebben een deadline. We hebben twee opties: (1) we zeggen dat we de gewenste functionaliteit niet kunnen leveren en dat ze later aan kunnen sluiten, of (2) we laten hen nu aansluiten maar met een nog incomplete versie van de gewenste functionaliteit.


## Voordelen, nadelen


Beide opties hebben natuurlijk hun voor- en nadelen. Het voordeel van (1) is dat het het team de tijd geeft om de gewenste functionaliteit te ontwerpen en implementeren volgens de architectuurprincipes die we onszelf gesteld hebben. Het voordeel van (2) is dat de gebruikers onmiddellijk aan de slag kunnen. Dat is een voordeel zowel voor de gebruikersgroep als voor de ontwikkelaars. Het team kan immers leren van de ervaringen van de gebruikers en dit als input gebruiken voor een tweede, derde of vierde versie van de functionaliteit.


De indruk bestaat misschien dat (2) functionele schuld opbouwt, maar dat is niet waar. Althans, het is niet waar dat *alleen* (2) functionele schuld opbouwt. Bij beide opties bouwen we functionele schuld op, maar alleen in het tweede geval is die schuld expliciet. Het is niet per se zo dat we in geval van (1) precies zouden leveren waar de gebruikersgroep behoefte aan heeft. We kunnen alleen maar hard maken dat we zouden opleveren waar we *op dit moment* denken dat ze behoefte aan hebben. Dit is nog zo'n zekerheid: naarmate de tijd verstrijkt, zal de feature zoals bedacht altijd onvolledig blijken.


## Technische schuld


Het verschil tussen de eerste en de tweede optie zit 'm daarom niet zozeer in de functionele schuld, maar in de technische schuld. Zoals gezegd, (1) geeft het team de tijd om een goed uitgewerkte oplossingsrichting te presenteren. (2) bestaat uit een oplossing waarvan we nu al weten dat die op middellange termijn aanpassing vereist.


Welnu, is dat erg? Niet per se, zolang de keuze voor technische schuld maar een *bewuste* is. Als het team duidelijk maakt dat de oplossingsrichting technische schuld met zich meebrengt *en afdwingt dat er op middellange termijn tijd wordt vrijgemaakt om die op te ruimen*, hoeft die schuld geen probleem op te leveren. Integendeel: dankzij die schuld zijn we in staat om op korte termijn - vóór de deadline - waarde te leveren.


Een team dat deze werkwijze serieus neemt, doet aan wat ik in een voorgaande blog heb omschreven als [incrementieve ontwikkeling](/blog/21/07/incrementele-versus-iteratieve-ontwikkeling/). Dat wil zeggen: nu iteratief werken om snel waarde te kunnen leveren, daarna overschakelen naar een incrementele werkwijze om de applicatie op te schonen.


## Uitdaging


Maar die werkwijze vereist wel een discipline, namelijk de discipline om de rommel die je tijdens dat proces hebt gemaakt ook echt op te ruimen. Dit is waar het vaak misgaat bij het ontwikkelen van software. Stakeholders denken - niet helemaal ten onrechte - dat nieuwe functionaliteiten in rap tempo kunnen worden opgeleverd. Maar ze hebben geen oog voor de effecten van die snelheid, die blijven buiten hun zicht. Ze raken gefrustreerd met het ontwikkelteam, dat, bang om teleur te stellen, genoegen gaat nemen met het introduceren van steeds meer technische schuld.


In dat geval glijdt de keuze voor die schuld steeds meer in het gebied van het onbewuste. Totdat de schuld de ontwikkelaars boven het hoofd is gegroeid.


Stakeholders meenemen in de afwegingen van bepaalde oplossingsrichtingen is één van de vele uitdagingen waar een softwareontwikkelaar voor staat. Het is een kwestie, ten eerste, van communicatie: de stakeholder meenemen in het softwareontwikkelproces en eerlijk zijn over de voor- en nadelen van je keuzes. Daarnaast is het een kwestie van professionaliteit: staan achter de code die je oplevert en het dus ook niet accepteren wanneer stakeholders je proberen te verleiden ondermaatse code op te leveren.
