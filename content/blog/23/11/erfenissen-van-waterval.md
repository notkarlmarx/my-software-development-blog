---
title: "Erfenissen van waterval"
author: "Karl van Heijster"
date: 2023-11-17T07:44:51+01:00
draft: false
comments: true
tags: ["agile ontwikkeling", "code reviews", "pair programming", "pull requests", "samenwerking", "test-driven development", "testen", "waterval"]
summary: "Op het Najaarsevenement van TestNet betoogde ik dat testers een belangrijke rol hebben te spelen in het reviewen van code. Tijdens de voorbereiding van mijn presentatie realiseerde ik me dat mijn team, alle Agile ambities ten spijt, in zijn denken nog diep verankerd zit in het gedachtegoed van de watervalopvatting van softwareontwikkeling."
---

Op het Najaarsevenement van [TestNet](https://www.testnet.org/) betoogde ik dat [testers een belangrijke rol hebben te spelen in het reviewen van code](/talks/waarom-testers-code-moeten-reviewen/ "'Waarom testers code moeten reviewen'"). Ik schreef er al eerder over, [hier](/blog/23/07/de-tester-als-code-reviewer/ "'De tester als code reviewer'") (maar zie ook [deze blog](/blog/23/09/drie-vragen-die-elk-pull-request-moet-beantwoorden/ "'Drie vragen die elk pull request moet beantwoorden'")). 


Tijdens de voorbereiding van mijn presentatie realiseerde ik me dat mijn team, alle [Agile](https://en.wikipedia.org/wiki/Agile_software_development "'Agile software development', Wikipedia") ambities ten spijt, in zijn denken nog diep verankerd zit in het gedachtegoed van de [watervalopvatting van softwareontwikkeling](https://en.wikipedia.org/wiki/Waterfall_model "'Waterfall model', Wikipedia").


## Hoe wij software ontwikkelen


Dit is hoe wij software ontwikkelen. Een programmeur pakt een taak op van de [Sprint Backlog](https://www.scrum.org/resources/what-is-a-sprint-backlog "'What is a Sprint Backlog?', scrum.org"). Hij programmeert een tijdje. Op een gegeven moment heeft 'ie het gevoel klaar te zijn, en maak een [*pull request*](/tags/pull-requests/ "Blogs met de tag 'pull requests'") (PR) aan. Een andere ontwikkelaar controleert zijn werk. De code wordt, na goedkeuring, uitgerold op de testomgeving. De tester test zijn code. Als alles goed gaat, dan geeft de tester goedkeuring om de wijziging door te zetten naar de acceptatieomgeving; als hij er een probleem in ontdekt, maakt hij een nieuwe taak aan op de Sprint Backlog -- en begint het verhaal opnieuw.


Voor veel teams is dit zo'n vanzelfsprekende manier van werken, dat ze niet eens meer de invloed van waterval op deze werkwijze herkennen. Maar neem de volgende punten in overweging:


1. Het werkproces bestaat uit afgebakende stappen die serieel worden doorlopen. Eerst wordt er ontwikkeld, dan wordt er code gereviewd, dan wordt er getest.

2. Elke stap in het proces kent één verantwoordelijke. Het programmeren is de verantwoordelijkheid van de programmeur, het reviewen die van zijn collega, het testen die van de tester.

3. De verhouding die collega's met elkaar hebben, is er een van controle. In elke volgende stap wordt het werk van de vorige gecontroleerd. Samenwerking tussen én binnen disciplines wordt (bewust of onbewust?) ontmoedigd. Als er samenwerking plaatsvindt, dan is dat *ondanks*, niet dankzij, het proces.


Hoewel Agile in naam het mainstream ontwikkelparadigma is anno 2023, werken veel teams feitelijk nog steeds op zoals ze twintig, dertig jaar geleden werkten -- de feedbackloops zijn alleen kleiner geworden (zie ook [deze blog](/blog/23/10/sprints-zijn-geen-miniwatervallen/ "'Sprints zijn geen miniwatervallen'")). De vorm van Agile is aangenomen, maar de inhoud is ongewijzigd gebleven. De erfenissen van waterval zijn nog steeds alomtegenwoordig.


## Aannames


De drie punten die ik hierboven noemde, komen voort uit aannames: de aanname dat er eerst moet worden ontwikkeld voordat er kan worden getest; de aanname dat ieder verantwoordelijk is voor zijn eigen stukje van het proces; de aanname dat controle nodig is om kwaliteit te kunnen leveren.


Er valt wat op die aannames af te dingen.


1. Software ontwikkelen hoeft niet plaats te vinden in welonderscheiden stappen. [*Pair programmers*](/tags/pair-programming/ "Blogs met de tag 'pair programming'") reviewen de code terwijl deze geschreven wordt. Ontwikkelaars die aan [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) doen, schrijven eerst een test, dan wat code, dan weer een test. Het is mogelijk om de hierboven beschreven stappen ongeveer tegelijkertijd uit te voeren, of in elk geval zonder strakke afbakening.

2. Goede software wordt niet in silo's ontwikkeld. Ontwikkelaars en testers hebben hun eigen expertisegebieden, maar ze zijn verantwoordelijk voor één en hetzelfde: het systeem in zijn geheel. Er bestaat geen fundamenteel onderscheid tussen productiecode aan de ene kant en testcode aan de andere. Het zijn twee kanten van dezelfde munt: kwalitatief hoogstaande software.

3. De noodzaak voor controle komt voort uit de eerste twee punten, het is het gevolg van het feit dat ontwikkelaars en testers onvoldoende met elkaar samenwerken. Want als je samenwerkt, als je code schrijft met een tester en collega-ontwikkelaar naast je, dan verdwijnt de behoefte om te willen controleren volledig. Wat valt er immers nog te controleren? -- je was erbij toen de software ontwikkeld werd!


De dingen die ik opschrijf zijn niet nieuw -- zelfs niet voor mij. [James Shore](https://www.jamesshore.com/) maakte hetzelfde punt in [*The Art of Agile Development*](https://www.oreilly.com/library/view/the-art-of/9780596527679/), nota bene [het op één na beste boek dat ik vorig jaar over softwareontwikkeling las](/blog/22/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2022-las/ "'De beste boeken over software ontwikkeling die ik in 2022 las'"). Maar het punt klikte pas echt toen ik gedwongen werd mijn eigen gedachten te formuleren over de rol van testers in het softwareontwikkeltraject. (Een goede reden voor elke ontwikkelaar om regelmatig een presentatie te geven!)


## Inzicht


Sterker nog, het gaf me een nieuw inzicht in het centrale punt van mijn presentatie. Testers moeten code reviewen, dat vond ik en dat vind ik nog steeds. 


Maar het is niet per se zo dat ze zich met PR's moeten bemoeien. Want PR's mogen dan geen expliciet onderdeel zijn van de watervalmethodologie, ze ademen haar achterliggende filosofie: ze introduceren een welonderscheiden fase waarin iemand anders de verantwoordelijkheid krijgt om de code te controleren.[^1] Het idee dat de tester een controlerende rol vervult bij het inspecteren van PR's (uiteengzet in [deze blog](/blog/23/07/de-tester-als-code-reviewer/ "'De tester als code reviewer'")), is in feite nog niet radicaal genoeg.


PR's kunnen in veel gevallen worden vervangen door *pair programming* (zoals uiteengezet in [deze blog](/blog/23/01/wel-code-reviews-geen-pull-requests/ "'Wel code reviews, geen pull requests'")). In teams waarin de Agile filosofie volledig wordt omarmd, zul je zien dat ontwikkelaars en testers elkaar regelmatig opzoeken om samen aan een stuk code te werken.


Pas dan heeft een team de erfenissen van waterval volledig van zich afgeschud.


[^1]: Maar: de context doet ertoe. In projecten waarin teamleden niet continu met elkaar *kunnen* samenwerken, zoals bij veel open source-projecten het geval is, is silovorming onvermijdelijk en controle wenselijk. Dit is ook de context waarin PR's oorspronkelijk werden geïntroduceerd. 
