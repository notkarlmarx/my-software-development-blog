---
title: "De wet van Postel"
author: "Karl van Heijster"
date: 2024-11-15T08:09:28+01:00
draft: false
comments: true
tags: ["eerlijke functies", "functies", "intentie van code", "leermoment", "proof of concept", "software ontwikkelen"]
summary: "Het is niet de verantwoordelijkheid van de aanroepende partij om de input van een functie te schiften opdat er valide waarden worden meegegeven. Een functie moet zo eerlijk mogelijk zijn in wat het accepteert -- maar daar waar er speelruimte bestaat is het de verantwoordelijkheid *van de functie zelf* om de inputs te valideren."
---

In [*Software Design for Flexibility*](https://mitpress.mit.edu/9780262045490/software-design-for-flexibility/ "'Software Design for Flexibility: How to Avoid Programming Yourself into a Corner', Chris Hanson & Gerald Jay Sussman @ MIT Press") van [Chris Hanson](https://people.csail.mit.edu/cph/) en [Gerald Jay Sussman](https://en.wikipedia.org/wiki/Gerald_Jay_Sussman "'Gerald Jay Sussman', Wikipedia") lezen we: 


> For maximum flexibility the range of outputs of a part should be quite small and well defined -- much smaller than the range of acceptable inputs for any part that might receive that output. (...) 
>
> In software engineering this principle is enshrined as "[Postel's Law](https://en.wikipedia.org/wiki/Robustness_principle "'Robustness principle', Wikipedia")" in honor of internet pioneer [John Postel](https://en.wikipedia.org/wiki/Jon_Postel "'John Postel', Wikipedia"). In [RFC760](https://www.rfc-editor.org/rfc/rfc760), describing the internet protocal, he wrote: "The implementation of a protocol must be robust. Each implementation must expect to interoperate with others created by different individuals. While the goal of this specification is to be explicit about the protocol there is the possibility of differing interpretations. In general, an implementation should be conservative in its sending behavior, and liberal in its receiving behavior." This is usually summarized as "Be conservative in what you do, be liberal in what you accept from others."


Ik vond het een uitdagend idee, omdat het op het eerste gezicht lijkt te conflicteren met de notie van [eerlijke functies](/blog/22/07/wat-zijn-eerlijke-functies/ "'Wat zijn eerlijke functies?'"), een notie die ik de afgelopen jaren heb geïnternaliseerd in de code die ik schrijf.


## Context


Uiteraard is de vraag niet zo simpel als: wie van ons twee heeft gelijk? (En trouwens, als dat de vraag zou zijn, zou ik nooit durven beweren dat *ik* dan degene ben die gelijk heeft -- een andere toepassing van het idee "*be liberal in what you accept from others*".) De context waarin Postel zijn zogenoemde wet formuleerde, verschilt enorm van de mijne. 


Postels inputs zijn implementaties van protocollen die verschillend geïnterpreteerd kunnen worden. Die van mij zijn het resultaat van functies die ik veelal zelf heb geschreven. In dat laatste geval is het gevaar van uiteenlopende interpretaties dermate klein dat er aannames mogen worden gedaan over dat wat een functie binnenkrijgt -- en het verlies in flexibiliteit dat daarmee gepaard gaat is in dat geval een feature en geen bug.


En toch kwam ik laatst in een situatie terecht waarvan ik dacht: had ik maar van de wet van Postel geweten!


## Toetsen genereren


Maar eerst: wat achtergrond. Mijn team ontwikkelt, ter vervanging van een [*legacy*](/tags/legacy-code/ "Blogs met de tag 'legacy code'") applicatie, een systeem om toetsen mee te construeren. Het uitgangspunt van de *legacy* applicatie was: stel de gebruiker in staat om het eindproduct, de toets, in te voeren. Het uitgangspunt van het nieuwe systeem is: ondersteun de gebruiker in het productieproces, en genereer dan aan het eind van dat proces op basis van de werkdocumenten het eindproduct, de toets.


Om gebruikers de kracht van dat idee te demonstreren, hadden we als [*proof of concept*](/tags/proof-of-concept/ "Blogs met de tag 'proof of concept'") (POC) een uitgeklede versie van die toetsgenerator ingebouwd. De code kon maar met één soort toetsvragen omgaan, toetsvragen waarin er een vraag werd gesteld over een tekstuele bron. Uiteindelijk zou het systeem ook om moeten kunnen gaan met audio- en videobronnen, maar dat viel buiten de scope van de POC.


Eindgebruikers waren enthousiast over het idee, de POC was geslaagd. Daarna deed de werkelijkheid zijn ding, verschoven prioriteiten en verzamelde de functionaliteit een dikke laag stof.


## Maanden later


Uiteindelijk, maanden later, kwam daar echter het moment waarop ook de anderssoortige bronnen moesten worden ondersteund -- een taak die een collega van me oppakte. Hij paste de code van de toetsgenerator netjes aan, schreef tests die bewezen dat deze nu ook met audio- en videobronnen om kon gaan, en maakte een [*pull request*](/tags/pull-requests/ "Blogs met de tag 'pull request'") (PR) aan. Ik bekeek het PR, was tevreden met de wijziging, en dat was dat -- dacht ik.


Want: het werkte niet. -- "Hoezo, het werkt niet?" -- "Nou, als ik een toets met een audiobron wil genereren, dan krijg ik niks." -- "Hoezo, dan krijg je niks?" -- "Zoals ik het zeg: dan krijg ik niks." -- "Maar die functionaliteit is toch geïmplementeerd en getest?" -- En toch: onze tester kreeg helemaal niks.


Ik bekeek de toetsgenerator en de bijbehorende tests, en vergeleek deze met de data die onze tester over het lijntje stuurde, en ik kon met geen mogelijkheid de oorzaak van de bug ontwaren.


## De verkeerde plek


Maar dat was omdat ik op de verkeerde plek keek. Want de bug zat niet in de toetsgenerator -- het zat in het stukje daarvóór.


Oorspronkelijk kon de toetsgenerator alleen omgaan met tekstuele bronnen -- en ging keihard op zijn neus wanneer je daar een audio- of videobron in probeerde te duwen. Dus in de aanroepende code had ik iets als in de volgende pseudocode geschreven:


```cs
var textItems = items.Where(i => i.Source is Text);
var assessmentTest = AssessmentTestGenerator.Generate(textItems);
```


Hadden we dan geen tests voor dit stukje code? Jawel, ik had er maanden geleden een integratietest voor geschreven -- met een tekstuele bron, niet met een audiobron. En niet helemaal onterecht, want op het moment van schrijven ondersteunden we nog helemaal geen audio- of videobronnen, zo'n test was in de context van de POC overbodig.


Toen we al die tijd later terugkeerden naar de toetsgenerator, was de aanroepende code uit ons blikveld verdwenen.


## Verantwoordelijkheid


Had ik maar van de wet van Postel geweten! Dan had ik de oorspronkelijke code zo geschreven dat 'ie items met audio- en videobronnen wel als input geaccepteerd had, en zou conservatief zijn geweest in de manier waarop ik daarmee omging. (Waarschijnlijk zou ik een [`NotImplementedException`](https://learn.microsoft.com/en-us/dotnet/api/system.notimplementedexception "'NotImplementedException Class', Microsoft documentatie") of iets dergelijks hebben opgegooid.)


Natuurlijk, de context waarin John Postel zijn wet formuleerde verschilt nog steeds enorm van de mijne -- misschien zelfs in zo'n mate dat het aanroepen van die wet strikt genomen niet helemaal gepast is. Maar zelfs al is dit geen letterlijke toepassing van de wet, dan nog denk ik in haar geest: ik had in mijn oorspronkelijke implementatie wat liberaler mogen zijn in wat voor inputs ik accepteerde. 


(Een alternatief zou kunnen zijn: ik zou de input van de `Generate`-functie hebben kunnen beperken tot een `IEnumerable<ItemsWithTextSource>` in plaats van een `IEnumerable<Item>`.)


Je zou de zaak ook zo kunnen zien: het is niet de verantwoordelijkheid van de aanroepende partij om de input van een functie te schiften opdat er valide waarden worden meegegeven. Een functie moet zo eerlijk mogelijk zijn in wat het accepteert, daar sta ik nog steeds achter -- maar daar waar er speelruimte bestaat is het de verantwoordelijkheid *van de functie zelf* om de inputs te valideren.
