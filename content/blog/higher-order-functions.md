---
title: "Higher order functions"
author: "Karl van Heijster"
date: 2024-07-05T21:22:55+02:00
draft: true
comments: true
tags: ["functioneel programmeren", "intentie van code", "software ontwikkelen", "testen"]
summary: "Waarom zou je *higher order functions* willen gebruiken? -- Niet alleen omdat ze er zo cool uitzien. Je introduceert HOFs wanneer je merkt dat één methodcall (of een stuk code met een methodcall erin) het verschil maakt tussen twee of meer identieke methods. Het is, kortom, een manier om hergebruik van code mogelijk te maken."
---

Leg eens uit: wat zijn *higher order functions* (HOFs)? Nou, het zijn functies die andere functies als hun argument hebben. Dus niet dit:


```cs
FilterListOnPropertyA(list, true);
```


Maar dit:


```cs
list.Where(i => i.A == true);
```


-- Inderdaad, voor wie gebruik maakt van [LINQ](https://learn.microsoft.com/en-us/dotnet/csharp/linq/ "'Language Integrated Query (LINQ)', Microsoft documentatie") zijn HOFs al een tweede natuur. Maar hun aanwezigheid is niet vanzelfsprekend in een van huis uit objectgeoriënteerde taal als C#.[^1] ([Lambda-uitdrukkingen](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions "'Lambda expressions and anonymous functions', Microsoft documentatie") werden bijvoorbeeld geïntroduceerd in [versie 3.0](https://en.wikipedia.org/wiki/C_Sharp_3.0 "'C Sharp 3.0', Wikipedia").)


C# kent grofweg twee soorten HOFs: `Action`s en `Func`s. Een `Action` retourneert geen resultaat, een `Func` wel. Dit is af te lezen aan de signatuur van de functies in kwestie. Een `Action<int>` neemt een `int` als input en retourneert niets, een `Func<int>` neemt niets als input en retourneert een `int`. (Een `Func<string, int>` neemt een `string` als input en retourneert een `int`.)


## Polly


Waarom zou je HOFs willen gebruiken? -- Niet alleen omdat ze er zo cool uitzien. Je introduceert HOFs wanneer je merkt dat één methodcall (of een stuk code met een methodcall erin) het verschil maakt tussen twee of meer identieke methods. Het is, kortom, een manier om hergebruik van code mogelijk te maken.


Een voorbeeld. Laatst hadden we een ontwerpdiscussie met een deel van het team. Een collega van me had wat *retry*-activiteit in onze integratietests gebouwd met [Polly](https://www.thepollyproject.org/), ter vervanging van enkele `Thread.Sleep`s. Maar er was een probleem: in tientallen tests kwam dezelfde code terug:


```cs
private ResiliencePipeline _pipeline = new ResiliencePipelineBuilder()
    .AddRetry(new RetryStrategyOptions 
    { 
        ShouldHandle = new PredicateBuilder().Handle<Exception>(), 
        Delay = TimeSpan.FromMilliseconds(500) 
    })
    .Build();

[TestMethod]
public async Task SomeTest()
{
    var sut = new SomeClass();
    await _pipeline.ExecuteAsync(async _ =>
    {
        var result = sut.ProduceResult("Some variable");
        result.Should().BeTrue();
    });
}
```


(De pipeline is geconfigureerd om de functie opnieuw af te trappen wanneer er een [exception](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/exceptions/ "'Exceptions and Exception Handling', Microsoft documentatie") op wordt gegooid. Dat gebeurt wanneer de *assertion* (in dit voorbeeld: `Result.Should().BeTrue()`) faalt. Dus als de test faalt, wordt er naar 500ms nogmaals geprobeerd de actie uit te voeren.)


Hoe zouden we het probleem van die codeduplicatie aan moeten vliegen? Ik stelde voor een helper-class te introduceren -- omdat goede naamgeving later komt, noemde ik 'm `RetryHelper`:


```cs
internal class RetryHelper
{
    private readonly ResiliencePipeline _pipeline = new ResiliencePipelineBuilder()
        .AddRetry(new RetryStrategyOptions
        {
            ShouldHandle = new PredicateBuilder().Handle<Exception>(),
            Delay = TimeSpan.FromMilliseconds(500)
        })
        .Build();

    internal async Task ExecuteAsync(Func<Task> action)
    {
        await _pipeline.ExecuteAsync(async _ =>
        {
            await action();
        });
    }
}
```


De logica om Polly mee te configureren: geabstraheerd naar één centrale plek. Een test die gebruik wilde maken van dit *retry*-gedrag, is daarmee van de verantwoordelijkheid voor deze configuratie verlost:


```cs
private ResiliencePipeline _retryHelper = new RetryHelper();

[TestMethod]
public async Task SomeTest()
{
    var sut = new SomeClass();
    await _retryHelper.ExecuteAsync(async () =>
    {
        var result = sut.ProduceResult("Some variable");
        result.Should().BeTrue();
    });
}
```


Let op de `Func<Task>` die aan `ExecuteAsync` mee wordt gegeven: een method, een stukje gedrag, die uitgevoerd moet worden binnen te aangeroepen method. Het is deze parameter die de `RetryHelper` flexibel genoeg maakt om in verschillende integratietests te gebruiken. De lambda-syntax houdt de test leesbaar.


## Overijverig


In mijn overijverigheid (en uit mijn liefde voor *higher order functions*) stelde ik -- ik weet niet wanneer ik moet stoppen -- zelfs voor om nog een tweede functie mee te geven:


```cs
internal class RetryHelper
{
    // ...

    internal async Task ExecuteAsync<T>(Func<Task<T>> act, Action<T> assert)
    {
        await _pipeline.ExecuteAsync(async _ =>
        {
            var result = await act();
            assert(result);
        });
    }
}
```


Let op het gebruik van een `Func` én een `Action`. Immers, we willen dat de *act* van de test een resultaat retourneert, zodat we deze kunnen gebruiken in de *assert* -- vandaar de `Func`. En omdat we willen dat dat stuk code asynchroon kan zijn, retourneert de `Func` een `Task<T>`. De *assert* hoeft geen resultaat te produceren, vandaar de `Action<T>`.


De aanroep zou er dan als volgt uit komen te zien:


```cs
[TestMethod]
public async Task SomeTest()
{
    var sut = new SomeClass();
    await _retryHelper.ExecuteAsync(
        async () => sut.ProduceResult("Some variable"),
        result => result.Should().BeTrue());
}
```


Maar dat vonden mijn collega's wat veel van het goede. Ik ben geneigd ze gelijk te geven -- althans, een deel van me is daartoe geneigd. Een ander deel zit zich ondertussen af te vragen hoe ik niet stiekem nóg een HOF'je in deze class weet te proppen. (Misschien bij de configuratie...?)


De les is: als je eenmaal begint te spelen met `Action`s en `Func`s, met *higher order functions*, dan kun je het niet helpen er plezier in te krijgen!


[^1]: Ik zeg "van huis uit", omdat C# misschien wel begonnen is als een typische taal voor haar tijd, maar aan één gebonden paradigma is de taal allang niet meer.
