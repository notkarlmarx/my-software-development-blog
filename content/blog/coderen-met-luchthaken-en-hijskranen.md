---
title: "Coderen met luchthaken en hijskranen"
author: "Karl van Heijster"
date: 2023-08-10T21:21:13+02:00
draft: true
comments: true
tags: ["beroepsdeformatie", "boeken", "filosofie", "test-driven development"]
summary: "In mijn vakantie las ik *Darwin's Dangerous Idea* van Daniel Dennett, het boek is een aanrader. Omdat ik een beroepsdeformatie heb, deed het me aan softwareontwikkeling denken."
---

In mijn vakantie las ik [*Darwin's Dangerous Idea*](https://www.google.de/books/edition/Darwin_s_Dangerous_Idea/bn-isXoTZmUC) van [Daniel C. Dennett](https://en.wikipedia.org/wiki/Daniel_Dennett "'Daniel Dennett', Wikipedia"), het boek is een aanrader. Omdat ik een [beroepsdeformatie](/tags/beroepsdeformatie/ "Blogs met de tag 'beroepsdeformatie'") heb, deed het me aan softwareontwikkeling denken. 


## Hijskranen en luchthaken


In het bijzonder Dennetts notie van [hijskranen en luchthaken](https://en.wikipedia.org/wiki/Darwin%27s_Dangerous_Idea#Skyhooks_and_cranes "'Skyhooks and cranes' in 'Darwin's Dangerous Idea', Wikipedia") (*cranes* en *skyhooks*) deed me opveren. De filosoof kijkt naar twee soorten ontwerpstrategieën. Strategieën die uitgaan van hijskranen, bouwen een complex op door, met kleine hijskranen, steeds grotere hijskranen te doen verrijzen, waarmee je de grote brokken bij elkaar kunt brengen. Luchthaken daarentegen hang je op aan de lucht, en daar hang je dan je ontwerp aan op.[^1]


De alerte lezer zal opmerken: luchthaken zijn fysiek onmogelijk. En dat klopt, maar in het echt -- in ons denken niet. 


*Darwin's Dangerous Idea* gaat over Darwins *dangerous idea*, de [evolutietheorie](https://en.wikipedia.org/wiki/Evolution "'Evolution', Wikipedia"), en de filosofische implicaties ervan. Een zo'n implicatie is dat het complexe moet worden opgebouwd uit het eenvoudige. Er is geen scheppingsmoment, geen God die de mens kleit -- mensen en apen hebben een gemeenschappelijke voorouder, en die heeft een gemeenschappelijke voorouder met de walvis, en uiteindelijk komen we allemaal voort uit eencelligen en wat daar nog aan vooraf ging.


Darwin is radicaal: er zijn geen luchthaken, alleen hijskranen.


## Cultuur


Dat geldt voor de natuur, althans -- in de mensenwereld ligt het anders, genuanceerder. In de culturele sfeer is schepping aan de orde van de dag: als we een presentatie geven, code schrijven, een blog pennen. Waar komen die creaties vandaan? Uit ons brein, met hulp van technologie, het brein van een ander in. Maar kan de neurologie ooit een verklaring geven van hoe Kafka's *Het proces*[^2] tot stand kwam? Dat klinkt onwaarschijnlijk. 


De cultuur barst uit haar voegen van luchthaken. (Geen wonder dat Darwin op zoveel verzet stuitte.)


Het is tekenend, zegt Dennett, dat [David Hume](https://plato.stanford.edu/entries/hume/ "'David Hume', Stanford Encyclopedia of Philosophy") in zijn [*Dialogues concerning Natural Religion*](https://plato.stanford.edu/entries/hume/#PRel, "'Philosophy of Religion' in 'David Hume', Stanford Encyclopedia of Philosophy") de beste argumenten vóór de evolutietheorie formuleert van zijn tijd, maar uiteindelijk alsnog moet concluderen: en toch moet er een schepper zijn.


"Een horloge kan zichzelf niet in elkaar zetten, laat staan dat het de tijd kan tonen."


We zijn verslaafd aan luchthaken -- maar daarmee missen we het wonder van hijskranen. Daarover later meer.


## De eerste regel


We zijn verslaafd aan luchthaken, ook als we coderen. Probeer eens na te gaan: hoe komt een nieuwe feature tot stand? -- Ik heb het niet over de specificatie van de feature, laten we aannemen dat deze voldoende is uitgewerkt. Hoe vertaalt de specificatie zich tot code? Wat brengt je ertoe de eerste regel te schrijven -- de juiste folder openen, een nieuwe class aanmaken, hoe kom je aan de naam?


Hier moet wel een luchthaak in het spel zijn. Het is als het moment waarop je bewust wordt dat je bewust bent -- zodra je het denkt te hebben, ontglipt het je.


*Je begint gewoon.* (Hier ligt misschien een link met die denkfout, dat een regel een andere regel nodig heeft om correct geïnterpreteerd te worden, en die regel heeft ook weer een regel nodig, *ad infinitum*. Ik kan de referentie niet vinden ([hier](https://plato.stanford.edu/entries/rule-following/ "'Rule-Following and Intentionality', Stanford Encyclopedia of Philosophy") misschien?), maar de oplossing van het probleem ligt in die zin.)


Coderen is scheppen, en een schepping is een luchthaak.


## Vastleggen


Maar moet coderen zo zijn? -- Op fundamenteel niveau misschien wel. Maar misschien kunnen we de luchthaak iets naar beneden halen met een hijskraan. (Of de grond wat omhoog) Kunnen we het scheppingsmoment expliciet maken?


We zouden vast kunnen leggen hoe dat moment eruit ziet. 


(Eén van de redenen waarom ik van filosofie houd, is dat het invalshoeken biedt van waaruit je een bekend fenomeen als nieuw ziet. Volgens Aristoteles begint filosofie bij verwondering -- en het is precies die verwondering die filosofie teweeg brengt. Als je eenmaal begint, kom je in een opwaartse spiraal terecht.)


We zouden vast kunnen leggen hoe dat eruit ziet in een test. Een test is een hijskraan waarmee je code construeert.[^3]


## *Dit*


Hoe komt een nieuwe feature tot stand? Allereerst besluit je: de code moet *dit* doen.


Let op: dit is nog *niet* het moment waarop je je eerste test schrijft! Je schrijft, in kladblok misschien zelfs, een lijst van dingen die de code moet kunnen, wil je de nieuwe feature kunnen realiseren. Die lijst, die je tijdesn het programmeren continu blijft updaten, wordt je leidraad bij het schrijven van je tests.


Maar, eerlijk is eerlijk, daarna ga je wel gauw je eerste test schrijven. Misschien, als je heel grondig bent, dan heb je nog een diagrammetje of twee getekend, maar -- onder ons -- echt nodig is dat niet.


## Hijskranen


Je codeert de intentie van de test in haar titel: *gegeven deze conditie, wanneer dit gebeurt, zal dit het resultaat zijn* (*Given When Then*).


Je eerste regel code resulteert in een compileerfout: deze class bestaat nog niet. Je genereert om en je test is weer groen[^4] (hijskraan.) Je roept een method aan op die class. Complieerfout: method bestaat niet. Maar twee toetsenbordaanslagen later wel (hijskraan).


Je specificeert het resultaat van die *method call*. De test faalt. Je switcht van je test naar je code. De simpelste oplossing voor dit probleem is: een *hard coded value* teruggeven -- en de test is groen (hijskraan).


Code moest eerst veel domme dingen kunnen voordat het slimme dingen kan.


## De tweede regel


De volgende test breidt het bouwwerk, je code uit. Het organisme evolueert, zogezegd. 


De eerste regel van [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) is: vertel iedereen over Test-Driven Development. De tweeede regel van TDD is: wijzig nooit de functionaliteit van de code zonder eerst een test voor die wijziging te hebben geschreven.


Als je je aan die tweede regel houdt, dan lost elke nieuwe iteratie van je code één simpel probleem op. (Je aan de eerste regel houden is vooral leuk om je collega's mee te irriteren.) Je code is als een organisme dat zich staande moet zien te houden onder een steeds verder uitdijende selectiedruk. Elke nieuwe test -- of liever: elke rode test -- werpt een probleem op dat de code moet zien op te lossen, wil het overleven. 


Zo wordt het organisme, eenvoudig stapje voor eenvoudig stapje, steeds complexer en -exer.[^5]


Op meer esoterische momenten meende ik uit "domme" algoritmische wijzigingen de geboorte van betekenis te destilleren -- ik had een leuke vakantie, is wat ik bedoel te zeggen.


## Bewustzijn


Je zou willen concluderen: TDD is een hijskraan waar we systemen mee bouwen; zonder TDD verlaat je jezelf op luchthaken.


Maar zo eenvoudig is het niet. Want waar komt die eerste test vandaan? Welke gebieden in de hersenen moeten er oplichten voordat je *given, when then* hebt uitgetikt? -- En ook: en als we het weten, wat dan? Is een hersenscan überhaupt te interpreteren zonder een idee te hebben van de context waarin ze gemaakt is? -- En om die context te schetsen, verlaat je je op ideeën van een hogere orde -- betekenis, de ultieme luchthaak.


Zo komen we bij de filosofie van het bewustzijn uit. Maar die berg zal ik niet beklimmen -- gelukkig is dit maar een eenvoudig softwareontwikkelblog.


[^1]: Vgl. Wittgensteins *Philosophische Untersuchungen*: op een gegeven moment komen de verklaringen tot een eind, en begint de handeling.

[^2]: Ook gelezen, vlak vóór de vakantie, en óók een aanrader! In mijn vakantie las ik *Het slot*, en die vond ik minder goed, maar nog steeds goed.

[^3]: De metafoor is op zich niet nieuw. Tests worden vaak als documentatie omschreven -- maar een net zo vaak genoemde metafoor is die van het vangnet. "*Scaffolding*" is een andere term die die in je opkomt. <br> Het verschil met de bouwmetafoor is dat de *scaffolding* nooit van je code af komt. Zo lang het systeem in de lucht is, blijven de steigers staan. Of misschien klopt de metafoor wel, maar hebben bouwprojecten, anders dan softwareprojecten, wel een duidelijk eindpunt. (Een gebouw duurt misschien even lang om te bouwen, maar blijft veel langer staan. Software rot sneller dan beton.)

[^4]: Zo lang een test geen *asserts* bevat, is er geen conditie om te falen, en zal de test dus altijd slagen.

[^5]: Niet relevant maar wel leuk: vergelijk dit met Dennetts karakterisering van de evolutietheorie als een *algoritmisch* proces.
