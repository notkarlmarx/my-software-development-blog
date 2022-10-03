---
title: "Identifiers zijn ook objecten"
author: "Karl van Heijster"
date: 2022-10-03T07:36:58+02:00
draft: false
comments: true
tags: ["clean code", "domeinmodel", "intentie van code", "primitive obsession"]
summary: "Het oneigenlijk gebruik van \"primitieve\" types voor iets wat eigenlijk op een domeinniveau gedefinieerd hoort te worden, wordt *primitive obsession* genoemd. Het gebruik van een ingebouwd type voor een Id, is een specifieke instantie daarvan. De oplossing is: gebruik een door *jou* (of liever: jouw team) gedefinieerd object om het Id mee weer te geven."
---

Hoe ziet een gemiddeld domeinobject eruit? Grote kans dat het lijkt op iets als dit:


```cs
public class Foo 
{
    public Guid Id { get; set; }
    public string Prop1 { get; set; }
    public string Prop2 { get; set; }
    // More properties...
}
```


En dat is op zich best wel prima. Maar kan het beter? Ik geloof van wel.


## Probleem #1


Laat ik je op een paar problemen wijzen. Stel, we hebben de volgende method:


```cs
public Foo GetFooThatBars(Guid fooId, Guid barId) 
{
    var foo = _fooRepository.Get(fooId);
    var bar = _barRepository.Get(barId);
    if (bar.Foos.Contains(foo)) 
    {
        return foo;
    }
    throw new Exception($"Bar '{barId}' does not contain Foo '{fooId}'")
}
```


Mijn vraag is: wat houdt een ontwikkelaar tegen om per ongeluk het `fooId` met het `barId` te verwisselen bij het coderen van een nieuwe feature? - Het antwoord is: niets. 


Natuurlijk, de namen van de parameters geven een goede hint voor wat betreft de volgorde. Maar als de ontwikkelaar daar overheen leest - omdat hij afgeleid is, of overwerkt, of omdat 'ie eenvoudigweg een sloridige lezer is -, dan is het einde oefening. De applicatie heeft er een verse nieuwe bug bij. 


Natuurlijk, met een beetje geluk pikt in codereviewer de bug eruit vóórdat de wijziging gemerged wordt naar de *develop*-branch. Maar daar op rekenen is een slechte strategie. Ook de codereviewer kan er overheen lezen - omdat hij afgeleid is, of overwerkt, of omdat 'ie een slordige lezer is. Code reviews zijn een slecht middel om bugs te achterhalen.[^1]


## Probleem #2


Laat ik nog een situatie schetsen. Stel, we hebben de volgende class:


```cs
public class FooBar 
{
    public Dictionary<Guid, Guid> Union { get; set; }
    // More properties...
}
```


In de property `Union` bevinden zich de `Foos` die bij de juiste `Bars` horen. Of: de `Bars` die bij de juiste `Foos` horen. 


Welke van de twee is het? Is het Id van `Foo` de *key* van dit `Dictionary`, van die van `Bar` de *value*? Of is het precies andersom?


(Zeg niet: "De class heet `FooBar`, dus het zal de eerste optie wel zijn." Dat is het probleem omzeilen. Want de meeste classes hebben niet de naamgevingsstructuur van dit voorbeeld. En trouwens, dan nog blijft het een aanname dat die structuur de opbouw van het `Dictionary` weergeeft.)


Je hebt in dit geval geen parameternamen om je beslissing op te baseren. Met een beetje geluk bevat de code wat unittests die je instrueren over het correcte gebruik van deze class. Maar wat als de programmeur - afgeleid, overwerkt, slordig - een fout heeft gemaakt in die tests? Durf je erop te vertrouwen dat de codereviewer daar op heeft gedubbelcheckt?


\- Eerlijk? Ik zou het niet doen. Want onlangs kwam ik precies zo'n situatie tegen als de bovenstaande - en in de unittests bleek de programmeur de Ids per ongeluk te hebben omgewisseld.


## Oorzaak


Wat is de oorzaak van onze moeilijkheden? Het feit dat er een `Guid` wordt gebruikt om het Id te modelleren.


