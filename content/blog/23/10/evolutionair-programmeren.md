---
title: "Evolutionair programmeren"
author: "Karl van Heijster"
date: 2023-10-06T08:06:45+02:00
draft: false
comments: true
tags: ["beroepsdeformatie", "boeken", "evolutie", "filosofie", "software architect (rol)", "software architectuur", "testen"]
summary: "Wat evolueert in de evolutieleer? Wat is de locus van evolutie? – En natuurlijk, dat is de beroepsdeformatie: wat evolueert er in onze codebase?"
---

Wat evolueert in de evolutieleer? Wat is de locus van evolutie? – En natuurlijk, dat is de [beroepsdeformatie](/tags/beroepsdeformatie/ "Blogs met de tag 'beroepsdeformatie'"): wat evolueert er in onze codebase?


## Darwin


Het antwoord op die eerste vraag is denk ik (ik heb [Daniel Dennetts](https://en.wikipedia.org/wiki/Daniel_Dennett "'Daniel Dennett', Wikipedia") [*Darwin's Dangerous Idea*](https://www.google.de/books/edition/Darwin_s_Dangerous_Idea/bn-isXoTZmUC) praktisch opgegeten, je zou denken dat ik het weet) soorten. Soorten sterven uit, nieuwe soorten ontstaan. – Maar ik vraag mezelf af: begrijp ik wat het betekent als ik zeg dat een soort geëvolueerd, veranderd is?


Wat zijn soorten anders dan verzamelingen organismen? De menselijke soort bestaat uit ruim 7 miljard levende individuen. Wat moet er gebeuren eer een deel van die miljarden zich afsplitsen tot een andere soort? Hoe lang ik me de stamboom ook voorstel, ik kan het moment niet vastpinnen.


(We zijn als de hoofdpersoon in [Michelangelo Antonioni](https://www.imdb.com/name/nm0000774/?ref_=tt_cl_dr_1 "'Michelangelo Antonioni', IMDB")'s [*Blow-Up*](https://www.imdb.com/title/tt0060176/ "'Blow-Up', IMDB"): hoe meer we inzoomen op het beeld, hoe vager, abstracter het moordslachtoffer wordt. Totdat het helemaal is verdwenen en je je afvraagt: was er wel een moord -- is dit niet dezelfde soort?)


## Achteraf


Dennett beantwoordt die puzzel uiteraard: de afsplitsing van een soort kunnen we pas achteraf vaststellen. Miljoenen jaren later kunnen we zeggen: toen en daar leefde de laatste gemeenschappelijke voorouders van deze soorten. Maar op het moment en op de plek waar ze leefden, waren ze niet van de rest te onderscheiden. Eva was een vrouw als alle andere.


De classificatie in soorten is in de (geologische) tijd bevroren. Als je een andere tijdschaal hanteert, verliest het concept zijn grip op de materie; het is de verkeerde abstractie voor het probleem.[^1] 


Hoe langer je over evolutie nadenkt, hoe meer je beseft dat Dennetts 500 pagina's tellende uiteenzetting maar de oppervlakte raakt van alle vragen die het oproept.


## Code


Hoe zit dat als we naar onze code kijken? Wat is de locus van verandering? 


Het kan niet de individuele regel code zijn: daarvan kun je je afvragen in hoeverre een wijziging een vernietiging van het origineel bewerkstelligt. Functies of classes zijn betere kandidaten, ze zouden als organismen (met een interne werking) kunnen worden gezien. 


Ontwerppatronen zijn samenwerkingsverbanden die worden gevormd, allianties die zich uitbreiden of dupliceren (denk: een democratie wordt gesticht), en die uiteindelijk ontbinden of vervangen worden. 


Coderegels zijn cellen, functies/classes zijn organismen, ontwerppatronen zijn groepen. -- Maar dan zitten we nog lang niet op het abstractieniveau waarop soorten zich bevinden.


## Architectuur


Dus -- zullen we het maar over architectuur hebben?


Toevallig las ik [*Building Evolutionairy Architectures*](https://evolutionaryarchitecture.com/ "evolutionaryarchitecture.com") van [Neal Ford](https://nealford.com/), [Rebecca Parsons](https://www.thoughtworks.com/profiles/leaders/rebecca-parsons) en [Patrick Kua](http://www.thekua.com/atwork/) vrij vroeg in mijn loopbaan. 


Juli 2020, om precies te zijn. Het zou dus zomaar kunnen dat ik in deze blog standpunten weergeef die niet (meer) overeenstemmen met die in Ford et al.. Alle interpretatiefouten zijn voor mijn rekening.


Hoe het ook zij, de opvatting van evolutie die uit het boek sprak vond ik destijds fascinerend, dat weet ik nog wel.[^2]


Volgens Ford et al. bevindt de locus van software-evolutie zich op het architecturele niveau. (De titel bood al een hint). Wat evolueert zijn systemen. En systemen zijn met elkaar samenwerkende delen code en communicatie met andere systemen. 


Systemen kunnen samen grotere systemen vormen. Naarmate we verder uitzoomen, zullen we andere opvattingen van wat deel is en wat het geheel (vgl. [Simon Browns](https://simonbrown.je/) [C4-model](https://c4model.com/)). In de praktijk zullen pragmatische overwegingen het abstractieniveau bepalen, bijvoorbeeld het businessdomein of de grenzen van de organisatie.[^3] 


## Overleven


Systemen willen overleven (-- of wij willlen dat). Maar dat kan een systeem alleen als het adequaat op haar omgeving reageert. Met mijn liefde voor [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD), zou ik denken dat deze passage over functionele correctheid ging, maar *Building Evolutionary Architectures* gaat een andere kant op. 


Architecturen overleven als hun interne werking optimaal op de omgeving is afgestemd, als het de juiste oplossing is voor het juiste probleem – complex, maar niet complexer dan nodig. Een volmaakt rationele weging van kwaliteitsattributen gegeven de gestelde eisen.


Die werkelijkheid begint op papier, een schets in lijntjes en doosjes van de applicatie. -- En verdomd, de eerste versie van het systeem heeft er inderdaad verdomd veel van weg.


## Metafoor


Het probleem met softwarearchitectuur is dat het architecturele proces, anders dan bij de bouw, doorlopend is. De metafoor misleidt ons als we denken dat de belangrijkste architectuurbeslissingen zijn genomen in Sprint 0. Je tekent geen compleet systeem op voorhand uit -- geen goed functionerend systeem in elk geval.


"Er zijn architectuurbeslissingen genomen in Sprint 0" -- meer kunnen we er niet over zeggen. Het is een eerste versie van het diagram, en er zullen er nog veel volgen, want softwarerequirements zijn de enige entiteit ter wereld waarvan er meer ontstaan naarmate je er meer wegwerkt.[^4]


De code bewijst zichzelf in de buitenwereld, en geeft daarmee nieuwe inzichten in de problemen waar die buitenwereld ons voor stelt. De applicatie sterkt zich wanneer ze deze lessen in zich opneemt. Hoe die problemen te incorporeren en op te lossen zonder de integriteit van de applicatie aan te tasten, dat is een architectureel vraagstuk. -- Dat is waarom elke "gewone" ontwikkelaar net zozeer een architect moet zijn.[^5]


## Kwantificeren


De vraag wordt dan: hoe kwantificeer je structurele integriteit?


Een antwoord zou kunnen zijn: door te meten in hoeverre het daadwerkelijke systeem overeenstemt met het ontwerp. Als een applicatie die is ontworpen volgens een drielagenarchitectuur, daadwerkelijk in drie lagen is onderverdeeld, dan is deze in staat te overleven.


Softwarearchitecten hebben (neem ik aan) andere dingen te doen dan verschillende codebases inspecteren op architecturele correctheid -- dit vraagt om automatisering. En inderdaad: er bestaat zoiets als [*NetArchTest*](https://github.com/BenMorris/NetArchTest) voor systemen die zijn ontwikkeld in .NET: "*A fluent API for .Net Standard that can enforce architectural rules in unit tests.*"[^6]


Ik heb die library ooit nog ge-*proof of concept*, vlak nadat ik *Building Evolutionary Architectures* had uitgelezen. Wat opviel was hoe moeilijk het was zulke tests -- Ford et al. noemt ze *fitness functions* -- te handhaven. Op het moment dat ik de eerste test schreef -- het systeem waar mijn team aan werkte was toen nog geen maanden oud --, bleek de applicatie al nauwelijks aan de eenvoudigste validatieregels op te leven. De architectuurtests zijn daarna grotendeels de ijskast in gegaan -- maar misschien kom ik daar nog op terug.


## Kundig


Destijds zat dit antwoord -- en de opvatting van evolutie die eruit volgde -- me al niet helemaal lekker. Ford et al. stelt dat een systeem overleeft als deze een structuur heeft die bepaalde architecturele principes honoreert (anders gezegd: als deze *architecturally fit* is).[^7]


Dat gaat er uiteraard van uit dat de architectuur, zoals bedacht, de juiste oplossing is voor het juiste probleem. *Building Evolutionary Architectures* veronderstelt het bestaan van kundige softwarearchitecten die een gewogen lijst van kwaliteitsattributen om kan zetten in een diagram met doosjes en lijntjes.


Die veronderstelling komt niet uit de lucht vallen; de schrijvers van het boek zijn zelf stuk voor stuk kundige architecten (neem ik aan). Maar de veronderstelling gaat niet in elke context, in elke organisatie op. Ik kan gelukkig niet uit eigen ervaring van onkundige architecten spreken, maar de koffieautomaat heeft in zijn leven genoeg horrorverhalen aangehoord.


Wat meten *fitness functions*: of het systeem architectureel goed in elkaar zit, of slechts dat het systeem zo in elkaar zit als ooit bedacht?


## Complex, eenvoudig


Elke ontwikkelaar kan beamen: het systeem zoals ontworpen is maar zelden net zo complex of eenvoudig als het op te lossen probleem. 


*Over engineering* is een reëel probleem. Een nodeloos complexe applicatie die slaagt voor elke nodeloos complexe *fitness function* blijft, eh, ingewikkelder dan nodig. 


En veranderende requirements ontmaskeren aannames als dat: aannames. Als de architectuur van tijd tot tijd dient te veranderen onder druk van veranderende functionele eisen, hoe kan een *fitness function* dan ooit duurzaam de kwaliteit van een systeem meten? 


-- Het is die vraag die ervoor zorgde dat mijn POC met *NetArchTest* bij een POC bleef. De architectuur van onze applicatie lijkt alleen nog in de verte op wat we oorspronkelijk bedachten.


Dus: is het idee van zulke tests niet bij voorbaat verloren?


## Tests


Zo ver zou ik niet willen gaan. Als ik vandaag een nieuwe POC met *NetArchTest* zou uitvoeren, zou ik dan tot dezelfde conclusie komen? Sindsdien heb ik een hoop geleerd over het schrijven van goede tests -- en met een beetje geluk ook het een en ander over softwarearchitectuur. 


Het zou kunnen dat ik mijn tests destijds te nauw gespecificeerd heb. Testte ik de architectuur of een implementatiedetail? -- Een vraag die in het voordeel van de laatste uitvalt wat betreft mijn functionele tests in die tijd. 


En stelde ik wel de juiste vragen? Had ik de architecturele volwassenheid met *NetArchTest* de architectuur te onderzoeken -- of probeerde ik, enthousiast door de techniek, architecturele regels te formuleren die vooral goed klonken?


Een stuk gereedschap is zo behulpzaam als degene die het hanteert.


## Waarschuwing


Bovendien zie ik wel degelijk de aantrekkingskracht van *fitness functions*. Het valt moeilijk te ontkennen dat ik genoeg softwareprojecten ten onder zijn gegaan aan technische schuld. De wereld zou er vast heel anders uit hebben gezien als die horden ontwikkelaars op tijd waren tegengehouden.


*Fitness functions* kunnen dienen als waarschuwingssignaal. Wat dat signaal betekent, hangt af van het systeem, het team, de organisatie. Het kan zijn: "Niet doen, deze beslissing gaat je nog duur komen te staan!" Maar wat ook mogelijk is: "Je introduceert hier technische schuld, weet je zeker dat je dit wil?"[^8]


Om hun werk te hoeven doen, hoeven *fitness functions* niet eeuwig te zijn. Functionele eisen kunnen ons dwingen de architectuur te herzien -- wat de *fitness functions* doen is ervoor zorgen dat er in elk geval geen rotzooi ontstaat op het moment dat we de architectuur tegen het licht houden. De belofte van het middel is om de accidentele complexiteit te beperken. Als het werkt, kunnen we er in elk geval van uitgaan dat het diagram en de code overeenstemmen. -- Dus als we weten hoe we het diagram om moeten gooien, dan weten we hoe we de code om moeten gooien. 


## Memetisch


-- Jeetje, ik ben volgens mij al heel lang aan het woord. (-- En dan heb ik nog geeneens softwareontwikkeling vanuit [memetisch](https://en.wikipedia.org/wiki/Memetics "'Memetics', Wikipedia") perspectief bekeken! --) Dus, eh, wat moeten we met deze gedachten? 


Ik heb de boel een beetje op de vrije loop gelaten, eerlijk gezegd, dus, eh... ik durf het je eerlijk gezegd niet te zeggen. Kan ik er in een volgende blog misschien op terugkomen?


[^1]: Wittgenstein zou misschien zeggen: de betekenis van een begrip is onbepaald, totdat er een gebruik voor is vastgelegd in het taalspel. Je kunt het concept uit het ene taalspel niet één op één overzetten in het nieuwe taalspel.

[^2]: Inmiddels is er een [tweede editie](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781492097532/ "'Building Evolutionary Architectures, 2nd Edition', O'Reilly") van dit boek verschenen, die ik eerlijk gezegd net zo graag wil lezen als de eerste versie.

[^3]: De grenzen van mijn organisatie zijn de grenzen van mijn wereld, vrij naar Wittgenstein.

[^4]: De hydra is een ander voorbeeld, maar dan hebben we ons heil al gezocht in fictie.

[^5]: Al blijft het in het ideale geval altijd mogelijk om hulp in te schakelen van een ontwikkelaar die "architect" in zijn titel heeft staan.

[^6]: "*Inspired by the [ArchUnit](https://www.archunit.org/) library for Java.*"

[^7]: Mijn liefde voor TDD wil me doen zeggen: het is *functionele* correctheid die bepaalt in hoeverre een systeem in staat is te overleven. Systemen die niet het probleem oplossen, of zelf teveel nieuwe problemen introduceren, worden uitgefaseerd. <br> De architect in me -- blijkbaar zit er een architect in me -- antwoordt: maar vanuit het perspectief van de architectuur is die correctheid incidenteel; waar het om gaat is een solide structurele ondersteuning te bieden waarbinnen die functionaliteit gerealiseerd kan worden. De architectuur van een systeem is de horizon waarbinnen functionele correctheid moet bestaan.

[^8]: Technische schuld -- en het wegwerken ervan -- biedt nog een interessante uitdaging voor het onderhoud van dit soort tests. Wat doe je op het moment dat je met technische schuld te maken krijgt: breid je de tests uit, gooi je ze weg, negeer je ze (tijdelijk?)? 
