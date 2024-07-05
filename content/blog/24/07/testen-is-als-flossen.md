---
title: "Testen is als flossen"
author: "Karl van Heijster"
date: 2024-07-05T07:54:55+02:00
draft: false
comments: true
tags: ["beroepsdeformatie", "test-driven development"]
summary: "Code unittesten is als je tanden flossen: de meeste mensen doen het niet, en als ze het doen, doen ze het op het verkeerde moment."
---

Code unittesten is als je tanden flossen: de meeste mensen doen het niet, en als ze het doen, doen ze het op het verkeerde moment.


## Over flossen


*1(a)*. Je zou je tanden moeten flossen. Met tweemaal daags poetsen krijg je het gros van de plak wel van je tanden. Maar de plak *tussen* je tanden, dat is moeilijk om met een borstel bij te komen. Poetsen alleen is niet voldoende om je tanden helemaal schoon te krijgen.


*2(a)*. Als je flost *nadat* je je tanden hebt gepoetst, dan maak je het jezelf onnodig moeilijk. Het poetsen heeft de plak tussen je tanden niet verwijderd, maar wel gehavend. De plak is uiteengevallen in kleinere brokken. Dat zorgt ervoor dat plak makkelijk achter kan blijven, zelfs als je grondig flost.


Het is beter om je tanden te flossen *voordat* je begint met poetsen. Omdat de tandplak dan nog niet is opgebroken, verwijdert een goede flosbeurt deze snel en efficiënt.


## Over testen


Met testen werkt het net zo.


*1(b)*. Je zou je code moeten unittesten. Een handmatige test is vaak wel voldoende om een *happy path* mee te valideren. Maar de *edge cases*, die zie je eenvoudig over het hoofd. 


(-- *Jij* ziet ze over het hoofd, maar de gebruikers van je code niet. En in het onvermijdelijke moment dat zo'n *edge case* hun data corrumpeert, zal het hen weinig kunnen schelen dat het *happy path* werkte.) 


Handmatig testen is niet voldoende om kwalitatief hoogwaardige software op te leveren.[^1]


*2(b)*. Als je test *nadat* je je code hebt geschreven, maak je het jezelf onnodig moeilijk. 


De code kan op zo'n manier opgezet zijn dat het nagenoeg onmogelijk is de boel goed en wel te testen.[^2] Je tests zijn een feedbackmechanisme: ze vertellen je iets over de kwaliteit van je ontwerp. Wanneer het nagenoeg onmogelijk is je code goed te testen, dan is je ontwerp ondermaats. Het probleem is: daar kom je pas achter op het moment dat je je code test. Als je dat doet nadat de feature geïmplementeerd is -- is het al te laat.


Tests helpen je bovendien een probleem op te delen in kleinere brokken. Een falende test geeft jezelf een concreet doel: mijn code moet nu *deze* test doen slagen (en de al bestaande tests niet breken). Dit structureert je ontwikkelwerkzaamheden. Zo lang er geen falende test is voor feature *x*, hoef je je nog niet met feature *x* bezig te houden.


## Conclusie


[Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) maakt programmeren niet alleen veiliger en makkelijker. Coderen, [één test per keer](/blog/22/04/een-test-per-keer/ "'Eén test per keer'"), is eenvoudigweg -- *leuker*. Het geeft een kick, elke keer als je een test van rood naar groen ziet gaan. En de immer uitdijende lijst aan groene tests bewijst bovendien: je maakt voortgang (boekt vooruitgang).


TDD produceert tevreden ontwikkelaars. En flossen produceert sprankelend schone tanden. Testen is als flossen: het levert een stralende lach op.


[^1]: Want "kwalitatief hoogwaardige software" betekent onder andere: automatisch geteste software. Ik sprak erover in [deze talk](/talks/waarom-testers-code-moeten-reviewen/ "'Waarom testers code moeten reviewen'").


[^2]: Dit speelt vooral bij *legacy* systemen. Maar ook hier speelt: "*legacy*" betekent o.a. dat het moeilijk te testen is. [Michael Feathers](https://michaelfeathers.silvrback.com/) definieert *legacy* code zelfs als ongeteste code, zie [deze blog](/blog/22/04/de-ontwikkelaar-als-chirurg/ "'De ontwikkelaar als chirurg'").
