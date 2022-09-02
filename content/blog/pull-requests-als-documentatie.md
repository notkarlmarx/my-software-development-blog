---
title: "Pull requests als documentatie"
author: "Karl van Heijster"
date: 2022-09-02T10:53:48+02:00
draft: true
comments: true
tags: ["boeken", "code reviews", "documentatie", "Google", "intentie van code", "naamgeving", "productiviteit", "pull requests", "samenwerking"]
summary: "Hoe vaak denk je na over de titel en omschrijving van je *pull request*? Als je een beetje op mij lijkt, dan is het antwoord: veel te weinig. Het goede nieuws is: je *hoeft* er niet over na te denken, want dat hebben de vriendelijke ontwikkelaars van Google al voor je gedaan. Onlangs las ik hun *Code Review Developer Guide* door, en vond daar een schat aan informatie."
---

Hoe vaak denk je na over de titel en omschrijving van je *pull request* (PR)? Als je een beetje op mij lijkt, dan is het antwoord: veel te weinig. ~~Eigenlijk zou je elke dag en elke nacht over de titel en omschrijving van je PR's moeten nadenken, vanaf het moment dat je begint met je eerste programmeerbaan tot het moment dat je eindelijk met pensioen gaat, en als ik eerlijk ben: misschien daarna ook nog een paar jaar, gewoon voor de zekerheid.~~


## Code Review Developer Guide


