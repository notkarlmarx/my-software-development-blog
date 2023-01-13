---
title: "Is pair programming minder efficiënt?"
author: "Karl van Heijster"
date: 2023-01-13T07:27:28+01:00
draft: false
comments: true
tags: ["code reviews", "efficiëntie", "pair programming"]
summary: "Mijn team worstelt een beetje met het vlot doorzetten van *pull requests*. Dus vertelde ik tijdens een borrel aan een collega uit een ander team van mijn voornemen vaker te *pair programmen*. Hij was geen fan."
---

Mijn team [worstelt een beetje met het vlot doorzetten van *pull requests* (PR's)](/blog/23/01/wel-code-reviews-geen-pull-requests/). Dus vertelde ik tijdens een borrel aan een collega uit een ander team van mijn voornemen vaker te *pair programmen*. 


Hij was geen fan.


"Stel," zei hij, "het kost me 40 uur om een stuk nieuwe functionaliteit te programmeren. Daarna kost het één uur voor een andere programmeur om die code te reviewen. Dan ben je in totaal 41 uur kwijt aan die feature. Als ik dat met *pair programming* op zou lossen, dan zouden we met z'n tweeën 40 uur aan die nieuwe functionaliteit programmeren - 80 uur dus - en besparen we ons daarna één uur aan codereviews. Het is veel minder efficiënt."


Dat is een interessante redenering, die ik ten gevolge van alle alcohol in mijn bloed op dat moment niet onderuit kon halen. Maar er valt volgens mij wel wat op af te dingen.


## Hoe lang?


Ten eerste: het is een aanname dat je met z'n tweeën even lang doet over het programmeren van een nieuwe feature als in je eentje. Het zou immers heel goed kunnen dat je een feature met z'n tweeën sneller afrondt dan in je eentje. Het is in theorie zelfs mogelijk dat je met z'n tweeën twee keer zo snel bent - 20 uur, 40 manuren; en in dat geval win je dat ene uurtje codereview.


Toegegeven, twee keer zo snel klinkt wel érg optimistisch. Maar het zou kunnen, bijvoorbeeld als één van beide programmeurs weet heeft van een open source *library* voor een probleem dat de ander handmatig zou hebben gelost.


Maar zelfs dan geef ik toe dat mijn optimisme niet gerechtvaardigd is. - Sterker nog, het omgekeerde zou ook het geval kunnen zijn: het zou zomaar kunnen dat *pair programming* lánger duurt dan in je eentje programmeren. Mijn punt is dit: het pessimisme van mijn collega is net zo ongerechtvaardigd. Het is een empirisch vraagstuk of *pair programming* ontwikkelaars in staat stelt sneller - in absolute uren, niet in manuren - features op te leveren.


## Hoe goed?


Ten tweede: het is een aanname dat de code die je met z'n tweeën schrijft van dezelfde kwaliteit is als de code die je in je eentje schrijft. En dat die aanname niet klopt, durf ik zonder empirisch onderzoek wel te stellen. Code die door één iemand is geschreven - in stilte, meestal - is over het algemeen minder expliciet doordacht dan code die door meer mensen tegelijkertijd is geschreven. Wie samenwerkt, móet immers zijn ontwerpkeuzes wel verantwoorden. Dit heeft gevolgen voor de korte en de lange termijn.


Voor de korte termijn geldt: eventuele problemen met de code worden pas ontdekt tijdens de codereview. Daarna volgt er extra werk. Nota bene: het argument van mijn collega gaat er stilzwijgend van uit dat er uit de traditionele codereview geen opmerkingen komen. Daarom kan hij zeggen: na 41 uur is deze feature afgerond. Maar na dat ene uur codereview zou er zomaar nog één, twee of tien uur aan werk uit kunnen komen. 


Voor de lange termijn geldt: sluimerende bugs of diepgravender ontwerpproblemen manifesteren zich pas later in de ontwikkelcyclus - hopelijk al tijdens het testen, en anders pas in productie. Ook hier komt extra werk uit. Dat werk zou ook opgeteld moeten worden bij de uren die het kost om de feature te implementeren. Het argument van mijn collega gaat er stilzwijgend van uit dat de feature na de codereview ook echt af is - klaar, voltooid, niks meer aan doen. Het is een empirisch vraagstuk of *pair programming* code met minder bugs oplevert of niet.


Nu zou je kunnen tegenwerping: *pair programming* garandeert niet per se dat er meer bugs in een vroeg stadium worden afgevangen. Als je twee slechte programmeurs bij elkaar zet, zullen ze samen buggy code schrijven. En dat klopt - maar dat klopt net zozeer voor de situatie waarin de ene slechte programmeur de buggy code van de andere slechte programmeur codereviewt. Het is dus geen argument tegen *pair programming* - het is wél een argument om zo min mogelijk slechte programmeurs in je team te willen hebben, waarvan akte.


## Hamvraag


De hamvraag is en blijft natuurlijk: is *pair programming* efficiënter dan *solo programming* gevolgd door een codereview - of niet? Het antwoord op die vraag heb ik niet, maar wie de moeite neemt om 'm te googlen, zal vast op een degelijke analyse stuiten. 


Persoonlijk vind ik dit een belangrijker vraag: levert *pair programming* meer waarde op dan *solo programming* gevolgd door een codereview - of niet? En hoewel ik geen degelijke analyse in mijn achterzak heb, neig ik 'm te willen beantwoorden met: ik vermoed van wel.


Eigenlijk weet ik aan het eind van deze blog maar één ding heel zeker: het argument van mijn collega is niet bijzonder overtuigend - maar de borrel was er des te leuker om.
