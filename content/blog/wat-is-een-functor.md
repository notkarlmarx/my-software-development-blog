---
title: "Wat is een functor?"
author: "Karl van Heijster"
date: 2022-09-09T11:15:13+02:00
draft: true
comments: true
tags: ["functioneel programmeren", "functors", "leermoment", "LINQ", "options"]
summary: "Wat is een *functor*, vraag je? Lang verhaal kort: *functors* zijn typen die een `Map`-functie implementeren. Wat is een `Map`-functie, vraag je? Lang verhaal kort: ken je LINQ? - heb je wel eens `Select` gebruikt? - nou, dat dus. Maar misschien loont het zich er nét iets langer bij stil te staan."
---

Wat is een *functor*, vraag je? Lang verhaal kort: *functors* zijn typen die een `Map`-functie implementeren.


Wat is een `Map`-functie, vraag je? Lang verhaal kort: ken je LINQ? - heb je wel eens [`Select`](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.select) gebruikt? - nou, dat dus.


## Lijsten


Oké, misschien loont het zich er nét iets langer bij stil te staan. De `Select`-functie transformeert alle elementen in een lijst van het type `T` naar het type `R`. Of, in functionele notatie (zie [deze blog](/blog/22/07/wat-zijn-eerlijke-functies/)): `Select: (IEnumerable<T>, (T -> R)) -> IEnumerable<R>`.


Een concreet voorbeeld:


```cs
var people = _peopleRepository.GetAll();
var ages = people.Select(p => p.Age);
```


De `GetAll`-functie op de `_peopleRepository` levert een `IEnumerable<Person>` op. De `Select`-functie accepteert die `IEnumerable` als eerste parameter.[^1] De tweede parameter is een `Func<T, R>`. In dit geval zegt die functie: geef me voor elke `Person p` de `p.Age` terug. Je stopt een `IEnumerable<Person>` in de `Select`-functie, en je krijgt een `IEnmerable<Age>` terug.


## Transformaties


Hoe moet je deze functionaliteit begrijpen? Je zou het zo kunnen zien: je transformeert als het ware de gebonden variabele van een lijst. Daar waar je eerst een lijst met personen had, heb je na de toepassing van de `Select`-functie een lijst met leeftijden.


Natuurlijk, dat klopt niet helemáál. LINQ omarmt immutability (zie [deze blog](/blog/22/05/heb-je-die-setter-echt-nodig/)), en dus krijg je eigenlijk een nieuwe lijst terug van een ander type. 


Misschien is dit een betere manier om het te zeggen: je stelt, met als uitgangspunt lijst *a* en op basis van een conditie *f*, een lijst *b* samen. (Maar een nóg betere manier om het te zeggen zou waarschijnlijk met wat minder variabelen gepaard gaan!)


## Opties


Dit idee blijft niet beperkt tot `IEnumerable`. Ook [Options](https://en.wikipedia.org/wiki/Option_type) (zie [deze](/blog/22/07/wat-zijn-eerlijke-functies/) en [deze](/blog/22/08/spelen-met-options/) blog) hebben een soortgelijke functie. Alleen heet die functie in deze context doorgaans geen `Select` maar `Map`. Dit is de functionele notatie ervan: `Map: (Option<T>, (T -> R)) -> Option<R>`.


Merk op dat de signatuur van deze functie qua vorm identiek is aan die van `Select`. Het enige verschil is dat `IEnumerable` door `Option` is vervangen. 


Je zou het zo kunnen zien: `Option` is, net als `IEnumerable`, een lijst met waarden. Maar daar waar `IEnumerable` honderden lijstitems kan hebben, zijn er voor Options maar twee: wel of geen waarde.


Opnieuw, een concreet voorbeeld:


```cs
var person = _peopleRepository.GetById(1);
var ages = person.Map(p => p.Age);
```


De `GetById`-functie op de `_peopleRepository` levert een `Option<Person>` op. De `Map`-functie accepteert die `Option` als eerste parameter. De tweede parameter is een `Func<T, R>`. In dit geval zegt die functie: geef me voor de `Person p` de `p.Age` terug. Er zijn twee mogelijke uitkomsten: ofwel er is een `Person p`, ofwel niet. Zo ja, dan krijg je `p.Age` terug; en zo nee, dan niet.


## Functors


Natuurlijk blijft dit idee niet beperkt tot lijsten en Options alleen. Het idee van een type dat `Map` implementeert kan nog verder gegeneraliseerd worden tot veel meer types die als container voor een bepaalde waarde fungeren. Als we naar de functionele notatie kijken, is het enige dat ons rest om het concrete type weg te abstraheren: `Map: (C<T>, (T -> R)) -> C<R>`.


`Map` kan zo worden gedefinieerd als een functie die een container `C<T>` accepteert, en een functie *f* met als vorm `(T -> R)`. Het retourneert een container `C<R>`, een wrapper voor de waarde(n) die het resultaat zijn van de toepassing van *f* op de binnenste waarden van de container.


## Voortgang


Die zin klinkt ontzettend krom, ik weet het, en dat komt omdat ik 'm min of meer letterlijk vertaald heb uit [Enrico Buonanno](https://twitter.com/la_yumba)'s [*Functional Programming in C# (Second Edition)*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition). Dat boek ploeg ik langzaam - en niet bijzonder zeker - door in een poging mijn C#-vaardigheden uit te breiden.


Het proces vordert langzaam, omdat het je eigen maken van een nieuw programmeerparadigma van je vraagt om je handen vuil te maken, zelf code te schrijven. Dat schuurt met hoe ik normaliter een boek lees - ver weg van mijn toetsenbord -, en daardoor ga ik er minder rap doorheen dan ik graag zou zien. 


Maar ik maak voortgang, en dat doe ik [naar goed gebruik](https://medium.com/my-learning-journal/why-you-should-learn-in-public-4fd3a6239549) in het openbaar. In deze [GitHub-repository](https://github.com/dotkarl/FunctionalProgrammingPlayground) schrijf ik mee met Buonanno en leg mijn gedachten over waar ik mee bezig ben vast. Het is een vreemde mix van demo-code en dagboekaantekeningen, een eerste opstap naar demoprojecten en uiteindelijk productiecode.


We komen er wel, `Func` voor `Func`!


[^1]: Dit is bij het lezen van de code minder duidelijk, omdat `Select` als [extension method](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods) is geïmplementeerd. Wie de method echter inspecteert - druk op `F12` in [Visual Studio](https://visualstudio.microsoft.com/) of bekijk [de documentatie](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.select) - ziet dat het zo is. 
