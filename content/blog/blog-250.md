---
title: "Blog #250!"
author: "Karl van Heijster"
date: 2024-04-19T13:14:11+02:00
draft: true
comments: true
tags: ["code reviews", "dotkarl", "filosofie", "functioneel programmeren", "intentie van code", "refactoren", "testen"]
summary: "Jeetje, ik blog alweer een tijdje! Er zijn 767 dagen voorbij gegaan sinds ik mijn honderdste blog schreef. Dus: feest! Vandaag blik ik terug op de laatste 150 blogs."
---

Jeetje, ik blog alweer een tijdje! Er zijn 767 dagen voorbij gegaan sinds ik [mijn honderdste blog](/blog/22/03/blog-100/ "'Blog #100!'") schreef. Dus: feest! Vandaag blik ik terug op de laatste 150 blogs.


## Ontwerp


De laatste tijd ben ik me op [ontwerpintuïties](/blog/23/12/codefluisteren/ "'Codefluisteren'") aan het richten. Het zijn reflecties op het nut en de schoonheid van verschillende manieren om code te structureren. De manier waarop we onze [Controllers dom hielden](/blog/24/03/hoe-we-onze-controllers-dom-hielden/ "'Hoe we onze Controllers dom hielden'") en [houden](/blog/24/04/hoe-we-onze-controllers-dom-houden/ "'Hoe we onze Controllers dom houden'") onderzocht ik als *case study*, het is een synthese van enkele van de inzichten die ik in de jaren op heb gedaan over ontwerp.


Een centraal idee achter dit thema is dat we als [vakmensen](/blog/23/08/overpeinzingen-over-vakmanschap/ "'Overpeinzingen (over vakmanschap)'") geen genoegen hoeven te nemen met moeilijke, lelijke code. -- Nee, we *mogen* er geen genoegen mee nemen. Daarom is het belangrijk om in [de verschillen tussen overerving en compositie met *dependency injection*](/blog/24/01/overerving-compositie-en-dependency-injection/ "'Overerving, compositie en dependency injection'") te duiken, en te mijmeren over de schoonheid van [symmetrische tegenover asymmetrische overerving](/blog/24/01/symmetrische-en-asymmetrische-overerving/ "'Symmetrische en asymmetrische overerving'") 


De kwaliteit (gebruiksgemak, schoonheid -- eenvoud, onderhoudbaarheid etc.) van onze code is onze verantwoordelijkheid. En die verantwoordelijkheid kunnen we alleen nemen als we onze ontwerpintuïties kunnen expliciteren, als we een ander uit kunnen leggen wat de voor- en nadelen van het ene ontwerp zijn tegenover het andere. Want alleen zo kan die ander onze ontwerpen kritisch bejegenen en verbeteren.


## Functioneel programmeren


