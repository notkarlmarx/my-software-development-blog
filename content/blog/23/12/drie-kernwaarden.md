---
title: "Drie kernwaarden"
author: "Karl van Heijster"
date: 2023-12-29T11:18:32+01:00
draft: false
comments: true
tags: ["kernwaarden", "procesverbetering"]
summary: "Onlangs beschreef ik hoe het formuleren van kernwaarden zou kunnen helpen in het verbeteren van het softwareontwikkelproces. Als oefening heb ik, voor mezelf, drie van zulke waarden geformuleerd, drie zaken die ik persoonlijk belangrijk vind wanneer ik software ontwikkel."
---

Onlangs beschreef ik [hoe het formuleren van kernwaarden zou kunnen helpen in het verbeteren van het softwareontwikkelproces](/blog/23/12/formuleer-je-kernwaarden/ "'Formuleer je kernwaarde'"). Als oefening heb ik, voor mezelf, drie van zulke waarden geformuleerd, drie zaken die ik persoonlijk belangrijk vind wanneer ik software ontwikkel.[^1] 


(Ik heb het onderstaande in de wij-vorm geformuleerd, omdat ik van mening ben -- zie kernwaarde #3 -- dat softwareontwikkeling een teamsport is. Kernwaarden hebben alleen belang als ze door het hele team gedragen worden.)


## 1. Kwaliteit


Alle software die we als team ontwikkelen, moet aan een bepaalde kwaliteitsstandaard voldoen. Dat betekent concreet (onder andere maar niet uitsluitend): de code moet zo eenvoudig en zo helder als mogelijk zijn; elke ontwerpkeuze moet inhoudelijk, op basis van argumenten, kunnen worden verdedigd door het team; het gedrag van de code wordt altijd geverifieerd en [gedocumenteerd door een descriptieve testsuite](/talks/altijd-up-to-date-documentatie-met-maximaal-descriptieve-tests/ "'Altijd up to date documentatie met maximaal descriptieve tests'"). Code die niet aan deze kwaliteitsstandaard voldoet, wordt niet gereleased naar de testomgeving, laat staan naar productie.


De focus op kwaliteit komt meerdere groepen ten goede. Ten eerste de eindgebruiker, omdat we deze hiermee de frustratie van bugs zoveel mogelijk besparen. Ten tweede de opdrachtgever, omdat het goedkoper is kwaliteit vanaf het begin in te bouwen, dan continu om een gebrek aan kwaliteit heen te moeten werken. Ten derde de ontwikkelaars zelf, eenvoudigweg omdat het plezierig is om in en met kwalitatief hoogstaande code te werken.[^2] 
  

De implicatie van hiervan is verstrekkend. Het betekent bijvoorbeeld: als er gekozen moet worden tussen een feature nu afleveren tegen een lagere standaard, of een feature later opleveren tegen de gebruikelijke standaard, dan kiezen we principieel voor het laatste. We doen liever één ding goed, dan tien dingen half.


Uitzonderingen op die regel zijn mogelijk -- we zijn als team pragmatisch --, maar alleen als er een realistisch plan klaarligt om de geïntroduceerde technische schuld terug te betalen. (Zie ook [deze blog](/blog/21/11/bewuste-technische-schuld/ "'Bewuste technische schuld'").) Verlagingen van de kwaliteitsstandaard zijn zeer zeldzaam en moeten grondig beargumenteerd worden.


## 2. Continue verbetering


Als team streven we ernaar continu onszelf te verbeteren. Dat geldt voor onze code, ons werkproces, en voor onszelf als professionals.


We leren continu nieuwe dingen over de problemen die we met code op proberen te lossen, en passen onze code continu aan naar de laatste inzichten. Refactoren is onze tweede natuur. We hoeven niemand toestemming te vragen om de structuur van de code te wijzigen; we zullen hooguit moeten beargumenteren in hoeverre de kosten van een grotere refactorslag opwegen tegen de baten. (Zie ook [deze blog](/blog/22/06/het-probleem-met-technische-schuld-op-je-backlog/ "'Het probleem met technische schuld op je backlog'").)


Als we merken dat een bepaalde werkwijze geen toegevoegde waarde oplevert of ons zelfs tegenwerkt, dan laten we die werkwijze vallen. Als we merken dat we een prima functionerende werkwijze kunnen vervangen door een betere werkwijze, dan kiezen we voor de betere.


We houden onze oren en ogen open voor nieuwe inzichten uit het werkveld die ons werk makkelijker kunnen maken. We houden onze vakliteratuur bij, zijn op de hoogte van nieuwe ontwikkelingen, nemen geen genoegen met uitspraken als "dat hebben we altijd zo gedaan."


Dit betekent dat het team tijd vrijmaakt om zichzelf te kunnen verbeteren. Dat zien we niet als kostenpost, maar als investering. De tijd die we nu pakken om onszelf te verbeteren, betaalt zich in de toekomst terug in kwalitatief betere oplossingen. Het doel van het team is niet om in een zo kort mogelijke tijd zoveel mogelijk code te schrijven. We plannen Sprints niet tot de nok toe vol, want dat gaat ten koste van ons vermogen te verbeteren. (Zie ook [deze blog](/blog/22/05/tevreden-ontwikkelaars-en-stakeholders-dankzij-speelruimte/ "'Tevreden ontwikkelaars én stakeholders dankzij speelruimte'").) We ruimen structureel tijd in om ervaring op te doen met nieuwe technieken, verwerken deze ervaringen in blogs of nieuwsbriefartikelen, demo's en presentaties. 


## 3. Samenwerking


Software ontwikkelen is een teamsport. Het mag nooit gebeuren dat we iets niet kunnen doen omdat er iemand ziek is of met vakantie. We geloven wel in expertise, maar niet in rollen. Iedereen moet elkaars basale werkzaamheden over kunnen nemen, maar we begrijpen dat sommigen die beter kunnen vervullen dan anderen.


Een team heeft voortrekkers en volgers, maar een team heeft geen leider. Niemands wil is wet, iedereens mening mag en moet gehoord worden. Het perspectief van een junior ontwikkelaar is net zoveel waard als dat van een senior (al is het te hopen dat de laatste over een uitgebreider palet aan argumenten en ervaringen beschikt dan de eerste). 


Maar de samenwerking houdt niet op bij de grenzen van het team. We delen kennis met collega-ontwikkelaars buiten het team en halen kennis bij hen op. We stemmen veelvuldig af met stakeholders om te valideren dat we het juiste bouwen. We zijn ons bewust van het feit dat onze kennis en kunde beperkt is, en verwelkomen alle hulp die we kunnen gebruiken.


## Tot besluit


Wij geloven dat het hooghouden van deze kernwaarden zal leiden tot de best mogelijke software die we op dat moment kunnen produceren.


Wij zullen niet marchanderen met onze kernwaarden. Wij zullen onszelf en onze collega's erop aanspreken wanneer zij niet in overeenstemming met onze kernwaarden handelen.


Wij weten dat we er niet in zullen slagen deze kernwaarden altijd en overal in ons gedrag te manifesteren, maar dat ontslaat ons niet van de plicht daar naar te streven. Wij doen ons best.


-- Welke kernwaarden wil jij hooghouden? 


[^1]: Deze lijst is -- als alles in het leven -- voorlopig, een eerste schets. Ik acht het niet onwaarschijnlijk dat mijn persoonlijke lijst van kernwaarden er heel anders uit zou komen te zien na discussie met team en/of management.


[^2]: Kernwaarden mogen best gemotiveerd worden door egoïstische motieven!