Dus wat is de oplossing? Ids als `int` of `string` modelleren? Nee, want in dat geval loop je tegen precies dezelfde problemen aan. Van al deze types valt het gebruik niet af te lezen. Want jouw team heeft deze types niet ontwikkeld voor *jouw* applicatie. Daarom zijn ze niet descriptief in *jouw* context.


Het oneigenlijk gebruik van dit soort "primitieve" types voor iets wat eigenlijk op een domeinniveau gedefinieerd hoort te worden, wordt [*primitive obsession*](https://wiki.c2.com/?PrimitiveObsession) genoemd.[^2] Het is een fenomeen dat zich overigens niet beperkt tot Ids. Het gebruik van een ingebouwd type voor een Id, is een specifieke instantie van *primitive obsession*. Andere voorbeelden zijn: domeinspecifieke berichten die als `string` gemodelleerd worden, of geldwaarden als `int` of `decimal`. 


## Oplossing


De oplossing is: gebruik een door *jou* (of liever: jouw team) gedefinieerd object om het Id mee weer te geven. Definieer een [class](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/classes) of [struct](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct) met een descriptieve naam voor deze specifieke functie: `FooId`, `BarId`. 


Vergelijk de onderstaande code eens met het eerste voorbeeld:


```cs
public Foo GetFooThatBars(FooId fooId, BarId barId) 
{
    var foo = _fooRepository.Get(fooId);
    var bar = _barRepository.Get(barId);
    if (bar.Foos.Contains(foo)) 
    {
        return foo;
    }
    throw new Exception($"Bar `{barId}` does not contain Foo '{fooId}'")
}
```


Wat gebeurt er nu als een afgeleide, overwerkte en/of slordige ontwikkelaar het `FooId` verwisselt met het `BarId`? Hij krijgt een compilerfout om zijn oren! De mogelijkheid om de fout te maken is effectief afgesneden.


En datzelfde geldt voor het tweede voorbeeld:


```cs
public class FooBar 
{
    public Dictionary<FooId, BarId> Union { get; set; }
    // More properties...
}
```


Het `Dictionary` zelf is nu glashelder over wat het verwacht van de ontwikkelaar. Zelfs de meest afgeleide, overwerkte en slordige ontwikkelaar krijgt het niet meer voor elkaar de oorspronkelijke bug te introduceren. 


## Makkelijk


Stel je eens voor dat alle code het zo moeilijk zou maken om programmeerfouten te maken! Stel je voor dat de codebase je, bij het implementeren van een nieuwe feature, als het ware bij de hand neemt bij het maken van elke volgende stap. Hoeveel sneller zou je dan - bugvrije! - code op kunnen leveren?


Goede code maakt het goede doen makkelijk, en een fout maken moeilijk. 


Natuurlijk, dat ideaalbeeld is nog ver weg. Maar je kunt morgen alvast één ding doen om die wereld een stapje dichterbij te brengen. Verhef de Ids in de code van de *primitives* die het nu zijn, naar volwaardige domeinobjecten. Identifiers zijn ook objecten - ook zij verdienen onze aandacht en liefde.


[^1]: Zie [deze](https://medium.com/swlh/code-reviews-fail-at-finding-bugs-a45957bad1ac) en [deze](https://bartoszgorka.com/code-review-is-not-for-catching-bugs) blog. Maar vooral: duik in je herinnering en probeer eens het aantal keren te tellen dat je succesvol een bug hebt achterhaald tijdens een code review. Valt tegen, toch?

[^2]: Maar merk op dat het probleem verder gaat dan de [ingebouwde](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types) of [primitieve](https://docs.microsoft.com/en-us/dotnet/api/system.type.isprimitive?view=net-6.0) types. Je zou elk denkbaar type kunnen gebruiken om een Id mee te modelleren - voor mijn part maak je gebruik van een [`Color`](https://docs.microsoft.com/en-us/dotnet/api/system.drawing.color?view=net-6.0) of [`Point`](https://docs.microsoft.com/en-us/dotnet/api/system.drawing.point?view=net-6.0). Ook dat lost het probleem niet op. Het probleem is niet dat de types primitief zijn, het probleem is dat ze de intentie van de code niet duidelijk weergeven.
