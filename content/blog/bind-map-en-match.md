---
title: "Bind, Map en Match"
author: "Karl van Heijster"
date: 2024-07-26T08:26:21+02:00
draft: true
comments: true
tags: ["functioneel programmeren", "mentaal model", "refactoren", "software ontwikkelen"]
summary: "Ik schrijf al twee jaar op dit blog over functioneel programmeren in C#, dus je zou denken dat ik de basis inmiddels wel een beetje zou moeten beheersen -- en toch overkomt het me nog regelmatig dat ik uitroep: och, zit het *zo*! Zo had ik onlangs -- na een hoop gepiel (en een beetje hulp van Scott Wlaschin) -- een openbaring met betrekking tot de `Map`- en `Bind`-functies."
---

Ik schrijf al twee jaar op dit blog over [functioneel programmeren](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'") in C#, dus je zou denken dat ik de basis inmiddels wel een beetje zou moeten beheersen -- en toch overkomt het me nog regelmatig dat ik uitroep: och, zit het *zo*! Zo had ik onlangs -- na een hoop gepiel (en een beetje hulp van [Scott Wlaschin](https://scottwlaschin.com/)) -- een openbaring met betrekking tot de `Map`- en `Bind`-functies (zie respectievelijk [deze](/blog/22/10/wat-is-een-functor/ "'Wat is een functor?'") en [deze blog](/blog/22/12/wat-is-een-monad/ "'Wat is een monad?'")).


## Casus


Ik was bezig in één van de [*vertical slices*](https://www.jimmybogard.com/vertical-slice-architecture/ "Jimmy Bogard, 'Vertical Slice Architecture'") in onze applicatie waarin een object wordt geupdatet. In pseudocode zag die class er ongeveer zo uit:


```cs
public async Task<CommandResult> Handle(
    UpdateCommand request, CancellationToken cancellationToken)
{
    var option = await _repository.Get(request.Id);
    return await option.Match(async original => {
        if (!IsValid(original, request.Updated))
        {
            return CommandResult.ValidationFailed;
        }
        original.Update(request.Updated);
        await _repository.Save(original);
        return CommandResult.Success;
    },
    () => CommandResult.NotFound);
}
```


Oftewel: we halen een object op uit onze [repository](https://martinfowler.com/eaaCatalog/repository.html "Edward Hieatt & Rob Mee, 'Repository' @ Martin Fowler") op basis van het meegegeven `Id`. De `Get`-method retourneert een `Option`, want er kan ofwel een object bestaan met dat `Id` ofwel niet. We handelen beide scenario's af met `.Match`. Als deze wel bestaat, dan doen we een validatie, updaten het oorspronkelijke object,[^1] slaan deze op in de repository en geven aan dat de operatie succesvol is verlopen. Als deze niet bestaat, geven we aan dat het oorspronkelijke object niet gevonden kan worden.


## Niet lekker


Deze opzet heeft me nooit helemaal lekker gezeten. We maken gebruik van een functioneel concept, de [*option*](/tags/options/ "Blogs met de tag 'options'"), maar benutten deze niet tot haar volle potentie. We pakken de *option* meteen uit en proppen vervolgens (1) validatie, (2) update, (3) opslaan en (4) het retourneren van een resultaat in één en dezelfde [lambda-expressie](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions "'Lambda expressions and anonymous functions'"). 


(Je zou kunnen stellen dat die lambda daarmee het [Single-Responsibility Principe](/tags/single-responsibility-principe/ "Blogs met de tag 'single-responsibility principe'") (SRP) schendt. Je zou kunnen stellen dat we, door deze verantwoordelijkheden bij elkaar te stoppen, we de testbaarheid van het systeem compromitteren -- we ontzeggen ons de mogelijkheid die zak in isolatie te testen. 


Maar het is de vraag in hoeverre deze argumenten zijn mijn ongemak met deze opzet verklaren. Is het écht nodig om binnen deze `Handler` een nieuwe method voor elke verantwoordelijkheid te definiëren? En is het wenselijk al die verantwoordelijkheden los van elkaar te testen? -- Nee, ik denk dat de reden van mijn ongemak ijdeler is dan dat: het *oogt* niet als functionele code.)


## `Option` of `Either`?


In een loos uurtje op een donderdagmiddag besloot ik de bovenstaande implementatie te refactoren.


Ik stelde mezelf de vraag: hoe zou ik het uitpakken van de *option* uit kunnen stellen? Ik realiseerde me: een `Option` is eigenlijk niet de juiste datatype hier, niet de juiste [*monad*](/tags/monads/ "Blogs met de tag 'monads'"). Wat vanuit het perspectief van het geheel op het spel staat, is niet een object-of-niet -- maar een object-of-*return type*. En wat retourneert de `Handle`-method? Een `CommandResult`. Dus ik begon hiermee:


```cs
public async Task<CommandResult> Handle(
    UpdateCommand request, CancellationToken cancellationToken)
{
    var option = await _repository.Get(request.Id);
    return await option.ToEither(CommandResult.NotFound)
        .Match(async original => {
            if (!IsValid(original, request.Updated))
            {
                return CommandResult.ValidationFailed;
            }
            original.Update(request.Updated);
            await _repository.Save(original);
            return CommandResult.Success;
        },
        error => error);
}
```


## Validatie


We hebben dus met een `Either` te maken, niet met een `Option`. -- En daar zouden we wat mee kunnen in die validatielogica. Als wie los zouden trekken, als we daar een functie van zouden maken, wat zou ons dat dan opleveren? Ofwel we retourneren een validatiefout, ofwel we retourneren het oorspronkelijke object.


```cs
public async Task<CommandResult> Handle(
    UpdateCommand request, CancellationToken cancellationToken)
{
    var option = await _repository.Get(request.Id);
    return await option.ToEither(CommandResult.NotFound)
        .Bind(original => Validate(original, request.Updated))
        .Match(async original => {
            original.Update(request.Updated);
            await _repository.Save(original);
            return CommandResult.Success;
        },
        error => error);
}

private EitherAsync<CommandResult, SomeObject> Validate(
    SomeObject original, SomeObject updated) =>
    IsValid(original, updated)
        ? original
        : CommandResult.ValidationFailed;
```


## `Bind`?


Dan, de volgende regel: het updaten van het origineel. Mijn eerste ingeving was om voort te gaan op het pad dat ik was ingeslagen -- en dus weer een `Bind` te gebruiken:


```cs
public async Task<CommandResult> Handle(
    UpdateCommand request, CancellationToken cancellationToken)
{
    var option = await _repository.Get(request.Id);
    return await option.ToEither(CommandResult.NotFound)
        .Bind(original => Validate(original, request.Updated))
        .Bind(original => 
            original.Update(request.Updated)) // Compiler error!
        .Match(async original => {
            await _repository.Save(original);
            return CommandResult.Success;
        },
        error => error);
}
```


Maar dat leverde een compileerfout op. Waarom? Omdat `Bind` een ander *return type* verwacht dan dat wat de lambda teruggeeft. We zouden dit op verschillende manieren op kunnen lossen. Bijvoorbeeld door het *return type* expliciet weer te geven:


```cs
public async Task<CommandResult> Handle(
    UpdateCommand request, CancellationToken cancellationToken)
{
    var option = await _repository.Get(request.Id);
    return await option.ToEither(CommandResult.NotFound)
        .Bind(original => Validate(original, request.Updated))
        .Bind<SomeObject>(original => 
            original.Update(request.Updated))
        .Match(async original => {
            await _repository.Save(original);
            return CommandResult.Success;
        },
        error => error);
}
```


Of door de lambda te wrappen in een method die wel het juiste *return type* definieert:


```cs
public async Task<CommandResult> Handle(
    UpdateCommand request, CancellationToken cancellationToken)
{
    var option = await _repository.Get(request.Id);
    return await option.ToEither(CommandResult.NotFound)
        .Bind(original => Validate(original, request.Updated))
        .Bind(original => Update(original, request.Updated))
        .Match(async original => {
            await _repository.Save(original);
            return CommandResult.Success;
        },
        error => error);
}

private static EitherAsync<CommandResult, SomeObject> Update(
    SomeObject original, SomeObject updated) =>
    original.Update(updated);
```


Maar beide opties voelen niet helemaal goed. Het is alsof we een vierkant blokje in een rond gat proberen te duwen. Natuurlijk, met een beetje krachtuitoefening krijgen we het heus wel voor elkaar, maar dat doet niets af aan het feit dat we eenvoudigweg op het verkeerde spoor zitten.


## Spoorweg


Dit is het moment waarop het kwartje bij mij eindelijk viel, over wat nu het verschil is tussen `Bind` en `Map`. `Bind` gebruik je wanneer je functie een *monad* retourneert -- dat is `Bind`, eh, `Bind` maakt: dat deze met *monads* om kan gaan. `Map` gebruik je wanneer je functie een "gewoon" object retourneert -- dat is wat `Map` `Map` maakt. (En dat is waarom je een *monad* in een *monad* krijgt, wanneer je `Map` gebruikt op een functie die een *monad* retourneert.)


Wlaschin gebruikt in [*Domain Modeling Made Functional*](https://pragprog.com/titles/swdddf/domain-modeling-made-functional/) een spoorwegenmetafoor.[^2] Er zijn twee sporen in onze keten van functies: ofwel we krijgen een `CommandResult` terug, ofwel het object zelf. Je zou `Bind` en `Map` kunnen zien als de spoorwissels. `Bind` is gebruik je in de context van een dubbel spoor, `Map` in de context van een enkel spoor.


Visueel ziet dat er zo uit (vergeef me mijn vreselijke [ASCII-art](https://en.wikipedia.org/wiki/ASCII_art "'ASCII art', Wikipedia")):


```
      =======
Bind:   \\
      =======

      =======
Map:    \\
         ====
```


De oplossing voor ons probleem is dan ook voor de hand liggend -- `Map` gebruiken in plaats van `Bind`:


```cs
public async Task<CommandResult> Handle(
    UpdateCommand request, CancellationToken cancellationToken)
{
    var option = await _repository.Get(request.Id);
    return await option.ToEither(CommandResult.NotFound)
        .Bind(original => Validate(original, request.Updated))
        .Map(original => original.Update(request.Updated))
        .Match(async original => {
            await _repository.Save(original);
            return CommandResult.Success;
        },
        error => error);
}
```


## Resultaat


De rest van de refactorslag is betrekkelijk eenvoudig. We gebruiken `Do` om het object op te slaan (want opslaan is een [*side effect*](https://en.wikipedia.org/wiki/Side_effect_(computer_science) "'Side effect (computer science)', Wikipedia")) en duwen op die manier de `Match` helemaal naar het eind van de keten. En als we de `ToEither` rechtstreeks aan onze eerste call naar de *repository* plakken, houden we één lange, ononderbroken reeks aaneengeregen functies over:


```cs
public async Task<CommandResult> Handle(
    UpdateCommand request, CancellationToken cancellationToken) => 
    await _repository.Get(request.Id)
        .ToEither(CommandResult.NotFound)
        .Bind(original => Validate(original, request.Updated))
        .Map(original => original.Update(request.Updated))
        .Do(async original => await _repository.Save(original))
        .Match(_ => CommandResult.Success, error => error);
```


Onze method is een *pipeline* geworden (zie [dit praatje](https://www.youtube.com/watch?v=ipceTuJlw-M "'Pipeline-oriented programming - Scott Wlaschin - NDC Porto 2023', YouTube") van meester Wlaschin voor een uitgebreide inleiding) -- en ik ben een stapje dichterbij het begrijpen van functioneel programmeren in C#. *Tuut-tuut!*



[^1]: Liefhebbers van functioneel programmeren zal het opgevallen zijn dat `original` gewijzigd wordt en vervolgens opgeslagen -- het is een *mutable* object. Dit is, helaas, een gevolg van de database die we gebruiken. Deze gooit een foutmelding op als we een "nieuw" object (i.e. de binnenkomende update) opslaan op de plek van de oorspronkelijke. De database sluit zo het gebruik van [*immutable*](/tags/immutability/ "Blogs met de tag 'immutability'") datastructuren uit.

[^2]: We zaten zojuist dus letterlijk metaforisch op het verkeerde spoor!
