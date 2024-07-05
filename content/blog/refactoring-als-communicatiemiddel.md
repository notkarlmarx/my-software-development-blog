---
title: "Refactoring als communicatiemiddel"
author: "Karl van Heijster"
date: 2024-07-05T08:05:09+02:00
draft: true
comments: true
tags: ["clean code", "communicatie", "eenvoud", "intentie van code", "refactoren", "software ontwikkelen", "zorg"]
summary: "We refactoren niet alleen om het makkelijker te maken de code te wijzigen, we refactoren ook om de code zo helder mogelijk te laten communiceren. En code die helder communiceert is op zijn beurt weer makkelijker om te wijzigen."
---

Een collega van me constateerde laatst: "Als jij een nieuwe feature toevoegt, dan besteed je veel tijd aan het [refactoren](/tags/refactoren/ "Blogs met de tag 'refactoren'") van de bestaande code. Ik heb dat zelf nog niet zo. Als ik een feature toevoeg, dan voeg ik 'm toe -- klaar."


Ik antwoordde: "Ik refactor niet omdat ik dat *leuk* vind," -- en corrigeerde mezelf onmiddellijk: "nee, dat is niet waar: ik vind refactoren *ontzettend* leuk om te doen. Dus ik refactor óók omdat ik het leuk vind. Maar ik refactor vooral omdat het daarna makkelijker is om de nieuwe feature toe te voegen, om 'm in de code te passen."


## Eerst opruimen?


