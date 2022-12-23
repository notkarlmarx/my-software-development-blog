---
title: "De programmeur, de filosoof"
author: "Karl van Heijster"
date: 2022-12-17T21:19:41+01:00
draft: true
comments: true
tags: ["domain-driven design", "filosofie"]
summary: "We kunnen als softwareontwikkelaars veel leren van Socrates' filosofische houding. \"Ik weet dat ik niets weet\" betekent: ik neem niets aan, ik luister alleen goed naar wat de ander zegt en probeer diens standpunt zo helder mogelijk te krijgen. Ik hoor aan, parafraseer en controleer of die parafrase klopt. Voorzichtig trek ik conclusies - niet om de ander onderuit te halen, maar om te kijken of ik op de juiste weg ben, de ander begrijp. En ook: of het verhaal van de ander klopt - wat dat dan ook moge betekenen. "
---

Niet lang geleden heb ik het idee opgevat om een oude blog van me - [deze](/blog/21/08/domain-driven-design-en-ludwig-wittgenstein/) - uit te werken tot iets groters, namelijk: een blogreeks. Vooruit, een praatje misschien. Waarom? Omdat ik een jaarlijks terugkerende behoefte heb om over het leven en werk van [Ludwig Wittgenstein](https://plato.stanford.edu/entries/wittgenstein/) (1889 - 1951) te spreken - iets anders kan het niet zijn.


Hoewel ik nu (*\*bekijkt [LinkedIn](https://www.linkedin.com/in/karl-van-heijster-833503aa/)\**) ruim vijf jaar met veel plezier als softwareontwikkelaar werk, voel ik me van binnen nog altijd een filosoof. Of liever gezegd: ik heb niet het gevoel ooit op te hebben gehouden met filosoferen, de afgelopen vijf jaar. (Hoewel, eerlijk is eerlijk, het aandeel filosofieboeken op mijn leeslijst drastisch is gedaald en daar een heleboel boeken over softwareontwikkeling voor in de plek zijn gekomen.)


Ik wil opnieuw over Wittgenstein hebben en over [Doman-Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design) (DDD), omdat de twee met elkaar verbonden zijn. Je zou kunnen zeggen: het zijn individuele vertegenwoordigers van een abstracter idee, namelijk dat filosofie en softwareontwikkeling zélf met elkaar verbonden zijn.


## Socrates


Inderdaad zijn er interessante parallellen tussen beide disciplines. Ik kan dat het best illustreren met een voorbeeld - en voor dit voorbeeld tover ik maar meteen één van de grootste filosofen allertijden tevoorschijn. [Socrates](https://plato.stanford.edu/entries/socrates/) (470/469 v.Chr - 399 v.Chr) was de meest wijze man van heel Athene.[^1] Socrates wist dat hij niets wist. - Beide uitspraken blijken tegelijkertijd waar te zijn.


We kennen Socrates niet van zijn geschriften - Socrates schreef niet. Wat we weten van de filosoof, weten we dankzij zijn studenten, met name dankzij [Plato](https://plato.stanford.edu/entries/plato/) en [Xenophon](https://en.wikipedia.org/wiki/Xenophon). Deze voerden Socrates op als personage in hun - fictieve, maar op waargebeurde feiten gebaseerde - dialogen. Daardoor is het soms moeilijk om te onderscheiden tussen Socrates' opvattingen en die van zijn studenten.


Feit is dat de denker een enorme invloed had op de filosofie van zijn tijd. Vóór Socrates richtte de Klassieke filosofie zich met name op pseudo-wetenschappelijke vraagstukken, zoals: waar is de wereld van gemaakt?[^2] [Thales van Milete](https://en.wikipedia.org/wiki/Thales_of_Miletus) meende dat het water was, [Heraclitus](https://plato.stanford.edu/entries/heraclitus/) dacht aan vuur. Socrates had weinig interesse in dit soort vragen. Hij richtte zich op praktische kwesties, ethische kwesties. Met zijn komst neemt de filosofie een ethische wending.


Socrates schreef niet - hij voerde gesprekken. Dat was onderdeel van zijn filosofische methode. Middels een spel van vraag en antwoord - het socratisch gesprek -, beklommen Socrates en zijn gesprekspartners steeds nieuwe treden op de trap naar Ware Kennis. Hij vroeg zich af: wat is Kennis, wat is Rechtvaardigheid? Wat is het Goede? Zijn toehoorders zeiden dan: "Socrates, dat is een makkie. Kennis - of Rechtvaardigheid, of het Goede - is *dit* en *dat* en daarmee is de kous af." Socrates vroeg dan door. "Maar hoe zit *dit* dan, hoe zit *dat* dan?" 


## De ontwikkelaar als filosoof


Komt dat bekend voor?


Het uitvragen van requirements heeft vaak veel weg van een socratisch gesprek. De ontwikkelaar stelt een vraag - "Als ik op deze knop druk, wat moet er dan gebeuren?" - en een stakeholder antwoord: "Dat is een makkie, *dit* en *dat*." Maar als je doorvraagt, blijkt het geen makkie te zijn. Mag een gebruiker met *die* en *die* rechten ook op die knop drukken? Wat als er een foutmelding terugkomt? Kan ik tussentijds afbreken?


We kunnen als softwareontwikkelaars veel leren van Socrates' filosofische houding. "Ik weet dat ik niets weet" betekent: ik neem niets aan, ik luister alleen goed naar wat de ander zegt en probeer diens standpunt zo helder mogelijk te krijgen. Ik hoor aan, parafraseer en controleer of die parafrase klopt. Voorzichtig trek ik conclusies - niet om de ander onderuit te halen, maar om te kijken of ik op de juiste weg ben, de ander begrijp.


## Aporie


En ook: of het verhaal van de ander klopt - wat dat dan ook moge betekenen. 


Want het gebeurde niet zelden dat de stellige overtuigingen van Socrates' gesprekspartners, bij filosofische inspectie wankel bleken. Niet zelden eindigden zijn discussies in een [aporie](https://en.wikipedia.org/wiki/Aporia), een impasse.[^3] Het antwoord op de vraag naar Kennis of Rechtvaardigheid of het Goede blijkt aan het eind van het gesprek juist verder weg dan aan het begin. 


Socrates wist dat hij niets wist, omdat hij wist dat elke expert het ook niet wist.


Ook dat kan een softwareontwikkelaar gebeuren. Processen die er op papier eenvoudig uitzien, worden snel mateloos complex als ze in software worden gegoten. De werkelijkheid is altijd weerbarstiger dan het idee - en iets weten, of denken te weten, is iets heel anders dan het in de praktijk kunnen. De (ogenschijnlijk?) eenvoudige mentale modellen van domeinexperts kunnen bij bevraging een latente complexiteit te verbergen.


Een softwareontwikkelaar is niet een machine die de verhalen van domeinexperts transcribeert naar code. Een softwareontwikkelaar is een volwaardige gesprekspartner die de verhalen van domeinexperts analyseert en bevraagt. Je zou het zo kunnen zeggen: het verzamelen van requirements is een vorm van conceptuele analyse. 


## Metafoor


In geen enkele softwareontwikkelpraktijk komt die conceptuele analyse zo zeer op de voorgrond te staan als in DDD. 


Het centrale probleem dat DDD oplost, is het probleem van de Metafoor - de term is afkomstig uit [Extreme Programming](https://en.wikipedia.org/wiki/Extreme_programming) (XP) en wordt daar voluit de [*System Metaphor*](https://explainagile.com/agile/xp-extreme-programming/practices/metaphor/) genoemd. De Metafoor is het geheel aan woorden, beelden, verhalen die ontwikkelaars gebruiken om het systeem te beschrijven. 


[Robert “Uncle Bob” Martin](https://en.wikipedia.org/wiki/Robert_C._Martin) geeft in [*Clean Agile*](https://www.oreilly.com/library/view/clean-agile-back/9780135782002/) ([recensie](/blog/21/11/agile-zijn-niet-agile-doen/)) een prachtig voorbeeld. Hij gaf aan in zijn jonge jaren eens te hebben gewerkt aan een applicatie die door het team werd omschreven als een vuilniswagen. De vuilniswagen reed rond, haalde pakketjes op en verwerkte die - dat was hoe ze de *flow* en functie van de applicatie voor elkaar begrijpelijk maakten.


Het was een vreselijke Metafoor - vooral omdat het suggereerde dat de gebruikers zich de hele dag met rommel bezighielden. 


Maar het was ook de verkeerde Metafoor - want geen enkele gebruiker sprak in die termen over het systeem. Welke woorden, beelden en verhalen zij gebruikten, doet er voor het verhaal niet eens toe. Welke Metafoor gebruikers ook zou hanteren, elke keer zou het team een vertaalslag moeten maken naar hun eigen Vuilniswagenmetafoor. En elke keer als ze dat zouden doen, dan zouden ze een deel van de oorspronkelijke Metafoor verliezen, of misbegrijpen, of vervormen. Een systeem dat niet dezelfde taal spreekt als haar gebruikers, spreekt onvermijdelijk over iets anders.


## Domain-Driven Design


Dat is het centrale inzicht van DDD. De applicatie en het systeem moeten dezelfde taal spreken. Als gebruikers spreken van een "product", dan spreekt de code van "`Product`". Een "order" is een "`Order`", een "gold member" een "`GoldMember`". Als gebruikers en ontwikkelaars dezelfde taal spreken, dan zullen ze een applicatie bouwen die doet wat de gebruikers willen - en dat doet op de manier waarop gebruikers dat verwachten.


Maar woorden zijn nooit alleen woorden. Woorden en beelden hebben hun implicaties, verhalen hun eigen logica. Om met een gebruiker te kunnen spreken, moet je niet alleen dezelfde woorden gebruiken. Je moet op dezelfde manier denken. Je moet je daarvoor een [*form of life*](https://plato.stanford.edu/entries/wittgenstein/#GramFormLife) - om een term van Wittgenstein te lenen - eigen maken. Onder de woorden ligt een wereld van aannames en gebruiken - en die zijn net zo belangrijk voor het begrip als de woorden zelf.


Gebruikers, domeinexperts en ontwikkelaars moeten over hetzelfde kunnen praten - en praten. Ontwikkelaars moeten een klein beetje domeinexpert worden.


Om dat te kunnen, spelen ontwikkelaars de rol van Socrates. DDD vraagt van ontwikkelaars om een beetje filosoof te worden.





[^1]: Althans, volgens het orakel van Delphi. Maar, vonden de Atheners, die kon het weten!


[^2]: Die periode wordt tegenwoordig, niet geheel toevallig, de [presocratische periode](https://plato.stanford.edu/entries/presocratics/) genoemd.


[^3]: De aanwezigheid van een aporie wordt tegenwoordig gezien als één van de argumenten om het waarheidsgehalte van een socratische dialoog te bepalen. Dat is waarom gemeend wordt dat de vroege dialogen van Plato - die gekenmerkt worden door hun levendigheid van gesprek en het uitblijven van definitieve antwoorden - een beter beeld geven van de historische Socrates. In zijn later werk neemt het personage Socrates een meer docerende houding aan. Plato gebruikt Socrates dan als spreekbuis voor zijn eigen ideeën.
