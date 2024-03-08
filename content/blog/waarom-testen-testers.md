---
title: "Waarom testen testers?"
author: "Karl van Heijster"
date: 2024-03-08T10:08:29+01:00
draft: true
comments: true
tags: ["aannames", "efficiëntie", "procesverbetering", "requirements", "samenwerking", "shift left", "software ontwikkelaar (rol)", "sprint retrospective", "testen", "tester (rol)", "test-driven development", "verantwoordelijkheid"]
summary: "Tijdens een Retrospective gaf onze tester aan dat hij omkwam in het werk. Eigenlijk verbaasde niemand dat. Ons team bestaat uit vijf ontwikkelaars en één tester, en die ene tester is verantwoordelijk voor het schrijven van geautomatiseerde tests voor de code van al die vijf ontwikkelaars. Je kunt op je vingers natellen dat die situatie niet houdbaar is. -- Dus wat te doen?"
---

Laatst hadden we een interessante discussie in het team, die raakt aan de kern van de verantwoordelijkheden van ontwikkelaars en testers. 


Tijdens een [Retrospective](/tags/sprint-retrospective/ "Blogs met de tag 'sprint retrospective'") gaf onze tester aan dat hij omkwam in het werk. Eigenlijk verbaasde niemand dat. Ons team bestaat uit vijf ontwikkelaars en één tester, en die ene tester is verantwoordelijk voor het schrijven van geautomatiseerde tests voor de code van al die vijf ontwikkelaars. Je kunt op je vingers natellen dat die situatie niet houdbaar is.


Dus wat te doen? We zouden de testcapaciteit kunnen verhogen. We zouden een ontwikkelaar kunnen aanwijzen om de komende Sprint een deel van de taken van onze tester over te nemen. Die ontwikkelaar zou zich dan *full time* (of in elk geval het grootste gedeelte van zijn tijd) moeten richten op het schrijven van geautomatiseerde tests voor het werk van zijn collega's. 


## Scheiding


Er is wat mij betreft een fundamenteel probleem met dat voorstel. Deze oplossing veronderstelt namelijk een strikte scheiding tussen het werk van testers en programmeurs. Testers testen en programmeurs programmeren. 


Maar dat is een veronderstelling die ik problematisch vind. Ik ben er stellig van overtuigd dat programmeurs de werking van hun code vast moeten leggen in tests. Sterker nog, de afwezigheid van tests bij een [*pull request*](/tags/pull-requests/ "Blogs met de tag 'pull requests'") (PR) is wat mij betreft voldoende aanleiding om het PR af te wijzen: de code is in dat geval nog niet productierijp. (Zie ook [deze](/blog/23/07/de-tester-als-code-reviewer/ "'De tester als code reviewer'") en [deze blog](/blog/23/09/drie-vragen-die-elk-pull-request-moet-beantwoorden/ "'Drie vragen die elk pull request moet beantwoorden'").)


Het is de verantwoordelijkheid van de ontwikkelaar te bewijzen dat de code zich zus en zo gedraagt. Het is niet de verantwoordelijkheid van de tester om te controleren of de code doet wat de ontwikkelaar zegt dat ze doet.


Daaruit volgt dat programmeren en testen geen welonderscheiden taken zijn. Beide zijn twee kanten van dezelfde munt: kwalitatief hoogstaande software ontwikkelen. (Dit punt formuleerde ik eerder in [deze talk](/talks/waarom-testers-code-moeten-reviewen/ "'Waarom testers code moeten reviewen'").) Dit compliceert de eenvoudige taakverdeling zoals die hierboven wordt verondersteld.


Mijn voorstel was dan ook: in plaats van een ontwikkelaar aan te wijzen om andermans werk te controleren, moeten we er strenger op toezien dat ontwikkelaar hun eigen code documenteren met een uitgebreide, descriptieve testsuite. (Zie met name [deze talk](/talks/altijd-up-to-date-documentatie-met-maximaal-descriptieve-tests/ "'Altijd up to date documentatie met maximaal descriptieve tests'").) Als gevolg daarvan zou de tester [veel minder tijd kwijt zijn](/blog/23/11/drie-feedbackloops-die-verbeteren-met-unit-tests/ "'Drie feedbackloops die verbeteren met unit tests'") aan zijn werkzaamheden. Hij hoeft in dat geval alleen nog maar de tests te lezen, in plaats van ze zelf te verzinnen en te schrijven, om erachter te komen of de code doet wat het moet doen. 


## Aannames


Een collega wierp daar tegenin: een programmeur die zijn eigen code test, test zijn eigen aannames. Je hebt een tweede set ogen nodig die je aannames kritisch tegen het licht houdt, en dat is de rol van de tester.


Dat is een interessant argument waar veel waarheid in zit, maar ook wat onwaarheid. Laten we met de eerste stelling beginnen. Test een programmeur die zijn eigen code test, *slechts* zijn eigen aannames, en betekent dat dat hij onjuiste aannames *noodzakelijk* (of *altijd* of zelfs *meestal*) niet op zal merken? Volgens mij niet.