Ik schuwde daarbij niet om over de grenzen van het objectgeoriënteerde paradigma te kijken. [Functioneel programmeren](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'") was voor mij de openbaring van het afgelopen jaar. Ik schreef over [functors](/blog/22/10/wat-is-een-functor/ "'Wat is een functor?'") en [monaden](/blog/22/12/wat-is-een-monad/ "'Wat is een monad?'") (waaronder [Options](/blog/22/08/spelen-met-options/ "'Spelen met Options'")), [het verschil tussen `.Select` en `.ForEach`](/blog/22/10/de-foreach-aan-het-eind-van-je-functieketen/ "'De ForEach aan het eind van je functieketen'") en ook [over `.Aggregate`](/blog/23/03/foreach-aggregate-en-select/ "'ForEach, Aggregate en Select'"), over [eerlijke functies](/blog/22/07/wat-zijn-eerlijke-functies/ "'Wat zijn eerlijke functies?'") (en [modellen](/blog/23/01/eerlijke-domeinmodellen/ "'Eerlijke domeinmodellen'")) en [*callback hell*](/blog/24/02/callback-hell/ "'Callback hell'").


Functioneel programmeren heeft mijn code eenvoudiger gemaakt, robuuster, descriptiever en eleganter. De vragen die ik me tegenwoordig stel als ik een stuk code voor mijn neus krijg, zijn niet meer dezelfde als vroeger. -- Ik ben gegroeid als ontwikkelaar (je kunt erover twisten of het de juiste kant op was).


Boven alles ben ik [Enrico Buonanno](https://medium.com/@enrico.buonanno) dank verschuldigd, zijn [*Functional Programming in C#*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition) (mijn [favoriete boek van 2022](/blog/22/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2022-las/ "'De beste boeken over software ontwikkeling die ik in 2022 las'")) heeft mijn manier van code schrijven voorgoed veranderd. ([Simon Painters](https://www.thecodepainter.co.uk/) [*Functional Programming with C#*](https://www.oreilly.com/library/view/functional-programming-with/9781492097068/) is ook leuk!) Ik pak het boek nog regelmatig uit de kast als ik mijn functionele vaardigheden wil slijpen.


## Testen


Maar codekwaliteit houdt niet op bij de grenzen van de code zelf, in welke stijl die ook geschreven is. Dat wat om de code ("dé code") heen gebeurt is net zo belangrijk. -- Mijn collega's zullen het onderhand wel moe zijn me over geautomatiseerd [testen](/tags/testen/ "Blogs met de tag 'testen'") te horen praten. 


Want erover praten deed ik. [Mijn honderdenéénste blog](/blog/22/03/agile-en-test-driven-development/ "'Agile en Test-Driven Development'") ging over [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'"), en [er](/blog/22/04/een-test-per-keer/ "'Eén test per keer'") [volgden](/blog/22/04/legacy-code-en-test-driven-development/ "'Legacy code en Test-Driven Development'") [er](/blog/22/05/nog-een-reden-om-testgedreven-te-ontwikkelen/ "'Nóg een reden om testgedreven te ontwikkelen'") [nog](/blog/22/06/mijn-eerste-testgedreven-stapjes/ "'Mijn eerste testgedreven stapjes'") [velen](/blog/22/08/test-driven-development-is-een-ontwerpdiscipline/ "'Test-driven development is een ontwerpdiscipline'"). TDD is een idee dat tegelijkertijd simpel en diep is. De basis leer je in vijf minuten, maar er meester in worden duurt jaren.


Ook voor de rol en inhoud van mijn tests was er uitgebreide aandacht. Ik schreef over [tests als documentatie](/blog/22/09/tests-als-documentatie/ "'Tests als documentatie'"), [vangnet](/blog/22/09/tests-als-vangnet/ "'Tests als vangnet'") en [ontwerpmiddel](/blog/22/09/tests-als-ontwerpmiddel/ "'Tests als ontwerpmiddel'"); [testscope](/blog/22/06/testen-via-de-voordeur/ "'Testen via de voordeur'") (ook [hier](/blog/22/11/test-het-systeem-niet-de-class/ "'Test het systeem, niet de class'") en [hier](/blog/22/12/tests-zijn-specs/ "'Tests zijn specs'")), [de unit in unit tests](http://blog/22/11/wat-is-een-unit/ "'Wat is een unit?'"), [testpiramides en -diamanten](/blog/22/07/zelfs-de-testpiramide-is-niet-meer-heilig/ "'Zelfs de testpiramide is niet meer heilig!'"), [het structureren van testclasses](/blog/22/12/over-de-volgorde-van-je-unit-tests/ "'Over de volgorde van je unit tests'"), [codeduplicatie in tests](/blog/23/02/waarom-dry-waarom-damp/ "'Waarom DRY? Waarom DAMP?'"), [het gebruik van productiedata](/blog/23/03/testen-met-productiedata/ "'Testen met productiedata'") -- de lijst gaat maar door en door.


Een deel van die inzichten bundelde ik in [*Altijd up to date documentatie met maximaal descriptieve tests*](/talks/altijd-up-to-date-documentatie-met-maximaal-descriptieve-tests/ "'Altijd up to date documentatie met maximaal descriptieve tests'"), een presentatie die ik met veel plezier op verschillende gelegenheden heb mogen geven. De tijd is mijn grootste vijand bij dit praatje -- er is genoeg materiaal om een collegereeks mee te vullen.


## Code review


De noodzaak van al dat gezwam over tests bleek [toen enkele van mijn collega's die praktijk lieten vallen](/blog/23/04/tijdreis/ "'Tijdreis'") en ze de waardevolle les leerden dat [het niet jouw verantwoordelijkheid is een onmogelijke deadline te halen](/blog/23/05/het-is-niet-jouw-verantwoordelijkheid-een-onmogelijke-deadline-te-halen/ "'Het is niet jouw verantwoordelijkheid een onmogelijke deadline te halen'") (en al helemaal niet door op kwaliteit te bezuinigen!). 


Het deed me mijn blik op [*pull requests*](/tags/pull-requests/ "Blogs met de tag 'pull requests'") (PR's) en [code reviews](/tags/code-reviews/ "Blogs met de tag 'code reviews'") richten. [We maakten onze tester een verplichte reviewer](/blog/23/07/de-tester-als-code-reviewer/ "'De tester als code reviewer'") en dat deed me denken aan [mijn eigen eerste code review](/blog/23/08/mijn-eerste-code-review/ "'Mijn eerste code review'"). Het wierp vragen op over [hoe je PR's -- en dus code -- eigenlijk leest](/blog/23/09/drie-vragen-die-elk-pull-request-moet-beantwoorden/ "'Drie vragen die elk pull request moet beantwoorden'") (ook in [deze](/blog/23/10/nog-enkele-reflecties-op-pull-requests/ "'Nog enkele reflecties op pull requests'") en [deze blog](/blog/23/11/waarom-wat-en-hoe/ "'Waarom, wat en hoe'")). En ook daar [vertelde](/talks/de-edele-kunst-van-het-pull-request/ "'De edele kunst van het pull request'") ik weer over op diverse gelegenheden.


Goed ontworpen code kan alleen gedijen in een goedaardige omgeving. Tests en (continue) code reviews zijn noodzakelijke voorwaarden voor het creëren van zo'n omgeving.


## Refactoren


Daarbij is het belangrijk om je te realiseren dat goed ontworpen code nooit -- ineens opduikt, ook niet in een ideale omgeving. Softwareontwikkeling is een empirische discipline: je probeert iets, inspecteert het resultaat, en past je code daarop aan. Die aanpassing kan -- nee, moet -- een wijziging in het ontwerp inhouden.


Ik heb op refactoren gereflecteerd [aan de hand van afwas](/blog/22/09/over-afwas-en-software/ "'Over afwas en software'"), [Tolstoj](/blog/22/05/refactoren-na-tolstoj/ "'Refactoren na Tolstoj'") en [chirurgie](/blog/22/04/de-ontwikkelaar-als-chirurg/ "'De ontwikkelaar als chirurg'"). Ik onderscheidde [twee stijlen van refactoren](/blog/22/08/twee-stijlen-van-refactoren/ "'Twee stijlen van refactoren'"), [dupliceerde methods (tijdelijk!)](/blog/23/07/waarom-ik-die-method-dupliceer/ "'Waarom ik die method dupliceer'") en [scheidde data ophalen van data manipuleren](/blog/22/08/scheid-data-ophalen-van-data-manipuleren/ "'Scheid data ophalen van data manipuleren'"). Het nauwgezet bekijken van je eigen refactorslagen zet je eigen verhouding tot je code op scherp.


Mijn mening over wat refactoren *is*, is in de loop der jaren veranderd. Vroeger zag ik het als het moment waarop je de ontwikkeling van nieuwe features officieel stilzette om je code grootscheeps onder handen te nemen. Tegenwoordig wordt elke wijziging die ik in een codebase doe omkranst door kleine refactorslagen: het herstructureren van een class of method voordat ik nieuwe functionaliteit toevoeg, het opruimen van de rommel die ik noodzakelijkerwijs maak wanneer die nieuwe functionaliteit vorm krijgt. Het leidde tot [een herwaardering](/blog/24/02/een-herwaardering-van-fowlers-refactoring/ "'Een herwaardering van Fowlers Refactoring'") van [Martin Fowlers](https://martinfowler.com/).


## Filosofie


Er werd ook [filosofisch](/tags/filosofie/ "Blogs met de tag 'filosofie'") op ontwerp gereflecteerd. Ik begon [mijn honderste blog](/blog/22/03/blog-100/ "'Blog #100!'") met wat gedachten over [Domain-Driven Design en Ludwig Wittgenstein](/blog/21/08/domain-driven-design-en-ludwig-wittgenstein/ "'Domain-Driven Design en Ludwig Wittgenstein'"). Het lijkt me passend om dit overzicht van de afgelopen 150 blogs af te sluiten in diezelfde hoek. 


De Wittgensteinbibliotheek is sindsdien aangevuld met [pseudofilosfische onderzoekingen](/blog/23/09/pseudofilosofische-onderzoekingen-i-en-ii/ "'Pseudofilosofische onderzoekingen (I & II)'") en een [logisch-filosofische *Abhandlung*](/blog/23/12/logisch-filosofische-verhandeling/ "'Logisch-filosofische verhandeling'"). Ik schreef daarnaast over het werk van (de [vorige week helaas overleden](https://nos.nl/artikel/2517489-amerikaanse-filosoof-en-uitgesproken-atheist-daniel-dennett-82-overleden "'Amerikaanse filosoof en uitgesproken atheïst Daniel Dennett (82) overleden', NOS")) [Daniel Dennett](https://en.wikipedia.org/wiki/Daniel_Dennett "'Daniel Dennett', Wikipedia") over evolutie. In die kruisbestuiving schreef ik over [evolutionair programmeren](/blog/23/10/evolutionair-programmeren/ "'Evolutionair programmeren'") en [luchthaken en hijskranen](/blog/23/09/coderen-met-luchthaken-en-hijskranen/ "'Coderen met luchthaken en hijskranen'"). Ik weet niet zeker of het overal filosofisch hout snijdt, maar het was een leuke intellectuele oefening.


Ook vakinhoudelijk was er ruimte voor fundamentele reflectie. Van [Anjana Vakil](https://anjana.dev/) leerde ik dat [objectgeoriënteerde code niet om objecten draait](/blog/23/06/objectgeorienteerd-programmeren-draait-niet-om-objecten/ "'Objectgeoriënteerd programmeren draait niet om objecten'"). Denk daar maar eens over na!


## Het goed doen


Code ontwerpen, testen, beoordelen, schrijven en herschrijven (maar niet per se in die volgorde) en daar dan weer op reflecteren (en soms [een nummer van Bob Dylan coderen](/blog/23/06/ode-aan-bod-dylan/ "'Ode aan Bob Dylan'")) -- het zijn de hoofdingrediënten van de afgelopen twee jaar *dotkarl*. 


Ik heb me in die tijd wel eens afgevraagd wat het is wat me drijft al die woorden aan elkaar te rijgen. Een antwoord waar ik mee kon leven was: "Om antwoord te krijgen op de vraag: hoe doe ik het *goed*?" Mijn gevoel zegt me dat ik de afgelopen jaren iets dichter bij dat doel ben gekomen.


-- Dus: op naar #500!