Dit komt ruwweg overeen met het beeld van refactoren dat [Kent Beck](https://www.kentbeck.com/) schetst in [*Tidy First?*](https://www.oreilly.com/library/view/tidy-first/9781098151232/ "Kent Beck, 'Tidy First?: A Personal Exercise in Empirical Software Design', O'Reilly Media, 2023"). In dat boek stelt hij de vraag: moet ik de code eerst opruimen, of zal ik de feature meteen toevoegen? De inzet van die vraag is duidelijk: het eenvoudiger maken om het gedrag te wijzigen.


Maar het antwoord is natuurlijk: *it depends*. Er zit een vraagteken in de titel van Becks boek, en dat is niet voor niets. Soms is het een goed idee om eerst te refactoren, maar soms ook niet. Dat hangt af van de staat van de code, de grootte van de wijziging, de tijdsdruk waaronder deze doorgevoerd wordt, de waarde die het (*nu*) oplevert, etc..


En toch: *meestal* is het een goed idee om eerst op te ruimen. Bij twijfel is het verstandig om het zekere voor het onzekere te nemen. Want een codebase gezond houden kost nu eenmaal werk; de boel een puinhoop maken (of: laten worden) kost daarentegen alleen maar tijd.[^1] (-- Althans, zo voelt het. In werkelijkheid is het probleem een gebrek aan [zorg](/tags/zorg/ "Blogs met de tag 'zorg'"), aan aandacht voor de structuur van de code.)


## Schoonheid


Tegelijkertijd voelt het antwoord dat ik gaf incompleet aan. Ik refactor niet *altijd* om de volgende feature eenvoudiger toe te kunnen voegen. En trouwens, soms is het eenvoudiger om de feature *nu* toe te voegen. Immers, ik zie *nu* dat als ik *deze* regels code aanpas -- als ik hier en hier een extra method call invoeg --, dat de boel dan zal werken zoals bedoeld. Het refactoren van de code zou me meer tijd kosten dan de wijziging eenvoudigweg doorvoeren.


Waarom kies ik er meestal dan toch voor om toch eerst te refactoren? Ik ben geneigd te willen zeggen: omwille van de [schoonheid](/tags/schoonheid/ "Blogs met de tag 'schoonheid'") van de code -- al is dat niet helemaal wat ik wil zeggen. 


Maar het is wel waar: ongerefactorde code is vaak lelijke code. Bestaande code waar een nieuwe feature in geforceerd is, in plaats van geïntegreerd, doet zeer aan mijn ogen. Het is code die ik niet graag lees en niet graag zie in mijn codebase. -- Het is code die mijn handen doen jeuken om 'm aan te passen, op te schonen.


## Helper


Laatst kwam ik zo'n stuk code tegen (ik schreef er [hier](WAT_ZEGT_DEZE_CODE) terloops over). Een feature van ons systeem is om de data erin te kunnen exporteren naar een op [XML](https://nl.wikipedia.org/wiki/Extensible_Markup_Language "'Extensible Markup Language', Wikipedia") gebaseerd uitwisselingsformaat, genaamd [QTI](https://nl.wikipedia.org/wiki/QTI_(bestandstype) "'QTI (bestandstype)', Wikipedia"). De code om de conversie van ons eigen datamodel naar QTI te maken is flink. Sommige delen ervan zijn om door een ringetje te halen, andere zijn wat rommeliger.


Het ergst zijn de classes met `Helper` in de naam -- een [antipatroon waar ik al eerder over schreef](/blog/21/04/neem-afscheid-van-helpers/ "'Neem afscheid van helpers'"). Ik had mezelf tot doel gesteld één van die helpers op te schonen. Die class bevatte een method die een stukje XML (*x*) als input nam, deze aanpaste (*x'*) op basis van een object uit ons datamodel, en vervolgens weer teruggaf. 


De method werd op één plek gebruikt. Op die plek werd de XML gegenereerd die als input diende voor de method in de helper. Dat deed die code op basis van een ander object uit ons datamodel.


Je zou de flow van het stuk code als volgt kunnen karakteriseren: *(a -> x) & ((x, b) -> x')*. Of: *((a -> x), b) -> x'*.


## Waarom?


Er zijn twee vragen die beantwoord moeten worden rondom dit stuk code. De eerste is: is dit de beste manier om dit te doen? Het antwoord daarop is: nee. De code bevat onnodige complexiteit. We kunnen immers ook zo bij het gewenste resultaat komen: door in één keer de juiste QTI te produceren op basis van beide objecten uit het datamodel -- oftewel *(a, b) -> x'*.


De tweede vraag is interessanter. Die luidt: waarom is de code dan desondanks *zo* opgezet, met al die onnodige complexiteit? En het antwoord daarop is: het was *op het moment van schrijven* eenvoudiger om de nieuwe feature (neem het tweede object mee in het produceren van de QTI) in de code te forceren, dan om 'm te integreren. 


En daarmee bedoel ik natuurlijk: het was op dat moment *voor de ontwikkelaar in kwestie* eenvoudiger om het zo te doen. Bijvoorbeeld omdat hij op dat moment geen andere manier zag. Misschien omdat 'ie het niet aandurde de code te refactoren. Misschien omdat die optie geeneens in 'm opkwam. Misschien omdat 'ie dacht: als het werkt dan werkt het, en dan is het goed.


## Vanzelfsprekend


De code zoals deze stond, deed verslag van de manier waarop ze tot stand was gekomen. Wie de code las, zag dat *x* oorspronkelijk op basis van *a* werd geproduceerd. En dat de wens om *b* daarin mee te nemen pas later naar boven was gekomen.[^2]


En *dat* is precies wat mijn handen doet jeuken om te refactoren. Want code hoort niet te zeggen: dit is hoe ik tot stand ben gekomen. Goede code leest alsof ze volstrekt vanzelfsprekend is, ze ziet eruit alsof ze er altijd zo uit heeft gezien. -- Dat is wat ik probeerde te zeggen toen ik sprak over schoonheid.


Goede code communiceert *alleen* de inhoud van het probleem en de oplossing. Goede code communiceert *niet* hoe ons begrip van de het probleem door de tijd heen is veranderd, en hoe onze oplossing tot stand is gekomen.


(Natuurlijk betekent dat niet dat zulke code geen enkele plek heeft in een codebase -- soms ontkom je er zelfs niet aan. De databasemigratiescripts die wij in versiebeheer hebben, doen keurig verslag van de manier waarop dat deel van onze code is geëvolueerd. Maar, en dat is het belangrijke punt, het datamodel zoals het er nu uitziet, zou eruit moeten zien alsof het altijd zo is geweest.)


## Communiceren


De schoonheid van code zit 'm in de helderheid waarmee ze een idee communiceert -- en dat betekent dat ze *alleen* dat ene idee uitdrukt. Om code in die staat te krijgen, is het nodig om continu te refactoren.


We refactoren niet alleen om het makkelijker te maken de code te wijzigen, we refactoren ook om de code zo helder mogelijk te laten communiceren. En code die helder communiceert is op zijn beurt weer makkelijker om te wijzigen.


[^1]: Op [Joy of Coding](https://joyofcoding.org/) zat ik op de eerste rij toen [Kevlin Henney](http://kevlin.tel/) een fantastisch praatje ([klik hier](https://www.youtube.com/watch?v=NMPeAW2RWdc "Refactoring Is Not Just Clickbait - Kevlin Henney - NDC London 2023") voor een versie daarvan) gaf over dit onderwerp. Na afloop stond 'ie ineens naast me en bracht ik prompt mijn bewondering voor 'm over. Wat Henney zo fascinerend maakt om te horen spreken, is dat zijn praatjes geen oplossing presenteren, maar een probleem verhelderen.

[^2]: Dat wil zeggen, wie de code *vanuit een bepaalde invalshoek* leest, zal die informatie eruit weten te destilleren. [Codefluisteren](/blog/23/12/codefluisteren/ "'Codefluisteren'") is een vaardigheid die niet in iedereen even goed ontwikkeld is. Ook Henney spreekt in sommige van zijn praatjes over softwareontwikkeling als een vorm van archeologie.
