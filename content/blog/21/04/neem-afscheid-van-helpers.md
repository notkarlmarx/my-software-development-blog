---
title: "Neem Afscheid Van Helpers"
date: 2021-04-23T10:03:25+02:00
draft: false
comments: true
tags: ["classes", "clean code", "leermoment", "naamgeving"]
summary: "Onlangs had ik het genoegen een nieuwe feature toe te mogen voegen in een class van meer dan 1000 regels code, genaamd de `ResourceHelper`. Hoe die class zo enorm uit de hand heeft kunnen lopen? Het begint, geloof ik, bij de naam..."
---

Onlangs had ik het genoegen een nieuwe feature toe te mogen voegen in de [*legacy code*](https://en.wikipedia.org/wiki/Legacy_code) die mijn team en ik nu al ruim een jaar uit de deur proberen te werken. Het is een rotklusje, maar een noodzakelijk kwaad tot ons gloednieuwe project die moloch daadwerkelijk kan vervangen. 


De taak was ogenschijnlijk simpel: een stukje [HTML](https://www.w3schools.com/html/) moest gewrapt worden in een [object](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/objects) en [geserialiseerd](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/serialization/) worden als [XML](https://www.w3schools.com/xml/). Onze inschatting? Drie [*story points*](https://www.scrum.org/resources/blog/why-do-we-use-story-points-estimating). Maar ik spoil alvast: het was meer dan drie *story points*. De wijziging die ik aan moest brengen, zat op verschillende plekken, maar het grootste gedeelte zat in een [class](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes) die `ResourceHelper` heet.


## Help!


Wat de `ResourceHelper` doet? Nou, hij helpt met *resources*, natuurlijk! 


En hoe! De class bestaat uit ruim 1000 regels code. Het gros daarvan zit in [methods](https://docs.microsoft.com/en-us/dotnet/csharp/methods) met namen als `ProcessResources` (105 regels) en `SaveResources` (98 regels). 


Eén van de vele redenen waarom die methods zo groot zijn, is dat er keer op keer in gecheckt wordt met welke *resource* we te maken hebben. Is het een *source text*? Ga dan naar `ProcessSoureText` (29 regels). Is het een [*stylesheet*](https://en.wikipedia.org/wiki/Style_sheet_(web_development))? `ProcessStylesheet` (12 regels). Een [*custom interaction*](https://www.imsglobal.org/forum/accessible-portable-item-protocol-public-forum/172531)? `ProcessCustomInteraction` (83 regels). (Dat is overigens iets anders dan een *portable custom interaction*, waarvan je de method name wel kunt raden en die wordt verwerkt in een method die "slechts" 42 regels kent. *Portability* heeft zo zijn voordelen, blijkt.)


Ik zou nog even door kunnen gaan met het opsommen van de verschillende *resources* die onze moloch ondersteunt, maar ik denk dat het punt wel duidelijk is.


## Wat een naam doet


Hoe heeft deze class zo verschrikkelijk uit de hand kunnen lopen? Eén reden (van de [vele](https://en.wikipedia.org/wiki/Anti-pattern#Software_engineering)) is dat hij oorspronkelijk, toen hij nog maar een stuk of 100 regels kende, `ResourceHelper` is genoemd. 


Die naam nodigt uit om alle *resource*-gerelateerde code daarin te dumpen en verder niet meer over het ontwerp van je class na te denken. Dat is al erg genoeg als het om een concreet object gaat. Maar een *resource* kan van alles zijn. En dat blijkt ook: het omvat alles van *source texts* tot *stylesheets* tot *custom interactions*. Waar komt al die logica voor al die objecten terecht? In de `ResourceHelper`. Het zijn immers *resources*, dus waar zouden ze anders thuishoren?


Het tweede gedeelte van die naam, maakt de situatie nog erger. "Helper" is zo generiek, dat de class als een magneet gaat fungeren die alle functionaliteiten rondom *resources* naar zich toe trekt. Daar valt het *processen* onder (wat dat ook moge betekenen), maar ook het opslaan, opvragen en uitlezen van het type *resource*. 


## Een alternatieve geschiedenis


Het is een goede gewoonte om je classes klein te houden. Hoe klein? Zoek een class op in je code base, willekeurig welke class. Heb je er een voor je? Goed: *kleiner dan dat*! 

Een kleine class begint met een goede naam. Kies een naam die beschrijft wat je class doet. En nee, "helpen" is geen goede optie. "Verwerken" ook niet, maar het is in elk geval al specifieker dan "helpen". 


Stel dat de oorspronkelijke auteur de `ResourceHelper` in eerste instantie `ResourceProcessor` zou hebben genoemd. Wat voor gevolgen zou dat kunnen hebben gehad?


Het zou er in elk geval voor hebben gezorgd dat alle methods die niets met dat *processen* te maken hebben, ergens anders terecht zouden zijn gekomen. Dat scheelt al een hoop regels code.


Misschien zou de oorspronkelijke auteur dan in hebben gezien dat deze class eigenlijk maar één [publieke](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/access-modifiers) method zou moeten hebben: `ProcessResources`. Misschien zou hij (of zij, maar laten we eerlijk zijn: het was een hij) hebben ingezien: ik heb verschillende *resources* en die moeten allemaal op hun eigen manier worden verwerkt. Weet je, ik maak hier een een [interface](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/interfaces/) van, of [baseclass](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes#class-inheritance) als de verwerking van verschillende *resources* genoeg overlap heeft. En ik geef elke *resource* zijn eigen implementatie in zijn eigen class.


## Afscheid


Zo zou het zomaar kunnen dat deze duizendregelige moloch beperkt was gebleven tot de oorspronkelijke 100 regels. En dat het mogelijk was geweest om een stukje HTML te wrappen in een object en dat te serialiseren als XML in minder dan drie *story points* - daadwerkelijk drie *story points*.


Wie weet, als de oorspronkelijke ontwikkelaars van onze moloch consequent zorgvuldig over naamgeving hadden nagedacht, misschien hadden we dan nooit een nieuw project op hoeven zetten om onze *legacy code* uit te faseren. 


Ik bedoel maar: neem afscheid van Helpers.
