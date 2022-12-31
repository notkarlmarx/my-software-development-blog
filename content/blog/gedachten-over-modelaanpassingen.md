---
title: "Gedachten over modelaanpassingen"
author: "Karl van Heijster"
date: 2022-12-31T14:29:53+01:00
draft: true
comments: true
tags: ["agile ontwikkeling", "datamigratie", "leermoment", "software ontwikkelen"]
summary: "Wanneer er modelwijzigingen in het spel zijn, dan is een wijziging van de code alléén niet voldoende. Je zult ook moeten zorgen voor een migratie die de oude data omzet naar het nieuwe model. Zo'n migratie kan verschillende vormen aannemen - *big bang* of stapje voor stapje -, maar dat 'ie er moet komen, staat vast. De vraag waar ik me op wil richten is: wannéér moet die migratie er komen?"
---

Mijn team kwam een tijd terug tot de conclusie dat we ons datamodel om moesten gooien om een nieuwe requirement te kunnen ondersteunen.


Dat is een pijnlijke constatering - maar niet omdat het vreemd is dat ons model niet bestand is tegen nieuwe requirements. Maar weinig code is bestand tegen nieuwe requirements. Sterker nog, het is een antipatroon om code te schrijven die allerlei mogelijke veranderingen aankan. Zulke code schent een van de fundamenteelste principes van Agile softwareontwikkeling: *schrijf eenvoudige code*.


Het is normaal dat code moet worden aangepast, naarmate er nieuwe requirements boven komen drijven. Dat is de enige manier voorwaarts.


## Data


Modelwijzigingen zijn pijnlijk, desalniettemin, en dat is omdat er bij dit soort codewijzigingen ook data komt kijken. 


Het aanpassen van een algoritme is klein bier vergeleken met dit soort wijzigingen. Zulke wijzigingen raken alleen code. (Al kun je je afvragen waar het onderscheid tussen code en data precies zit - en dat is overigens precies wat ik [Kevlin Henney](http://kevlin.tel/) een tijd terug zag doen tijdens een sessie op [DevTernity](https://devternity.com/).) Aangenomen dat je wijziging het bestaande gedrag intact houdt, en daar bovenop nieuw gedrag bouwt, kun je deze in één keer doorzetten naar je *develop*-branch.


Wanneer er modelwijzigingen in het spel zijn, dan is een wijziging van de code alléén niet voldoende. Je zult ook moeten zorgen voor een migratie die de oude data omzet naar het nieuwe model. Zo'n migratie kan verschillende vormen aannemen - *big bang* of stapje voor stapje (zie [deze](/blog/21/09/stapje-voor-stapje-data-migreren/) en [deze](/blog/21/10/evolutionaire-datamigratie-met-fluentmigrator/) blog) -, maar dat 'ie er moet komen, staat vast.


## Wanneer


De vraag waar ik me op wil richten is: wannéér moet die migratie er komen?


Een voor de hand liggend antwoord is: nu meteen. Of, preciezer: vóórdat je de nieuwe feature inbouwt op basis van de nieuwe requirement. Om deze te kunnen ondersteunen is het nodig dat de code gebruik maakt van het nieuwe model.


Maar het probleem daarvan is: hoe weet je dat het nieuwe model *klopt*? Wat is de *test case* voor dit nieuwe model? De nieuwe requirement die we net noemden? In hoeverre hebben we grip op die requirement? Het zou zomaar kunnen dat je al je data gemigreerd hebt, begint te coderen aan de nieuwe feature, en er dan achter komt dat je iets over het hoofd hebt gezien.


\- Dat is geen fout in je manier van werken. Dat ís je manier van werken. Wie Agile software ontwikkelt, leert elke iteratie iets nieuws over het probleem- en/of oplossingsdomein waar 'ie in werkt. Wie inziet dat het model niet volledig voldoet, lijdt geen nederlaag, maar een overwinning.


Natuurlijk, als je de vorige Sprint al je data hebt gemigreerd naar een nieuw model, en er deze Sprint achter komt dat dat model niet helemaal is wat het moet zijn, dan *voelt* het wel als een nederlaag.


## Wachten


Mijn team kwam daarom tot de conclusie: laten we met die migratie nog even wachten. Laten we deze Sprint een nieuw model optuigen náást het oude model, en de Sprint erop kijken in hoeverre het nieuwe model voldoet.


Het bleek een goede keus te zijn, want een stuk of zes, zeven verhitte discussies later kregen verschillende delen in het model een totaal andere invulling dan voorheen verwacht. Theorie en praktijk bleken meermaals uiteen te liggen. Wat er op papier goed uit zag, leverde in de code problemen op. Zaken konden worden versimpeld, of moesten juist worden uitgebreid om de nieuwe feature rond te krijgen.


Het model staat niet los van de code. Pas door met de code aan de slag te gaan, kregen we grip op het model. - Niet dat alle discussies die we hadden vóórdat we aan de feature begonnen, zinloos waren. Maar de oplossing die we op basis van die discussies bedacht hadden, was er duidelijk een op basis van een incompleet begrip van de oplossing.


## Volwassen


Dit is misschien een open deur, maar wat blijkt: je hóeft nog helemaal niet je data om te hebben gezet, vóórdat je aan de feature begint. Het enige wat je nodig hebt is een model en een boel unittests die de nieuwe requirements goed weergeven. Je kunt - nee, je móet - hier een hele tijd mee spelen, voordat je kunt zeggen: nu is het nieuwe model volwassen genoeg om de data te migreren.


Ons oorspronkelijke plan was: het model aanpassen en de data migreren in Sprint 1, de nieuwe feature coderen in Sprint 2, en op basis van feedback de boel verfijnen in Sprint 3. Maar wat we deden was: het model aanpassen in Sprint 1; daarna beginnen met de feature; op basis van tests met dummy-data feedback verzamelen, en de boel verfijnen in Sprint 2 en 3. Uiteindelijk migreeerden we de data veel later dan gedacht.


En gelukkig maar, want het model was nog lang niet volwassen genoeg om dit in Sprint 1 te kunnen doen.


Dus ja, modelwijzigingen zijn pijnlijk omdat er datamigraties bij komen kijken. De truc is daarom om ze verantwoord uit te voeren. En verantwoord wil in dit geval zeggen: pas als je zeker weet dat het nieuwe model voldoet. De enige manier om daar achter te komen, is door het tegen de nieuwe feature te testen.


Datamigratie komt het laatst kijken in de ontwikkelcyclus - niet het eerst.