Onjuiste aannames zullen met name een grote rol spelen bij ontwikkelaars die hun werk achteraf testen. Dat komt omdat ze deze veelal ongemerkt in hun code introduceren. Ontwikkelaars houden van [*flow*](/tags/the-zone/ "Blogs met de tag 'the zone'"), en wie uren achtereen de code uit zijn vingers laat vloeien, maakt gedachteloos de ene beslissing na de andere. 


Tegen de tijd dat deze ontwikkelaars de werking van hun code vastleggen met tests, hebben ze een hoop tijd met een bepaalde implementatie doorgebracht. Dat heeft ervoor gezorgd dat ze deze als gezaghebbend zijn gaan zien. Hun [mentale model](/blog/22/08/wat-is-jouw-mentale-model/ "'Wat is jouw mentale model?'") heeft zich aangepast aan de code zoals deze er staat. Het gevaar van eigen aannames testen is in dat geval reëel.


## TDD


[Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) kan dit effect dempen. (Zie ook [deze blog](/blog/23/04/wij-van-tdd-eend/ "'Wij van TDD-eend...'").) Een TDD'er wisselt tijdens het schrijven van code continu van perspectief: specificeren (*red*), implementeren (*green*), ontwerpen (*refactor*). Zo voorkomt TDD dat een ontwikkelaar in een *flow* raakt. 


TDD is daarnaast een uitstekend middel is om ontwikkelaars bewust te maken van hun eigen aannames. Wie een falende test schrijft, maakt een aanname expliciet: de aanname dat de code correct functioneert als die test slaagt. Wie een aanname expliciet maakt, geeft zichzelf de mogelijkheid om te reflecteren op diens validiteit. Zo helpt TDD om de ontwikkelaar kritisch naar zijn eigen werk te kijken.[^1]


Hieruit volgt dat ook de tweede stelling van het argument genuanceerd moet worden. Onjuiste aannames kunnen aan het licht gebracht worden door iets anders dan een tweede set ogen, namelijk: dezelfde set ogen die de code vanuit een ander perspectief bezien. Maar die rol kunnen die ogen alleen spelen als de eigenaar ervan een proces volgt dat regelmatig van perspectief wisselt.


Daarmee zeg ik natuurlijk niet dat het makkelijk is om je eigen aannames aan het licht te brengen. Integendeel, ik erken voluit dat dit verdomd moeilijk kan zijn, zelfs als je TDD't. De waarheid van die tweede stelling zit 'm dan ook in het feit dat het veel eenvoudiger is voor een ander om jouw onjuiste aannames boven tafel te krijgen. En daarom is een tweede set ogen absoluut wenselijk.


## Eerder


Dan komen we ten slotte bij de derde stelling: het is de tester die deze rol vervult. De tester vormt de tweede set ogen. Ook deze stelling is waar -- en onwaar. Het is waar: in de praktijk komen de onjuiste aannames die we als ontwikkelaar maken inderdaad aan het licht dankzij het werk van onze tester.


Maar het is onjuist te denken dat deze rol *alleen* of *bij uitstek* door de tester kan worden vervuld. Een ontwikkelaar (of zelfs een stakeholder) zou onjuiste aannames immers net zo goed aan het licht kunnen brengen. Dat is één van de redenen waarom [*pair programming*](/tags/pair-programming/ "Blogs met de tag 'pair programming'") bestaat.


Sterker nog, het zou zelfs *beter* zijn als een *pairende* ontwikkelaar onjuiste aannames aan het licht brengt. Als we het wenselijk vinden om verkeerde aannames te signaleren, waarom zouden we daar dan mee wachten tot nadat de code is geschreven en overgedragen aan de tester? Waarom zouden we niet ons best doen om deze tijdens de ontwikkeling af te vangen? Hoe eerder zo'n aanname gecorrigeerd wordt, des te minder schade kan deze immers aanrichten. 


## Verantwoordelijkheid


Samenvattend: een programmeur die zijn eigen code test, kan desondanks zijn best doen zijn eigen aannames kritisch tegen het licht te houden. Het helpt om iemand bij dit proces te betrekken, maar dat hoeft niet per se de tester te zijn.


Het zou niet de rol van de tester moeten zijn om verkeerde aannames aan het licht te brengen. Als de tester deze aan het licht brengt, zijn we ruimschoots aan de late kant. 


Het is de verantwoordelijkheid van het hele team om deze zo snel mogelijk te identificeren. Als mijn overpeinzingen in deze blog kloppen, dan is een combinatie van TDD met *pair programming* een effectievere manier om deze in een zo vroeg mogelijk stadium af te vangen.


Zo ontlasten we onze tester, zonder dat we een ontwikkelaar tot tester hoeven te bombarderen.


[^1]: Let op, ik zeg heel bewust: "TDD *maakt bewust*...", "TDD *geeft de mogelijkheid*...", "TDD *helpt*...". Ik zeg niet: TDD *voorkomt* dat je als ontwikkelaar onjuiste aannames maakt -- dat is een te sterke claim. Maar: ook een tester die achteraf je code test, voorkomt niet per se dat onjuiste aannames de code in sluipen!
