---
title: "YAGNI veronderstelt tests"
author: "Karl van Heijster"
date: 2024-02-09T11:25:44+01:00
draft: true
comments: true
tags: ["leermoment", "mentaal model", "testen", "vertrouwen", "YAGNI"]
summary: "Er zijn twee soorten ontwikkelaars: ontwikkelaars die roepen: \"*You ain't gonna need it*\", en ontwikkelaars die mompelen: \"Ja ja, dat roep je wel, maar ik bouw het voor de zekerheid toch maar in.\" Ik behoor tot het eerste kamp; enkele van mijn collega's tot het tweede. -- Maar waarom?"
---

Er zijn twee soorten ontwikkelaars: ontwikkelaars die roepen: "*You ain't gonna need it*" ([YAGNI](/tags/yagni/ "Blogs met de tag 'YAGNI'"), en ontwikkelaars die mompelen: "Ja ja, dat roep je wel, maar ik bouw het voor de zekerheid toch maar in." Ik behoor tot het eerste kamp; enkele van mijn collega's tot het tweede. 


Mijn redenering is als volgt. Alle code die ik niet schrijf hoef ik niet te schrijven, dus dat bespaart me tijd. Alle code die ik niet schrijf hoef ik niet te onderhouden, dus dat bespaart me werk. Alle code die ik niet schrijf hoef ik niet te debuggen, dus dat scheelt me hoofdbrekens. Dus hoe minder code ik schrijf *die geen onmiddellijke waarde toevoegt* (een belangrijke kwalificatie!), hoe beter.


## Verbaasd


Lang heb ik me erover verbaasd dat mijn collega's daar anders tegenaan keken. Als er werd gevraagd om te kunnen zoeken op een titelveld, bijvoorbeeld, dan bouwden ze óók de mogelijkheid in op de beschrijving te zoeken. Omdat ze dachten: nu vraag je om de titel, tuurlijk, maar straks ga je ook om de beschrijving vragen, en dan heb ik dan geen werk meer aan. Ze redeneerden: het is nu voor mij een kleine moeite, dus waarom zou ik het niet doen? 


Maar als blijkt dat er nooit om de functionaliteit wordt gevraagd om te kunnen zoeken op de beschrijving, dan is de code complexer dan nodig -- met alle onderhoudslast die daarbij komt kijken. Denk eens aan alle frustratie die je je had kunnen besparen wanneer blijkt dat een moeilijk reproduceerbare bug voort bleek te komen uit een stuk code waar niemand om heeft gevraagd en daarom door helemaal niemand wordt gebruikt!


## Een wereld zonder tests


Opeens viel er een kwartje: mijn collega's leven nog altijd in een wereld zonder tests, zonder vangnet.[^1] Hun [mentale model](/tags/mentaal-model/ "Blogs met de tag 'mentaal model'") is nog niet aangepast naar een nieuwe situatie, waarin code eenvoudig te wijzigen is omdat er een uitgebreide testsuite is die je onmiddellijke feedback geeft over de werking van het systeem. Ze voelen de implicaties van een goede testcoverage nog niet in hun vezels. 


Ga maar na hoe de wereld eruitziet zonder zo'n vangnet. In zo'n situatie vormt elke codewijziging een risico. Een verandering in het ene deel van het systeem kan, zonder dat je het weet, een ander deel van het systeem om zeep helpen. Je denkt als ontwikkelaar daarom wel twee keer na voordat je code aanraakt -- ofwel om het gedrag te wijzigen, ofwel om de code te refactoren. In zo'n wereld loont het zich om te denken: ik bouw deze feature nu alvast in, want nu zit ik diep in deze materie en nu zie ik het wanneer ik iets kapotmaak. Inderdaad: nu is het nog een kleine moeite. Als ik het straks doe, is alle context die ik nu in mijn hoofd heb verdwenen, en ik heb geen garantie dat ik die dan terug kan halen.


Dit is de wereld waar mijn collega's soms tientallen jaren in hebben gebivakkeerd. De gewoonten die ze zich in die jaren eigen hebben gemaakt, zijn niet eenvoudig af te schudden.


## Voorwaarden


Wanneer je een goede, uitgebreide testsuite hebt, is voor altijd vastgelegd aan welke voorwaarden het gedrag van een deel code moet voldoen. De context is bewaard gebleven. Sterker nog, er is een automatisch mechanisme in werking dat je waarschuwt wanneer er niet meer aan de verwachte voorwaarden wordt voldaan. Daarom is het niet langer risicovol om de code te wijzigen. Wanneer je je daar bewust van bent, zul je niet langer terughoudend zijn om dat te doen.


Dat opent de ruimte om te kunnen zeggen: er wordt nu nog niet om deze functionaliteit gevraagd, maar ik ben er vrij zeker van dat ik deze straks redelijk eenvoudig toe moet kunnen voegen. En zelfs al blijkt het minder eenvoudig dan gedacht, dan nog weet ik de middelen heb om ervoor te zorgen dat ik de huidige werking van het systeem in elk geval niet ongewild om zeep help. Tests geven je de informatie die je nodig hebt om iets *later* zonder risico te wijzigen.


Het is niet voldoende om te roepen dat je *dit* of *dat* nu nog niet nodig hebt, en daarom niet hoeft te programmeren. Je moet een team laten zien dat ze de middelen hebben om het te bouwen wanneer het nodig is. YAGNI veronderstelt tests. 


[^1]: Ik bedoel natuurlijk: ze *denken* te leven in zo'n wereld, want met mij in je team kom je er niet mee weg om code te wijzigen zonder bijbehorende tests te hebben geschreven. Zie ook [deze](/blog/23/09/drie-vragen-die-elk-pull-request-moet-beantwoorden/ "'Drie vragen die elk pull request moet beantwoorden'") en [deze blog](/blog/23/07/de-tester-als-code-reviewer/ "'De tester als code reviewer'").
