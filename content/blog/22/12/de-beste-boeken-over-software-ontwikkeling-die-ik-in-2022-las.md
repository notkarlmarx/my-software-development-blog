---
title: "De beste boeken over software ontwikkeling die ik in 2022 las"
author: "Karl van Heijster"
date: 2022-12-27T23:09:12+01:00
draft: false
comments: true
tags: ["boeken"]
summary: "Eindejaarslijstjestijd! Net als vorig jaar en het jaar daarvoor heb ik dit jaar weer enkele fantastische boeken over softwareontwikkeling mogen lezen. Dit waren mijn vijf favorieten - en vijf eervolle vermeldingen."
---

Eindejaarslijstjestijd! [Net als vorig jaar](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/) en [het jaar daarvoor](/blog/21/05/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2020-las/) heb ik dit jaar weer enkele fantastische boeken over softwareontwikkeling mogen lezen. Dit waren mijn vijf favorieten - en vijf eervolle vermeldingen.


## Top 5


### 1. Enrico Buonanno - [*Functional Programming in C#, Second Edition*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition)


Het is niet mijn gewoonte om boeken op deze lijst te zetten die ik nog niet uit heb gelezen - laat staan op de eerste plek -, maar voor *Functional Programming in C#* maak ik graag een uitzondering. Dit boek las ik eenmal tot halverwege, en daarna begon ik opnieuw met een toetsenbord erbij. Het nog altijd uitdijende resultaat van die inspanningen valt te bekijken in [deze GitHub repositoy](https://github.com/dotkarl/FunctionalProgrammingPlayground).


