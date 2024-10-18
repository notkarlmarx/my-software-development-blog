---
title: "Is TDD alleen nuttig als iedereen het doet?"
author: "Karl van Heijster"
date: 2024-10-18T10:04:07+02:00
draft: true
comments: true
tags: ["test-driven development", "verandering"]
summary: "Het is geen geheim dat ik een liefhebber ben van Test-Driven Development. Ik schrijf er regelmatig over op dit blog, probeer mijn collega's de kneepjes van de praktijk eigen te maken, en laat het onderwerp graag ter sprake komen wanneer ik vakgenoten spreek op gebruikersgroepen of conferenties. -- Vaak krijg ik de repliek: \"Allemaal leuk en wel, dat TDD, maar dat heeft eigenlijk alleen maar zin als iedereen in het team het doet.\" Daarmee implicerend: en dat is waarom *ik* het niet doe."
---

Het is geen geheim dat ik een liefhebber ben van [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD). Ik schrijf er regelmatig over op dit blog, probeer mijn collega's de kneepjes van de praktijk eigen te maken, en laat het onderwerp graag ter sprake komen wanneer ik vakgenoten spreek op gebruikersgroepen of conferenties.


Om de aloude grap over veganisten te parafraseren: "Hoe weet je of iemand TDD't? -- Maak je geen zorgen, diegene *vertelt* je dat wel."


## Repliek


Vaak krijg ik de repliek: "Allemaal leuk en wel, dat TDD, maar dat heeft eigenlijk alleen maar zin als iedereen in het team het doet." Daarmee implicerend: en dat is waarom *ik* het niet doe.


Het is waar: de voordelen van TDD zijn het grootst wanneer iedereen in het team het doet. Dan is elk deel van de codebase [testbaar én getest](/blog/24/07/goede-code-is-geteste-code/ "'Goede code is geteste code'"), het [ontwerp](/blog/22/08/test-driven-development-is-een-ontwerpdiscipline/ "'Test-driven development is een ontwerpdiscipline'") van de code [zo simpel als nodig](/blog/24/04/test-driven-development-en-yagni/ "'Test-Driven Development en YAGNI'") en bovendien [makkelijk te refactoren](/blog/22/09/tests-als-vangnet/ "'Tests als vangnet'") als er behoefte is aan de afhandeling van complexere *use cases*.


Wanneer iedereen in een team TDD't, dan is een groene testsuite voldoende om te kunnen concluderen: de code kan uitgerold worden naar productie. (Aangenomen, uiteraard, dat ze TDD gebruiken om *hoogwaardige* tests te schrijven. Voor een schets van wat dat inhoudt, zie [deze blog](/blog/24/10/de-zen-van-testen/ "'De zen van testen'").)


## Repliek op de repliek


Maar: wanneer niet iedereen in een team TDD't, dan valt eigenlijk alleen dat laatste voordeel weg. Het is dan niet meer mogelijk om te beslissen tot een uitrol op basis van de tests *alleen*. Het is dan nodig dat er handmatig wordt nagegaan of er geen regressies zijn geïntroduceerd sinds de laatste uitrol.


De andere voordelen blijven echter bestaan -- in elk geval voor de delen van de code die met TDD zijn ontwikkeld. Die delen zullen testbaar én getest zijn, zo simpel als nodig en eenvoudig te refactoren.


Waarom zou je die voordelen teniet willen doen, alleen omdat er andere delen van de codebase bestaan die niet aan hetzelfde kwaliteitsniveau voldoen?


## Alles of niets


Het argument dat TDD alleen zin heeft als iedereen in het team het doet, valt ten prooi aan de ["alles of niets"-denkfout](https://en.wikipedia.org/wiki/Splitting_(psychology) "'Splitting (psychology)', Wikipedia"). De redenering is: "Als we niet *alle* voordelen van TDD kunnen hebben, dan kunnen we er net zo goed *geen* hebben."


Maar dat is natuurlijk onzin. Het is beter om een deel van de voordelen te hebben dan helemaal niets. Het is beter om tien of twintig of dertig procent kwalitatief hoogwaardige code in je codebase te hebben, dan nul. Natuurlijk, honderd procent zou nóg beter zijn -- maar laat het goede niet ten koste gaan van het perfecte.


Het is gekkenwerk goede gewoonten te laten varen in najaging van het perfecte. Want de goede gewoonten brengen ons daar juist dichterbij -- zelfs al is de volmaakte perfectie een ideaal dat we nooit kunnen bereiken. 


## Een gewenste conclusie


Waarom nemen zoveel mensen genoegen met zo'n overduidelijke redeneerfout? Mijn vermoeden is: omdat ze naar een gewenste conclusie toe redeneren. De vraag wordt dan: waarom wensen zoveel mensen te concluderen dat TDD geen zin heeft?


Misschien omdat ze hun programmeergewoonten niet willen aanpassen. Ze zijn tevreden met de manier waarop ze nu software ontwikkelen, en vechten ervoor die status quo te behouden. -- Misschien omdat ze slechte ervaringen hebben met TDD. Misschien hebben ze het een tijdje geprobeerd en lukte het niet en zijn ze er toen mee opgehouden. -- Of misschien hebben ze teveel overenthousiaste verhalen gehoord van mensen zoals ik. Misschien hebben dogmatici (zoals ik?) hen zodanig de lust om te TDD'en ontnomen, dat ze de hakken in het zand hebben gezet. 


En tóch geloof ik dat TDD een betere manier is om software te ontwikkelen dan testen-achteraf. Ook wanneer niet het hele team het doet.
