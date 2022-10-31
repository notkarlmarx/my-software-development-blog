---
title: "Wat is een monad?"
author: "Karl van Heijster"
date: 2022-10-28T10:10:56+02:00
draft: true
comments: true
tags: ["functioneel programmeren", "leermoment", "monads", "options"]
summary: "Wat is een *monad*, vraag je? Simpel: monaden zijn de meest fundamentele zijnden in het universum - ondeelbaar, onafhankelijk, zowel geestelijk als lichamelijk - de bouwblokken van de werkelijkheid, die tezamen een door God geschapen harmonieus geheel vormen - overigens zonder elkaar te beïnvloeden; het zijn perfect op elkaar afgestemde atomen die in autonoom opereren maar in hun zijn het voltallige universum spiegelen. Althans, dat is wat Gottfried Wilhelm Leibniz onder \"monaden\" verstond. Maar dit is nu eenmaal een blog over softwareontwikkeling, dus je zal wel dat functionele spul bedoelen."
---

Wat is een *monad*, vraag je? Simpel: monaden zijn de meest fundamentele zijnden in het universum - ondeelbaar, onafhankelijk, zowel geestelijk als lichamelijk - de bouwblokken van de werkelijkheid, die tezamen een door God geschapen harmonieus geheel vormen - overigens zonder elkaar te beïnvloeden; het zijn perfect op elkaar afgestemde atomen die in autonoom opereren maar in hun zijn het voltallige universum spiegelen. Althans, dat is wat [Gottfried Wilhelm Leibniz](https://plato.stanford.edu/entries/leibniz/) onder "[monaden](https://plato.stanford.edu/entries/leibniz/#MetLeiIde)" verstond.


Maar dit is nu eenmaal een blog over softwareontwikkeling, dus je zal wel [dat functionele spul](https://en.wikipedia.org/wiki/Monad_(functional_programming)) bedoelen.


## Container


Een *monad* is een softwareontwerppatroon uit de wereld van het functioneel programmeren. Het is een container die een bepaalde waarde wrapt, met als doel veel voorkomende operaties te encapsuleren. 


*Monads* zijn in principe niets nieuws voor vaste lezers van dit blog. Eén soort *monad* hebben we hier al eerder behandeld: de [Option](/blog/22/08/spelen-met-options/). Het gedrag dat deze *monad* encapsuleert, is de check op het al dan niet [null](https://en.wikipedia.org/wiki/Null_pointer) zijn van de waarde. 


Maar er zijn ook andere soorten *monads*. Een [Try](https://louthy.github.io/language-ext/LanguageExt.Core/Monads/Alternative%20Value%20Monads/Try/Try/index.html) is een wrapper die exception handling voor je afvangt. Maar ook verzamelingen zijn zoals een [`Array`](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/arrays/) zijn *monads*.


## Formeel


Formeel bezien moet een *monad* aan twee vereisten voldoen: hij moet een `Return`- en een `Bind`-functie definiëren. (Nota bene, de functies hoeven niet per se onder die naam bekend te staan.) De functies hebben de volgende signatuur (waarbij `M` staat voor "*monad*"):


`Return: T -> M<T>`
`Bind: (M<T>, (T -> M<R>)) -> M<R>`


De eerste stelt je in staat om een waarde te wrappen in de *monad*. Middels `Bind` kun je operaties op die waarde uitvoeren binnen de context van die *monad*. Belangrijker nog, het stelt je in staat om meerdere van zulke operaties met elkaar te combineren met behulp van [*method chaining*](https://en.wikipedia.org/wiki/Method_chaining).


De potentie van die opzet laat zich raden. Als we ons even beperken tot de context van Options, dan maakt dit het mogelijk om op [declaratieve manier](https://en.wikipedia.org/wiki/Declarative_programming) te specificeren welke (*single-responsiblity*!) operaties je allemaal op een waarde uit wil voeren, zonder ook maar één keer op null te hoeven controleren. Dat vereenvoudigt code aanzienlijk.


Geen wonder dat [Sander Hoogendoorn](https://sanderhoogendoorn.com/) *monads* [één van de belangrijkste inzichten in zijn carrière](https://sanderhoogendoorn.com/the-zen-of-programming/) noemde. (Zie ook [deze blog] (LINK_TECHORAMA).) Zo begeesterd als Hoogendoorn ben ik nog niet - maar dat is omdat ik nog nauwelijks met *monads* gewerkt heb buiten [LINQ](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/) om. Maar als die ervaring een indicatie is voor hoe plezierig die stijl van programmeren werkt, dan kan ik zijn enthousiasme begrijpen.


## `Bind` en `Map`


[Eerder heb ik het over *functors* gehad](/blog/22/10/wat-is-een-functor/) - en *monads* hebben daar wel wat van weg. Een *functor* implementeert de `Map`-functie, en die heeft wel wat weg van de `Bind` (waarbij `F` staat foor "*functor*"): `(F<T>, (T -> R)) -> F<R>`. 


Het verschil tussen beide zit 'm in de tweede parameter. `Bind` is bedoeld om *monads* te kunnen chainen. `Map` is daar niet voor geschikt. Als je `Map` zou loslaten op een *monad* dan levert dat geneste *monads* op. [Enrico Buonanno](https://twitter.com/la_yumba) geeft in [*Functional Programming in C# (Second Edition)*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition) het volgende voorbeeld daarvan:


```cs
Console.WriteLine("Please enter your age");
string input = Console.ReadLine();

// Int.Parse wraps the user input in an Option
Option<int> ageInt = Int.Parse(input);
// Option<int> is used as input for the Map-function, 
// resulting in an Option<Option<int>>
Option<Option<int>> age = ageInt.Map(i => Age.Create(i));
```

*Monads* en *functors* zijn dus welonderscheiden entiteiten. Toch hebben ze wel wat overlap met elkaar. Elke *monad* is ook een functor. `Map` kan namelijk geïmplementeerd worden door `Bind` en `Return` te combineren. Maar niet elke *functor* is ook een *monad*. `Bind` kan namelijk niet worden gedefinieerd in termen van `Map`.
