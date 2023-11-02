---
title: "Pseudofilosofische onderzoekingen (I & II)"
author: "Karl van Heijster"
date: 2023-09-22T07:54:36+02:00
draft: false
comments: true
tags: ["bloggen", "domain-driven design", "filosofie", "leren", "Wittgenstein, Ludwig"]
summary: "Ik ga vandaag geen blog schrijven. Ik zal genoegen nemen met enkele aantekeningen die ik maanden geleden op papier zette, geïnspireerd door Marcus Aurelius en door Ludwig Wittgenstein. Het spreekt voor zich dat mijn overpeinzingen beduidend minder diepzinnig zijn dan die van beide grootheden."
---

Het is -- op het moment van schrijven -- de laatste dag voor aanvang van mijn vakantie (-- op het moment dat je dit leest ben ik al lang en breed en uitgerust terug aan het werk). De eerlijkheid gebiedt me te zeggen dat mijn hoofd bij zon is, en zee en strand en bier.


Ik ga vandaag geen blog schrijven -- ook zulke dagen zitten er tussen. Ik zal genoegen nemen met enkele aantekeningen die ik maanden geleden op papier zette, geïnspireerd door [Marcus Aurelius](https://plato.stanford.edu/entries/marcus-aurelius/ "'Marcus Aurelius', Stanford Encyclopedia of Philosophy") en door [Ludwig Wittgenstein](https://plato.stanford.edu/entries/wittgenstein/ "'Ludwig Wittgenstein', Stanford Encyclopedia of Philosophy") (zie respectievelijk [deze blog](/blog/23/08/overpeinzingen-over-vakmanschap/ "'Overpeinzingen (over vakmanschap)'") en [deze blog](/blog/21/08/domain-driven-design-en-ludwig-wittgenstein/ "'Domain-Driven Design en Ludwig Wittgenstein'")).


Het spreekt voor zich dat mijn overpeinzingen beduidend minder diepzinnig zijn dan die van beide grootheden.


Fijne vakantie, iedereen!


---


## Over bloggen


Het doel van een blog is niet -- of: niet alleen -- een ander iets te leren, maar om orde te scheppen in de eigen gedachten.


Een blog is geslaagd als het een accuraat beeld geeft van het huidige begrip. Daarom berust een uitspraak als "ik weet er niet genoeg van om erover te schrijven" op een misvatting.


Het niet weten (er niet genoeg van weten) is de een noodzakelijke voorwaarde om te kunnen leren. En weten dat je iets niet weet -- je van je eigen beperkingen bewust zijn -- is een van de verstandigste dingen die je kunt doen.


Juist *omdat* je er nog niet genoeg van weet, schrijf je erover. Als je het al zou weten, zou er niets over te schrijven zijn. Een blog wordt dan een klus.


Een blog is pas interessant als deze deel is van een zoektocht.


Een blog zit er soms ook naast -- moet er soms ook naast zitten. Dan generaliseert deze te veel, of wordt het detail voor een hoofdlijn aangezien.


Met fouten breng je een goed idee in kaart.


Vraag jezelf af: onder welke omstandigheden klopt dit niet, gaat dit niet op? Een idee kent altijd een context.


Een idee bewijst zich in gedachten en de praktijk – en soms in die volgorde.


Denk, als je *writer's block* hebt: geen enkele blog is te mager om te publiceren -- het proces is belangrijker dan de uitkomst. *[Dit is geen rechtvaardiging voor je luiheid, Karl!]*


---


## Over *ubiquitous language*


"Maar taal is ambigu!" -- Dat klopt, soms. Het is eerder: taal kan ambigu zijn. Merk op dat je domeinexperts zonder problemen over “producten” kunnen spreken. Blijkbaar ervaren zij de term niet als ambigu.


Vraag jezelf af: is de term ambigu, of suggereert ons begrip van de term een ambiguïteit? -- Het is een open vraag of die ambiguïteit in het echt bestaat of slechts in ons begrip.


Als je zegt: jullie zeggen steeds "product", maar eigenlijk bedoelen jullie "order product" en "shipping product" (wat dat ook moge betekenen), dan ben je een erfgenaam van de vroege Wittgenstein. -- Er is een vroege Wittgenstein en een late Wittgenstein, Wittgenstein I en II respectievelijk (zo worden ze in de literatuur genoemd). 


Wittgenstein I stelt zichzelf in de [*Tractatus Logico-Philosophicus*](https://www.gutenberg.org/files/5740/5740-pdf.pdf "Ludwig Wittgenstein, 'Tractatus Logico-Philosophicus' (PDF)"), dat is zijn eerste meesterwerk, hij stelt zich in dat eerste werk een tamelijk ambitieus doel: alle filosofische problemen oplossen. Allemaal. (Hij is net als ons, vind je niet?) Dat doet hij door de taal te analyseren, te ontleden in haar logische vorm. Wittgenstein beschrijft welke vorm taal moet hebben om te kunnen functioneren -- en dat is een logische vorm. 


De logica was in die tijd een nieuw leven ingeblazen door het werk van logicus en filosoof [Gottlob Frege](https://plato.stanford.edu/entries/frege/ "'Gottlob Frege', Stanford Encyclopedia of Philosophy"). Hij had een [logische notatie](https://en.wikipedia.org/wiki/Begriffsschrift "'Begriffsschrift', Wikipedia") ontwikkeld waarvan sommigen dachten dat deze de ware aard van ons dagelijks taalgebruik kon tonen. Want aan de oppervlakte is onze taal misleidend. 


Neem de zin "De huidige koning van Frankrijk is kaal." Niet waar, toch? Want er is helemaal geen huidige koning van Frankrijk. -- Maar wacht even. Als er geen huidige koning van Frankrijk is, hoe kan die dan niet kaal zijn? Het is alsof je deze code ziet: `PresentKingOfFrance.IsBald` – dit is `false`, maar hoe? – deze code gooit geen `NullReferenceException`. Dat komt omdat je, logisch bezien, iets heel anders zegt. Eigenlijk zeg je dit: Er is een individu *x* waarvoor geldt dat *x* is de huidige koning van Frankrijk en *x* is kaal en… *[[opzoeken]](https://plato.stanford.edu/entries/descriptions/#RusTheDes "'Russell's Theory of Descriptions' in 'Descriptions', Stanford Encyclopedia of Philosophy")*. 


De logische vorm, de dieptestructuur, is anders dan de zin aan de oppervlakte, dan de oppervlaktestructuur doet vermoeden: *-- jullie zeggen wel "product", maar jullie bedoelen eigenlijk "order product" en "shipping product"*.


Deze aanpak werkt… enigszins. Althans, hij heeft zo zijn voordelen. Je code respecteert het [Single-Responsiblity Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle "'Single-responsibility principle', Wikipedia") (SRP) bijvoorbeeld weer, dat is goed. Maar software ontwikkelen is trade-offs afwegen, dus vraag jezelf af: tegen welke prijs? 


De code en de domeinexperts spreken niet meer dezelfde taal. Je code spiegelt het domein niet meer, je bent een nieuwe [*System Metaphor*](https://wiki.c2.com/?SystemMetaphor "'System Metaphor', C2 Wiki") aan het ontwikkelen -- eentje die veel wegheeft van wat de domeinexperts zeggen, dat wel (nu nog), maar inmiddels wel is geschreven in een taal waar je een vertaaltabel bij nodig hebt. 


Een mentale vertaaltabel, zul je misschien zeggen, maar voor het voorbeeld is het goed om dat expliciet te maken: stel je een concrete vertaaltabel voor tussen de termen in je code en de termen die door de experts gebezigd worden (cf. [PI](https://edisciplinas.usp.br/pluginfile.php/4294631/mod_resource/content/0/Ludwig%20Wittgenstein%2C%20P.%20M.%20S.%20Hacker%2C%20Joachim%20Schulte.%20Philosophical%20Investigations.%20Wiley.pdf "Ludwig Wittgenstein, 'Philosophical Investigations' (PDF)") #1). Je hebt geen *ubiquitous language* meer, nu. Je bent geen DDD meer aan het beoefenen.


Dit is de uitdaging: een domein modelleren dat (1) het SRP respecteert én (2) de taal van de experts spiegelt. 
