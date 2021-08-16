---
title: "Check Op Permissies, Niet Op Rollen"
author: "Karl van Heijster"
date: 2021-08-13T11:04:42+02:00
draft: true
comments: true
tags: ["autorisatie", "intentie van code", "incrementele ontwikkeling", "leermoment", "open-closed principe", "software ontwikkelen"]
summary: "Op een gegeven moment begon onze autorisatiecode uit de hand te lopen. De code in onze front-end was haast onleesbaar geworden van alle rollenchecks die de logica vervuilde. Erop terugkijkend, hadden we twee fouten gemaakt in onze oorspronkelijke implementatie. Ten eerste hadden we gebruikers de mogelijkheid gegeven meerdere rollen te hebben, en ten tweede bevonden onze checks zich op een te grof niveau."
---

Toch nog even over [die Kwestie Autorisatie](/blog/21/07/de-kwestie-autorisatie/).


Zoals ik zei, op een gegeven moment begon onze autorisatiecode uit de hand te lopen. De code in onze front-end was haast onleesbaar geworden van alle rollenchecks die de logica vervuilde.


Erop terugkijkend, hadden we twee fouten gemaakt in onze oorspronkelijke implementatie. Ten eerste hadden we gebruikers de mogelijkheid gegeven meerdere rollen te hebben, en ten tweede bevonden onze checks zich op een te grof niveau.


## Hoeveel rollen is genoeg?


Het idee achter het hebben van meerdere rollen, was dat we op die manier een flexibel systeem konden ontwikkelen dat snel kon inspringen op bepaalde behoeften. Door gebruikers niet te beperken tot één rol, zouden we makkelijk nieuwe functionaliteiten kunnen ontsluiten door de relevante gebruikers een extra rol toe te kennen.


Het bleek nodeloos complex. Verschillende rollen kunnen elkaar namelijk bijten. Stel, we hebben twee rollen *a* en *b*. Gebruikers met rol *a* hebben toegang tot een functionaliteit *x*, en gebruikers met rol *b* niet. Duidelijk, toch? Maar wat als een gebruiker zowel rol *a* als *b* heeft? Heeft diegene dan toegang tot die functionaliteit of niet?


Dit probleem is al moeilijk genoeg wanneer een gebruiker twee rollen heeft. Maar wat gebeurt er als er sprake is van drie, vijf of tien rollen? Het aantal condities waar je als programmeur rekening mee moet houden, neemt exponentieel toe met elke rol. Dit levert een ware onderhoudsnachtmerrie op.


Bovendien, het is de vraag of deze flexibiliteit in rollen überhaupt wel nodig is. De bedrijfsinhoudelijke processsen waar we voor ontwikkelen, zijn stabiel, relatief eenvoudig en kennen welonderscheiden rollen. Het is niet zo dat gebruikers constant van in hun rol wisselen in het bedrijfsproces, dus waarom wel in onze code?


Het team besloot daarom om het wisselen tussen rollen te laten vallen. Gebruikers krijgen één rol, en die houden ze.


## Waar check je op?


Dit alleen is echter niet voldoende om de complexiteit van de code te verminderen. Onze front-end ontsloot aanvankelijk bepaalde functionaliteiten door te checken op rol. Heeft een gebruiker rol *a*? Dan heeft deze toegang. Heeft die gebruiker rol *b*, dan niet. Eenvoudig genoeg, zou je denken.


Maar wat als zowel rol *a* als *b* toegang moeten hebben tot een bepaalde functionaliteit? Zouden we dan een check in moeten bouwen die controleert of de gebruiker één van beide rollen heeft?


Dat zou een mogelijke oplossing kunnen zijn. Maar het is een arbeidsintensieve. Dat betekent dat er een codewijziging zou moeten worden doorgevoerd, elke keer wanneer de inhoudelijke invulling van de rol verandert. En ook hier neemt de complexiteit weer toe naarmate er meer rollen bij komen.


## Permissies


Het team heeft daarom iets anders bedacht om op te checken: permissies. Het idee hierachter is heel eenvoudig. Bepaalde rollen hebben bepaalde permissies. Deze kunnen overlappen. Als zowel rol *a* als *b* toegang hebben tot een bepaalde funcitonaliteit *x*, dan hebben ze beide de permissie *toegang_functionaliteit_x*.


Ik haal deze tabel er nog eens bij. De rollen zijn gespecificeerd in de eerste rij. De permissies zijn gespecificeerd in de eerste kolom.


|                   | Rol *a* | Rol *b* | Rol *c* |
| ----------------- | ------- | ------- | ------- |
| **Permissie *x*** | x       |         | x       |
| **Permissie *y*** | x       | x       |         |
| **Permissie *z*** |         |         | x       |
<br>


Je zou rollen kunnen zien als een *shorthand* voor het hebben van een bepaalde set permissies. In plaats van op de rol te checken, checken we op de permissies.


Daardoor wordt het mogelijk om rollen inhoudelijk te wijzigen, zonder codewijzigingen door te voeren.[^1] Wanneer rol *b* alsnog toegang nodig heeft tot functionaliteit *x*, dan is dat een kwestie van het toekennen van een extra permissie. De code aan de front end blijft ongewijzigd, want die controleerde toch al op *toegang_functionaliteit_x*. 


## Hetzelfde, maar dan anders


In wezen is dit niets nieuws. Sterker nog, uiteindelijk is dit precies wat onze vorige check ook deed. 


Maar het verschil tussen checken op rollen en permissies is als volgt. Wanneer je op rol checkt, blijven de permissies die bij een bepaalde rol horen, impliciet. Door op permissies zelf te checken, word je gedwongen om te expliciet specificeren wat datgene is wat een rol mag en wat niet. Dat maakt de intentie van die oorspronkelijke rollencheck zichtbaar voor de ontwikkelaar.


Hoewel er veel meer permissies zijn dan rollen, verminderen onze checks op permissies de complexiteit van de code. Want bij elke welonderscheiden functionaliteit hoort één permissie, in plaats van een veelvoud aan (combinaties van) rollen.


Tegelijkertijd behoudt het de flexibiliteit. Want rollen kunnen nu worden uitgebreid met bepaalde permissies, mocht daar behoefte aan zijn. Op deze manier kunnen functionaliteiten worden ontsloten zonder codewijzigingen.


Daarom: check op permissies, niet op rollen.


[^1]: Daarmee voldoet deze oplossing, anders dan de oorspronkelijke, tevens aan het [*open-closed principe*](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle). Tel uit je winst!
