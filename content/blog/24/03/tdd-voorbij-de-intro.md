---
title: "TDD voorbij de intro"
author: "Karl van Heijster"
date: 2024-03-08T08:22:55+01:00
draft: false
comments: true
tags: ["filosofie", "test-driven development"]
summary: "Vandaag laat ik liever even iemand anders aan het woord. -- Hoewel, \"even\"? Romeu Moura neemt in de onderstaande twee video's uit-ge-breid de tijd om zijn toehoorders kennis te laten maken met zijn test-gedreven ontwikkelproces. In niets ontziend detail neemt hij elke beslissing onder de loep en analyseert hij, reflecteert -- op het proces net zozeer als op zichzelf."
---

Vandaag laat ik liever even iemand anders aan het woord. -- Hoewel, "even"? [Romeu Moura](https://www.linkedin.com/in/romeu/) neemt in de onderstaande twee video's uit-ge-breid de tijd om zijn toehoorders kennis te laten maken met zijn test-gedreven ontwikkelproces. In niets ontziend detail neemt hij elke beslissing onder de loep en analyseert hij, reflecteert -- op het proces net zozeer als op zichzelf. 


Ik had 't Moura niet kwalijk genomen als 'ie z'n praatje *The Fenomenology of TDD* had genoemd. Of [*Discourse de la Méthode de TDD*](https://plato.stanford.edu/entries/descartes-method/). Of [*Sein und Test*](https://plato.stanford.edu/entries/heidegger/#BeiTim). Of [*Phänomenologische Untersuchungen, Erster Teil: Prolegomena zur reinen TDD*](https://plato.stanford.edu/entries/husserl/).


## Verdiepen


Wat ik bedoel te zeggen is: onderstaand is leuk voor als je 'n keertje een uurtje over hebt en je je kennis van [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) wil verdiepen (-- *verdiepen* inderdaad; dit is geen praatje voor wie nieuwe TDD'ers!).


{{<youtube id="kDfuP88hVgU" title="TDD: Beyond the intro, part one - Romeu Moura - DDD Europe 2023" >}}
<br>


Het bovenstaande uur zit vol met praktische tips als "formuleer voordat je begint met het schrijven van tests een ruwe versie van je begrip van het probleem in commentaar; dit biedt een *road map* voor wat je wil bereiken", "besteed op voorhand niet teveel aandacht aan de naam van je test; de kans is aanzienlijk dat je de test weggooit of aanpast" en "houd de geteste code aanvankelijk in dezelfde file als je tests; de vraag waar de code hoort te staan is een andere dan de vraag naar het gedrag van de code."


## Inzicht


Maar mijn favoriete inzicht komt naar voren in het tweede deel, waarin Moura TDD vanuit een filosofische lens benadert:


{{<youtube id="QVpu19o6TsU" title="TDD: Beyond the intro, part two - Romeu Moura - DDD Europe 2023" >}}
<br>


Het schrijven van een test is het bevragen van een stuk code: "Krijg ik *dit* resultaat als ik de code op *deze* manier aanroep?" Het antwoord op die vraag is "ja" of "nee"; *hoe* de code antwoord op die vraag geeft, is vanuit het perspectief van de test irrelevant. Een goede ontwikkelaar schrijft daarom zo simpel, zo lelijk mogelijke -- *slechte* -- code om de test te laten slagen. 


Waarom schrijven TDD'ers *bewust* zulke slechte code om tests van rood naar groen te krijgen? Omdat het dwingt tot het stellen van betere vragen, tot het schrijven van meer tests. Wie meer code schrijft dan waar de tests om vragen, ontneemt zichzelf de noodzaak te code te blijven bevragen. -- Dat is het moment waarop aannames het voor het zeggen krijgen, waarop bugs de code in sluipen en tests ophouden het gedrag te [documenteren](/blog/22/09/tests-als-documentatie/ "'Tests als documentatie'"). 


Moura leert ons: TDD is niet een trucje om de testcoverage van je code op orde te krijgen. Het is een visie op software ontwikkelen.
