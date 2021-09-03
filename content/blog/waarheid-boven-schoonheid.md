---
title: "Waarheid boven schoonheid"
author: "Karl van Heijster"
date: 2021-08-11T16:41:08+02:00
draft: true
comments: true
tags: ["clean code", "filosofie", "schoonheid", "software ontwikkelen", "waarde"]
summary: "Als softwareontwikkelaars hebben we de luxe ons niet bezig te hoeven houden met de metafysische grondstructuur van de werkelijkheid, wat het ontwikkelen van onze applicaties aanzienlijk vereenvoudigt. Maar dezelfde hang naar schoonheid die ik bij filosofen zo amusant vind, duikt bij tijden ongemerkt in mijn eigen werk op."
---

Volgens [Aristoteles](https://nl.wikipedia.org/wiki/Aristoteles) zijn er [tien categorieën van zijn](https://plato.stanford.edu/entries/aristotle-categories/): (1) substantie; (2) kwantiteit; (3) kwaliteit; (4) relatie; (5) plaats; (6) tijd; (7) toestand; (8) hebben; (9) doen, en (10) ondergaan. 

[Immannuel Kant](https://nl.wikipedia.org/wiki/Immanuel_Kant) onderscheidde er [twaalf](https://plato.stanford.edu/entries/categories/#KanCon), verdeeld in vier groepen van drie: (a) kwantiteit, bestaande uit (1) algemeen, (2) bijzonder, (3) singulier; (b) kwaliteit, bestaande uit (4) bevestigend, (5) ontkennend, (6) oneindig; (b) relatie, bestaande uit (7) categorisch, (8) hypothetisch, (9) disjunctief, en ten slotte (d) modaliteit, bestaande uit (10) problematisch, (11) assertorisch, (12) apodictisch.


## Esthetische metafysica


Prachtige systemen, natuurlijk. Maar al tijdens mijn studie filosofie bekroop me een ongemakkelijk gevoel bij het idee dat de metafysische grondstructuur van de werkelijkheid zulke esthetische vormen aannam. Is het niet al te toevallig dat onze ogenschijnlijk chaotische wereld zich zo perfect liet schikken naar een rond getal bij Aristoteles, of zo'n gebalanceerde hiërarchie als bij Kant?


De vraag stellen is hem beantwoorden, natuurlijk. Hoewel beide filosofen dikke boeken aan filosofische argumentatie bij elkaar schreven om de keuze voor hun categorieën te rechtvaardigen, durf ik best te stellen dat ze zich in hun oplossing (óók) hebben laten inspireren door hun gevoel voor schoonheid. En misschien is het geen brug te ver om te stellen dat de waarheid van hun theorieën daar onder te leiden heeft gehad.


## Schoonheid en code


Als softwareontwikkelaars hebben we de luxe ons niet bezig te hoeven houden met de metafysische grondstructuur van de werkelijkheid, wat het ontwikkelen van onze applicaties aanzienlijk vereenvoudigt. Maar dezelfde hang naar schoonheid die ik bij filosofen zo amusant vind, duikt bij tijden ongemerkt in mijn eigen werk op. 


Dat gebeurt bijvoorbeeld wanneer ik twee businessentiteiten een gelijkaardige structuur wil geven. Zo'n keuze maak je om een bepaalde eenheid in je code aan te brengen, niet omdat die gelijkaardige structuur gelijkaardige zaken in de wereld reflecteert. 


Een andere zonde: soms breid ik de API van onze back-end uit met CRUD-methoden voor bepaalde objecten, ook wanneer de front-end daar (nog) geen gebruik van maakt. De symmetrie van het systeem krijgt in zo'n geval voorrang op het toevoegen van waarde.


## Voordelen


Helemaal van de pot gerukt is die praktijk niet. Symmetrisch opgezette code kan makkelijker zijn om tegenaan te programmeren. Een ontwikkelaar kan dan op basis van zijn ervaringen met eerdere objecten, voorspellen hoe deze met een nieuw object moet interacteren. Dat verhoogt zijn ontwikkelsnelheid. En CRUD-operaties zijn zo alom aanwezig in applicaties, dat het opvallend genoemd mag worden wanneer ze ergens ontbreken.


Een mooi opgezet systeem heeft niet alleen waarde in zichzelf, of zijn eigen schoonheid, het is kan ook makkelijker zijn om in te werken. En het kan je als ontwikkelaar motiveren om extra je best te doen om geen boeltje van je code te maken.


## Waarheid boven schoonheid


Maar het kan ook een valkuil zijn. Symmetrisch opgezette code kan belangrijke verschillen in functie verhullen. En CRUD-methoden die worden gebruikt, voegen niet alleen nutteloze onderhoudslast toe, ze vergroten ook het oppervlak waarop een hacker je applicatie aan kan proberen te vallen. 


Schoonheid moet geen doel op zich zijn. Wanneer deze niet binnen de perken wordt gehouden door het domein - de werkelijke wereld - dat je modelleert, heeft het de potentie om een last te worden, waar het een toevoeging had moeten zijn. Daarom: *waarheid boven schoonheid* - in de softwareontwikkeling net zozeer als in de filosofie.
