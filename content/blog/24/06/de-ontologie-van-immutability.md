---
title: "De ontologie van immutability"
author: "Karl van Heijster"
date: 2024-06-28T08:19:23+02:00
draft: false
comments: true
tags: ["filosofie", "immutability", "mentaal model"]
summary: "Het gebruik van *immutable* datastructuren maak je code veiliger, eenvoudiger en beter onderhoudbaar. Toch voelt het voor de meesten van ons vreemd, een totaal nieuw object te instantiëren wanneer één property wijzigt. -- Waarom?"
---

Het gebruik van [*immutable*](/tags/immutability/ "Blogs met de tag 'immutability'") (onveranderlijke) datastructuren maak je code veiliger, eenvoudiger en beter onderhoudbaar. (Zie [deze](/blog/22/05/heb-je-die-setter-echt-nodig/ "'Heb je die setter echt nodig?'") en [deze blog](/blog/24/06/immutability-en-het-single-responsibility-principe/ "'Immutability en het Single-Responsibility Principe'").) Toch voelt het voor de meesten van ons vreemd, een totaal nieuw object te instantiëren wanneer één property wijzigt. -- Waarom?


## Performance


Eén van de redenen die ontwikkelaars daarvoor aanvoeren, is dat het inefficiënt is op het gebied van performance. Een nieuw object instantiëren kost meer geheugen dan een bestaand object aanpassen. Dat geheugen moet weer vrij worden gemaakt door de [garbage collector](https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals "'Fundamentals of garbage collection', Microsoft documentatie"), en dat heeft een impact op de performance van een systeem.


Dit is een geldig argument in de context van systemen die enorm hoge performance als essentiële requirement hebben. Maar dat geldt niet voor het gros van de systemen die we bouwen. En bovendien is zitten de knelpunten op het gebied van performance maar zelden op plekken als deze. Inefficiënte databasequeries of een veelvoud aan netwerkverkeer vormen veel grotere problemen.


Het is interessant om te observeren dat zorgen over de performance van een systeem lang niet altijd ondersteund worden door *benchmarks* die bewijzen dat een bepaalde oplossingsrichting inderdaad de desastreuze effecten hebben die men veronderstelt. Tot die informatie boven tafel is gehaald, zijn zulke argumenten weinig waard. 


## Ontologie


