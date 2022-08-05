---
title: "Spelen met Options"
author: "Karl van Heijster"
date: 2022-08-05T10:42:07+02:00
draft: false
comments: true
tags: ["functioneel programmeren", "intentie van code", "leermoment", "options"]
summary: "Options vormen de brug tussen totale en gedeeltelijke functies. Het is een type dat de eigenlijke *return value* van een functie wrapt. In het geval dat de mapping zinvol is, dan geeft de functie een Option terug met daarin de gezochte waarde. En als de mapping dat niet is, dan geeft deze een Option terug zónder die waarde. Wat het resultaat dus ook is, één ding weet je zeker: je krijgt een Option terug. De functie is altijd eerlijk."
---

Eerder schreef ik over [eerlijke functies en hoe Options daar een rol in kunnen spelen](/blog/22/07/wat-zijn-eerlijke-functies/). Daar wil ik vandaag wat dieper op in gaan.


## Totale en gedeeltelijke functies


Wat zijn [Options](https://en.wikipedia.org/wiki/Option_type)? Daarvoor moet je eerst wat weten over functies. Je kunt functies opvatten als datgene wat de waarden uit domein A mapt naar de waarden uit domein B. Stel, je hebt een domein A met daarin alle kleine letters van het alfabet, en een domein B met daarin alle hoofdletters. De functie `ToUpper` mapt dan elke letter één op één van domein A naar domein B. 


Dit is een voorbeeld van een *totale functie*. Een totale functie mapt elk element in een domein naar een element in een ander domein.


Maar niet elke functie is een totale functie. Een voorbeeld dat [Enrico Buonanno](https://twitter.com/la_yumba) in [*Functional Programming in C# (Second Edition)*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition) noemt, is het mappen van een `string` naar een `int`. `"1"` zou je kunnen parsen naar `1`. Hetzelfde zou je nog kunnen zeggen voor `"One"`. Maar welke integerwaarde correspondeert met `Unicorn`? Het aantal stringwaarden is oneindig veel groter dan het aantal integerwaarden. En niet elke stringwaarde zal zinvol naar een integerwaarde kunnen worden gemapt.


Dit is een voorbeeld van een *gedeeltelijke functie*. Een gedeeltelijke functie mapt sommige maar niet elk element in een domein naar een element in een ander domein.


## Options als brug


Je zou kunnen zeggen: als die mapping niet zinvol kan worden gedefinieerd, dan gooi je een Exception op, of je geeft `null` terug. Maar, zoals ik in [mijn eerdere blog](/blog/22/07/wat-zijn-eerlijke-functies/) uiteenzette, breng je daarmee wel een offer. Je maakt het gros van je functies daarmee per definitie oneerlijk. Als we voor één van deze twee opties kiezen (*no pun intended*) zeggen we daarmee eigenlijk: jammer joh, maar eerlijkheid is voor gedeeltelijke functies niet weggelegd.


Dat is voor een taal als [C#](https://docs.microsoft.com/en-us/dotnet/csharp/) - waar iets als een eerlijke functie allesbehalve een gemeenplaats is - misschien een acceptabele oplossing. Maar voor een functionele taal geldt dat natuurlijk niet. Het hoeft niet te verbazen dat dat soort talen een constructie hebben verzonnen om op een eerlijke manier met gedeeltelijke functies om te kunnen gaan. En daar komen Options dus om de hoek kijken.


Options vormen de brug tussen totale en gedeeltelijke functies. Het is een type dat de eigenlijke *return value* van een functie wrapt. In het geval dat de mapping zinvol is, dan geeft de functie een Option terug met daarin de gezochte waarde. En als de mapping dat niet is, dan geeft deze een Option terug zónder die waarde. Wat het resultaat dus ook is, één ding weet je zeker: je krijgt een Option terug. De functie is altijd eerlijk.


## Expliciete afhandeling


Natuurlijk is de afhandeling van een lege waarde (in de functionele literatuur *None* genoemd) niet dezelfde als die van een gezochte waarde (*Some*). Wie een Option gebruikt, wordt daarom gevraagt om expliciet te definiëren wat er moet gebeuren in het geval de waarde gevonden wordt, en wanneer dat niet zo is.


Je zou een Option daarom kunnen zien als een expliciete `null`-check. Als je een Option terugkrijgt *moet* je twee condities afhandelen. Vergelijk dat eens met de normale gang van zaken als je in C# programmeert. Hoe vaak heb je niet een `null`-check ingebouwd nádat er een vervelende bug op de productieomgeving omhoog kwam borrelen?[^1] - En hoe gerustgesteld was je na zo'n fix dat precies dezelfde `NullReferenceException` niet op een andere plek op zou borrelen?


Options kunnen hier een uitweg bieden. 


## Waar haal je Options vandaan?


Tot zover het theoretische gedeelte van deze blog. Laten we onze handen vuil maken.


Het concept van een Option komt uit de wereld van de functionele programmeertalen en bestaat daarom niet *out of the box* in C#. ([F# kent ze uiteraard wel.](https://docs.microsoft.com/en-us/dotnet/fsharp/language-reference/options)) Om met Options aan de slag te kunnen gaan, zul je ze zelf toe moeten voegen, of een [NuGet](https://www.nuget.org/) package naar binnen moeten halen.


Voor de oefening is het natuurlijk heel leuk om eigenhandig de functionaliteit rondom Options uit te schrijven, maar in een productieomgeving is die keuze niet verdedigbaar. Het is als softwareontwikkelaar niet per se je taak om code te schrijven. Het is je taak om met code - en niet per se jouw code! - problemen op te lossen. (Zie ook [deze blog](/blog/22/03/enums-switch-statements-en-solid-7/).) Of, in de taal van [strategische subdomeinen](/blog/22/06/de-ontdekking-van-strategische-subdomeinen/): Options behoren tot het generieke subdomein. Het is een probleem dat al voor jou is opgelost.


Buonanno heeft een eenvoudige `Option` uitgeprogrammeerd die [hier](https://github.com/la-yumba/functional-csharp-code) te vinden is. Maar die code is bedoeld om de lezer van *Functional Programming in C#* vertrouwd te maken met functionele programmeerconcepten in C#, en is dus niet geschikt om in een productieomgeving te gebruiken. 


Een betere oplossing vinden we in het [LanguageExt](https://www.nuget.org/packages/LanguageExt.Core)-package, waarvan de broncode [hier](https://github.com/louthy/language-ext) te vinden is. (Dit is overigens dezelfde library als waar ik in [mijn eerdere blog](/blog/22/07/wat-zijn-eerlijke-functies/) naar verwees via de [video](https://www.youtube.com/watch?v=OJjVvPINlYA) van [Nick Chapsas](https://nickchapsas.com/).) Dit project wordt op het moment van schrijven nog zeer regelmatig onderhouden en is daarom een goede keus voor een applicatie die daadwerkelijk productie draait.


## Spelen met Options


Ik heb een vrijdagochtend uitgetrokken om wat te spelen met de `Options` in deze library. [Het resultaat daarvan is op GitHub te vinden](https://github.com/dotkarl/FunctionalProgrammingPlayground/tree/master/FunctionalProgrammingPlayground/Options) ter lering en vermaak. Wat volgt is een verslag van mijn *spielerei*.


### Instantiatie


Allereerst: hoe instantieer je een `Option`? Of liever: hoe instantieer je een *Some* en een *None*? *LanguageExt* blijkt verschillende smaken te ondersteunen. 


De - voor mij althans - meest voor de hand liggende manier was deze:


```cs
var some = new Some<string>("value");
```


Tevreden met het resultaat ging ik op zoek naar een `None`-type, maar dat vond ik niet. Wel het wat minder intuïtieve `OptionNone`:


```cs
var newNone = new OptionNone();
var defaultNone = OptionNone.Default;
```


Die inconsistentie zat me dwars. Dit kon onmogelijk de juiste manier zijn om die types te instantiëren. Al gauw stuitte ik op een omweg via het `Option`-type zelf:


```cs
var some = Option<string>.Some("value");
var none = Option<string>.None;
```


Dat zag er al wat beter uit! Maar helemaal tevreden was ik nog steeds niet, want deze oplossing vond ik wat aan de breedsprakige kant. Het type van de *Some* zou mijns inziens immers afgeleid moeten kunnen worden van de waarde die je meegeeft. En het is al helemaal absurd dat je het type mee moet geven voor een *None* die zich niet eens voor het type interesseert! Immers: niet gevonden is niet gevonden, of je nu een `string` of een `int` verwacht.


Ik dook in de [documentatie](https://louthy.github.io/language-ext/LanguageExt.Core/index.html) en er blijkt inderdaad een eenvoudiger manier te zijn. Die vraagt echter wel van je dat je een [*Prelude*](https://louthy.github.io/language-ext/LanguageExt.Core/Prelude/) als statische *using* opneemt in je class:


```cs
using static LanguageExt.Prelude;

var some = Some("value");
var none = None;
```


Zeg nu zelf: dat ziet er toch prachtig uit!


### Afhandeling


Dan: de expliciete afhandeling van beide condities. Als ik Buonanno mag geloven, dan is een `Match`-functie daarvoor de gebruikelijke manier in de wereld van het functioneel programmeren. En inderdaad, een `Option` kent een `Match` die twee `Func`s als argumenten verwacht: één voor de succesconditie (gevonden) en één voor de foutconditie (niet gevonden). 


Ik nam het voorbeeld van Buonanno over en schreef een simpele functie die iemand alleen begroet als zijn of haar naam bekend is:


```cs
private static string Greet(Option<string> greetee) => greetee.Match(
    (name) => $"Hello, {name}",
    () => "Sorry, who?");
```


Als je deze functie een `Option` meegeeft die *Some* is, dan retourneert 'ie de eerste functie. Als de `Option` *None* blijkt te zijn, dan wordt de tweede functie teruggegeven.


Merk op dat `Match` de programmeur vraagt om de afhandeling van beide condities direct na elkaar uit te schrijven. Maar ik weet toevallig dat `Option` ook nog verschillende helper methods die je in staat stellen om één conditie te specifieren, namelijk `IfSome` en `IfNone`. Die methods retourneren echter een `Unit`, en om de implicaties daarvan te overzien, zal ik eerst nog even wat dieper in Buonanno moeten duiken, ben ik bang. Op dit moment durf ik daar daarom nog niet zoveel over te zeggen, wellicht is dat iets voor een volgende blog.


## Lessen


Tijd voor wat reflectie. Nu de vrijdagochtend tot een eind komt, word ik door twee verschillende gevoelens bevangen.


Enerzijds heb ik het idee dat ik Options conceptueel aardig gevat heb. Ik hoop dat de lezer dat, op basis van het eerste deel van deze blog, met me eens zal zijn.


Anderzijds heb ik me erover verbaasd hoe klein de stapjes zijn die ik op het gebied van syntax heb gezet. Ik kan een *Some* en een *None* instantiëren en een `.Match` aanroepen - en daar eindigt de voortgang. Ik heb overwogen om het tweede deel van deze blog daarom maar te schrappen. Dat ik dat niet gedaan heb, is omdat ik denk dat er een les in schuilt - twee, zelfs. 


Eerst: iets nieuws leren gaat met vallen en opstaan, en dat kost nu eenmaal tijd. Het belangrijkst is die te nemen - en te blijven nemen. De eerste stappen op nieuwe grond zijn wankel, altijd. Waar het om gaat is dat je vooruitkomt, niet de snelheid waarmee dat gebeurt.


En ook: hoe ervaren je ook bent in het ene programmeerparadigma (of -taal, library etc.), dat betekent nog niet dat je uit de voeten kunt met het andere. Wie iets nieuws leert, herinnert zichzelf eraan hoe weinig hij of zij eigenlijk weet. Dat noopt tot bescheidenheid. We zijn allemaal leerlingen - en als we het goed doen, ons hele leven lang. 


[^1]: Vóór de introductie van [*non-nullable reference types*](https://docs.microsoft.com/en-us/dotnet/csharp/nullable-references) in C# 8, kende de taal zelfs geen enkele manier om defensief programmeren in geval van `null` af te dwingen. En ook sindsdien is dat dwingende aspect alleen weggelegd voor de verstandige programmeur die zijn [*warnings* als *errors* configureert](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-options/errors-warnings).
