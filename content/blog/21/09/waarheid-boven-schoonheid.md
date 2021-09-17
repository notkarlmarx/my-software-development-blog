---
title: "Waarheid boven schoonheid"
author: "Karl van Heijster"
date: 2021-09-17T08:20:55+02:00
draft: false
comments: true
tags: ["clean code", "filosofie", "schoonheid", "software ontwikkelen", "waarde"]
summary: "Anders dan Aristoteles, Kant en Wittgenstein, hebben we als softwareontwikkelaars de luxe ons niet bezig te hoeven houden met de metafysische grondstructuur van de werkelijkheid. Dat vereenvoudigt het ontwikkelen van onze applicaties aanzienlijk. Maar dezelfde hang naar schoonheid die ik bij filosofen zo amusant vind, duikt bij tijden ongemerkt in mijn eigen werk op. "
---

Volgens [Aristoteles](https://nl.wikipedia.org/wiki/Aristoteles) zijn er [tien categorieën van zijn](https://plato.stanford.edu/entries/aristotle-categories/): (1) substantie; (2) kwantiteit; (3) kwaliteit; (4) relatie; (5) plaats; (6) tijd; (7) toestand; (8) hebben; (9) doen, en (10) ondergaan. 

[Immannuel Kant](https://nl.wikipedia.org/wiki/Immanuel_Kant) onderscheidde er [twaalf](https://plato.stanford.edu/entries/categories/#KanCon), verdeeld in vier groepen van drie: (a) kwantiteit, bestaande uit (1) algemeen, (2) bijzonder, (3) singulier; (b) kwaliteit, bestaande uit (4) bevestigend, (5) ontkennend, (6) oneindig; (c) relatie, bestaande uit (7) categorisch, (8) hypothetisch, (9) disjunctief, en ten slotte (d) modaliteit, bestaande uit (10) problematisch, (11) assertorisch, (12) apodictisch.


[Ludwig Wittgenstein](https://nl.wikipedia.org/wiki/Ludwig_Wittgenstein) zette er in zijn [vroege periode](https://plato.stanford.edu/entries/wittgenstein/#EarlWitt) behoorlijk de schaar in. Volgens hem bestond de wereld uit feiten, en waren feiten niets meer dan combinaties van objecten. Maar belangrijker nog, volgens hem was het onmogelijk om op metafysisch niveau over de wereld te spreken (behalve blijkbaar in een [reeks genummerde aforismen](https://www.gutenberg.org/files/5740/5740-pdf.pdf)). 


## Esthetische metafysica


Prachtige systemen, natuurlijk. Maar al tijdens mijn studie filosofie bekroop me een ongemakkelijk gevoel bij het idee dat de metafysische grondstructuur van de werkelijkheid zulke esthetisch plezierige vormen aannam. Is het niet al te toevallig dat onze ogenschijnlijk chaotische wereld zich zo perfect liet schikken naar een rond getal bij Aristoteles, zo'n gebalanceerde hiërarchie als bij Kant, of zo'n eenvoudige taxonomie als bij Wittgenstein?


De vraag stellen is hem beantwoorden, natuurlijk. Aristoteles en Kant schreven dikke boeken aan filosofische argumentatie bij elkaar om de keuze voor hun systemen te rechtvaardigen; Wittgenstein was wat spaarzamer met zijn woorden. Toch durf ik best te stellen dat ze zich in hun oplossing (óók) hebben laten inspireren door hun gevoel voor schoonheid. En misschien is het geen brug te ver om te stellen dat de waarheid van hun theorieën daar onder te leiden heeft gehad.


## Schoonheid en code


Anders dan Aristoteles, Kant en Wittgenstein, hebben we als softwareontwikkelaars de luxe ons niet bezig te hoeven houden met de metafysische grondstructuur van de werkelijkheid. (Al voelt dat soms wel zo. De metafysicie van weleer weten niet hoe goed ze het hadden zich niet bezig te hoeven houden met de processen die de business soms bij elkaar verzint!) Dat vereenvoudigt het ontwikkelen van onze applicaties aanzienlijk. Maar dezelfde hang naar schoonheid die ik bij filosofen zo amusant vind, duikt bij tijden ongemerkt in mijn eigen werk op. 


Dat gebeurt bijvoorbeeld wanneer ik twee businessentiteiten een gelijkaardige structuur wil geven. Zo'n keuze maak je om een bepaalde eenheid in je code aan te brengen, niet omdat die gelijkaardige structuur gelijkaardige zaken in de wereld reflecteert. Een andere zonde: soms breid ik de API van onze back-end uit met [CRUD](https://nl.wikipedia.org/wiki/CRUD)-methoden voor bepaalde objecten, ook wanneer de front-end daar (nog) geen gebruik van maakt. De symmetrie van het systeem krijgt in zo'n geval voorrang op het toevoegen van waarde.


## Voordelen


Helemaal van de pot gerukt is die praktijk niet. Symmetrisch opgezette code kan makkelijker zijn om tegenaan te programmeren. Een ontwikkelaar kan dan op basis van zijn ervaringen met eerdere objecten, voorspellen hoe deze met een nieuw object moet interacteren. Dat verhoogt zijn ontwikkelsnelheid. En CRUD-operaties zijn zo alom aanwezig in applicaties, dat het opvallend genoemd mag worden wanneer ze ergens ontbreken.


Een mooi opgezet systeem heeft niet alleen waarde in zichzelf, of in zijn eigen schoonheid, het kan ook makkelijker zijn om mee te werken. En het kan je als ontwikkelaar motiveren om extra je best te doen om geen boeltje van je code te maken. Lelijke code daarentegen verslonst haast vanzelf.


## Waarheid boven schoonheid


Maar het kan ook een valkuil zijn. Symmetrisch opgezette code kan belangrijke verschillen in functie verhullen. Aan het eind van de dag moeten businessoverwegingen doorslaggevend zijn in de opzet van je model. En CRUD-methoden die niet worden gebruikt, voegen niet alleen nutteloze onderhoudslast toe, ze vergroten ook het oppervlak waarop een hacker je applicatie aan kan proberen te vallen. 


Schoonheid moet geen doel op zich zijn. Wanneer deze niet binnen de perken wordt gehouden door het domein - de werkelijke wereld - dat je modelleert, heeft het de potentie om een last te worden, in plaats van van toegevoegde waarde te zijn. Daarom: *waarheid boven schoonheid* - in de softwareontwikkeling net zozeer als in de filosofie. 


Wellicht prefereer ik daarom het meest van al de [latere filosofie](https://plato.stanford.edu/entries/wittgenstein/#LateWitt) van Wittgenstein. Daarin doorgrondt hij de aard van taal en werkelijkheid in een ogenschijnlijke chaos die haar onderwerpen recht doet. Maar hoe chaotisch softwareontwikkeling soms ook mag zijn, tóch houd ik mijn eigen code liever iets schoner dan dat.
