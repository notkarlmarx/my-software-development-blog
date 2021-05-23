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


Het op runtime-niveau uitvragen van de eigenschappen van een class is niet gratis. Er is relatief veel processorkracht voor nodig. En onze class is op dit moment zo opgezet dat deze dure operatie elke keer wordt uitgevoerd als een ClaimProvider wordt opgehaald. Voor één gebruiker met lees-, schrijf- en verwijderrechten zou deze method al drie keer worden aangeroepen. Dat is al drie keer een performance-penalty. 


En stel je nu eens voor dat de `ClaimsHelper` wordt aangeroepen een een [foreach-loop](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/foreach-in) met 100 of 1.000 of misschien wel 10.000 gebruikers.


## Langzamer, maar hoeveel langzamer?


Wat te doen? 


Allereerst moeten we inzichtelijk maken hoe groot de performance penalty is die onze nieuwe opzet met zich meebrengt. Hiervoor gebruik ik een [open source](https://en.wikipedia.org/wiki/Open-source_model) project genaamd [BenchmarkDotNet](https://github.com/dotnet/BenchmarkDotNet).[^1] Deze tool roept de verschillende versies van `GetClaimsForUser()` aan die we in de loop van deze reeks hebben gemaakt, en houdt de snelheid en het geheugengebruik van elke implementatie bij.


Het is belangrijk om over dit soort gegevens te beschikken vóórdat je gaat refactoren om de performance van je code te verbeteren. Dat reflection een impact heeft op de snelheid van je applicatie is aannemelijk, maar pas als je weet hoe groot die impact is, kun je een geïnformeerde keuze maken over de vraag of die refactorslag de moeite waard is. 


Een kanttekening daarbij is dat de performance-penalty waar we het hier over hebben zich in termen van nanoseconden bevindt. De kans is groot dat dat verlies wegvalt tegenover veel duurdere operaties, zoals het aanspreken van een database. Desalniettemin, dat ontslaat je als ontwikkelaar niet van de plicht om een evenwicht te vinden tussen onderhoudbare en performante code. 


Onze tool levert de volgende informatie op, gesorteerd van de snelste implementatie naar de langzaamste:


| Method | Gem. | Foutmarge | Standaarddeviatie | Mediaan | 
|-------------------- |-----------:|----------:|------------------:|---------:|
| [GetClaimsForUserV02](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V02/ClaimsHelper.cs) | 1.134 us | 0.0226 us | 0.0390 us | 1.136 us |
| [GetClaimsForUserV00](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Original/ClaimsHelper.cs) | 1.194 us | 0.0237 us | 0.0633 us | 1.183 us |
| [GetClaimsForUserV01](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V01/ClaimsHelper.cs) | 1.218 us | 0.0271 us | 0.0755 us | 1.199 us |
| [GetClaimsForUserV03](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V03/ClaimsHelper.cs) | 9.231 us | 0.1828 us | 0.5096 us | 9.151 us |

<br/>

(V00 is de originele code. De oplopende versies zijn gerefactord: V01 op basis van het *Single responsibility* principe; V02 de op basis van het *Dependency inversion*-principe, en V03 op basis van het *Open closed*-principe.)


Zoals je ziet, ontlopen V01 en V02 van de `ClaimsHelper` het origineel nauwelijks. V02 lijkt zelfs nog iets sneller te zijn, maar dat verschil valt binnen de foutmarge en is dus verwaarloosbaar.


V03 is daarentegen bijna acht keer langzamer dan de rest. *Ouch!*


## Langzaamaan steeds iets beter


In wat volgt zal ik de stappen laten zien die ik heb ondernomen in een poging de performance van de `ClaimsProviderFactory` te verbeteren. 


Maar eerst een disclaimer. Ondanks dat ik toch al een paar jaar programmeer, was refactoren op basis van performanceoverwegingen een relatief nieuwe ervaring voor me. Het viel me op dat ik me in mijn ontwikkeling als ontwikkelaar met name heb gefocust op het schrijven van leesbare en onderhoudbare code. 


Performancevraagstukken hebben in mijn dagelijks ontwikkelwerk eigenlijk nauwelijks een rol gespeeld. Voor een deel is dat misschien geluk of luxe geweest. Maar het zegt denk ik ook iets over het belang van performance ten opzichte van lees- en onderhoudbaarheid. Deze eigenschappen van de code moeten op orde zijn vóórdat je kunt gaan optimaliseren voor performance.


Dat gezegd hebbende, mijn eerste indruk was om de lijst `ClaimProviders` (of liever: de lijst van types die `IProvideClaims` implementeren) te vangen in een globale variabele. Deze lijst verschilt immers niet van aanroep tot aanroep en kan dus in het geheugen bewaard blijven.


{{< gist notkarlmarx a5571b15998ff4b86de84d368152ff0b "ClaimProviderFactoryV04.cs">}}


Maar helemaal tevreden over deze aanpak was ik niet. `_claimProviderTypes` heeft hier de functie van een instance variable, terwijl de class static is en dus geen instanties heeft. Dit ontwerp wil twee dingen tegelijkertijd. 


(De class is overigens static, omdat de winst van het bewaren van de variabelen verloren gaat als er elke keer een nieuwe instantie van moet worden gemaakt. Althans, ik denk dat dat de reden is waarom ik hier een static class van heb gemaakt. Om eerlijk te zijn maakte ik die keuze met mijn onderbuik. Als ik onzin blijk te praten, dan hoor ik het graag.)


Ik vroeg me af hoe ik de statische aard van de class kon rijmen met de noodzaak van een geïnstantieerde variabele. Het antwoord: het [singleton-patroon](https://en.wikipedia.org/wiki/Singleton_pattern).


{{< gist notkarlmarx a5571b15998ff4b86de84d368152ff0b "ClaimProviderFactoryV05.cs">}}


Met een singleton zorg je ervoor dat je aanroepende code telkens dezelfde instantie van een object aanroept. Dit is een ideaal patroon voor wanneer je de performance impact van de instantiatie een object wil beperken. 


Voor deze specifieke use case is dit patroon zelfs misschien wat teveel van het goede. De complexiteit van de code neemt ten opzichte van de performancewinst (denk erom: we hebben het over nanoseconden) dusdanig toe, dat ik wel twee keer erover na zou denken om deze code in productie te nemen. Maar dit is een oefening in het opkrikken van performance, dus hier is het op zijn plek.


## Een tussenstand


Laten we eens kijken hoe onze pogingen tot nu toe zich verhouden tot de oorspronkelijke metingen:


|              Method | Gem. | Foutmarge | Standaarddeviatie |  Mediaan | 
|-------------------- |-----:|----------:|------------------:|---------:|
| [GetClaimsForUserV05](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V05/ClaimsHelper.cs) | 4.211 us | 0.1071 us |     0.3124 us | 4.128 us |
| [GetClaimsForUserV04](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V04/ClaimsHelper.cs) | 4.575 us | 0.0913 us |     0.1624 us | 4.551 us |
| [GetClaimsForUserV03](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V03/ClaimsHelper.cs) | 9.231 us | 0.1828 us |     0.5096 us | 9.151 us |

<br/>

(V04 is de versie met de static variabele; V05 de singleton-implementatie.)


De performance is in V04 al gehalveerd ten opzichte van V03! Dat is een enorme winst voor zo'n kleine wijziging! Vergeleken daarbij is de winst van V05 bescheiden. Een echte verrassing hoeft dat niet te zijn: V05 is een doorontwikkeling van V04, maar geen volledig nieuwe implementatie.


Desalniettemin, beide implementaties zijn nog steeds vier keer zo langzaam als de snelste versie. Kunnen we echt niet beter dan dit?


## Is dat echt nodig?


Vrees niet: dat kunnen we! De truc zit 'm in het nagaan waar er reflection wordt gebruikt, en jezelf af te vragen of deze daar nodig is. Als je kijkt naar de refactorslag van V03 naar V04 en V05, dan hebben we niet meer gedaan dan het aantal aanroepen van `GetAllImplementationsOfIProvideClaims()` terugbrengen naar één. 


`GetClaimProviderForPermission()` maakt echter ook gebruik van reflection, namelijk om de `Permission`-property uit te lezen. Deze method wordt nog steeds elke keer aangeroepen wanneer we een call naar `GetClaimProvider()` maken. Is dit echt nodig?


Nou, nee. We kunnen de `ClaimProviders` en de bijbehorende `Permissions` bij de eerste aanroep van de singleton opslaan in een [dictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=net-5.0). Deze kunnen we uitlezen wanneer we een `ClaimsProvider` nodig hebben, zonder gebruik te hoeven maken van reflection.


Qua performance is een dictionary een goede keuze. Deze heeft namelijk een waarde van [*O*(1)](https://en.wikipedia.org/wiki/Big_O_notation). Dat wil zeggen dat het aantal stappen dat nodig is om de juiste entry in een dictionary te vinden, niet verandert met het aantal entries. Of er nu 3 `ClaimProviders` zijn of 3000, het is niet van invloed op hoe snel we de juiste te pakken hebben, als we eenmaal weten wat de bijbehorende `Permission` is.


De uiteindelijke implementatie is als volgt:


{{< gist notkarlmarx a5571b15998ff4b86de84d368152ff0b "ClaimProviderFactoryV06.cs">}}


## De eindstand


Dit is het moment van de waarheid. Heeft het gebruik van een dictionary de performance van deze code voldoende opgekrikt om te kunnen wedijveren met de oorspronkelijke implementaties?


Dit is de eindstand:


| Method | Gem. | Foutmarge | Standaarddeviatie | Mediaan | 
|-------------------- |-----------:|----------:|------------------:|---------:|
| [GetClaimsForUserV02](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V02/ClaimsHelper.cs) | 1.134 us | 0.0226 us | 0.0390 us | 1.136 us |
| [GetClaimsForUserV00](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Original/ClaimsHelper.cs) | 1.194 us | 0.0237 us | 0.0633 us | 1.183 us |
| [GetClaimsForUserV01](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V01/ClaimsHelper.cs) | 1.218 us | 0.0271 us | 0.0755 us | 1.199 us |
| [GetClaimsForUserV06](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V06/ClaimsHelper.cs) | 1.388 us | 0.0276 us | 0.0526 us | 1.380 us |
| [GetClaimsForUserV05](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V05/ClaimsHelper.cs) | 4.211 us | 0.1071 us |     0.3124 us | 4.128 us |
| [GetClaimsForUserV04](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V04/ClaimsHelper.cs) | 4.575 us | 0.0913 us |     0.1624 us | 4.551 us |
| [GetClaimsForUserV03](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V03/ClaimsHelper.cs) | 9.231 us | 0.1828 us | 0.5096 us | 9.151 us |

<br/>


V06 is drie keer zo snel dan V05 en komt dicht in de buurt van V01!


[^1]: Met dank aan [Nick Chapsas](https://www.youtube.com/channel/UCrkPsvLGln62OMZRO6K-llg), die de werking van het project in deze [video](https://www.youtube.com/watch?v=EWmufbVF2A4) beter uitlegt dan ik in tekst zou kunnen doen.
