---
title: "Test third party code"
author: "Karl van Heijster"
date: 2022-10-28T11:24:07+02:00
draft: true
comments: true
tags: ["boeken", "contracttesten", "testen", "third party code", "verantwoordelijkheid"]
summary: "Het updaten van *third party* code is net zozeer een risicovolle onderneming als het niet updaten ervan. In beide gevallen loop je kans op de introductie van bugs. Er is een uitweg uit dat probleem. En die uitweg is - zoals meestal in softwareontwikkeling - testen, testen, testen."
---

Code die je niet schrijft, maar wel gebruikt, is ook *jouw* code. Het is code waar jij voor verantwoordelijk bent - niet in de zin dat je die code per se hoeft te onderhouden[^1], maar wel in de zin dat als die code breekt, *jouw* code breekt.


Je bent verantwoordelijk voor de werking van de applicatie als geheel, of je nu honderd procent van alle regels code zelf hebt geschreven, of de boel slechts aan elkaar hebt gelijmd met blokjes die anderen voor je hebben aangeleverd.


## Plichten


Bij het gebruik van *third party* code komen enkele plichten kijken. 


De eerste is om zoveel mogelijk *up to date* te blijven met de nieuwste versies van die code. Wie - bewust of onbewust - achterloopt met het updaten van *third party* code, loopt daarmee een veiligheidsrisico. Een groot deel van de updates in *third party* code is immers niet bedoeld om nieuwe functionaliteit toe te voegen, maar om (security)bugs te fixen.


De tweede plicht die je als gebruiker van *third party* code hebt, is om ervoor te zorgen dat je applicatie blijft werken als je overstapt op een nieuwe versie. Dat is geen gegeven. Een update kan een API zodanig aanpassen dat je code breekt. Dat is vervelend, maar overkomelijk. Je komt er bij het compileren van je code immers al achter dat er een probleem is.


Maar updates kunnen ook subtielere problemen met zich meebrengen. Een update kan een bug fixen waar jouw code (handig?) gebruik van maakte. Dat hoeft niet per se in een veranderde interface te resulteren. De wijziging is op het syntactisch niveau compatibel met jouw gebruik ervan - maar op semantisch niveau niet meer. 


Het updaten van *third party* code is dus net zozeer een risicovolle onderneming als het niet updaten ervan. In beide gevallen loop je kans op de introductie van bugs. 


## Contract


Er is een uitweg uit dat probleem. En die uitweg is - zoals meestal in softwareontwikkeling - testen, testen, testen. Je behoort andermans code die te testen. 


De reden waarom je andermans code test, is echter een andere dan waarom je je eigen code test. In het geval van je eigen code, wil je er zeker van zijn dat de code geen bugs bevat.[^2] In het geval van *third party* code - dat wil zeggen: bij veelgebruikte *libraries* met miljoenen downloads - mag je er gerust van uitgaan dat de code zich op functioneel niveau naar behoren gedraagt.


Je test andermans code om het contract dat je met een *third party* aangaat expliciet vast te leggen. Je tests geven de ontwikkelaars in je team volgende informatie: dit zijn de functies die we uit hebben besteed aan deze externe partij, en dit zijn de *outputs* die we verwachten bij deze *inputs*. Niet voor niets worden dit soort tests *contracttests* genoemd.


## Efficiënt


Tests zijn de efficiëntste manier om te valideren dat de door jouw gebruikte *third party* code bij elke update blijft functioneren zoals voorheen. 


Wanneer de tests slagen, weet je dat je met zekerheid kunt zeggen dat eventuele bugs in je applicatie in elk geval niet dáár door veroorzaakt worden. 


En wanneer de tests falen, geven deze je alle informatie die je nodig hebt om het nieuwe gedrag in kaart te brengen. Als de tests niet meer compileren, dan geeft een goede *library* aan welke nieuwe methods de oude vervangen. Als de methods nieuwe waarden teruggeven, dan brengen de tests onmiddellijk in kaart wát die waarden precies zijn. Dit geeft je een enorme voorsprong in het diagnosticeren van het probleem.


## Omgaan met verandering


Software ontwikkelen is geen soloactiviteit. Je zult hoe dan ook gebruik maken van andermans code. En andermans code zal hoe dan ook veranderen - net als die van jou. 


Je kunt op drie manieren omgaan met die verandering: deze negeren en op het beste hopen; deze schoorvoetend slikken en op het beste hopen; of deze omarmen, testen en met zekerheid voorwaarts gaan.


Test *third party* code. - O, en lees ook [*Software Mistakes and Tradeoffs*](https://www.manning.com/books/software-mistakes-and-tradeoffs) van [Tomasz Lelek](https://www.linkedin.com/in/tomaszlelek/?locale=en_US) en [Jon Skeet](https://codeblog.jonskeet.uk/), want zij verwoorden het in hoofdstuk 9 een stuk beter dan ik. 


[^1]: Hoewel een bijdrage door de gebruikers van Open Source-projecten wel gewaardeerd wordt, zie ook [deze blog] (TECHORAMA).


[^2]: Althans, voor zover tests je die zekerheid kunnen geven. Een testsuite kan nooit bewijzen dat een codebase géén bugs bevat, het kan alleen bewijzen wanneer dat wél het geval is.
