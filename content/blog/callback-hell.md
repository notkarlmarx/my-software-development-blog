---
title: "Callback hell"
author: "Karl van Heijster"
date: 2023-12-08T10:31:21+01:00
draft: true
comments: true
tags: ["functioneel programmeren", "leermoment", "LINQ",  "monads", "options", "refactoren"]
summary: "In mijn werk als C#-ontwikkelaar maak ik veelvuldig gebruik van functionele programmeerconcepten. Als een functie me een object `T` teruggeeft *of niet*, dan codeer ik dat netjes in de signatuur van die functie door een `Option<T>` terug te geven. Dat dwingt de aanroepende partij om beide scenario's expliciet af te handelen. Hartstikke handig! -- Maar: niet zonder zijn eigen set problemen. Want wat gebeurt er als je meerdere functies achter elkaar aanroept die allemaal een `Option<T>` teruggeven? Dan komen we terecht in wat men *callback hell* noemt."
---

Er was een tijd dat ik over [functors](/blog/22/10/wat-is-een-functor/ "'Wat is een functor?'") en [monads](/blog/22/12/wat-is-een-monad/ "'Wat is een monad?'") schreef -- maar die tijd ligt al ver achter ons. Maar dat ik er niet over geschreven heb, betekent niet dat ik me sindsdien niet verder heb verdiept in [het functionele programmeerparadigma](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'"). In mijn werk als [C#](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/ "'C# programming guide', Microsoft documentatie")-ontwikkelaar maak ik, met een beetje hulp van onze vrienden van [*LanguageExt*](https://github.com/louthy/language-ext "'language-ext', GitHub"), veelvuldig gebruik van functionele programmeerconcepten.


Als een functie me een object `T` teruggeeft *of niet*, dan codeer ik dat netjes in de signatuur van die functie door een [`Option<T>`](https://github.com/louthy/language-ext#option "'Option', LanguageExt GitHub") terug te geven. (Zie onder andere [deze](/blog/22/07/wat-zijn-eerlijke-functies/ "'Wat zijn eerlijke functies?'") en [deze blog](/blog/22/08/spelen-met-options/ "'Spelen met Options'").) Dat dwingt de aanroepende partij om beide scenario's -- er wordt een object geretourneerd (`Some`), of niet (`None`) -- expliciet af te handelen. Een voorbeeld:


```cs
var result = GetOption(true).Match(
    value => value,
    () => "No value");

private Option<string> GetOption(bool some) =>
    some
        ? "Value"
        : None;
```


Hartstikke handig! 


## Uitdagingen


-- Maar: niet zonder zijn eigen set problemen -- of laat ik liever zeggen: uitdagingen. Want wat gebeurt er als je meerdere functies achter elkaar aanroept die allemaal een `Option<T>` (of een andere monad[^1]) teruggeven? Onlangs betrapte ik mezelf erop code te schrijven als deze:


```cs
var result = GetOption1().Match(
    v1 => GetOption2(v1).Match(
        v2 => GetOption3(v2).Match(
            v3 => DoSomething(v3),
            () => "No value 3"),
        () => "No value 2"),
    () => "No value 1");
```


Dit is wat [Enrico Buonanno](https://twitter.com/la_yumba) *callback hell* noemt in [*Functional Programming in C#*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition) (een [aanrader](/blog/22/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2022-las/ "'De beste boeken over software ontwikkeling die ik in 2022 las'")!). Wie die benaming wat te heftig vindt, suggereert hij het niet minder heftige "*pyramid of doom*."


De reden voor beide benamingen spat van het scherm. De opeenstapeling van *callback*-functies leidt tot een geneste structuur. De code neemt de vorm van een piramide aan, wat de leesbaarheid van de code niet ten goede komt. We doen hier iets verkeerd -- maar wat?


## `Bind`


Ik heb een goede middag lopen stoeien met de code voordat ik 'm in een acceptabele vorm geduwd kreeg. Het probleem zit 'm in het overmatig gebruik van `Match`. `Match` dwingt de gebruiker van de `Option<T>` af om `Some` en `None` af te handelen -- *direct* af te handelen.


Maar we kunnen de afhandeling van beide scenario's ook uitstellen. Dat krijgen we voor elkaar door niet `Bind` aan te roepen.[^2] `Bind` stelt ons in staat de ene monad naar de andere te transformeren. En dat stelt ons in staat om functies te *chainen*. Zo dus::


```cs
var result = GetOption1()
    .Bind(GetOption2)
    .Bind(GetOption3)
    .Match(DoSomething, () => "No value 1, 2 or 3");
```


Het resultaat van `GetOption1` wordt, *als deze `Some` is*, doorgegeven aan `GetOption2`; het resultaat van `GetOption2` wordt, *als deze `Some` is*, doorgegeven aan `GetOption3`, enzovoort. Als één van de resultaten `None` is, dan wordt de keten afgekapt, en handelen we de `None`-conditie af in de `Match` onderaan.


## Option, of...?


De code hierboven is functioneel (*no pun intended*) equivalent aan deze:


```cs
var result = GetOption1().Match(
    v1 => GetOption2(v1).Match(
        v2 => GetOption3(v2).Match(
            v3 => DoSomething(v3),
            () => "No value 1, 2 or 3"),
        () => "No value 1, 2 or 3"),
    () => "No value 1, 2 or 3");
```

Dat lijkt redelijk op de oorspronkelijke *pyramid of doom*, maar niet helemaal. Wat we nog missen is een unieke afhandeling voor elk individueel geval van `None`. Hoe krijgen we dat voor elkaar?


Laten we een stapje terug doen. Waar zijn we mee bezig? We *chainen* enkele functies aan elkaar die een `Option<T>` teruggeven. Voor elk van die functies geldt dat we een `string` terug willen geven met een foutmelding erin, als de uitkomst van die functie `None` is. -- Dat komt er in wezen op neer: we willen ofwel een `T` terugkrijgen, ofwel een `string`.


*Wat we nodig hebben is niet een* `Option<T>`, *maar een* `Either<string, T>`.


## Conversie


Betekent dat dat we onze methods moeten herschrijven om een `Either<string, T>` terug te geven? -- Dat zou een optie (*no pun intended*) kunnen zijn als de functies alleen in deze specifieke context gebruikt worden. Maar als het een functie betreft die op verschillende plekken in de codebase wordt gebruikt, dan is deze oplossingsrichting van tafel.


Gelukkig hoeven we niets te herschrijven. `Option<T>` en `Either<L, R>` liggen in elkaars verlengde. Het zijn beide monads die twee scenario's ondersteunen. Sterker nog, je zou `Option<T>` kunnen zien als een `Either<None, T>`.[^3] Het hoeft dan ook niet te verbazen dat *LanguageExt* een conversiemethode op `Option<T>` biedt: `ToEither`.


Dat leidt tot:


```cs
var result = GetOption1().ToEither("No value 1")
    .Bind(v1 => GetOption2(v1).ToEither("No value 2"))
    .Bind(v2 => GetOption3(v2).ToEither("No value 3"))
    .Match(DoSomething, errorMessage => errorMessage);
```


## LINQ


Is dit fantastisch leesbare code? Ik ben er nog niet over uit. Maar onze reis stopt nog niet hier. We kunnen, als we willen, deze code herschrijven met gebruik van de vaak vergeten [LINQ query syntax](https://learn.microsoft.com/en-us/dotnet/csharp/linq/write-linq-queries "'Write LINQ queries in C#', Microsoft documentatie"). Zo dus:


```cs
var result = (from v1 in GetOption().ToEither("No value 1")
             from v2 in GetOption2(v1).ToEither("No value 2")
             from v3 in GetOption3(v2).ToEither("No value 3")
             select v3)
             .Match(DoSomething, errorMessage => errorMessage)
```


Hoe is dit mogelijk? Dat is omdat LINQ een zuiver functioneel stuk C# is! `IEnumerable<T>` is óók een monad, en `SelectMany` is de LINQ-specifieke implementatie van `Bind`.


En daarmee zijn we bij de eindbestemming van deze refactorslag aanbeland. We hebben een uitweg gevonden uit de *callback hell*, onze *pyramid of doom* is afgebroken en omgevormd naar een paar regels code die we eenvoudig van boven naar beneden kunnen lezen.


## Gewetensvraag


En tóch ben ik nog niet helemaal uitgepraat over dit stuk code. Want hoe leuk ik het ook vond om een middag te stoeien met deze functionele variant van C#, bleef ik toch met een knagend gevoel in mijn maag zitten. 


Dit is de gewetensvraag die elke ontwikkelaar zich moet stellen: *is het verstandig dit soort code te introduceren in je codebase?*


Want hoe elegant en leesbaar het resultaat ook is, functionele C# is verre van idiomatische C#. Wat gebeurt er wanneer mijn teamgenoten een bug in mijn code lokaliseren? Kunnen ze deze nog zonder hulp (of zonder onnodig lange debugsesies) oplossen? En wat gebeurt er wanneer het team een nieuwe collega mag verwelkomen? Begrijpt deze wat er hier gebeurt? Wat als 'ie vers is afgestudeerd van de hogeschool? En als 'ie een doorgewinterde C#-veteraan is?


Ik zal eerlijk zijn. Hoe mooi ik functionele code ook vind, ik weet niet of het nu per se zo'n goede keus was om mijn code op die manier te schrijven. 


-- Maar het duiveltje op mijn linkerschouder voegt daaraan toe: maar zo lang niemand me tegenhoudt, zal ik er mee doorgaan. Het engeltje aan de rechterkant brengt hoopvol in dat het team em ik er misschien nog wat van opsteken.



[^1]: Voor het gemak beperk ik me in deze blog tot voorbeelden met `Option<T>`'s, omdat ik deze in het dagelijks werk het meest gebruik. Maar *LanguageExt* kan nog verschillende andere handige monads als [`Either<L, R>`](https://louthy.github.io/language-ext/LanguageExt.Core/Monads/Alternative%20Value%20Monads/Either/Either/index.html "'Either', LanguageExt documentatie") en [`Try<A>`](https://louthy.github.io/language-ext/LanguageExt.Core/Monads/Alternative%20Value%20Monads/Try/Try/index.html "'Try', LanguageExt documentatie").

[^2]: Ik schreef al eerder over deze functie, in [deze blog](/blog/22/12/wat-is-een-monad/ "'Wat is een monad?'"). Maar, concludeerde ik die middag in kwestie tot mijn eigen ongenoegen: niet bijzonder helder. Wellicht dat de dames en heren van *LanguageExt* zelf [het beter lukt](https://github.com/louthy/language-ext#monad "'Monad', LanguageExt GitHub").

[^3]: Strikt genomen zijn de twee condities in een *either*-monad gelijkwaardig aan elkaar. Maar de praktijk is vaak weerbarstiger. Het is in de wereld van het functioneel programmeren, in geval van ongelijkwaardigheid, gebruikelijk om het linkerscenario van een *either* te zien als de foutconditie, en het rechterscenario als de succesconditie. Ezelsbruggetje: *left is wrong, right is right*.
