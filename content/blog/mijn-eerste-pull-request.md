---
title: "Mijn Eerste Pull Request"
author: "Karl van Heijster"
date: 2021-05-21T11:46:50+02:00
draft: true
comments: true
tags: []
summary: ""
---

[Eerder](/blog/21-06-07-overwegingen-bij-het-uitzoeken-van-een-thema) schreef ik dat ik een nieuw thema voor deze blog wilde uitproberen. Mijn eerste keus, [*hello-friend*](https://themes.gohugo.io/hugo-theme-hello-friend/), bleek niet helemaal wat ik ervan gehoopt had. Gelukkig had ik een tweede keus achter de hand: [*mini*](https://themes.gohugo.io/hugo-theme-cactus-plus/), een thema dat zijn naam eer aandoet.


## Eenvoud


Wat me beviel aan dit thema was de stijlvolle eenvoud ervan. Eén relatief smalle kolom met daarin een voorproefje van je blogs, meer niet. Het wat kleinere lettertype straalde een zekere ontwikkeldheid uit. En de minimalistische afbeelding die erboven prijkte, gaf het geheel een smaakvolle afwerking, vond ik. 


Deze keer, voordat ik keek hoe mijn blog in op z'n *mini*'s uit zou zien, keek ik eerst even de broncode door. (Ik had geleerd van mijn eerdere ervaringen.) Die zag er erg verzorgd uit, gelukkig maar. Enthousiast haalde ik haalde de code binnen.


## Bedenkingen


Maar ook hier geldt weer: je hebt niet lang nodig om erachter te komen wat je mist ten opzichte van wat je nu hebt. Geen [i18n](https://en.wikipedia.org/wiki/Internationalization_and_localization), bijvoorbeeld. Dat betekende dat ik zelf aan de slag moest gaan, als ik de taal van mijn blog consistent wilde houden. 
 
 
Daarnaast... waarom breken die woorden zo raar af? 


Wat blijkt: *mini* vult de regel gewoon uit tot het eind en gaat op de volgende regel vrolijk verder, einde van een woord of niet. Een vreselijke en onbegrijpelijke keuze, als je het mij vraagt. Het maakt van een mooi minimalistisch thema een ontzettende bende. 


(Maar ik zie dat de maker van het thema uit China komt. Misschien dat zijn keuze in het Chinees minder vreselijk en onbegrijpelijk is.)


## Fix #1


Dat ik besloot beide issues onmiddellijk aan te pakken, is tekenend voor mijn enthousiasme voor dit thema. 


Het afbreken van de woorden bleek met een [eenvoudige CSS-aanpassing](https://github.com/nodejh/hugo-theme-mini/pull/95/files) zó opgelost te zijn. Mijn eerste pull request op GitHub - en dus mijn eerste bijdrage aan de open source community - was daarmee is een feit! Twee regels code: zo bescheiden kan een begin zijn.


(Wat ik op dat moment nog niet zou weten, was dat het ook mijn eerste *twijfelachtige* bijdrage aan een open source-project zou zijn. [Husnul Anwari](https://github.com/husnulhamidiah) - *"just an ordinary developer"* - wees me bijna twee weken later op het feit dat mijn oplossing *deprecated* was. Gelukkig bleek dat eenvoudig te fixen. Men zegt niet voor niks: vier ogen zien meer dan twee.)


## Fix #2


Het toevoegen van i18n was een uitstekend zelfstudieprojectje voor op een vrijdagochtend. Niet alleen verving ik de huidige tekst door variabelen, ik voegde meteen ondersteuning voor Nederlands toe. Dit bleek nog best een interessante uitdaging. De maanden dienden namelijk ook vertaald te worden, waardoor er een heuse vertaaltabel bijgevoegd moest worden.


Dat het bij een vrijdagochtendproject bleef, heb ik overigens geheel te danken aan [*tale*](https://themes.gohugo.io/tale-hugo/), mijn huidige thema, van wie ik de implementatie volledig afkeek. Het kan niet vaak genoeg gezegd worden: *tale* is een geweldig thema.


Mijn tweede bijdrage aan de open source community was al wat flinker: [acht gewijzigde bestanden](https://github.com/nodejh/hugo-theme-mini/pull/96/files). *I'm on fire!*


## Is dit de ware?


Na al dat werk zou je haast denken: dit moet 'm wel worden, het nieuwe thema van *dotkarl*. En eerlijk is eerlijk, *mini* was heel dichtbij. Ik heb zelfs een [branch op GitHub](https://github.com/notkarlmarx/my-software-development-blog/tree/mini-theme) klaarstaan met de code.


Maar geheel in lijn van de twijfelachtige stakeholder waar ik me mee identificeer, wees ik *mini* op het laatste moment af. Om een pietluttige reden, uiteraard.


Wat blijkt nu namelijk: het thema plaatst een spatie na elke link. Als je in het luchtledige linkt is dat niet erg, maar zodra er een leesteken zoals een punt of een afsluitend haakje achteraan komt, ziet het er... nu ja, niet uit. 


Hoe langer ik ernaar keek, hoe meer het lettertype me ook tegen ging staan. De gewetensvraag was dan ook een tijdlang: moet ik er langer naar kijken of niet?


## Conclusie


Het antwoord is eigenlijk simpel: nee, weg ermee! *mini* was een serieuze concurrent van *tale*, dat moet gezegd worden, maar het kan er toch niet aan tippen.  Dus ja, *tale* blijft voorlopig. 


Niet slecht voor het eerste wat ik tegenkwam, toch?


## ...en die fixes dan?


O ja, de fixes! Die staan nog [allebei open](https://github.com/nodejh/hugo-theme-mini/pulls). Net als een stuk of wat pull requests van de afgelopen drie jaar, zie ik nu ik er zo naar kijk. Laat dat dus de les zijn: 


- **Ga na hoe actief een open source component wordt onderhouden, voordat je besluit 'm te gaan gebruiken!** Begrijp me niet verkeerd, een keer bijdragen aan een open source project is hoe dan ook aan te raden omdat het op zichzelf leerzaam is. Maar als je het component daadwerkelijk wil gebruiken, wees er dan zeker van dat je je verbindt aan iets wat met zijn tijd meegroeit.

  Al was het maar om ervoor te zorgen dat de tijd die jij erin hebt gestoken, niet alléén leerzaam voor jou was.