Nee, volgens mij ligt de oorzaak van dat ongemak -- *excusez-moi*, nu neemt de filosoof in mij het woord -- in [de ontologie die we in ons dagelijks leven hanteren](https://seop.illc.uva.nl/entries/natural-language-ontology/ "'Natural Language Ontology', Stanford Encyclopedia of Philosophy") en die we onbewust meenemen in het [mentale model](/tags/mentaal-model/ "Blogs met de tag 'mentaal model'") waarmee we onze code lezen en schrijven.


In het dagelijks taalgebruik zeggen we dingen als: "Het ding verandert van kleur." Daarmee impliceren we: er is iets wat onveranderlijk blijft -- het object zelf, of haar essentie -- en iets wat verandert.[^1] En dat introduceert op de achtergrond tijd als relevante variabele. Iets wat verandert, verandert in de tijd; en dat wat hetzelfde blijft, blijft hetzelfde in die tijd.


Het ding -- één en hetzelfde ding -- was blauw op tijdstip *t<sub>0</sub>* maar rood op tijdstip *t<sub>1</sub>*. Daarom willen we code schrijven als:


```cs
var thing = new Thing { Color = "blue"};
thing.Color = "red";
```


En dat is waarom er van [objectgeoriënteerde code](/tags/objectgeoriënteerd-programmeren/ "Blogs met de tag 'objectgeoriënteerd programmeren'") zo vaak wordt gezegd dat het ons in staat stelt om onze manier van denken te spiegelen in onze code. We kunnen onze mentale modellen uitprogrammeren, want we denken vaak in termen van objecten die bestaan in de tijd.


## Ruimte(tijd)


Maar -- vervolgt de, *excusez-moi*, filosoof -- deze dingenontologie is slechts één manier om de werkelijkheid te duiden. We hoeven de wereld niet per se in te delen in dingen die blijven voortbestaan in de tijd. En als we willen programmeren met *immutable* datastructuren, dan zullen we dit mentale model ook los moeten laten.


Je zou het zo kunnen zien: we zien de dingen doorgaans als bestaand in een container. We zouden die container als driedimensionaal (ruimte) of vierdimensionaal (ruimtetijd) kunnen karakteriseren. In een driedimensionaal model zeggen we dingen als: het object heeft op tijdstip *t<sub>1</sub>* de coördinaten 1-1-1, en op tijdstip *t<sub>2</sub>* 1-1-2 -- oftewel: het object is de hoogte in gegaan. In het vierdimensionale model zeggen we: het object had eerst de coördinaten 1-1-1-1, en nu 1-1-2-2.


Welk model we hanteren, de onderliggende premissen blijft hetzelfde: we hebben objecten en we hebben containers waarin deze objecten bestaan. Dat zijn twee verschillende dingen: de containers zijn geen onderdeel van het object. 


## Waarden


Maar we zouden de objecten ook anders kunnen karakteriseren. We zouden ze ook kunnen definiëren op basis van de eigenschappen die we hen normaal toeschrijven én hun plek in de ruimte(tijd). We zouden de coördinaten ook onderdeel kunnen maken van het object zelf. We beschrijven de objecten dan, om wat programmeurstaal te lenen, zuiver in termen van hun waarden, en niet op basis van hun referentie.


Objecten in de traditionele zin van het woord, houden dan op te bestaan. Er is geen "ding" meer wat bestaat in ruimte en tijd. Dat wat vroeger één object was, is nu een opeenvolging van clusters van waarden. Er is niet één voortdurend object op *t<sub>1</sub>* en *t<sub>2</sub>*, er zijn twee "objecten" waarvan de eerste *t<sub>1</sub>*  als waarde heeft, en de tweede *t<sub>2</sub>*.


## Refactoring


Deze zienswijzen zijn functioneel (*no pun intended*) equivalent aan elkaar. Het enige wat verschilt is het onderliggende model op basis waarvan we de dingen interpreteren. Er wordt als het ware een ander raster op de wereld gelegd, waardoor er verschillende soorten onderverdelingen ontstaan, ook al blijft de wereld hetzelfde. 


Je zou kunnen zeggen: we hebben ons denkmodel gerefactord. Wat eerst onderdeel was van de container waarin drie- of vierdimensionale objecten zich bevonden, is nu onderdeel van de objecten zelf gemaakt. 


Je zou het kunnen vergelijken met het verhuizen van een variabele op class-niveau naar een functieparameter, waardoor de functie `static` gemaakt kan worden. Het gedrag van de code blijft hetzelfde -- onze tests slagen nog altijd --, maar haar structuur is veranderd. 


## Vraag


Het werpt een interessante vraag op. Laten we aannemen dat *immutable* code de voorkeur verdient boven haar *mutable* variant, en dat onze natuurlijke manier van denken *mutability* veronderstelt. Is de claim van voorstanders van objectgeoriënteerde code, dat deze programmeerstijl ons in staat stelt om onze natuurlijke manier van denken in code te spiegelen, dan een reden om objectgeoriënteerd te programmeren *of juist niet*?


Wat is onze opdracht als programmeurs? Onze huidige manier van denken zo goed mogelijk in code zien te vatten? Of onze manier van denken zodanig aanpassen dat dit de beste (veiligste, eenvoudigste, makkelijkst onderhoudbare) code oplevert?


Of duik ik dan, *excusez-moi*, te diep een filosofisch konijnenhol in?


[^1]: Op basis van het onveranderlijke deel beschouwen we het object als nog altijd hetzelfde object. Het veranderlijke wordt daarmee gedegradeerd naar "maar" een toevallige eigenschap van dat object. Zie ook [deze blog](/blog/23/01/eerlijke-domeinmodellen/ "'Eerlijke domeinmodellen'").