Functioneel programmeren is niet alleen een manier van denken, het is ook een manier van doen: ik moest met [Buonanno](https://twitter.com/la_yumba) meeschrijven om me het functionele paradigma eigen te maken - en ik ben daar nog steeds lerende in. Dat dat [paradigma](https://www.karlvanheijster.com/blog/21/10/low-code-een-nieuw-paradigma/) radicaal verschilt van de objectgeoriënteerde, moge duidelijk zijn. 


Het idee dat mijn huidige manier van code schrijven het meest heeft beïnvloed, is dat van [eerlijke functies](/blog/22/07/wat-zijn-eerlijke-functies/). Je code is meer dan alleen een instructie voor een machine - het is een communicatiemiddel naar je collega's en je toekomstige zelf toe. Een eerlijke functie communiceert haar werking louter en alleen middels haar signatuur: *dit* gaat erin, *dat* komt eruit - meer is het niet. 


Met het gebruik van [*monads*](/blog/22/12/wat-is-een-monad/) kun je de intentie van dat *dit* en *dat* nog verder verduidelijken. Een [Option](https://www.karlvanheijster.com/blog/22/08/spelen-met-options/) geeft bijvoorbeeld aan: dit object kan ook *niets* zijn. - En het is ook een fantastische manier om vervelende boilerplate code te vermijden, zoals de obligate en immer vervelende null-check.


Dit boek heeft mijn manier van code schrijven veranderd, en is - hoewel nog steeds niet helemaal uitgelezen - daarom een welverdiende nummer één.


### 2. James Shore - [*The Art of Agile Development, Second Edition*](https://www.jamesshore.com/v2/books/aoad2)


Ik bevind me in de luxepositie om mijn hele softwareontwikkelcarrière lang al heel aardig volgens het boekje te mogen Scrummen. Toen ik [*Clean Agile*](/blog/21/11/agile-zijn-niet-agile-doen/) las (vorig jaar nog een [eervolle vermelding](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/)!), ontdekte ik echter dat er veel meer bij Agile komt kijken dan alleen iteratief ontwikkelen.


*The Art of Agile Development* van [James Shore](https://www.jamesshore.com/) is een zeer compleet overzicht van allerlei praktijken die Agile teams naar een hoger niveau kunnen stuwen. Van [Test-Driven Development (TDD)](/blog/22/05/nog-een-reden-om-testgedreven-te-ontwikkelen/) tot [incidentanalyses](/blog/22/05/incidentanalyse-zonder-schuldigen/) tot [*user stories*](/blog/22/02/de-rol-van-user-stories/) tot de notie van [speelruimte](/blog/22/05/tevreden-ontwikkelaars-en-stakeholders-dankzij-speelruimte/): dit boek bevat een schat aan kennis. Het is wat mij betreft verplichte kost voor elke ontwikkelaar die zichzelf en zijn team continu wil verbeteren.


### 3. Robert C. Martin - [*Clean Craftmanship: Disciplines, Standards, and Ethics*](https://www.pearson.com/en-us/subject-catalog/p/clean-craftsmanship-disciplines-standards-and-ethics/P200000009529/9780136915713)


Tot nog toe is er geen jaar voorbijgegaan zonder dat [Robert *Uncle Bob* Martin](http://cleancoder.com/products) in een of andere hoedanigheid op mijn eindejaarslijstje prijkte (in 2020 stond 'ie zelfs op [de eerste én tweede plek](/blog/21/05/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2020-las/)!) - en dit jaar gaat niet anders zijn. 


*Clean Craftmanship* is een oproep aan ontwikkelaars om zichzelf en hun vakgebied te professionaliseren. De tijd dat we weg konden komen met buggy software die voor tachtig, zeventig of zestig procent doet wat de eindgebruiker verwacht, is definitief voorbij. 


Er komt heel wat kijken bij het zijn van een softwarevakman - een ferm "nee" kunnen verkopen aan je manager, bijvoorbeeld -, maar het allerbelangrijkst is: testen. Testen, testen, testen. Ondanks zijn brede opzet, neemt TDD de helft van dit boek in beslag - en terecht. Als je vandaag de dag professioneel programmeert en nog niet TDD't, stop dan *nu* waar je mee bezig bent en lees dit boek.


### 4. Felienne Hermans - [*The Programmer's Brain: What every programmer needs to know about cognition*](http://cleancoder.com/products)


In mijn [recensie](/blog/22/08/hoe-hersenwetenschap-programmeurs-kan-helpen/) van [Hermans'](https://www.felienne.com/) boek schreef ik:


> *The Programmer’s Brain* zit vol met (...) boeiende, door wetenschappelijk onderzoek onderbouwde observaties. Of het nu gaat over naamgeving, [de verschillende rollen die variabelen in code kunnen hebben](/blog/22/07/de-elf-rollen-van-variabelen/), of [de verschillende manieren waarop beginnende en gevorderde ontwikkelaars code lezen](/blog/22/08/hoe-review-je-eigenlijk-code/), Hermans weet op elke pagina wel een interessant inzicht uit haar hoge hoed te toveren. 
>
>(...) 
>
> De beste boeken over softwareontwikkeling, zijn de boeken die professionals in staat stellen om op een nieuwe manier naar hun vakgebied te kijken. Daar slaagt *The Programmer’s Brain* met verve in. Het boek is een absolute aanrader voor iedereen die op regelmatige basis met code werkt - of met softwareontwikkelaars. 


En om mijn werkgeheugen niet al te zeer te belasten, laat ik het daar voor nu bij :-)


### 5. Michael C. Feathers - [*Working Effectively with Legacy Code*](https://www.oreilly.com/library/view/working-effectively-with/0131177052/)


Deze klassieker van [Michael Feathers](https://michaelfeathers.silvrback.com/) is verplichte kost voor iedereen die met *legacy code* werkt. - En dat is: iedereen. Want Feathers is er glashelder over: alle code die niet door unittests wordt gedekt is *legacy code*. Hij is nu misschien nog niet verrot, maar dat is een kwestie van tijd. En om de code dan nog op de rit te krijgen, zul je [je handen vuil moeten maken](/blog/22/04/de-ontwikkelaar-als-chirurg/) - het liefst met de tips en trucs uit dit boek in het achterhoofd natuurlijk! 


## Eervolle vermeldingen


De volgende boeken verdienen een eervolle vermelding:


- Saleem Siddiqui - [*Learning Test-Driven Development: A Polyglot Guide to Writing Uncluttered Code*](https://www.oreilly.com/library/view/learning-test-driven-development/9781098106461/) [[blog](/blog/22/03/agile-en-test-driven-development/), [blog](/blog/22/04/een-test-per-keer/), [blog](/blog/22/04/to-polyglot-or-not-to-polyglot/) en [blog](/blog/22/04/legacy-code-en-test-driven-development/)]
- Vlad Khononov - [*Learning Domain-Driven Design: Aligning Software Architecture and Business Strategy*](https://www.oreilly.com/library/view/learning-domain-driven-design/9781098100124/) [[blog](/blog/22/07/zelfs-de-testpiramide-is-niet-meer-heilig/)]
- Cyrille Martraire - [*Living Documentation: Continuous Knowledge Sharing by Design*](https://www.oreilly.com/library/view/living-documentation-continuous/9780134689418/) [[blog](/blog/22/10/pull-requests-als-documentatie/)]
- Tomasz Lelek & Jon Skeet - [*Software Mistakes and Tradeoffs: How to make good programming decisions*](https://www.manning.com/books/software-mistakes-and-tradeoffs) [[blog](LINK_TEST_THIRD_PARTY_CODE)]
- Mike Cohn - [*Succeeding with Agile: Software Development Using Scrum*](https://www.oreilly.com/library/view/succeeding-with-agile/9780321660534/)
