---
title: "Mijn Eerste Pull Request"
author: "Karl van Heijster"
date: 2021-05-21T11:46:50+02:00
draft: true
comments: true
tags: []
summary: ""
---

Eerder [HIER EEN LINK] schreef ik dat ik een nieuw thema voor deze blog wilde uitproberen. Mijn eerste keus, [*hello-friend*](https://themes.gohugo.io/hugo-theme-hello-friend/), bleek niet helemaal wat ik ervan gehoopt had. Gelukkig had ik een tweede keus achter de hand: [*mini*](https://themes.gohugo.io/hugo-theme-cactus-plus/), een thema dat zijn naam eer aandoet.


## Eenvoud


Wat me beviel aan dit thema was de stijlvolle eenvoud ervan. Eén relatief smalle kolom met daarin een voorproefje van je blogs, meer niet. Het wat kleinere lettertype straalde een zekere ontwikkeldheid uit. En de minimalistische afbeelding die erboven prijkte, gaf het geheel een smaakvolle afwerking, vond ik. 


Deze keer, voordat ik keek hoe mijn blog in op z'n *mini*'s uit zou zien, keek ik eerst even de broncode door. Ik had geleerd van mijn eerdere ervaringen. Die zag er erg verzorgd uit, gelukkig maar. Enthousiast haalde ik haalde de code binnen.


## Bedenkingen


Maar ook hier geldt weer: je hebt niet lang nodig om erachter te komen wat je mist ten opzichte van wat je nu hebt. Geen i18n, bijvoorbeeld, dat is wel een pak minder. 
 
 
En... waarom breken die woorden zo raar af? Wat blijkt: *mini* vult de regel gewoon uit tot het eind en gaat op de volgende regel vrolijk verder, einde van een woord of niet. Een vreselijke en onbegrijpelijke keuze, als je het mij vraagt. Het maakt van een mooi minimalistisch thema een ontzettende bende.


## Fix #1


Dat ik besloot beide issues onmiddellijk aan te pakken, is tekenend voor mijn enthousiasme voor dit thema. Het afbreken van de woorden bleek met een [eenvoudige CSS-aanpassing](https://github.com/nodejh/hugo-theme-mini/pull/95/files) zó opgelost te zijn. 


Mijn eerste pull request op GitHub - en dus mijn eerste bijdrage aan de open source community - was daarmee is een feit! Twee regels code: zo bescheiden kan een begin zijn.


(Wat ik op dat moment nog niet zou weten, was dat het ook mijn eerste *twijfelachtige* bijdrage aan een open source-project zou zijn. [Husnul Anwari](https://github.com/husnulhamidiah) - *"just an ordinary developer"* - wees me bijna twee weken later op het feit dat mijn oplossing *deprecated* was. Gelukkig bleek het euvel eenvoudig te fixen. Men zegt niet voor niks: vier ogen zien meer dan twee.)


---


## Fix #2



Volgende stap: i18n toevoegen. Dit was wel wat meer werk. Maar je leert hier heel veel van. O trouwens, de implementatie daarvan heb ik vrijwel volledig van *tale* afgekeken. *tale* is geweldig.





Dat beviel zo goed, dat ik meteen besloot om i18n toe te voegen, met ondersteuning voor het Nederlands, uiteraard. Het is tekenend voor hoe serieus ik dit thema nam als kandidaat.


Er is nog wel een klein puntje dat me tegenhoudt: het thema plaatst een spatie na elke link. Als je in het luchtledige linkt is dat niet erg, maar zodra er een leesteken zoals een punt of een afsluitend haakje achteraan komt, ziet het vreselijk uit. Hoe langer ik ernaar kijk, hoe meer het lettertype me ook tegen gaat staan. De gewetensvraag: moet ik er langer naar kijken of niet?


## Conclusie


*mini* is een serieuze concurrent van *tale*, dat moet gezegd worden. Maar hoe langer ik bezig was met andere thema's, hoe meer het me opviel hoe net *tale* is opgezet. Het is mooi minimalistisch, makkelijk uit te breiden, heeft i18n... Het is duidelijk een thema dat met veel zorg is uitgecodeerd.


Dit was me bijvoorbeeld nooit opgevallen: op de homepagina is de complete tekst - datum, titel, preview - aanklikbaar. Dat is zó gebruiksvriendelijk. Als je dit gewend bent, valt het je pas op hoe lomp een *Lees meer*-knop is.


Dus ja, *tale* blijft voorlopig. Niet slecht voor het eerste wat ik tegenkwam.