Het goede nieuws is: je *hoeft* er niet over na te denken, want dat hebben de vriendelijke ontwikkelaars van Google al voor je gedaan. Onlangs las ik hun [*Code Review Developer Guide*](https://google.github.io/eng-practices/review/) door, en vond daar een schat aan informatie.


Mijn favoriete zin uit dat hele document is [deze](https://google.github.io/eng-practices/review/reviewer/standard.html):


> The primary purpose of code review is to make sure that the overall code health of Google’s code base is improving [!] over time.


Maar over die zin ga ik het vandaag niet hebben, ik wil het graag hebben over wat er aan een code review vooraf gaat. Dat is: de manier waarop je je PR presenteert aan de codereviewer.


## Waar te beginnen


In een [eerdere blog] (LINK) raadde ik codereviewers aan te beginnen met het beoordelen van de tests. Het idee daar achter is: als er geen tests in het PR besloten liggen, dan heeft de maker van het PR niet bewezen dat zijn of haar code correct functioneert, en is er niet aan de randvoorwaarden van het wijzigen van de codebase voldaan. 


Bovendien voorzien de tests de codereviewer van context bij zijn beoordeling. De tests voorzien de codereviewer van voorbeelden hoe de nieuwe code gebruikt dient te worden. In die zin fungeren ze [als documentatie] (LINK).


Ik sta nog steeds achter wat ik in die blog zei, maar ik erken dat ik eigenlijk een stap over heb geslagen. Het allereerste wat je als codereviewer doet, is de titel van het PR lezen - en, wanneer aanwezig, ook de beschrijving. Meer nog dan welke testsuite dan ook, geeft dit de context om het PR te kunnen beoordelen.


Des te belangrijker dus om goed na te denken over die titel en die omschrijving.


## Slechte titels


Ga maar na: hoe helpen de volgende titels de codereviewer in zijn beoordeling van je PR?


> - Fix build
>
> - Fix bug
>
> - Add patch
>
> - Phase 1
>
> - Added helper function


En dan heb ik het nog niet gehad over de omschrijvingen, want... nou ja, meestal zit er helemaal geen omschrijving bij een PR. Mijn collega's en ik gebruiken de omschrijving eigenlijk vooral om aan te geven wat er nog *niet* in een PR zit, in de vorm van *TODO*'s.


Het gevolg is dat de codereviewer de noodzakelijke context uit het PR zelf zal moeten halen. Je vraagt aan de codereviewer om de rationale te destilleren uit de oplossing. Dat is een arbeidsintensief proces. Hij moet zichzelf (of jou!) vragen stellen als: "Wat heeft de build gebroken?" - "Om welke bug gaat het?" - "Waarom deze patch?" - "Fase 1 van... wat precies?" - "Waar helpt deze functie me bij?"


Dat is op zichzelf al vervelend genoeg. Maar het wrede aan deze situatie is dat de maker van het PR die context al heeft. Hij of zij laat met dit soort titels dus de kans liggen het werk van de codereviewer te vergemakkelijken. Dat is niet alleen inefficiënt, dat is ronduit oncollegiaal - als je erover nadenkt (wat je dus veel te weinig doet).


## Betere titels


Hoe moet het dan wel? Daar is de *Code Review Developer Guide* heel duidelijk over ([hier](https://google.github.io/eng-practices/review/developer/cl-descriptions.html#firstline)). De titel biedt een korte beschrijving van wat er gedaan is. Het is een volledige zin, geschreven in de gebiedende wijs.


In de titel staat dus *wat* de build fixte, *welke* bug verholpen is, *wat* de patch inhoudt, *wat* fase 1 behelst, of *wat* de helperfunctie verhelpt:


> - Add missing semicolon to start up logic
>
> - [Swap key and value for FooBar Dictionary] (LINK Identifiers)
>
> - Improve performance of Foo module by simplifying design
> 
> - Add GET method on BarController
>
> - Simplify Baz validation


Het is belangrijk dat de titel descriptief is, want deze is je primaire informatiebron in de versiegeschiedenis van je codebase. Een ontwikkelaar die op zoek gaat naar de oorzaak van een bug, zou niet in de code moeten hoeven kijken om het juiste PR met de relevante wijziging te kunnen achterhalen. De titel zou voldoende indicatie moeten geven.


## *Release notes*


Daarnaast: als de titels van je PR's op orde, dan zou je in principe *release notes* moeten kunnen genereren op basis van deze informatie. Nu weet ik dat maar weinig ontwikkelaars zich al te zeer interesseren voor het maken van *release notes* - maar dat is júist waarom het belangrijk is om de titels op orde te hebben. Dit bespaart je immers het werk om deze notities zelf van de grond af aan op te stellen! (Al zal er, en daar moet ik eerlijk in zijn, waarschijnlijk altijd een handmatige redactieslag nodig blijven.)


[Cyrille Martraire](http://cyrille.martraire.com/) gaat in [*Living Documentation*](https://www.oreilly.com/library/view/living-documentation-continuous/9780134689418/) nog een stapje verder hierin. Hij stelt voor om metadata aan de titel toe te voegen, die door een *release notes*-generator geïnterpreteerd kan worden om zo een optimale gebruikservaring te bieden. Die metadata hoeft niet ingewikkeld te zijn - het kan een eenvoudig lijstje zijn als *FEATURE*, *BUG*, *REFACTOR* -, als deze maar consequent wordt toegepast. 


## Beschrijving


Dan, de omschrijving. De *Code Review Developer Guide* schrijft hierover ([hier](https://google.github.io/eng-practices/review/developer/cl-descriptions.html#informative)):


> [T]he description should fill in the details and include any supplemental information a reader needs to understand the changelist holistically. It might include a brief description of the problem that’s being solved, and why this is the best approach. If there are any shortcomings to the approach, they should be mentioned. If relevant, include background information such as bug numbers, benchmark results, and links to design documents.


Met andere woorden: de omschrijving bevat de rationale achter het PR. Het bevat informatie over het probleem, en erin staat beschreven waarom deze oplossing de beste is. (Nota bene, dit betekent niet per se "technisch de beste". Ook factoren als tijd en geld kunnen een rol spelen bij het kiezen van een oplossing.) Kort gezegd: hierin wordt het *waarom* van het PR uit de doeken gedaan.


## Besparen


Bedenkt eens hoeveel werk zo'n korte omschrijving een codereviewer zou kunnen besparen! Als deze aan de omschrijving alleen al kan aflezen dat de gekozen oplossing suboptimaal is, dan bespaart diegene zich daarmee de moeite diep in de code te duiken om tot dezelfde conclusie te komen. In principe zou op basis van de omschrijving alleen een alternatieve aanpak kunnen worden voorgesteld. De tijd die een codereviewer wordt bespaard met zo'n beknopte omschrijving, kan hij steken in het actief meedenken van een betere oplossing.


Door de rationale in de omschrijving van een PR te stoppen, bepaar je de codereviewer niet alleen werk, je waarborgt ook dat toekomstige ontwikkelaars altijd kunnen achterhalen waarom een bepaalde wijziging is doorgevoerd. Dat geeft hen munitie om code in de toekomst te wijzigen - of juist niet. Zonder deze informatie worden ontwikkelaars terughoudend in het aanpassen van code. Ze weten immers niet of een ogenschijnlijk onlogische oplossing niet met goede reden is geïmplementeerd.


De rationale achter een bepaalde oplossing is bij uitstek een van die dingen die moeilijk vast te leggen is in de code zelf. Code vertelt je alleen iets over het *wat*, niet het *waarom*. PR's kunnen die leegte opvullen. Meer nog: doordat ze gekoppeld zijn aan kleine, gefocuste wijzigingen, maken ze het makkelijk om deze documentatie stapje voor stapje uit te breiden.


## Nadenken


De conclusie moge duidelijk zijn: ik ga de komende tijd wat beter nadenken over de titels en omschrijvingen van mijn PR's. Jij ook, hoop ik?


Mocht je wat inspiratie op willen doen, de *Code Review Developer Guide* geeft [hier](https://google.github.io/eng-practices/review/developer/cl-descriptions.html#good) enkele voorbeelden van goede titels en omschrijvingen.
