---
title: "De Architect, Het Team en De Business"
date: 2021-05-24T11:33:22+02:00
draft: false
comments: true
tags: ["agile ontwikkeling", "empathie", "samenwerking", "software architect (rol)", "software ontwikkeling"]
summary: "Ik vind dat een softwarearchitect mee moet draaien in een ontwikkelteam. Mijn leiddingevende is daar minder van overtuigd. 'Vind je dan ook dat een architect mee moet draaien met de business?' vroeg hij me tijdens een discussie - retorisch uiteraard. Maar toen ik erover nadacht, vroeg ik me af: waarom eigenlijk niet?"
---

Ik vind dat een architect mee moet draaien in een ontwikkelteam. Of liever: ik vond dat een architect mee moest draaien in een Scrumteam, [totdat ik erachter kwam dat er andere invullingen van de rol van architect bestonden dan als architect-ontwikkelaar](blog/21-05-10-wat-wil-je-zijn-een-architect-of-een-ontwikkelaar). 


## Waarom een architect moet programmeren


Toch vind ik dat er nog steeds goede redenen zijn voor een architect om zijn handen vuil te maken de concrete implementatie van zijn ontwerp. 


Ten eerste stelt het de architect in staat om de implementatie van zijn ontwerp te monitoren. Door dicht op de code te blijven zitten, zal hij er snel achter komen waar ontwerp en implementatie uiteen beginnen te lopen. 


Een architect die nooit codeert, loopt het risico pas in een laat stadium op te merken dat het team zijn ontwerp niet volgt. En, belangrijker nog: *waarom* het team dat ontwerp niet volgt!


Ten tweede, en daaraan gerelateerd, is coderen de snelste manier voor een architect om erachter te komen waar de pijnpunten in zijn ontwerp zitten. Een architect die op papier fantastische ontwerpen maakt die in de praktijk niet werken, is een waardeloze architect. 


Natuurlijk, een goed functionerend team zal pijnpunten terugkoppelen, of de architect nu onderdeel van het team is of niet. Maar er gaat niets boven *hands on*-ervaring. Een architect die nooit codeert, loopt het risico de fouten in zijn ontwerp te wijten aan (een gebrek aan) de vaardigheden van het implementerende team. 


Ten derde verbetert coderen de vertrouwensrelatie tussen de architect en het team. Hoe dichter de architect bij het team staat, hoe sneller de twee kunnen schakelen om problemen in zijn ontwerp te agenderen en te verhelpen.


## ...of toch niet?


Dit zijn allemaal punten die ik naar voren bracht gedurende een bijna twee uur durende discussie met mijn leidinggevende over softwareontwikkeling en de rol van de architect daarin. 


Helemaal overtuigd was hij niet. Naar zijn idee is een architect iets anders dan (of misschien beter: niet per se hetzelfde als) een ontwikkelaar. Daaruit volgt dat een architect ook andere verantwoordelijkheden heeft. 


Een architect levert architectuurdiagrammen op en schrijft *proofs of concept*. Hij maakt het team bewust van hun rol en verantwoordelijkheid in het herkennen van architecturele problemen in de code. En die lost hij op, in samenspraak met het team. In principe kan hij al die dingen zonder ook maar één regel productiecode te hoeven schrijven.


De architect van een huis, merkte mijn leidinggevende op, houdt zich immers ook niet bezig met het leggen van bakstenen.


## Samenwerken


Helemaal overtuigd was ik niet. De vergelijking tussen een ~~echte~~ architect en een softwarearchitect loopt mank. Een architect is in staat om een huis volledig uit te tekenen vóórdat er ook maar één bouwvakker aan de slag gaat. Een softwarearchitect heeft die luxe niet. 


De agile beweging is juist opgekomen in reactie op de misvatting dat een softwareapplicatie volledig op voorhand kan worden uitgetekend.


Die misleidende vergelijking is de reden waarom Eben Hewitt in [*Semantic Software Design*](https://www.oreilly.com/library/view/semantic-software-design/9781492045946/) liever spreekt van *softwaredesigners* dan van *softwarearchitecten*. Het is een metafoor die minder nadruk legt op de technische aspecten van softwarearchitectuur, en meer op de creatieve.


Een andere vergelijking die Hewitt voorstelt, is die met een filmregisseur. Een goede regisseur steekt voordat de opnamen beginnen veel tijd in het voorbereiden van elke scène. De *story boards* die hij maakt zou je kunnen zien als zijn architectuurdiagrammen. Maar het is onvoorstelbaar dat een filmregisseur op de dag zelf niet op de set aanwezig is, omdat er toch al opgetekend is hoe de scène er uiteindelijk uit moet komen te zien.


Welke vergelijking je ook kiest, feit is dat een ontwikkelteam en een architect zijn samen verantwoordelijk voor het uiteindelijk op te leveren product. Meedraaien met het team is een efficiënte manier om die samenwerking invulling te geven, om de redenen die ik hierboven heb genoemd.


## En de business dan?


Maar een architect moet niet alleen met het ontwikkelteam samenwerken, wierp mijn leidinggevende tegen. Toen stelde hij een heel interessante vraag: "Vind je dan ook dat een architect met de business mee moet draaien?" 


Mijn antwoord destijds was: ook die vergelijking loopt mank. De aard van de samenwerking is niet hetzelfde. De architect werkt met de business samen om hun wensen en behoeften in kaart te brengen en hun problemen op te lossen. De architect werkt met het team samen om die oplossing te realiseren.


Ik sta nog steeds achter dat antwoord, maar de conclusie die ik eraan verbind is niet dezelfde. Aanvankelijk meende ik dat daaruit volgde dat de architect wel met het team mee moest draaien, maar niet met de business. 


## Waarom niet?


Maar nadat onze discussie was bezonken, vroeg ik me af: waarom zou je eigenlijk *niet* met de business meedraaien? Een dagje meelopen met de mensen op de werkvloer is misschien wel de snelste manier om in kaart te brengen waar ze in hun dagelijkse werkzaamheden behoefte aan hebben.


En de argumenten lopen ruwweg parallel aan degene die ik hierboven heb genoemd. Ten eerste stelt het de architect in staat te monitoren of de bedachte oplossing wordt gebruikt zoals bedoeld. Ten tweede stelt het hem in staat te ervaren hoe goed zijn oplossing aansluit op het businessprobleem. En ten derde vergroot het de vertrouwensrelatie tussen de architect en de klant. 


Sterker nog, waarom ophouden bij een architect? Waarom lopen we als ontwikkelaars eens in de zoveel tijd niet standaard een dagje mee met de gebruikers van onze software? Misschien hebben ontwikkelaars nog wel meer profijt van deze aanpak, want de meest urgente (maar niet per se belangrijkste) problemen die gebruikers hebben met een applicatie bevinden zich vaak juist in de details.


Ik kan me geen snellere (en meer confronterende) manier indenken om in te zien waar onze software te verbeteren valt en om empathie te krijgen voor onze eindgebruikers. 


Want er zit een gat tussen het implementeren van *user stories* aan de hand van acceptatiecriteria en het daadwerkelijk gebruiken van software. Vaak genoeg heb ik meegemaakt dat een feature die op papier goed werkte, in de praktijk schuurde. Alleen kwamen we daar als team pas maanden, soms zelfs jaren na de implementatie van die functionaliteit achter.


Als we aannemen dat één van de doelen van agile ontwikkeling het wegnemen van de barrières tussen IT en de business, waarom zou een architect of ontwikkelaar dan *niet* meelopen met de business?
