---
title: "Wat zijn eerlijke functies?"
author: "Karl van Heijster"
date: 2022-06-03T11:18:47+02:00
draft: true
comments: true
tags: ["classes", "functioneel programmeren", "intentie van code"]
summary: "Uit Enrico Buonanno's *Functional Programming in C# (Second Edition)* leerde het concept van een *eerlijke functie* kennen - en dat maakte me bewust van de oneerlijkheid van de code die ik doorgaans schrijf. Wat zijn eerlijke functies? Voordat we die vraag kunnen beantwoorden, moeten we eerst een antwoord geven op een onderliggende vraag, en dat is: wat is een functie überhaupt?"
---

Uit [Enrico Buonanno](https://twitter.com/la_yumba)'s [*Functional Programming in C# (Second Edition)*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition) leerde het concept van een *eerlijke functie* kennen - en dat maakte me bewust van de oneerlijkheid van de code die ik doorgaans schrijf.


Wat zijn eerlijke functies? Voordat we die vraag kunnen beantwoorden, moeten we eerst een antwoord geven op een onderliggende vraag, en dat is: wat is een functie überhaupt? - Geen onbelangrijke vraag, er is nota bene een compleet [paradigma](/blog/21/10/low-code-een-nieuw-paradigma/) naar vernoemd!


## Functies


De term [*functie*](https://nl.wikipedia.org/wiki/Functie_(wiskunde)) komt uit de wiskunde en betekent drukt de afhankelijkheid van een element uit met een ander element. In de wiskunde zijn die elementen traditioneel getallen. Stel, we hebben de functie `*f*(*x*+1)`, dan arrangeert deze functie het getal `1` met `2`, `2` met `3`, en `938` met `939`. Het steeds eerstgenoemde getal in die opsomming behoort tot de ene set, het tweede genoemde getal behoort tot de andere set. Je zou een functie kunnen zien als een vertaaltabel van de ene set naar de andere.


Functies hoeven niet per se afhankelijkheden tussen getallen uit te drukken, natuurlijk. Laat ik dat met een eenvoudig (en schaamteloos gejat) voorbeeld illustreren. We veronderstellen twee sets, beide bestaande uit letters. De eerste set bestaat uit kleine letters (`a`, `b`, `c` etc.) en de tweede uit hoofdletters (`A`, `B`, `C` etc.). Een functie is dat wat de elementen uit beide sets met elkaar arrangeert. Een functie als `ToUpper` brengt een eenvoudige vertaling tot stand van de ene set naar de andere.


En zo geldt hetzelfde voor complexere objecten. Als je bijvoorbeeld naar [LINQ](https://docs.microsoft.com/en-us/dotnet/api/system.linq?view=net-6.0) kijkt, dan vertaalt [`Where`](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.where?view=net-6.0) de ene `IEnumerable` in een andere, die aan een bepaalde voorwaarde voldoet. En [`Select`](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.select?view=net-6.0) vertaalt een `IEnumerable<TSource>` zelfs in een `IEnumerable<TResult>`. De vertaling hoeft dus niet per se het type te behouden.


Het gebruik van het woord "vertaling" is niet toevallig. Een [`Dictionairy`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=net-6.0) in C# wordt doorgaans opgevat als een datatype, maar je zou het net zo goed als een functie op kunnen vatten. Het `Dictionairy` vertaalt immers een input (de `Key`) naar een welbepaalde output (de `Value`), precies zoals een functie doet. 


## Een eerlijke functie


Nu we weten wat functies zijn, kunnen we ons afvragen: wat zijn eerlijke functies? En het antwoord is eigenlijk vrij eenvoudig: een eerlijke functie is een functie die doet wat zijn [signatuur](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods#method-signatures) belooft. 


Deze (triviale) functie is bijvoorbeeld eerlijk:


```cs
public static int PlusOne(int i) => i + 1;
```

De signatuur van deze functie - aan de linkerkant van de `=>` - belooft een `int` als input te nemen en een `int` als output weer uit te spugen. De implementatie van de functie - rechts van de `=>` - maakt die belofte waar. Er is geen enkele manier waarop je iets anders dan een `int` terug uit deze functie terug zou kunnen krijgen, gegeven het feit dat je er een `int` in stopt.


De wereld van het functioneel programmeren kent trouwens zijn eigen notatie voor het weergeven van een signatuur. In dit geval is die als volgt: `PlusOne: int -> int`.


## Een oneerlijke functie...


Deze (net zo triviale functie) is niet eerlijk:


```cs
public static int PlusOne(int i) => (i >= 0) 
    ? (i + 1) 
    : throw new ArgumentException("Value cannot be less than 0!");
```


De signatuur van deze functie belooft opnieuw een `int` als output terug te geven, gegeven een `int` als input: `PlusOne: int -> int`. 


Maar de implementatie laat een heel ander verhaal zien. Voor getallen groter dan 0 doet de signatuur inderdaad wat het belooft. Maar voor negatieve getallen wordt de belofte - als je het zo wil noemen - van de signatuur verbroken: er wordt een `ArgumentException` teruggegeven. Dat is een gegeven waar je alleen van op de hoogte kan zijn als je de implementatie van de functie hebt bekeken.


Nu zou je kunnen denken dit probleem te ondervangen door betere naamgeving, `PositivePlusOne` bijvoorbeeld. En hoewel dat wel degelijk een verbetering is, maakt dat de functie nog niet *eerlijk*. De eerlijkheid van een functie wordt puur en alleen bepaald door de input(s) en output(s), niet de naam. Ook `PositiveOneOrThrowArgumentException` lost het probleem niet op (en is bovendien ontzettend lelijk). De signatuur belooft immers nog steeds een `int` voor een `int` terug te geven - de `ArgumentException` zelf is nog steeds nergens te bekennen. 


## Weten waar je aan toe bent


De reden om eerlijke functies te willen, laat zich raden. Wie een eerlijke functie gebruikt, kan er altijd zeker van zijn een bepaald type output te verwachten bij een bepaald type input. Je hoeft je er geen zorgen om te maken dat de code zich ooit op een onverwachte manier zal gedragen. Je hoeft niet in de implementatie te spieken of je voor verrassingen komt te staan. *Als je functies eerlijk zijn, weet je waar je aan toe bent.* 


En dat dat je ontwikkelsnelheid zal verhogen en het aantal bugs zal verlagen, is een voorspelling waar ik me best aan durf te wagen.


## Problemen


Waarom schrijven we dan niet altijd eerlijke functies? Dat is omdat de lat voor eerlijkheid enorm hoog ligt. Het impliceert bijvoorbeeld dat je nooit meer een Exception op mag gooien vanuit je code! 


En de problemen gaan nog dieper. Laten we een method veronderstellen die een bepaalde `Resource` uit een database ophaalt, op basis van een [`Guid`](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-6.0). Bekijk de volgende signatuur eens:


```cs
public static Resource GetResourceById(Guid id);
```


Of, in de functionele notatie: `GetResourceById: Guid -> Resource`.


Is dit een eerlijke functie? - *Nee!* Hoe ik dat weet, zonder naar de implementatie te hebben gekeken? Vraag je eens af: wat gebeurt er als de `Resource` die bij de `Guid` hoort niet gevonden kan worden?


We weten dat de code sowieso geen Execption op mag gooien, want daarmee zou deze oneerlijk worden. Het alternatief zou dus moeten zijn: dan geef je een waarde terug die aangeeft dat de `Resource` niet gevonden is. En die waarde is in C# doorgaans `null`. Gegeven een `Guid`, krijg je ofwel een `Resource` terug, ofwel `null` - maar dat is niet wat de signatuur beloofde! Die beloofde immers een `Resource`. Anders gezegd: de signatuur geeft niet aan dat de bij een `Guid` horende `Resource` ook níet gevonden kan worden.


## Het gedoe met classes


Je zou deze beperking af kunnen proberen te vangen door gebruik te maken van het [*Null object*-patroon](https://en.wikipedia.org/wiki/Null_object_pattern).[^1] Dat is een ontwerppatroon waarbij er bij niet-gevonden waarden geen `null` terug wordt gegeven, maar een door de programmeur gedefinieerd `Resource`-object dat als "niet aanwezig" kan worden gedefinieerd door de caller van de functie.


Maar, net als bij het aanpassen van de naam hierboven, lost dat het fundamentele probleem niet op. De `Resource` *an sich* is immers nog steeds nullable. Het probleem is in de praktijk misschien opgelost, maar in principe is het mogelijk om `null` terug te krijgen. De oneerlijkheid van de functie is maar één programmeerfout verwijderd. Oftewel: om zekerheid te kunnen verkrijgen, zul je alsnog de implementatie na moeten lopen. 


De implicatie hiervan is verstrekkend. Gegeven het feit dat classes in C# nullable zijn (sterker nog, ze hun *default*-waarde is `null`!) is een signatuur met een class erin *per definitie* oneerlijk.


## Hoop


Is er dan geen hoop voor eerlijke functies in C#? Natuurlijk wel! En daarvoor geef ik nu graag het woord aan [Nick Chapsas](https://nickchapsas.com/):


{{<youtube id="OJjVvPINlYA" title="Should you stop returning null? | Functional C#" >}}
<br>


Maar de vraag is natuurlijk: vind je dit als objectgeoriënteerde programmeur een overtuigend verhaal?


[^1]: Een alternatief is gebruik te maken van [*Non-nullable reference types*](https://docs.microsoft.com/en-us/dotnet/csharp/nullable-references), zoals geïntroduceerd in C# 8. Buonanno bespreekt dit alternatief op pagina's 90-92 van *Functional Programming in C# (Second Edition)* - en serveert deze optie af. Voor deze blog laat ik deze oplossingsrichting daarom buiten beschouwing.
