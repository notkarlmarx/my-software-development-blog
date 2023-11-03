---
title: "Logisch-filosofische verhandeling"
author: "Karl van Heijster"
date: 2023-11-02T13:36:21+01:00
draft: true
comments: true
tags: ["boeken", "DRY", "eenvoud", "filosofie", "intentie van code", "testen", "Wittgenstein, Ludwig"]
summary: "Ik spijkerde mijn Wittgenstein onlangs bij, het deed me (omdat ik, zie je, een beroepsdeformatie heb) denken aan softwareontwikkeling."
---

Ik spijkerde mijn Wittgenstein onlangs bij, het deed me (omdat ik, zie je, een [beroepsdeformatie](/tags/beroepsdeformatie/ "Blogs met de tag 'beroepsdeformatie'") heb) denken aan softwareontwikkeling.

 
(Voor de luie lezer: [deel I](#i) gaat over filosofie, [deel II](#ii) over code.)


# I.


In zijn [*Tractatus Logico-Philosophicus*](https://en.wikipedia.org/wiki/Tractatus_Logico-Philosophicus "'Tractatus Logico-Philosophicus', Wikipedia") schrijft [Ludwig Wittgenstein](https://plato.stanford.edu/entries/wittgenstein/ "'Ludwig Wittgenstein', Stanford Encyclopedia of Philosophy") (§5.451):


> If logic has primitive ideas these must be independent of one another. If a primitive idea is introduced it must be introduced in all contexts in which it occurs at all. One cannot therefore introduce it for one context and then again for another. For example, if denial is introduced, we must understand it in propositions of the form "*~p*," just as in propositions like "*~(p v q)*," "*(∃x). ~fx*" and others. We may not first introduce it for one class of cases and then for another, for it would then remain doubtful whether its meaning in the two cases was the same, and there would be no reason to use the same way of symbolizing in the two cases.[^1]


Ik ben maar een amateurinterpreet, maar ik geloof dat Wittgenstein hier zegt: betekenis is bepaald, is eeuwig, verandert niet. (Bedoelt hij: in een volmaakt logische taal, of in überhaupt elke taal? -- Ik weet het niet, ik ben maar een amateurinterpreet.) 


## Ondubbelzinnig


Een teken kan niet in de ene context het ene aanduiden, en in een andere het andere. (-- Ah, een volmaakt logische taal dus.) In zulke gevallen moet de taal twee tekens introduceren, elk met één enkele ondubbelzinnige betekenis.


Daaruit volgt dat de betekenis bij de definitie van het teken ondubbelzinnig is vastgelegd voor elke context waar deze in voor kan komen. Een volmaakte taal weerspiegelt de wereld: één teken voor één ding. -- Wat die dingen zijn? In de context van namen zijn het objecten. Logische connectieven staan voor operaties. ("Maar zijn operaties een onderdeel van de wereld?" -- De amateurinterpreet worstelt met zulke vragen)


Wittgenstein geeft een voorbeeld van zo'n operatie: de ontkenning, negatie ("*~*"). Deze operatie keert de waarheidswaarde van een propositie om. "Het regent niet" is waar als het niet regent en onwaar als het dat wel doet. "Het regent niet niet" is waar als het regent en onwaar als het dat niet doet.


Wat het betekent om de waarheidswaarde van een propositie om te keren, is -- *moet*? -- voor elke mogelijke propositie bepaald zijn. Dat is waarom we precies kunnen berekenen wat de omgekeerde waarheidswaarde van de ontkenning van een samengestelde propositie ("*p v q*") vormt.


## In context


Ik herlas de *Tractatus* omdat ik een boek recenseerde, [*Tractatus in Context: The Essential Background for Appreciating Wittgenstein's Tractatus Logico-Philosophicus*](https://www.routledge.com/Tractatus-in-Context-The-Essential-Background-for-Appreciating-Wittgensteins/Klagge/p/book/9780367465568) van [James C. Klagge](http://jamesklagge.net/). Het gros van het boek bestaat uit het propositie voor propositie becommentarieëren van Wittgensteins meesterwerk. Klagge voorziet de lezer van filosofische achtergronden -- veel [Russell](https://plato.stanford.edu/entries/russell/ "'Bertrand Russell', Stanford Encyclopedia of Philosophy") en [Frege](https://plato.stanford.edu/entries/frege/ "'Gottlob Frege', Stanford Encyclopedia of Philosophy"), hier en daar wat [Schopenhauer](https://plato.stanford.edu/entries/schopenhauer/ "'Arthur Schopenhauer', Stanford Encyclopedia of Philosophy") en [Kant](https://plato.stanford.edu/entries/kant/ "'Immanuel Kant', Stanford Encyclopedia of Philosophy") --, wijst naar verhelderende passages uit dagboeken en brieven, wijdt uit over de historische context. Het is een feest, echt waar -- maar alleen voor de *die hard* Wittgensteiniaan.


In zijn commentaar op §5.451 wijst Klagge op de invloed van [Freges *Grundgesetze der Arithmetik*](https://plato.stanford.edu/entries/frege-theorem/ "'Frege’s Theorem and Foundations for Arithmetic', Stanford Encyclopedia of Phisosophy"). Maar hij citeert [Giuseppe Peano](https://nl.wikipedia.org/wiki/Giuseppe_Peano "'Giuseppe Peano', Wikipedia"), een Italiaans wiskundige-filosoof-logicus:


> But if the *definiendum* contains variable letters,... then, so far as I can see, it is in general necessary to give conditional or hypothetical definitions of the expression, and to give as many definitions as there are kinds of entities on which we perform this operation. Thus, the formula *a + b* will be first defined when *a* and *b* are integers, then a second time when they are fractions, then again when they are irrational or complex...[^2]


Volgens Peano ligt de betekenis van een teken -- in sommige gevallen althans -- helemaal niet voor alle mogelijke proposities vast. Natuurlijke getallen en irrationele getallen zijn allebei getallen, maar daar volgt niet uit dat je weet hoe je *π + √2* moet uitrekenen, alleen omdat je *7 + 5* wel kan. Er ligt een betekenis vast voor het optellen van natuurlijke getallen, en een betekenis vast voor het optellen van irrationele, en beide worden vertegenwoordigd door het *+*-teken.


## *(Flash forward)*


(Het is opmerkelijk hoezeer Peano's beschrijving van het geven van een definitie aanvoelt als het uitprogrammeren van een oplossing. We zouden zijn voorbeeld zelfs in de praktijk kunnen brengen: we zouden een type kunnen definiëren en daar [de `+`-operator van kunnen overschrijven](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/operator-overloading "'Operator overloading - predefined unary, arithmetic, equality and comparison operators', Microsoft documentatie"). We zouden dan de betekenis van het teken hebben gedefinieerd -- een instructie van het gebruik van dit teken in code.


Maar als we een tweede type introduceren, dat al dan niet lijkt op het eerste, dan zouden instanties daarvan zich, wanneer ze bij elkaar worden "opgeteld", niet hetzelfde gedragen als die van het eerste type. We zouden de `+`-operator opnieuw moeten herdefiniëren om in lijn te zijn met die van het eerste type.)


## Uitbreiding


Merk op wat Peano's opmerking doet met Wittgensteins bezwaar tegen het gedeeltelijk vastleggen van betekenis. "Als we de betekenis van een teken niet voor *alle* mogelijke gevallen vastleggen," zegt hij, "dan kunnen we nooit zeker weten of de betekenis van "*~*" in "*~p*" hetzelfde is als die in "*(∃x). ~fx*"." Peano antwoordt: "Ze zijn ook niet hetzelfde."


Wat er gebeurd is, is dat er een *keuze* gemaakt wordt bij het definiëren van een teken in een nieuwe context. We hebben dan als taalgemeenschap de keuze om de betekenis in lijn te brengen met het gebruik van het woord in bestaande contexten. -- Dat wil zeggen dat het gebruik van het teken in gelijkvormige gevallen correspondeert met het oorspronkelijk gebruik. Maar in ongelijkvormige gevallen breiden we het oorspronkelijk gedrag uit met een nieuwe set gedragingen (die al dan niet "vanzelfsprekend" voort lijken te vloeien uit het eerder gebruik). 


Is de betekenis in context *a* hetzelfde als in context *b*? In sommige gevallen wel. Maar andere gevallen komen maar in één van beide contexten voor, daar kunnen we de vergelijking niet maken. (Ongemerkt herinterpreteren we "betekent hetzelfde" als "gedraagt zich niet anders dan" -- en zo lost de verschuiving in betekenis op voor onze ogen.)


Uiteindelijk zo Wittgenstein Peano gelijk geven. Klagge citeert enkele relevante passages uit [*Philosophical Investigations*](https://en.wikipedia.org/wiki/Philosophical_Investigations "'Philosophical Investigations', Wikipedia") §§66-71:


> With the progress of science the meaning of this same formula is always being further extended. The various meanings of the symbol *a + b* have common properties; but these are insufficient to determine all the values that this expression can have... I do not see how they suffice to determine all the possible meanings...


# II.


Deze gedachten schoten in één flits allemaal door mijn hoofd toen ik op [Techorama](https://techorama.nl/) een praatje bijwoonde van [Dennis Doomen](https://www.continuousimprover.com/) over zijn ervaringen met het oplappen van *legacy*-software. Hij had het over het dupliceren van methods. De zaal was in oproer: * -- maar hoe zit het met DRY?!*


Ik zit in team Doomen. [DRY (Don't Repeat Yourself)](/tags/dry/ "Blogs met de tag 'DRY'") gaat over duplicatie van informatie (en dus niet, zoals soms gedacht, over duplicatie van code!). Wanneer dezelfde informatie op verschillende plekken gedefinieerd staat in de codebase, dan moeten we deze op verschillende plekken wijzigen als deze dient te veranderen. 


-- Het is een slordigheid: met vier boodschappenbriefjes in omloop is de kans dat je iets vergeet meer dan verviervoudigd.


## Doel


Met code is het anders. Niet alle gelijkvormige code heeft een zelfde functie. Een boodschappenlijstje lijkt op een *to do*-lijstje, maar dient een ander doel. We hoeven het soort papier waarop beide gekrabbeld worden niet gelijk te trekken om hen hun doel te laten vervullen.


Sterker nog, die wens pakt regelmatig in ons nadeel uit. Wanneer je een lokale functie schrijft, dan kan en mag je aannames doen over de omstandigheden van die functie. Voor globale functies geldt die luxe niet. De prijs voor de uiterlijke contextonafhankelijkheid van zulke functies moet worden opgehoest door innerlijk alle mogelijke contexten te overwegen. -- De vraag is: wegen de kosten van die innerlijke complexiteit op tegen de baten van contextonafhankelijkheid? 


Het is eenvoudiger een functie te hergebruiken dan een nieuwe te schrijven. Maar het is eenvoudiger een nieuwe te schrijven dan een bestaande te herschrijven.


In onze wens om code eenvoudig te houden introduceren we lokale instanties van nodeloze complexiteit.


(Dat is ook waarom er andere testdesiderate bestaan voor globale en lokale functies. Een vuistregel: lokale code kun je als implementatiedetail testen van een groter geheel; globale code test je in isolatie. Beide soorten tests vertellen de lezer (en debugger) wat over de intentie van de code: *dit* is niet bedoeld om door iets anders aangeroepen te worden, en daarom gebeurt dat ook niet in deze test; *dat* is wél bedoeld om door een ontwikkelaar aangeroepen te worden, en deze tests tonen hoe je dat doet.)


## Taal en betekenis


"Laten we deze code generiek maken" is een uitspraak die volgt op een lange lijst voordelen, overpeinzingen, en af- en overwegingen. Een premature abstractie brengt kosten met zich mee: bij het ontwerp, de implementatie, het moeizaam gebruik, en de uiteindelijke refactorslag. Het is niet iets wat je moet doen omdat je je donderdagmiddag om moet krijgen.


Naar Peano: laten we eerst de `+` voor integers definiëren, en dan die van de fractalen en de irrationele nummers, en laten we dán pas kijken of we die code generiek kunnen maken *en of we dat wel moeten willen.*


En dus: laten we niet, zoals Wittgenstein, alle mogelijke scenario's waar deze operator in voor kan komen vóór willen zijn.


Code is niet *als* een taal -- het *is* een taal. De tekens van code -- methods, parameters, variabelen -- hebben net zoveel betekenis als de tekens van de taal. En net als de tekens van de taal, wordt hun betekenis bepaald door de contexten waarin ze gebruikt worden. Dat is een centraal Wittgensteiniaans inzicht, en het is relevant voor de manier waarop we software ontwikkelen.


[^1]: Vertaling van [C. K. Ogden](https://en.wikipedia.org/wiki/Charles_Kay_Ogden "'Charles Kay Ogden', Wikipedia").


[^2]: James C. Klagge, *Tractatus in Context*, p. 172.
