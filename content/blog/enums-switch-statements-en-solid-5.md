---
title: "Enums, Switch Statements en Solid - Deel 5"
date: 2021-05-06T04:41:16+02:00
draft: true
comments: true
tags: []
summary: ""
---

# SOLID en performance


Vorige week refactorde ik een stuk code om meer in lijn te zijn met het [*Open-closed* principe](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle). In plaats van een harde afhankelijkheid te coderen in de class die een ClaimProvider teruggeeft op basis van een `Permission`, gebruikten we [reflection](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/reflection) om deze classes op [runtime](https://en.wikipedia.org/wiki/Runtime_(program_lifecycle_phase)) terug te geven.


De class die we daarvoor aanmaakten, was een flink stuk groter dan de oorspronkelijke method:


{{< gist notkarlmarx 6bffec16a479461005daae78756edf72 "ClaimProviderFactory.cs">}}


Maar het grootste probleem van deze class is niet het aantal regels code, want dat is met 29 regels nog altijd zeer bescheiden. Het grootste probleem is de performance-impact die de keuze voor reflection met zich meebrengt. 


Het op runtime-niveau uitvragen van de eigenschappen van een class is niet gratis. Er is relatief veel processorkracht voor nodig, en onze class is op dit moment zo opgezet dat deze dure operatie elke keer wordt uitgevoerd als een ClaimProvider wordt opgehaald. Voor één gebruiker met lees-, schrijf- en verwijderrechten zou deze method al drie keer worden aangeroepen. Dat is al drie keer een performance-penalty. 


En stel je nu eens voor dat de `ClaimsHelper` wordt aangeroepen een een [foreach-loop](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/foreach-in) met 100 of 1.000 of misschien wel 10.000 gebruikers.


## Langzamer, maar hoeveel langzamer?


Wat te doen? 


Allereerst moeten we inzichtelijk maken hoe groot de performance penalty is die onze nieuwe opzet met zich meebrengt. Hiervoor gebruik ik een [open source](https://en.wikipedia.org/wiki/Open-source_model) project genaamd [BenchmarkDotNet](https://github.com/dotnet/BenchmarkDotNet).[^1] Deze tool roept de verschillende versies van `GetClaimsForUser()` aan die we in de loop van deze reeks hebben gemaakt, en houdt de snelheid en het geheugengebruik van elke implementatie bij.


Het is belangrijk om over dit soort gegevens te beschikken vóórdat je gaat refactoren om de performance van je code te verbeteren. Dat reflection een impact heeft op de snelheid van je applicatie is aannemelijk, maar pas als je weet hoe groot die impact is, kun je een geïnformeerde keuze maken over de vraag of die refactorslag de moeite waard is. 


Een kanttekening daarbij is dat de performance-penalty waar we het hier over hebben zich in termen van nanoseconden bevindt. De kans is groot dat dat verlies wegvalt tegenover veel duurdere operaties, zoals het aanspreken van een database. Desalniettemin, dat ontslaat je als ontwikkelaar niet van de plicht om een evenwicht te vinden tussen onderhoudbare en performante code. 


Onze tool levert de volgende informatie op, gesorteerd van de snelste implementatie naar de langzaamste:


|              Method | Gemiddelde | Foutmarge | Standaarddeviatie |  Mediaan | 
|-------------------- |-----------:|----------:|------------------:|---------:|
| [GetClaimsForUserV02](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V02/ClaimsHelper.cs) |   1.134 us | 0.0226 us |         0.0390 us | 1.136 us |
| [GetClaimsForUserV00](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Original/ClaimsHelper.cs) |   1.194 us | 0.0237 us |         0.0633 us | 1.183 us |
| [GetClaimsForUserV01](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V01/ClaimsHelper.cs) |   1.218 us | 0.0271 us |         0.0755 us | 1.199 us |
| [GetClaimsForUserV03](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V03/ClaimsHelper.cs) |   9.231 us | 0.1828 us |         0.5096 us | 9.151 us |


(V00 is de originele code. De verdere versies zijn gerefactord: V01 op basis van het *Single responsibility* principe; V02 de op basis van het *Dependency inversion*-principe, en V03 op basis van het *Open closed*-principe.)


Zoals je ziet, ontlopen V01 en V02 van de `ClaimsHelper` het origineel nauwelijks. V02 lijkt zelfs nog iets sneller te zijn, maar dat verschil valt binnen de foutmarge en is dus verwaarloosbaar.


V03 is daarentegen bijna acht keer langzamer dan de rest. *Ouch!*


## Langzaamaan steeds iets beter


...


|              Method | Gemiddelde | Foutmarge | Standaarddeviatie |  Mediaan | 
|-------------------- |-----------:|----------:|------------------:|---------:|
| GetClaimsForUserV02 |   1.134 us | 0.0226 us |         0.0390 us | 1.136 us |
| GetClaimsForUserV00 |   1.194 us | 0.0237 us |         0.0633 us | 1.183 us |
| GetClaimsForUserV01 |   1.218 us | 0.0271 us |         0.0755 us | 1.199 us |
| GetClaimsForUserV06 |   1.388 us | 0.0276 us |         0.0526 us | 1.380 us |
| GetClaimsForUserV05 |   4.211 us | 0.1071 us |         0.3124 us | 4.128 us |
| GetClaimsForUserV04 |   4.575 us | 0.0913 us |         0.1624 us | 4.551 us |
| GetClaimsForUserV03 |   9.231 us | 0.1828 us |         0.5096 us | 9.151 us |


[^1]: Met dank aan [Nick Chapsas](https://www.youtube.com/channel/UCrkPsvLGln62OMZRO6K-llg), die de werking van het project in deze [video](https://www.youtube.com/watch?v=EWmufbVF2A4) beter uitlegt dan ik in tekst zou kunnen doen.
