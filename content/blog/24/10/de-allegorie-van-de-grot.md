---
title: "De allegorie van de grot"
author: "Karl van Heijster"
date: 2024-10-18T08:50:10+02:00
draft: false
comments: true
tags: ["agile ontwikkeling", "intentie van code", "filosofie", "objectgeoriënteerd programmeren"]
summary: "Plato zegt: stel je een groep mensen voor, vastgebonden -- in een grot dus. Hun hele leven lang zien ze alleen de schaduwen op de muren, van bewakers die verhalen vertellen voor een groot vuur. Die groep mensen zou denken dat de schaduwen op de muur de echte dingen zijn."
---

Wat is de allegorie van de grot?[^1] [Plato](https://plato.stanford.edu/entries/plato/ "'Plato', Stanford Encyclopedia of Philosophy") zegt: stel je een groep mensen voor, vastgebonden -- in een grot dus. Hun hele leven lang zien ze alleen de schaduwen op de muren, van bewakers die verhalen vertellen voor een groot vuur. 


Die groep mensen zou denken dat de schaduwen op de muur de echte dingen zijn. -- En we kunnen het hen niet kwalijk nemen. De mens is geneigd zijn eigen wereld voor waarheid te houden. *(Maar wij weten beter -- toch?)*


-- En stel dat we één van de gevangenen los zouden breken, en mee zouden sleuren naar de uitgang van de grot. Het zou een vreselijke worsteling zijn. Eenmaal buiten zou hij eerst naar de schaduwen van de dingen kijken en denken dat dát de werkelijkheid was. Maar naarmate zijn ogen aan het licht wenden, zag hij de werkelijkheid zoals hij echt was.


En als hij terug zou gaan naar zijn medegevangenen, zouden zij hem niet geloven. En als hij zou proberen hen te bevrijden, zou hij met vijandigheid tegemoet getreden worden.[^2] 


## Schaduwen


De schaduwen in de grot zijn niet de werkelijkheid. Ze zijn een afbeelding van een hogere werkelijkheid. (Eigenlijk zijn ze een afbeelding van een afbeelding; de tableau vivants van de bewakers worden met *beelden van* bomen, paarden etc. gemaakt.[^3])


De clou is natuurlijk: wij -- wij, mensen, stervelingen, wij zijn als de gevangenen in de grot. -- Wij zien schaduwen voor de werkelijkheid aan. -- Wij zijn vastgeketend, gedwongen tot een afgeleide werkelijkheid. *(-- En wij zullen de gevangene die is losgebroken niet geloven!)*


In Plato’s wereld zijn er twee werkelijkheden, die van de veranderlijke ervaring en die van de eeuwige Ideeën.[^4] Het is de taak van de filosoof de hogere werkelijkheid te kennen. Vandaar de vraag: hoe verhouden die werkelijkheden zich tot elkaar? 


## Paarden


In de werkelijkheid zijn er een heleboel paarden. Al die paarden zijn verschillend -- ze hebben verschillende groottes, kleur, blik in de ogen --, maar toch zijn het allemaal paarden. Dat is wat ze gemeenschappelijk hebben: ze delen in de Idee Paard (cf. ze hebben *de Vorm van Paard*).


(Maar die weergave is wellicht te statisch. Vergeet niet dat de bewakers <span style="text-decoration:underline">verhalen</span> uitbeeldden met hun tableau vivants. We lopen het risico Plato’s metafysica plat te slaan tot een dingenontologie[^5] -- maar misschien was zijn universum betekenisvol op een andere manier. *(einde bericht)*)


De Idee is wat de dingen tot de dingen maakt. De Idee legt betekenis in de wereld. Zonder Boom geen schaduw van een boom. En zoals zijn schaduw verdwijnt als de boom gekapt wordt, verdwijnt rechtvaardigheid als Rechtvaardigheid ophoudt te bestaan (cf. verdwijnt *het bos als Boom ophoudt te bestaan*).


## Objecten, classes


Als softwareontwikkelaar -- ik heb een [beroepsdeformatie](/tags/beroepsdeformatie/ "Blogs met de tag 'beroepsdeformatie'") -- deed het me denken aan objecten en classes.[^6]


Wat is een [object](https://en.wikipedia.org/wiki/Object-oriented_programming "'Object-oriented programming', Wikipedia")? Een instantiatie van een [class](https://en.wikipedia.org/wiki/Class_(computer_programming) "'Class (computer programming)', Wikipedia"). Wat is een class? De definitie van een object. Een class beschrijft welke eigenschappen (properties) en gedragingen (methods) een object kan hebben. -- Een object is een paard. Een class is een `Horse`. (Ik schreef [hier](/blog/21/07/objectgeorienteerd-denken/ "'Objectgeoriënteerd denken'"), [hier](/blog/23/01/eerlijke-domeinmodellen/ "'Eerlijke domeinmodellen'") en [hier](/blog/23/06/objectgeorienteerd-programmeren-draait-niet-om-objecten/ "'Objectgeoriënteerd programmeren draait niet om objecten'") over objectgeoriënteerd programmeren.)


In de Idee is vastgelegd hoe een ding eruitziet zoals in een class is vastgelegd hoe een object gebruikt kan worden. (-- En ik vroeg me af: interpreteer ik mijn code aan de hand van Plato of Plato aan de hand van mijn code?) 


Paard `"Betty"` (de instantiatie) kan alleen de naam Betty hebben als het ding dat haar definitie vormt (de class), een property `Name` heeft. -- En wat is `Name`? Een simpele `string`? Of heeft het zijn eigen definitie, `Name`? (Vraag je af: mag een paard een naam hebben met een cijfer erin? Of een "#"? Waarom wel of niet?) 


## Afleiding


Maar daarna dacht ik: dat is een afleidingsmanoeuvre, natuurlijk -- een illusie, een [*red herring*](https://en.wikipedia.org/wiki/Red_herring "'Red herring', Wikipedia"). Want de Idee is niet iets wat in de code bestaat -- *(viel me in een ondeelbaar moment in:)* <span style="font-variant:small-caps;">de code is de grot!</span>


Softwareontwikkelaars zitten vastgeketend aan hun bureaustoel, blik gefixeerd op scherm 2, en als 'ie nooit opkijkt loopt 'ie het risico de inhoud van de daarop afgebeelde [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment "'Integrated development environment', Wikipedia") voor waarheid aan te zien.


Als wij als softwareontwikkelaars ons blikveld vernauwen, als we ons exclusief op de code richten, dan zien we een schaduw voor de werkelijkheid aan. *(Wij, wij programmeurs zijn gevangenen in de grot!)*


Code is een schaduw, code is een model. Code is een voorstel: stel dat deze Ideeën (classes) bestaan (en dat ze zich zus of zo tot elkaar verhouden). -- Of: [Domain-Driven Design](/tags/domain-driven-design/ "Blogs met de tag 'domain-driven design'") is een oefening in het opstellen van een [ontologie](https://plato.stanford.edu/entries/logic-ontology/ "'Logic and Ontology', Stanford Encyclopedia of Philosophy"), een model van de dingen die het geval moeten zijn, wil de businesslogica een ([eventueel](https://en.wikipedia.org/wiki/Eventual_consistency "'Eventual consistency'")) consistent geheel vormen.


## Buiten de grot


Buiten de grot, dat is het werk dat je eindgebruikers doen met de applicatie die jij ontwikkelt. Dat is stakeholders die productiviteitsverbeteringen verwachten op basis van jouw werk. 


In die werkelijkheid moet de programmeur-filosoof (gevangene) zien te overleven. In het begin zal hij de codestructuren waar hij de logica in propt nog als werkelijkheid zien, maar als zijn ogen wennen aan het licht van de (business)werkelijkheid, ziet hij pas echt de waarde van zijn werk.


In de echte wereld leven betekent: zien dat je systeem verschil maakt. Feedback krijgen van echte gebruikers. Reageren op hun bevindingen. Hun gebruikerservaringen verbeteren. -- Het epitoom, kortom, van [agile ontwikkelen](/tags/agile-ontwikkeling/ "Blogs met de tag 'agile ontwikkeling'").


Dat zal dan wel vergelijkbaar zijn met Plato’s Idee van het Goede – daar hebben we het nog geeneens over gehad! -- en dat gaat ook niet gebeuren. (Of toch: vraag je eens af, hoe ziet een baseclass `Good` eruit?)


(Of: is een `object` van zichzelf al goed?)


[^1]: Ik luisterde naar de [*Very Bad Wizards*](https://verybadwizards.com/)-podcast, [een dubbelaflevering](https://verybadwizards.com/episode/episode-289-shadows-on-the-wall-platos-cave-pt-1 "'Episode 289: Shadows on the Wall (Plato's Cave Pt. 1)', Very Bad Wizards") [over Plato's allegorie van de grot](https://verybadwizards.com/episode/episode-290-blinded-by-the-light-platos-cave-pt-2 "'Episode 290: Blinded by the Light (Plato's Cave Pt. 2)', Very Bad Wizards"). Het volgende schreef ik bij ondergaande zon in de tuin.

[^2]: Het beeld doet denken aan het ideaal van een romantisch genie, denk Mozart, Van Gogh (misschien ook [Wittgenstein](/tags/wittgenstein-ludwig/ "Blogs met de tag 'Wittgenstein, Ludwig'")?).

[^3]: Na al die jaren [filosofie studeren](/blog/24/05/over-filosofie-en-software-ontwikkelen/ "'Over filosofie en software ontwikkelen'") weet ik nog steeds niet of dit feit in een interpretatie meegenomen moet worden, of dat het slechts een handig *plot device* is om dingen als bomen uit te kunnen beelden.

[^4]: Grieks: εἶδος (eîdos); in het Engels ook wel vertaald als “Forms”. Een vertaling als “Vorm” brengt interessante connecties mee, zoals de [vormelijke oorzaak](https://en.wikipedia.org/wiki/Four_causes "'Four causes', Wikipedia") van [Aristoteles](https://plato.stanford.edu/entries/aristotle/ "'Aristotle', Stanford Encyclopedia of Philosophy").

[^5]: Ja jeetje, wat betekent dat? In de woorden van [Heidegger](https://plato.stanford.edu/entries/heidegger/ "'Martin Heidegger', Stanford Encyclopedia of Philosophy") (of hoe ik me ze herinner): metafysica als de leer van de zijnden (de taxonomie van dingen die bestaan). Maar daar staat een ander soort metafysica tegenover, die van het zijn (van *de manier waarop* de zijnden zijn). Heidegger schetst het zijn van de mens, het erzijn, in zijn hoofdwerk [*Sein und Zeit*](https://en.wikipedia.org/wiki/Being_and_Time "'Being and Time', Wikipedia") (1927). (Zie ook [voetnoot 4](/blog/24/09/refactoring-en-hannah-arendt/#fn:4) van [deze blog](/blog/24/09/refactoring-en-hannah-arendt/).)

[^6]: [Barry O'Reilly](https://leanpub.com/u/barrymoreilly "Barry O'Reilly @ Leanpub") maakt hetzelfde punt in [dit uitstekende praatje](https://www.youtube.com/watch?v=H8ZOp8ayluU "'The Philosophy of Architecture - Barry O'Reilly - NDC Oslo 2024', YouTube") over filosofie en softwarearchitectuur.
