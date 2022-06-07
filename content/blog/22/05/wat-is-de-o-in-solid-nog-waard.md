---
title: "Wat is de O in SOLID nog waard?"
author: "Karl van Heijster"
date: 2022-05-30T08:59:07+02:00
draft: false
comments: true
tags: ["agile ontwikkeling", "clean code", "interface segregatie principe", "leermoment", "open-closed principe", "refactoren", "single-responsibility principe", "software architectuur", "SOLID", "verandering"]
summary: "Een ontwikkelaar die eens code schrijft en deze nooit meer aan denkt te hoeven passen, is een ontwikkelaar die rot in zijn applicatie verwelkomt. Een al te strikte naleving van het *Open-closed* principe (OCP) getuigt van een ronduit onverantwoorde houding - in elk geval binnen de context van Agile ontwikkeling. Waar komt de aantrekkingskracht van het OCP dan vandaan? "
---

Hey kijk, een video:


{{<youtube id="Ko0eV7BGcXs" title="SOLID Revisited : The State of the Matter - Phil Nash - NDC TechTown 2021" >}}
<br>


In deze [NDC-lezing](https://ndcconferences.com/) houdt [Phil Nash](https://philna.sh/) de [SOLID-principes](/tags/solid/) eens kritisch tegen het licht. Ik vond het een prikkelende onderneming, want deze principes zijn één van de eerste dingen die ik als programmeur aangeleerd kreeg - en vooral één van de eerste programmeergerelateerde zaken die vat kregen op mijn filosofenbrein.


## Heilig


O ja, [ik heb dus filosofie gestudeerd](/blog/21/07/mijn-loopbaanwending/). Ik vond de syntax van [C#](https://docs.microsoft.com/en-us/dotnet/csharp/) leren dus een behoorlijke klus. Wat zeg ik, ik heb er maanden over gedaan om te begrijpen hoe [events](https://docs.microsoft.com/en-us/dotnet/standard/events/) in elkaar steken. Zelfs nu nog weet ik het niet precies (waarschijnlijk omdat traditionele events best wel overbodig zijn geworden in moderne applicaties - ik gebruik ze in elk geval vrijwel nooit meer[^1]).


Maar de SOLID-principes, die spraken me wel aan. Ze spraken me aan, omdat ze niet gingen over de *nitty gritty* implementatiedetails waar zoveel traditionele programmeurs enthousiast van worden. Ze gingen over de ideeën daar achter - ideeën over hoe goede code eruit ziet, en vooral het waarom daarvan. Dingen waar je, zeg maar, over zou kunnen filosoferen.


Ik heb de SOLID-principes lange tijd daarom ook als vrijwel heilig beschouwd. - Niet zonder reden, overigens. [Robert *"uncle Bob"* Martin](http://cleancoder.com/products) - die SOLID voor het eerst in haar huidige vorm formuleerde - houdt in [*Clean Architecture*](https://www.pearson.com/us/higher-education/program/Martin-Clean-Architecture-A-Craftsman-s-Guide-to-Software-Structure-and-Design/PGM333762.html) een overtuigend betoog over waarom deze principes fundamenteel zijn voor het opzetten van onderhoudbare applicaties.[^2]


## Vraagtekens


Terug naar die lezing van Nash: je kunt je vraagtekens bij de heiligheid van SOLID zetten. Sterker nog, het lijkt me gezond dat van tijd tot tijd te doen. En eerlijk waar, hij maakt een paar goede punten. 


Bijvoorbeeld: wat is het [Interface segratatie principe](https://en.wikipedia.org/wiki/Interface_segregation_principle) (ISP) anders dan het [*Single-Responsibility* principe](https://en.wikipedia.org/wiki/Single-responsibility_principle) (SRP) toegepast op [interfaces](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface)? - Vooral een mooie gelegenheid om een I in SOLID te fietsen, blijkt. De SOLD-principes... tja, het klinkt niet onaardig, maar ik ben toch nog niet helemaal, eh, verkocht. Het klinkt mij nog niet, eh, solide genoeg in de oren.


Maar aan het eind van de dag zou je die kritiek als oppervlakkig af kunnen schrijven. Hij gaat over de vorm waarin het principe gegoten is, maar aan de geldigheid van het SRP - toegepast op interfaces of niet - tornt het niet.


## O?


De O in SOLID, het [*Open-closed* principe](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle) (OCP), komt er minder makkelijk vanaf. Zoals bekend stelt dat principe dat software-entiteiten open moeten staan voor uitbreiding, maar gesloten moeten zijn voor aanpassing. Anders gezegd: een wijziging in de ene class moet niet tot gevolg hebben dat een andere class aangepast moet worden om te blijven werken.


Dat klinkt logisch genoeg. Maar waarom? Als softwareontwikkelaars zijn we constant bezig bestaande code aan te passen. Sterker nog, dat is een belangrijk deel van ons werk. Nieuwe wensen, nieuwe functionaliteiten, nieuwe specificaties brengen nieuwe inzichten - ook rondom bestaande code. En niet zelden behoeft die code daarom aanpassing. 


Hetzelfde sentiment als in Nashs lezing, kwam ik tegen in [*The Art of Agile Development*](https://www.oreilly.com/library/view/the-art-of/9780596527679/) van [James Shore](https://www.jamesshore.com/).[^3] Een essentieel onderdeel van Agile softwareontwikkeling, is het constant refactoren van bestaande code. - Dat is zo'n beetje het tegenovergestelde van code schrijven die gesloten is voor aanpassing!


Een ontwikkelaar die eens code schrijft en deze nooit meer aan denkt te hoeven passen, is een ontwikkelaar die rot in zijn applicatie verwelkomt. Een al te strikte naleving van het OCP getuigt van een ronduit onverantwoorde houding - in elk geval binnen de context van Agile ontwikkeling.


## Aantrekkingskracht


Waar komt de aantrekkingskracht van het OCP dan vandaan? Zowel Nash als Shore brengen de hypothese naar voren dat dit principe ontstond in een tijd dat het uitrollen van nieuwe code een pijnlijke onderneming was. Om die pijn te minimaliseren, deden ontwikkelaars er goed aan zo min mogelijk bestaande code aan te hoeven passen.


In hoeverre die hypothese hout snijdt, kan ik moeilijk beoordelen - daarvoor loop ik nog niet lang genoeg mee. Maar ik heb er mijn vraagtekens bij. Binnen de context van een [plug-in architectuur](https://medium.com/omarelgabrys-blog/plug-in-architecture-dec207291800), kan ik me voorstellen dat een pijnlijke uitrol een rol speelde bij het omarmen van het OCP. (Sterker nog, je zou kunnen stellen dat zo'n opzet de architecturele belichaming van het OCP vormt!)


Maar het gros van de [enterprise applicaties](https://en.wikipedia.org/wiki/Enterprise_software) had en heeft geen plug-in architectuur. Die zijn opgezet als [monoliet](https://microservices.io/patterns/monolithic.html). En het uitrollen van een monoliet wordt niet pijnlijker of minder pijnlijk al naargelang je code is opgezet via het OCP of niet. 


De eigenlijk aantrekkingskracht van het principe lijkt me wat dichter bij huis te liggen. Je wil niet, elke keer als je bepaalde functionaliteit toevoegt, ergens een `if`-statement toe willen voegen. En je wil al helemaal niet op dertien plekken in je applicatie een `if`-statement toe willen voegen! Niet alleen omdat dat vervelend is voor de ontwikkelaar, maar vooral omdat zo'n opzet lijkt te smeken om de introductie van bugs.


## Volwassenheid


Ik geloof dat dat implicaties heeft voor het OCP - niet voor het belang ervan, maar voor de mate waarin je het toe dient te passen of niet.


Stel, je hebt een nieuwe codebase. Je voegt een feature toe. Die implementeer je, zoals het hoort in Agile ontwikkeling, zo eenvoudig mogelijk. Vervolgens voeg je een verwante feature toe. Ook die implementeer je zo eenvoudig mogelijk. Als dat betekent dat het onderscheid tussen die features met een `if`-statement wordt afgehandeld, dan is dat maar zo. - Anders gezegd: in een vroeg stadium van ontwikkeling, hoef je het OCP nog niet strikt te volgen.


De situatie verandert wanneer de applicatie volwassener wordt. Naarmate er meer verwante features worden toegevoegd, wordt het onwenselijk om deze middels een steeds verder uitdijende lijst `if`-statements af te handelen. Pas op dat moment ga je nadenken over het OCP. - Zeker als je weet dat er nog meer verwante features op de planning staan.


Anders gezegd: het belang van het OCP hangt af van de volwassenheid van de codebase. Hoe volwassener de codebase, hoe belangrijker het is het OCP te volgen. En dus ook: des te onvolwassener de codebase, des te makkelijker je als ontwikkelaar weg kunt komen met minder uitbreidbare code.


## Eenvoud


Hierin verschilt het OCP van het SRP. Want of een applicatie nu gloednieuw is, of al tegen zijn *end of life* aanhikt, het is volgens mij altijd een goed idee om verantwoordelijkheden in code zo goed mogelijk te scheiden.


Waar zit het onderscheid in? Het antwoord is, denk ik: eenvoud. Code die het SRP respecteert, is eenvoudiger code. Maar dat kan niet per se gezegd worden van code die is opgezet volgens het OCP.


Ga maar na. Stel dat je code welgeteld één *use case* moet ondersteunen. Zou je per se op die code het OCP al moeten toepassen? Nee, want dat voegt complexiteit toe die niet inherent is aan het probleemdomein. En bij twee (verwante) *use cases*? Misschien, maar waarschijnlijk nog niet: een `if`-statement is een eenvoudiger oplossing. 


Pas naarmate het aantal (verwante) *use cases* toeneemt, komt er een omslagpunt waarop het volgen van het OCP eenvoudiger code oplevert dan het negeren ervan. - Dat is het moment waarop je als ontwikkelaar een stap terugzet en begint te refactoren, vóórdat je de volgende feature implementeert.


## S(O)L(I)D


Wat betekenen deze observaties voor de SOLID-principes? Een voor de hand liggende conclusie is: niet elk principes is gelijk geschapen. Het ISP is een afgeleide van het SRP - de laatste staat dus "hoger", in zekere zin, dan de eerste. En het OCP wordt van belang naarmate de volwassenheid van de codebase toeneemt - en in die zin staat ook dit principe dus "lager" dan het SRP.


Daaruit volgt een tweede conclusie: code hoeft niet alle SOLID-principes te respecteren om het predikaat "goede code" te verdienen. Software ontwikkelen is een pragmatische aangelegenheid. Het is aan de ontwikkelaar om zich constant af te vragen: is dit *goed genoeg*? - hoeveel meerwaarde levert het verder verfijnen van deze code op, ten opzichte van de huidige implementatie? 


De SOLID-principes zijn richtlijnen bij de beantwoording van die vraag. Maar heilig? Nee, dat zijn ze zeker niet.


[^1]: De door mij wel vaker aangehaalde [Nick Chapsas](https://nickchapsas.com/) vraagt zich niet voor niks af: [*Are events in C# even relevant anymore?*](https://www.youtube.com/watch?v=NmmpXcMxCjY) In die video presenteert hij overigens een aantrekkelijk alternatief voor de standaard ondersteunde variant.


[^2]: Oplettende lezers hebben vast en zeker wel onthouden dat *Clean Architecture* het [op één na beste boek over softwareontwikkeling was dat ik in 2020 las](/blog/21/05/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2020-las/). Het beste boek was [*Clean Code*](https://www.pearson.com/us/higher-education/program/Martin-Clean-Code-A-Handbook-of-Agile-Software-Craftsmanship/PGM63937.html).


[^3]: Oplettende lezers denken nu vast: daar heb je 'm weer! Ja, ik ben dol op dit boek, het moet gezegd.
