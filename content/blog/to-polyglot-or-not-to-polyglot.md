---
title: "To polyglot or not to polyglot"
author: "Karl van Heijster"
date: 2022-03-11T12:27:40+01:00
draft: true
comments: true
tags: ["boeken", "polyglot", "test-driven development"]
summary: "Laten we aannemen dat sommige programmeerproblemen zich meer voor objectgeoriënteerde talen lenen, en andere meer voor functionele.[^1] Is het dan niet logisch om de taal te kiezen die het best bij het probleem past? Het antwoord op die vraag is: ja en nee. Ja, het is verstandig om *the right tool for the job* te kiezen - dat is een open deur. Maar zelfs als we aannemen dat de ene taal zich beter leent voor het probleem, is het maar de vraag of het verstandig is dat *jij* die taal *nu* inzet om *dat probleem* op te lossen. "
---

# Gedachten naar aanleiding van *Learning Test-Driven Development* - Deel 3


*Onlangs las ik* [Learning Test-Driven Development](https://www.oreilly.com/library/view/learning-test-driven-development/9781098106461/) *van [Saleem Siddiqui](https://www.linkedin.com/in/ssiddiqui/). Ik zal met de deur in huis vallen: het boek is een aanrader. Zo erg zelfs, dat ik er wel vier blogs uit wist te persen! Vandaag: over het leren van meerdere programmeertalen.*


De ondertitel van *Learning Test-Driven Development* is *A Polyglot Guide to Writing Uncluttered Code*. Het boek behandelt TDD in drie talen: [Go](https://go.dev/), [JavaScript](https://nl.wikipedia.org/wiki/JavaScript) en [Python](https://www.python.org/).


Vanuit een marketingpectief is dit een goede zet, natuurlijk. Door TDD in drie talen aan te bieden, spreekt Siddiqui een groter publiek aan dan wanneer 'ie zich tot één van die drie talen beperkt had.


Maar ook inhoudelijk bezien is de keuze voor een meertalige aanpak te verdedigen. TDD is immers niet gebonden aan een specifieke taal - zelfs niet aan een programmeerparadigma. Het is een universele praktijk. Of je nu objectgeoriënteerde of functionele code schrijft, de praktijk van TDD loont zich altijd. 


Siddiqui geeft aan dat zijn boek op meerdere manieren gelezen kan worden. Je kunt het boek bijvoorbeeld drie keer doorlopen - één keer voor elke taal. Of je kunt het van begin tot eind lezen, waarbij je voor elke feature van taal naar taal overstapt. Een mengvorm tussen beide is natuurlijk ook mogelijk.


## Zinvol


De vraag werpt zich echter op: hoe zinvol is dat? Aangenomen dat ik al overtuigd ben van de universaliteit van TDD, waarom zou ik dezelfde tests en functionaliteit in drie verschillende talen willen implementeren? Ik stel die vraag, onder andere naar aanleiding van deze video van [Tim Corey](https://www.iamtimcorey.com/):


{{<youtube id="IeN4mrGBNQU" title="Why Shouldn't I Choose the Best Language for the Job?" >}}
<br>


In die video vraagt Corey zich af waarom je je in verschillende programmeertalen zou willen verdiepen. Je kunt je verschillende redenen indenken, bijvoorbeeld dat het goed staat op je CV. Of dat het leren van verschillende talen je kennis verbreedt over wat er allemaal mogelijk is in code. En dat kan ook zijn weerslag hebben in je moederprogrammeertaal. Wie zich in [F#](https://fsharp.org/) verdiept, zal meer oog krijgen voor de [functionele delen](https://hamidmosalla.com/2019/04/25/functional-programming-in-c-sharp-a-brief-guide/) van [C#](https://docs.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/).


Een andere reden valt af te lezen uit de titel van Coreys videopodcast. Laten we aannemen dat sommige programmeerproblemen zich meer voor objectgeoriënteerde talen lenen, en andere meer voor functionele.[^1] Is het dan niet logisch om de taal te kiezen die het best bij het probleem past?


## ...of toch niet?


Het antwoord op die vraag is: ja en nee. Ja, het is verstandig om *the right tool for the job* te kiezen - dat is een open deur. Maar zelfs als we aannemen dat de ene taal zich beter leent voor het probleem, is het maar de vraag of het verstandig is dat *jij* die taal *nu* inzet om *dat probleem* op te lossen. 


Je een programmeertaal eigen maken kost namelijk tijd. Het is niet voldoende om de syntax te kennen. Je moet ook een idee hebben van de achterliggende concepten van een taal, en het ecosysteem eromheen. Wat voor *libraries* zijn er beschikbaar? Hoe zet je een unit test op? 


Dat soort dingen vragen om praktijkervaring - en die heb je, of die heb je niet. En in dat laatste geval is het - buiten de context van een demoapplicatie - ronduit onverantwoord om de in theorie "beste" taal voor het probleem te kiezen.


Een illustratie - niet eens op het niveau van talen, maar over een framework. Mijn team heeft ervaring met [HTML](https://nl.wikipedia.org/wiki/HyperText_Markup_Language) en [CSS](https://nl.wikipedia.org/wiki/Cascading_Style_Sheets), en heeft voldoende JavaScript gezien om zich [TypeScript](https://www.typescriptlang.org/) zonder al te veel problemen eigen te maken. Maar dat betekent niet dat we zó kunnen beginnen een [Angular](https://angular.io/)-applicatie in elkaar te zetten. We hebben moeten leren wat [componenten](https://angular.io/api/core/Component) en [services](https://angular.io/guide/architecture-services) en [modules](https://angular.io/guide/architecture-modules) zijn en hoe ze zich tot elkaar verhouden. En de weg naar het schrijven van een simpele unit test was [lang en pijnlijk](/blog/22/01/de-leercurve-van-angulartests-beklimmen-deel-1/).


Precies om die reden zegt Corey dan ook: waak ervoor teveel talen (c.q. frameworks) op je CV te zetten. Wie een half jaar ervaring heeft op twaalf talen en in dertien frameworks, heeft feitelijk nul ervaring in allemaal!


## JavaScript, Go


Daarmee zeg ik niet dat het niet zinvol is om van tijd tot tijd een nieuwe programmeertaal te leren. De voordelen die ik hierboven noemde, die blijven overeind staan. Maar het is goed om je te realiseren dat het leren van een taal een *commitment* is. Een polyglot is niet iemand die meerdere talen spreekt, een polyglot spreekt meerdere talen *vloeiend*. En dat gebeurt niet van de ene op de andere dag.


Ik heb *Learning Test-Driven Development* tweemaal doorlopen: de eerste keer in JavaScript en de tweede keer in Go. De eerste keer omwille van de TDD, en de tweede keer om van de taal te proeven. En hoewel dat me een gevoel heeft gegeven van Go's syntax, zou ik niet durven beweren enige ervaring te hebben in die taal. 


Hoe zinvol die exercitie was? Ik ben in elk geval niet gaan twijfelen aan de waarde van TDD, veel meer kan ik er niet over zeggen!


## Meer in deze reeks


1. [Agile en Test-Driven Development] (LINK)
2. [Eén test per keer] (LINK)
3. ***To polyglot or not to polyglot***
4. Legacy code en Test-Driven Development [binnenkort]


[^1]: Dit is een controversieel statement, afhankelijk van hoe je 'm uitlegt. Het is niet zo dat de ene of de andere taal *per definitie* beter bij een probleem past of niet. Het is wel zo dat een taal bepaalde features kan hebben die de oplossing eenvoudiger of eleganter maken dan een andere taal. De hamvraag is eigenlijk: wat maakt het dat een bepaalde taal beter geschikt is voor een bepaald programmeerprobleem dan een andere taal? - en het is niet duidelijk of daar eenvoudig antwoord op te geven valt.
