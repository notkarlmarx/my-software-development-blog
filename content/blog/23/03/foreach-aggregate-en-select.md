---
title: "ForEach, Aggregate en Select"
author: "Karl van Heijster"
date: 2023-03-10T07:33:25+01:00
draft: false
comments: true
tags: ["functioneel programmeren", "LINQ"]
summary: "`ForEach` gebruik je alleen als je een `Action` - zonder *return value*! - uit wil voeren voor elke lijstwaarde. `Select` gebruik je als je een resultaat verwacht. En `Aggregate` gebruik je als je het verschil tussen beide uit wil leggen. Of - vooruit - als je wil aggregeren."
---

Een tijdje terug werkte ik met een collega van me aan een datamigratie in onze [DocumentStore](https://nl.wikipedia.org/wiki/NoSQL) (zie ook [deze blog](/blog/21/09/stapje-voor-stapje-data-migreren/)). Hij werkte aan een stukje code, dat ik vervolgens reviewde, en soms andersom, en we vonden zelfs hier en daar de tijd om te *pairen* (zie ook [hier](/blog/23/01/wel-code-reviews-geen-pull-requests/) en [hier](/blog/23/01/is-pair-programming-minder-efficient/)).


Gedurende dat proces betrapte hem meermaals op het schrijven van een variant op de volgende code:


```cs
public List<Transformed> Transform(IEnumerable<Original> someList)
{
    var result = new List<Transformed>();
    someList.ToList().ForEach(o => result.Add(new Transformed 
    {
        Id = Guid.NewGuid(),
        SomeProperty = o.SomeProperty,
        OtherProperty = o.OtherProperty
    }));
    return result;
}
```


Ik zeg "betrapte" en dat impliceert dat er iets mis is met deze code - wat maar deels waar is. Laat ik vooropstellen: er is niks mis met deze code in zoverre dat deze functioneert. De code doet wat het moet doen, namelijk een lijst van het ene type omzetten naar die van een ander type.


## Accumulator


Sterker nog, de code volgt een bekend patroon in de wereld van het functioneel programmeren, namelijk dat van een *accumulator*. Een accumulator is een type dat in het verlengde ligt van een [*functor*](/blog/22/10/wat-is-een-functor/)[^1] of [*monad*](/blog/22/12/wat-is-een-monad/), bedoeld om waarden mee te aggregeren. 


De method die dat type implementeert om dat te doen, wordt in de literatuur doorgaans *fold* of *reduce* genoemd. De intentie van de method is om een lijst van waarden terug te brengen tot één waarde - al kan hij ook gebruikt worden om een nieuwe lijst aan waarden te genereren. We zouden de bovenstaande method dus kunnen herschrijven met een *fold* of *map*.


\- Of met `Aggregate` - want dat is hoe de method heet in [LINQ](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/). Omdat mijn voorbeelden in [C#](https://learn.microsoft.com/en-us/dotnet/csharp/) zijn, zal ik die naam in het vervolg van deze blog blijven gebruiken.


Om zijn doel voor elkaar te kunnen krijgen, heeft `Aggregate` twee argumenten nodig: een initiële waarde, ook wel de *seed* of *source* genoemd, en een functie die uitlegt hoe de oorspronkelijke input moet worden geaggregeerd. 


[Enrico Buonanno](https://twitter.com/la_yumba) gebruikt in [*Functional Programming in C#*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition) de volgende metafoor om dat concept toe te lichten. Stel, je hebt een verzameling citroenen waar je limonade van wil maken. De citroenen zijn de oorspronkelijke input. Het - in eerste instantie lege - glas waar de limonade in terechtkomt is de *seed*. En het uitpersen van de citroenen is de aggregatiefunctie.


## Plussen


Je kunt veel verschillende dingen uitdrukken met de `Aggregate`-method. Je kunt er bijvoorbeeld de som van een reeks getallen mee berekenen[^2]:


```cs
public int Sum(IEnumerable<int> list) =>
    list.Aggregate(0, (seed, i) => seed + i);
```


De oorspronkelijke input van deze method is de `list` van het type `IEnumerable<int>`. De *seed* is een `int`, en in eerste instantie is deze 0, want we hebben nog niets bij elkaar opgeteld. De functie verwacht twee inputargumenten: de *seed* en een `int`, oftwel: een lijstwaarde. De functie telt die lijstwaarde op bij de de *seed*.


Je zou ook een `Count`-method kunnen definiëren in termen van `Aggregate`: 


```cs
public int Count(IEnumerable<object> list) =>
    list.Aggregate(0, (seed, _) => seed++);
```


In dit geval is de precieze lijstwaarde voor ons niet relevant, want we zijn alleen geïnteresseerd in het aantal. We kunnen deze dus invullen als een *discard* (`_`). De functie hoeft niets anders te doen dan de `seed` op te hogen en te retourneren voor elke lijstwaarde.


## Transformatie middels aggregatie


We kunnen de method van mijn collega ook omschrijven naar een `Aggregate`. Kijk nog maar eens naar die method: alle elementen zijn aanwezig. De oorspronkelijke input is `someList`, de *seed* is `result` en de functie is dat wat de `List<Original>` naar een `List<Transformed>` omzet.


Maar om de code werkend te krijgen, moeten we wel die functie wel wat herschrijven:


```cs
public List<Transformed> Transform(IEnumerable<Original> someList) =>
    someList.Aggregate
    (
        Enumerable.Empty<Transformed>(), 
        (result, o) => result.Append(new Transformed 
        {
            Id = Guid.NewGuid(),
            SomeProperty = o.SomeProperty,
            OtherProperty = o.OtherProperty
        })
    );
```


In plaats van `Add` te kunnen gebruiken, moeten we onze toevlucht nemen tot `Append`. Waarom? 


`ForEach` verwacht een `Action`, oftewel: een expressie die *geen* waarde teruggeeft. `Add` geeft geen waarde terug. Als we naar de definitie van die method kijken, dan zien we dat die `void` is. 


`Aggregate` verwacht daarentegen een `Func`, oftewel: een expressie die *wel* een waarde teruggeeft. `Append` neemt een `IEnumerable<T>` als input en retourneert een `IEnumerable<T>` met de toegevoegde lijstwaarde.


Je zou het zo kunnen zien: `Aggregate` doorloopt alle lijstwaarden, en elke keer als hij dat doet, vervangt hij de *seed* door de nieuw teruggegeven waarde. Vóór aanvang van het loopen, is de lijst nog leeg; na de eerste keer wordt deze vervangen door een lijst met één `Transformed`; na de tweede keer door een lijst met twee `Transformed`s, et cetera.


Dat voelt misschien wat tegenintuïtief. Waarom een bestaande lijst vervangen door een nieuwe, in plaats van de oorspronkelijke lijst te aan te vullen met een nieuwe waarde? Dat heeft wat te maken met het functionele paradigma en haar nadruk op *immutability* (zie [deze blog](/blog/22/05/heb-je-die-setter-echt-nodig/)). In het kort: door steeds met een nieuw object te werken, weet je zeker dat het object waar je mee werkt niet in de tussentijd is aangepast zonder dat je het wist. Het geeft je als programmeur wat meer zekerheid.


## `Select`


Misschien zit je al een tijdje te denken: *jongen, dat kan toch véél simpeler allemaal?!* En daar heb je gelijk in. Want LINQ kent al een method die functioneel hetzelfde doet als de bovenstaande implementaties doen: `Select`.


```cs
public List<Transformed> Transform(IEnumerable<Original> someList) =>
    someList.Select(o => new Transformed 
    {
        Id = Guid.NewGuid(),
        SomeProperty = o.SomeProperty,
        OtherProperty = o.OtherProperty
    });
```


Waarom dan eerst al dat geëmmer over `ForEach` en `Aggregate`? Omdat het zich loont te weten wanneer je wat gebruikt! `ForEach` gebruik je alleen als je een `Action` - zonder *return value*! - uit wil voeren voor elke lijstwaarde. `Select` gebruik je als je een resultaat verwacht. 


En `Aggregate` gebruik je als je het verschil tussen beide uit wil leggen. Of - vooruit - als je wil aggregeren.


[^1]: Sterker nog, je kunt een functor definiëren in termen van een accumulator. Maar die oefening laat ik aan de lezer.


[^2]: Deze method maakt gebruik van de zogenaamde [*expression body members*](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members), een syntax die wat onnodige opsmuk weghaalt wanneer je method uit niet meer dan één regel bestaat.
