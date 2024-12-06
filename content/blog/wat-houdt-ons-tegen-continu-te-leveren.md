---
title: "Wat houdt ons tegen continu te leveren?"
author: "Karl van Heijster"
date: 2024-12-06T10:49:50+01:00
draft: true
comments: true
tags: ["continuous delivery", "continuous integration", "scrum", "verandering"]
summary: "CI/CD houdt meer in dan het alleen inrichten van een buildserver: het is een heel andere manier van werken. Het verlangt van je dat je je werkt anders opdeelt, dat je in kleine stapjes werkt, dat alle code die je schrijft continu van hoge kwaliteit is. *Continuous delivery* vraagt van ontwikkelaars dat ze bepaalde gewoontes -- gewoontes waar ze zich goed bij voelen -- te herzien."
---

Vorige week schreef ik over [een praatje](https://www.youtube.com/watch?v=eZKVxtbmtMI "'Agile and Architecture: a meeting of the undead - Einar Høst - NDC Oslo 2024', YouTube") van [Einar Høst](https://einarwh.wordpress.com/). Daarin merkt hij ironisch op dat de implementatie van [Agile](/tags/agile-ontwikkeling/ "Blogs met de tag 'agile ontwikkeling'") -- nota bene: het idee individuen en hun interacties meer waarde hebben dan processen en tools --, is verworden tot: gebruik *dit* proces met *deze* tool.


Een deel van het probleem ligt bij het feit dat de softwareontwikkelcultuur een popcultuur is waarin ideeën niet volledig worden doordacht. Maar dat is maar de helft van het verhaal. Vandaag wil ik een andere vraag stellen: in hoeverre zijn ontwikkelaars bereid de werkwijzen te herzien waar zich comfortabel bij voelen?


## Terrarium


Høst zegt: een [Scrummende](/tags/scrum/ "Blogs met de tag 'scrum'") ontwikkelaar is als een zijderups. Wat bedoelt hij daarmee?


De zijderups is één van de meest gekweekte insecten ter wereld. De reden laat zich raden: de larve spint een cocon van een zeer stevige draad, die wordt gebruikt bij de productie van zijde. Om zoveel mogelijk rendement uit deze beestjes te halen, worden ze gekweekt in een terrarium waar de condities optimaal zijn om zoveel mogelijk larven voort te brengen. -- Dit is, dat spreekt voor zich, een uitstekende deal voor de zijderups.


Ontwikkelaars leveren geen larven op, maar code. En ook hier geldt: het rendement moet zo hoog mogelijk zijn. Dus wordt er een terrarium gecreëerd -- de Sprint -- waarbinnen de condities voor de ontwikkelaar zo optimaal mogelijk zijn om zoveel mogelijk code te schrijven. Dat betekent: zo min mogelijk contact met allerlei moeilijke mensen als managers en eindgebruikers -- dat bewaren we wel voor de [Sprint Review](/tags/sprint-review/ "Blogs met de tag 'Sprint Review'").


## Ironie


Dit is, net als voor de zijderups, een uitstekende deal voor de ontwikkelaar. Zij kunnen zich concentreren op waar ze zich prettig bij voelen -- code schrijven -- en beperken de momenten tot een minimum dat ze verantwoording af moeten leggen of moeilijke nieuwe wensen moeten inpassen.


Høsts karakterisatie is ook hier doordrenkt ironie, natuurlijk. Want het hele idee van Scrum *qua* Agile ontwikkelmethode was nu juist om werkende software op te leveren die is ontstaan in samenwerking met de klant. -- "*Working software over comprehensive documentation*," zegt het [Agile manifest](https://agilemanifesto.org/ "'Manifesto for Agile Software Development', Kent Beck et al."), en: "*Customer collaboration over contract negotiation*!"


Om daadwerkelijk *agile* te worden -- let op de kleine letter: het doel van *Agile* is wendbaarheid! --, moeten ontwikkelaars een deel van hun comfortabele positie prijsgeven. Ze zullen uit het terrarium moeten breken, bepleit Høst, en vaker in gesprek moeten gaan met stakeholders en eindgebruikers. Dat is niet in hun eigen belang, maar in het belang van de mensen die grof geld betalen om de voor hen zo prettige condities in het terrarium te handhaven!


## *Continuous delivery*


Niet lang nadat ik Høst had horen spreken, zag ik de onderstaande video van [Christian Johansen](https://cjohansen.no/) over [*continuous delivery*](https://en.wikipedia.org/wiki/Continuous_delivery "'Continuous delivery', Wikipedia").


{{<youtube id="hnETs-UVQec" title="How to deliver continuously - Christian Johansen - NDC Oslo 2024" >}}
<br>


Ik pleit al enige tijd in mijn team, met een boek als [*Accelerate*](https://itrevolution.com/product/accelerate/)[^1] in de hand, voor het implementeren van praktijken die ons in staat stellen continu te leveren -- maar helaas met wisselend resultaat. Maar met Høst en Johansen in het achterhoofd, begrijp ik beter waarom mijn pogingen stranden.


Johansen legt veel nadruk op het feit dat [CI/CD](https://en.wikipedia.org/wiki/CI/CD "'CI/CD', Wikipedia") meer inhoudt dan het alleen inrichten van een buildserver: het is een heel andere manier van werken. Het verlangt van je dat je je werkt anders opdeelt, dat je in kleine stapjes werkt, dat alle code die je schrijft continu van hoge kwaliteit is ([en dus gedekt door tests](/blog/24/07/goede-code-is-geteste-code/ "'Goede code is geteste code'")). 


*Continuous delivery* vraagt van ontwikkelaars dat ze bepaalde gewoontes -- gewoontes waar ze zich goed bij voelen -- te herzien.


## Wat houdt ons tegen?


Wat zijn die gewoonten? De volgende lijst komt in me op, maar is vast en zeker niet uitputtend:


- Werken in grote stappen. Om continu stabiele software uit te kunnen leveren, is het nodig om in kleine stapjes te werken. Grote stappen zijn disruptief: ze brengen risico's met zich mee die je je niet kunt veroorloven als je code onmiddellijk wordt uitgerold op de productieomgeving. 

- Code breken. Om continu elkaars wijzigingen te kunnen integreren, moet de code continu in werkende staat worden gehouden. Refactorslagen waarbij de tests langere tijd op rood staan -- of erger nog: zonder tests --, zijn uit den boze. 

- Werken in isolatie. Het klinkt tegenintuïtief continu codewijzigingen van collega's te moeten integreren in je code. Het gezond verstand (of wat zich als zodanig maskeert) dicteert daarom: houd wijzigingen apart van elkaar en integreer pas als je klaar bent. Maar dat heeft lagere softwarekwaliteit tot gevolg, pijnlijker integraties en leidt tot werken in grotere stappen.

- Testtaken delegeren naar de tester. Wanneer jouw code onmiddellijk op de productieomgeving wordt uitgerold, is een solide [vangnet](/blog/22/09/tests-als-vangnet/ "'Tests als vangnet'") van geautomatiseerde tests een absolute noodzakelijkheid. Eerst een feature implementeren en daarna de tests schrijven om te zien of deze doet wat het moet doen, is er niet meer bij.


Al deze problemen zijn in wezen al opgelost *mits de werkwijzen worden omarmd die continuous delivery mogelijk maken*. -- De opdracht luidt nu dus: hoe krijg ik mijn collega's zover dat ze hun gekoesterde gewoontes opgeven voor een nieuwe manier van werken? 


[^1]: Eén van [mijn favoriete boeken die ik het afgelopen jaar over softwareontwikkeling las] (LINK).