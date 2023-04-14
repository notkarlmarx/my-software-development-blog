---
title: "Wij van TDD-eend..."
author: "Karl van Heijster"
date: 2023-04-14T07:59:12+02:00
draft: false
comments: true
tags: ["pair programming", "requirements", "shift left", "software ontwikkelen", "testen", "test-driven development", "the zone"]
summary: "Het is waar: uit het feit dat er tests zijn, valt niet te concluderen dat het systeem functioneert zoals verwacht - preciezer: zoals de eindgebruiker verwacht. Er valt hooguit uit te concluderen dat het systeem functioneert zoals de schrijver van de tests verwachtte. En als de schrijver van de tests tevens de ontwikkelaar van de code is, dan vormen de tests niet meer dan een verslaglegging van de aannames die de ontwikkelaar had tijdens de implementatie. En tóch geloof ik dat TDD het probleem van mijn collega - mijn feature voldoet niet aan de (impliciete?) requirements - had kunnen verhelpen."
---

Mijn team kent een soort van *running gag*: iemand brengt een probleem naar voren, en ik zeg dan dat tests de oplossing vormen.


Laatst, bijvoorbeeld, sprak een collega tijdens onze retrospective zijn irritatie uit over een feature waar hij keer op keer op keer naar terugkeerde, omdat onze tester steeds maar weer een nieuwe bug vond. Terwijl hij zijn verhaal deed, plakte ik een afbeelding van de drie stadia van Test-Driven Development (TDD) naast zijn virtuele post-it: [*red-green-refactor*](/blog/22/03/agile-en-test-driven-development/).


## *Is* en *ought*


"Jaha," kreunde hij - en schoot prompt in de verdediging. TDD had geen zin, in dit geval, want *Wij van WC-eend*.


De reclameslogan zal eenieder bekend zijn:


{{<youtube id="YsvHeLUOoxs" title="Wij van WC-EEND adviseren... WC-EEND" >}}
<br/>


*"Wij van WC-eend adviseren... WC-eend!"* - Ja, nogal wiedes! De slager die zijn eigen vlees keurt zal, weinig verrassend, tot de conclusie komen dat 'ie topvlees in de aanbieding heeft. Net zo zal een ontwikkelaar die zijn eigen tests schrijft, tot de conclusie komen dat zijn code precies doet wat verwacht wordt.


Zo zit de wereld natuurlijk niet in elkaar. En dat komt omdat er een fundamenteel verschil is tussen dat was *is* en dat wat *zou moeten* - en de tweede valt, *dixit* [David Hume](https://plato.stanford.edu/entries/hume/) (1711-1776), [met geen mogelijkheid uit de eerste af te leiden](https://plato.stanford.edu/entries/hume-moral/#io). (Zie ook [deze blog](/blog/21/12/goede-code-documenteert-zichzelf-niet/).)


En het is waar: uit het feit dat er tests zijn, valt niet te concluderen dat het systeem functioneert zoals verwacht - preciezer: zoals de eindgebruiker verwacht. Er valt hooguit uit te concluderen dat het systeem functioneert zoals de schrijver van de tests verwachtte. En als de schrijver van de tests tevens de ontwikkelaar van de code is, dan vormen de tests niet meer dan een verslaglegging van de aannames die de ontwikkelaar had tijdens de implementatie.


## Expliciet


En tóch geloof ik dat TDD zijn probleem - mijn feature voldoet niet aan de (impliciete?) acceptatiecriteria of requirements - had kunnen verhelpen. 


Maar niet omdat TDD je op magische wijze achter de juiste requirements laat komen - helemaal niet. Er is altijd een kans - en misschien niet eens een kleine kans - dat je test niet precies het juiste gedrag beschrijft. Het hebben van tests *op zichzelf* is niet voldoende om correctheid te garanderen, dat hebben we net al geconcludeerd.


Maar wat die test wél doet, is expliciet maken wat volgens jou de juiste requirements zijn. De waarde daarvan valt moeilijk te overschatten. Want de aanname dat *dit* of *dat* is hoe het systeem zou moeten functioneren, maak je toch wel - dat heeft mijn collega ook gedaan zonder TDD, met al het *rework* van dien. 


Het voordeel van het schrijven van de test, is dat je de kans geeft om een moment afstand te nemen en je af te vragen: is dit inderdáád wat ik wil dat het systeem doet? - En waarop baseer ik mijn antwoord op die vraag? Heeft iemand - een analist, een eindgebruiker, de tester - me dat expliciet verteld, of maak ik hier een aanname?


## *Shift left*


Wanneer je geen bevredigend antwoord vindt op die vraag, is het tijd om hulp in te schakelen. TDD biedt een mooie kans om te *pair programmen*.


Hier is een gek idee: haak de tester aan. Laat 'm je nu nog incomplete set tests laten zien. "Nu doet de code zus en zo," zeg je, "maar over *dit* deel twijfel ik nog. Wat denk je, klopt deze test zo?"


Misschien wel, misschien niet - het punt is: je weet dat *nu*, en niet pas nádat je uren verder bent en de feature volledig hebt geïmplementeerd (of denkt te hebben geïmplementeerd). Het is een concreet voorbeeld van de [*shift left*](https://devopedia.org/shift-left)-gedachte: haal testen, kwaliteit en evaluatie naar voren in het ontwikkelproces. Hoe eerder je je aannames valideert, des te beter is de software die je schrijft.


## *The zone*


TDD is een manier om ervoor te zorgen dat je niet in [*the zone*](/blog/21/07/stoor-me-niet-ik-zit-in-the-zone/) raakt. Want zodra je daarin terecht komt, ga je aannames maken om in *the zone* te blijven. In plaats daarvan haalt TDD je constant uit de flow van implementatie - het oplossingsdomein - om je te dwingen je aannames expliciet te maken - en je aandacht te richten op het probleemdomein.


Een ontwikkelaar die als een razende test na test na test schrijft, zonder ooit stil te staan bij waar 'ie mee bezig is, doet inderdaad niet meer dan zijn aannames documenteren. Maar het is ontzettend moeilijk om als een razende te coderen wanneer je TDD't - en dat is niet per ongeluk.


Dus ja, TDD is wel degelijk een oplossing voor de frustrerende praktijk van continu *rework*. *Wij van TDD-eend adviseren... TDD-eend!*
