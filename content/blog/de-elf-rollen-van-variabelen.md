---
title: "De elf rollen van variabelen"
author: "Karl van Heijster"
date: 2022-06-17T07:39:28+02:00
draft: true
comments: true
tags: ["boeken", "clean code", "code reviews", "intentie van code", "ontwerppatronen", "variabelen"]
summary: "Pas wanneer de vanzelfsprekendheid van code in het geding komt, gaan we nadenken - écht nadenken - over wat er op je scherm staat en waarom. Pas dan wordt de vraag \"Wat doet deze variabele hier precies?\" relevant. Goed, vraag jezelf nu eens af: als dat moment komt, hoe beschrijf je de rol van een variabele dan? - Heb je enig idee waar je moet beginnen bij het beantwoorden van die vraag?"
---

Vraag je je tijdens het lezen van code wel eens af: wat doet deze variabele hier precies?


Het antwoord is waarschijnlijk: ja, maar alleen als de rol van die variabele volslagen onduidelijk is, de eerste keer wanneer je ogen over de code glijden. - Dat zou mijn antwoord zijn, althans. 


## Nadenken


En dat is ook logisch. Goed geschreven code is immers code die je niet laat nadenken. Goede code gaat gepaard met een hum bij elke regel: "Hm oké oké, *makes sense*, oké..." Sterker nog, in één van de eerste hoofdstukken van [Robert C. Martins](http://cleancoder.com/products) [*Clean Code*](https://www.pearson.com/us/higher-education/program/Martin-Clean-Code-A-Handbook-of-Agile-Software-Craftsmanship/PGM63937.html) wordt het titelbegrip zelfs gedefinieerd als code die je niet laat nadenken.


Pas wanneer de vanzelfsprekendheid van code in het geding komt, gaan we nadenken - écht nadenken - over wat er op je scherm staat en waarom. Pas dan wordt de vraag waar ik mee begon relevant. Goed, vraag jezelf nu eens af: als dat moment komt, hoe beschrijf je de rol van een variabele dan? - Heb je enig idee waar je moet beginnen bij het beantwoorden van die vraag?


Misschien wel, misschien niet. Ik vermoed dat als ik twintig ontwikkelaars om een antwoord zou vragen, ik twintig verschillende antwoorden zou krijgen. 


## Generiek, specifiek


Waarom? Als we het over variabelen hebben, dan hebben we het daar ofwel in extreem generieke termen over, ofwel in extreem specifieke. We spreken ofwel van [*fields*](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/fields) of [*variabelen*](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/variables) of het datatype: `string`, `integer` etc., ofwel van `nrOfRecords`, `validationResult`, `customerAddress` etc..


Maar "Het is een *method scoped* variabele" is natuurlijk geen antwoord op de vraag welke rol die variabele speelt. En hetzelfde geldt voor "Dat is het `validationResult`". Dat is wat er staat, inderdaad, maar *waarom* staat het daar? - Het staat elke ontwikkelaar vrij om op geheel eigen wijze die vraag te beantwoorden.


## Elf rollen


In [*The Programmer's Brain*](https://www.manning.com/books/the-programmers-brain) van [Felienne Hermans](https://www.felienne.com/) vond ik een interessante manier om de rol van variabelen te categoriseren. Hermans citeert [Jorma Sajaniemi](https://www.researchgate.net/scientific-contributions/Jorma-Sajaniemi-8611097) van de [Universiteit van Oost-Finland](https://www.uef.fi/en). Volgens hem zijn vrijwel alle variabelen onder te brengen in elf rollen. 


Die luiden als volgt[^1]:


- *Fixed value*. Een variabele wiens waarde niet meer verandert na initialisatie. Je kunt hierbij denken aan velden die het [`const`-keyword](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/const) in C# gebruiken of een [`ReadOnlyList`](https://docs.microsoft.com/en-us/dotnet/api/microsoft.sqlserver.management.sdk.sfc.readonlylist-1?view=sql-smo-160), maar het kan ook gaan om "gewone" variabelen die bij wijze van spreken "toevallig" niet meer gewijzigd worden in de code. 

- *Stepper*. De waarde die je gebruikt om over een lijst te itereren. Het standaardvoorbeeld is de `i` in een [for-loop](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/statements/iteration-statements#the-for-statement). Maar er bestaan ook gecompliceerder *steppers*, zoals `size = size / 2` in een [*binary search*-algoritme](https://nl.wikipedia.org/wiki/Bisectie). 

- *Flag*. Een variabele die aangeeft dat er iets gebeurd is of het geval is, zoals `hasErrors` of `isDownloaded`. Meestal zijn dit booleans, maar dat hoeft niet per se. Het kunnen ook integers zijn of datums.

- *Walker*. Een *walker* "loopt" een datastructuur "door" en is in die zin vergelijkbaar met een *stepper*. Het verschil zit 'm in de soorten datastructuren. Een *stepper* itereert altijd over een lijst met waarden die op voorhand bekend is. Een *walker* houdt zich daarentegen met op voorhand onbekende waarden bezig. Een voorbeeld is het doorlopen van een [gelinkte lijst](https://nl.wikipedia.org/wiki/Gelinkte_lijst) om de positie te vinden waar een nieuw element ingevoerd moet worden.

- *Most recent holder*. Een variabele die de laatste in een reeks waarden "vasthoudt". Een voorbeeld is een kopie van het laatste element die door een *stepper* wordt ontsloten: `element = list[i]`. 

- *Most wanted holder*. Vaak ben je op zoek naar een bepaalde waarde, wanneer je een lijst doorloopt. Wanneer je die vindt, bewaar je die in een *most wanted holder*. Standaardvoorbeelden zijn de laagste waarde, de hoogste waarde, of de eerste die aan een bepaalde conditie doet. Een *most wanted holder* kan zowel het eindresultaat zijn van die zoektocht, of de beste match die je tot nu toe hebt gevonden.

- *Gatherer*. Een variabele die data verzamelt en aggregeert tot één waarde. Denk bijvoorbeeld aan het totaal aantal werkuren in een lijst met alle werkuren die je deze week hebt bijgehouden.

- *Container*. Een datastructuur die verschillende elementen vasthoudt. De elementen kunnen worden toegevoegd en verwijderd. Denk aan [lijsten](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=net-6.0), [arrays](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/arrays/), [stacks](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=net-6.0) etc..

- *Follower*. Voor sommige algoritmen is het noodzakelijk om bij te houden wat de vorige (of volgende) waarde was (of zal zijn). Een *follower* is dus altijd gekoppeld aan een andere waarde. Denk aan de pointer die wijst naar de vorige waarde in een gelinkte lijst. 

- *Organizer*. Een getransformeerde versie van een andere variabele om deze verder te kunnen verwerken. Denk aan een gesorteerde lijst. 

- *Temporary*. Een tijdelijke variabele die veelal voor de leesbaarheid wordt geïntroduceerd. Denk aan het resultaat van een berekening dat verderop meermaals in de code wordt gebruikt, of een variabele die wordt geïntroduceerd om data om te kunnen wisselen. Veelal heten deze variabelen ook `t` of `temp`.


## Gedeelde taal


De rollen die Sajaniemi definieert, zijn niet door hem uitgevonden. Ze beschrijven patronen die steeds opnieuw terugkeren in verschillende codebases, over verschillende programmeerparadigma's heen. 


Het doel van de lijst is dan ook niet om nieuwe informatie te verschaffen, maar om labels te geven aan dat wat ontwikkelaars intuïtief al vaak aanvoelen. De rollen creëren een gedeelde taal om over variabelen te spreken.


In die zin hebben ze veel weg van [ontwerppatronen](https://www.karlvanheijster.com/tags/ontwerppatronen/). Ook ontwerppatronen worden immers niet uitgevonden, maar ontdekt. En primaire doel van het vastleggen van ontwerppatronen, is om ontwikkelaars een manier te geven om eenvoudig over bepaalde oplossingen te kunnen praten. Je zou Sajaniemi's rollen kunnen zien als een soort mini-ontwerppatronen, toegepast op variabelen.


## Vragen


Dus de volgende keer als je je afvraagt: wat doet deze variabele hier precies? - stel jezelf dan eens de volgende vragen: is het een contante? Wordt er hier tijdelijk iets opslagen, misschien? Of wordt er op een conditie gecheckt?


En als je collega je tijdens een code review het vuur aan de schenen legt, zeg dan: "Dit is een *walker* (of een *gatherer* of een *organizer*). Misschien geven die twintig ontwikkelaars in de toekomst dan wel twintig keer hetzelfde antwoord wanneer ze worden gevraagd naar de rol van een variabele!


[^1]: Ik hanteer de Engelse benamingen om de potentie van die rollen als gedeelde taal te maximaliseren. In deze vorm zouden ze immers ook in code vastgelegd kunnen worden. Hermans maakt enkele interessante opmerkingen hierover in relatie tot de [Hongaarse notatie](https://nl.wikipedia.org/wiki/Hongaarse_notatie).
