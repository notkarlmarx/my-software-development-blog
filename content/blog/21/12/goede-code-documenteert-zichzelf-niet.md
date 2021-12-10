---
title: "Goede code documenteert zichzelf (niet)"
author: "Karl van Heijster"
date: 2021-12-10T08:21:32+01:00
draft: false
comments: true
tags: ["clean code", "communicatie", "documentatie", "filosofie", "intentie van code"]
summary: "Uit de code valt niet af te leiden wat de specificaties zouden moeten zijn. Om met David Hume (1711-1776) te spreken: een *ought* valt niet af te leiden uit een *is*. Wie zegt dat goede code zichzelf documenteert, maakt zich schuldig aan de naturalistische dwaling. En toch zit er een kern van waarheid in het idee dat goede code zichzelf documenteert."
---

Mijn teamgenoten en ik zijn geen softwareontwikkelaar geworden omdat we zo graag documentatie schrijven. Daarom zeggen we: "Goede code documenteert zichzelf," en daarmee zijn we er vanaf.


Toch? Nou nee, want op het moment dat er vragen rondom de code rijzen, dan roepen we collectief uit: "Hadden we dat maar gedocumenteerd!"


## Descriptief vs. normatief


Goede code documenteert zichzelf niet. De reden daarvoor is best wel principieel, eigenlijk. Feitelijke code - goed of slecht - is descriptief. Het hoe en wat van de code geeft de feitelijke stand van zaken weer. Functionele of technische specificaties daarentegen zijn normatief. Deze geven een ideële toestand weer, een maatstaf waar de feitelijke code naast kan worden gelegd om beoordeeld te worden.


Uit de code valt niet af te leiden wat de specificaties zouden moeten zijn. Om met [David Hume](https://plato.stanford.edu/entries/hume/) (1711-1776) te spreken: [een *ought* valt niet af te leiden uit een *is*](https://plato.stanford.edu/entries/hume-moral/#io). Wie zegt dat goede code zichzelf documenteert, maakt zich schuldig aan de [naturalistische dwaling](https://nl.wikipedia.org/wiki/Naturalistische_dwaling). 


## Gewenste conclusies


Waarom dat argument er dan toch doorheen glipt? 


Voor een deel zal dat komen doordat minder goede argumenten graag geaccepteerd worden als ze een gewenste conclusie ondersteunen. Een *die hard* documentalist (bestaan die?) die daarnaast ook wel eens wat code schrijft, zou misschien wat minder snel geneigd zijn onze gebrekkige argumentatie te accepteren.


Bovendien, onze ontwikkelcapaciteit is beperkt en de wensen van onze gebruikers groot. Het is niet verrassend dat iets als documentatie dan als één van de eerste dingen overboord wordt gegooid tijdens het programmeren. Nog los van de voorkeuren van het ontwikkelteam, het schrijven van documentatie is eigenlijk nooit urgent. [Belangrijk? Misschien](https://nl.wikipedia.org/wiki/Eisenhower-methode), maar urgent in elk geval niet.


## En toch...


En toch schuilt er een zekere waarheid in onze gebrekkige argumentatie. Je zou kunnen stellen dat goede code zichzelf documenteert in de volgende zin: als code goed opgezet is, dan valt elke toevoeging van slechte code onmiddellijk op.


Dat geldt voor kwaliteitsstandaarden op het allerlaagste niveau, zoals leesbaarheid. Maar ook op hoger niveau geldt bijvoorbeeld dat een flagrante schending van een architectuurprincipe makkelijk opgemerkt wordt, als de rest van de code architectureel helder in elkaar zit. Dat is één van de vele redenen om je code zo eenvoudig mogelijk te houden.


Code is een drager van informatie. Goede code zorgt er niet alleen voor dat het applicatie doet wat het moet doen, maar communiceert ook de intentie van de code naar de softwareontwikkelaar. En wat is de intentie van code anders dan functionele of technische specificatie?


## Zijn zoals het hoort


Dus nee, goede code documenteert zichzelf niet. En toch is goede code niet louter descriptief. Eenvoud en leesbaarheid communiceren wel degelijk een bepaalde boodschap naar de lezer, een idee dat de code *is zoals het hoort*. 

Complexe en obscure code communiceert daarentegen niets. Nou ja, hooguit: raadpleeg de documentatie om te snappen wat hier gebeurt. Aangenomen dat je die geschreven hebt, natuurlijk!
