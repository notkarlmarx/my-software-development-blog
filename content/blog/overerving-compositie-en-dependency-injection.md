---
title: "Overerving, compositie en Dependency Injection"
author: "Karl van Heijster"
date: 2023-11-24T08:51:19+01:00
draft: true
comments: true
tags: ["classes", "compositie", "dependency injection", "inheritance", "intentie van code", "objectgeoriënteerd programmeren", "single-responsibility principe", "software ontwikkelen", "SOLID"]
summary: "Mijn collega had -- gedachteloos, naar mijn idee -- overerving toegepast om de nieuwe functionaliteit een plek te kunnen geven. De afgelopen maanden had ik gemerkt dat dit voor hem, en veel van mijn andere teamgenoten, een *go to*-oplossing vormt. Maar ik was niet helemaal tevreden met de code die dat oplevert. Ik voelde meer voor een oplossing die gebruik maakt van compositie. Het leek me een mooie gelegenheid om wat ideeën over deze concepten op papier te zetten."
---

Onlangs had ik wat interessante discussies met een collega over het ontwerp van onze code. Onze twistpunten waren allesbehalve theoretisch, we spraken niet over een classdiagram van een stuk nieuwbouw. Nee, onze handen waren vuil, we zaten midden in de herstructering van een bestaand stuk code om nieuwe functionaliteit mogelijk te maken. 


Mijn collega had -- gedachteloos, naar mijn idee -- [overerving](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming) "'Inheritance (object-oriented programming)', Wikipedia") toegepast om de nieuwe functionaliteit een plek te kunnen geven. De afgelopen maanden had ik gemerkt dat dit voor hem, en veel van mijn andere teamgenoten, een *go to*-oplossing vormt. Maar ik was niet helemaal tevreden met de code die dat oplevert. Ik voelde meer voor een oplossing die gebruik maakt van [compositie](https://en.wikipedia.org/wiki/Object_composition "'Object composition', Wikipedia"). Het leek me een mooie gelegenheid om wat ideeën over deze concepten op papier te zetten.


## Duplicatie


Wanneer we programmeren, komt het regelmatig voor dat ons gevraagd wordt twee features te implementeren die sterk op elkaar lijken, op één ding na. Dat is een probleem dat we op verschillende manieren op zouden kunnen lossen. Eén oplossing zou bijvoorbeeld kunnen zijn om de code van de ene feature te dupliceren en in het duplicaat het relevante deel te wijzigen. 


Dat werkt, maar een bijzonder nette oplossing valt het niet te noemen. Codeduplicatie levert problemen op voor de onderhoudbaarheid van code. Als er een bug in de originele code blijkt te zitten, dan zullen we deze op beide plekken aan moeten passen. Of als er een extra feature toegevoegd moet worden die in beide gevallen moet worden ondersteund, dan moeten we deze op twee plekken toevoegen. Dat is foutgevoelig en inefficiënt. (Gelukkig zijn er -- in mijn omgeving althans -- maar weinig ontwikkelaars voor wie codeduplicatie een serieuze optie is voor dit probleem.)


We zullen dus een andere oplossing moeten vinden. Gelukkig zijn er mogelijkheden te over op dit gebied. Ik zal er in deze blog twee behandelen: overerving en compositie met [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection "'Dependency injection', Wikipedia") (DI).


## Toetsen publiceren (1)


Ik zal de verschillen tussen de verschillende opties uiteenzetten aan de hand van een voorbeeld uit onze praktijk: toetsconstructie. Hoogover ziet het proces van toetsconstructie er zo uit: een toets wordt geconstrueerd, en vervolgens wordt deze door een kandidaat afgenomen. 


De constructie vindt plaats in het ene systeem, de afname in een ander systeem. Om dat voor elkaar te krijgen, moeten beide systemen dezelfde taal spreken. De toets in de constructieomgeving moet daarom worden omgezet naar een formaat dat de afnameomgeving begrijpt. In de praktijk wordt daar de op XML gebaseerde [QTI-standaard](https://nl.wikipedia.org/wiki/QTI_(bestandstype) "'QTI (bestandstype)', Wikipedia") voor gebruikt. Het omzetten van een toets naar QTI wordt "publicatie" genoemd.


Over de details van de standaard hoeven we het nu (gelukkig!) niet te hebben. Wat relevant is voor ons voorbeeld, is dat een toets bestaat uit een inhoud en wat metadata. De code voor het publiceren van een toets zou er, in extreem versimpelde vorm, zo uit kunnen zien:


```cs
public class AssessmentTestPublisher 
{
    public PublishedTest Publish(AssessmentTest test)
    {
        var testContent = ConvertTestContent(test);
        var metadata = ConvertMetdata(test);
        return new PublishedTest(testContent, metadata);
    }

    private XDocument ConvertTestContent(AssessmentTest test)
    {
        // Transform AssessmentTest to XML 
    }

    private XDocument ConvertMetdata(AssessmentTest test)
    {
        // Transform Metadata to XML 
    }
}
```


## Complicatie


Daar waar standaarden bestaan, bestaan aanhangers van standaarden. En daar waar aanhangers van standaarden bestaan, bestaat er geen uniformiteit.


QTI is vrij alomtegenwoordig in de toetswereld. Wat betreft de inhoud van een toets spreken veel afnameomgevingen dezelfde taal. Voor metadata ligt het wat gecompliceerder. Daar leven verschillende standaarden naast elkaar. De ene afnameomgeving verwacht metadata in formaat *x*, de andere in formaat *y*.


De uitdaging is: hoe ondersteunen we beide scenario's zonder onnodige codeduplicatie te introduceren? (Het voorbeeld is niet toevallig, natuurlijk: dit was precies het onderwerp van de discussie met mijn collega.)


## Verantwoordelijkheden


Dit zou een mogelijke oplossing kunnen zijn:


```cs
public class AssessmentTestPublisher 
{
    public PublishedTest Publish(AssessmentTest test, string metadataFormat)
    {
        var testContent = ConvertTestContent(test);
        var metadata = ConvertMetdata(test, metdataFormat);
        return new PublishedTest(testContent, metadata);
    }

    private XDocument ConvertTestContent(AssessmentTest test)
    {
        // Transform AssessmentTest to XML 
    }

    private XDocument ConvertMetdata(AssessmentTest test, string metadataFormat)
    {
        if (metadataFormat == "x")
        {
            // Transform Metadata to XML
            // for standard x
        }
        
        // Transform Metadata to XML
        // for standard y
    }
}
```


We hebben een extra parameter toegevoegd, `metadataFormat`, die ons in staat stelt om te kunnen differentiëren tussen verschillende soorten metadata. (Het betreft hier een parameter van het type `string`, en dat is een vreselijke keuze natuurlijk. Maar het gaat me nu even niet om het type: een `bool` of `enum` zou dezelfde problemen opleveren.)


Het probleem van deze oplossing is dat de code nu niet meer het [*Single-Responsibility Principe*](/tags/single-responsibility-principe/ "Blogs met de tag 'single-responsibility principe'") (SRP) -- de S in [SOLID](/tags/solid/ "Blogs met de tag 'SOLID'") -- respecteert. Deze class heeft, als het op de metadata aankomt, twee verantwoordelijkheden: het genereren van metadata à la *x* en het genereren van metadata à la *y*. 


## Asymmetrische overerving


Het liefst zouden we beide verantwoordelijkheden naar elk hun eigen class abstraheren.


In de praktijk kom ik regelmatig constructies tegen als deze:


```cs
public class AssessmentTestPublisherX 
{
    public PublishedTest Publish(AssessmentTest test)
    {
        var testContent = ConvertTestContent(test);
        var metadata = ConvertMetdata(test);
        return new PublishedTest(testContent, metadata);
    }

    private XDocument ConvertTestContent(AssessmentTest test)
    {
        // Transform AssessmentTest to XML 
    }

    protected virtual XDocument ConvertMetdata(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard x
    }
}

public class AssessmentTestPublisherY : AssessmentTestPublisherX
{
    protected override XDocument ConvertMetadata(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard y
    }
}
```


Er wordt hier gebruik gemaakt van overerving om codeduplicatie te voorkomen. De delen van de code die hergebruikt worden, staan in de baseclass, de delen die moeten variëren worden in de subclass overschreven met de variant in kwestie.


Mijn voornaamste probleem met deze oplossingsrichting is, als ik eerlijk ben, van esthetische aard. Scenario *x* en *y* zijn gelijkwaardig aan elkaar, maar om de een of andere reden is de code voor *x* in de baseclass terechtgekomen en die van *y* in de subclass. Dat suggereert dat *x* op de een of andere manier primair is ten opzichte van *y*, en dat is niet het geval.


Ik heb geen idee of er al een term bestaat voor deze praktijk. Ik noem het "asymmetrische overerving" -- de redenen waarom laten zich hopelijk raden.


## Symmetrische overerving


Een nettere oplossing zou de volgende zijn:


```cs
public abstract class AssessmentTestPublisher
{
    public PublishedTest Publish(AssessmentTest test)
    {
        var testContent = ConvertTestContent(test);
        var metadata = ConvertMetdata(test);
        return new PublishedTest(testContent, metadata);
    }

    private XDocument ConvertTestContent(AssessmentTest test)
    {
        // Transform AssessmentTest to XML 
    }

    protected abstract XDocument ConvertMetdata(AssessmentTest test);
}

public class AssessmentTestPublisherX : AssessmentTestPublisher
{
    protected override XDocument ConvertMetadata(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard x
    }
}

public class AssessmentTestPublisherY : AssessmentTestPublisher
{
    protected override XDocument ConvertMetadata(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard y
    }
}
```


De gedeelde logica zit in een baseclass, en de varianten zijn nu elk in hun eigen subclass ondergebracht. De manier van overerven is symmetrisch, zou je kunnen zeggen. De code voelt alsof deze in evenwicht is.


Maar ook deze oplossingsrichting is niet ideaal. Want de overerving heeft gezorgd voor een sterke koppeling tussen de code in de baseclass en die in de subclasses. De code om de metadata in het juiste formaat te genereren kan niet los worden gezien van de code om toetsen naar QTI om te zetten.


Dat hoeft niet erg te zijn -- en in ons versimpelde voorbeeld is het dat ook niet. Maar een vaak gezien gevolg hiervan is dat code die in base- en subclasses leeft, steeds meer met elkaar verweven raakt. Methods in subclasses roepen methods in baseclasses aan, methods in baseclasses vertrouwen op logica in subclasses. Dat komt de onderhoudbaarheid van de code niet ten goede. Code wijzigen wordt een netelige onderneming.


Met name wanneer de overervingsstructuren dieper worden, neemt de complexiteit enorm toe -- tot het punt dat je als ontwikkelaar continu heen en weer moet pingpongen tussen verschillende classes om te begrijpen wat er nu precies gebeurt. De koppeling zorgt dus ook voor een hogere cognitieve last voor de lezer van de code.


## Compositie


Dit is het punt waarop ik voorzichtig het punt in zou willen brengen dat overerving niet de enige manier is om codeduplicatie tegen te gaan. Als we onze classes op een andere manier op zouden zetten, dan zouden we helemaal geen behoefte hebben aan overerving -- en zo alle problemen voorkomen die erbij komen kijken.


In de objectgeoriënteerde wereld is het een mantra: [*composition over inheritance*](https://en.wikipedia.org/wiki/Composition_over_inheritance "'Composition over inheritance', Wikipedia"). Je zou compositie kunnen karakteriseren als het opbouwen van een complex type uit meerdere eenvoudiger typen. 


In plaats van één class te hebben met daarin alle functionaliteit, splits je deze op in kleinere classes die elk verantwoordelijk zijn voor hun eigen deelfunctionaliteit. De uiteindelijke functionaliteit ontstaat uit de samenwerking tussen de verschillende classes.


## Toetsen publiceren (2)


Laten we, voordat we ons druk gaan maken over de variaties in metadata, eerst teruggaan naar de oorspronkelijke versie van de code:


```cs
public class AssessmentTestPublisher 
{
    public PublishedTest Publish(AssessmentTest test)
    {
        var testContent = ConvertTestContent(test);
        var metadata = ConvertMetdata(test);
        return new PublishedTest(testContent, metadata);
    }

    private XDocument ConvertTestContent(AssessmentTest test)
    {
        // Transform AssessmentTest to XML 
    }

    private XDocument ConvertMetdata(AssessmentTest test)
    {
        // Transform Metadata to XML 
    }
}
```

In onze `AssessmentTestPublisher` kunnen we twee deelverantwoordelijkheden onderscheiden: het omzetten van inhoud van de `AssessmentTest` naar QTI, en het omzetten van de de metadata van de `AssessmentTest`. Laten we beginnen de class op te splitsen naar deelverantwoordelijkheid:


```cs
public class TestContentConverter
{
    public XDocument Convert(AssessmentTest test)
    {
        // Transform AssessmentTest to XML 
    }
}

public class MetadataConverter
{
    private XDocument Convert(AssessmentTest test)
    {
        // Transform Metadata to XML 
    }
}
```


Nu richten we onze blik op de `AssessmentTestPublisher`. De verantwoordelijkheid van deze class -- het omzetten van een `AssessmentTest` naar een `PublishedTest` -- zal hetzelfde blijven. Maar die verantwoordelijkheid gaan we heel anders invullen. Daar waar de oorspronkelijke versie *inhoudelijk* de verantwoordelijkheid droeg voor deze omzetting, heeft deze nieuwe versie slechts de verantwoordelijkheid die omzetting te *coördineren*: 


```cs
public class AssessmentTestPublisher 
{
    private readonly TestContentConverter _testContent;
    private readonly MetadataConverter _metadata;

    public AssessmentTestPublisher()
    {
        _testContent = new TestContentConverter();
        _metdata = new MetaConverter();
    }

    public PublishedTest Publish(AssessmentTest test)
    {
        var testContent = _testContent.Convert(test);
        var metadata = _metdata.Convert(test);
        return new PublishedTest(testContent, metadata);
    }
}
```


Natuurlijk zijn we er nu nog niet. Er zijn twee problemen met deze code: de code voor het converteren van de inhoud en metadata van de toets is nog steeds sterk gekoppeld aan deze class -- via de instantiatie van beide converters in de constructor. Bovendien hebben we geen mogelijkheid om te variëren in het formaat van de metadata.


## Interface


Laten we ons eerst op het eerste probleem focussen -- want dit zal ons ook naar een oplossing van het tweede probleem leiden. Sterker nog, het is de harde koppeling die ons nu belemmert te variëren in de manier waarop we metadata converteren. De `AssessmentTestPublisher` moet ontkoppeld worden van de concrete implementatie van de `MetadataConverter`.


Dat doen we door een interface te introduceren:


```cs
public interface IMetadataConverter
{
    XDocument Convert(AssessmentTest test);
}
```


De `AssessmentTestPublisher` moet gebruik gaan maken van deze interface, in plaats van de concrete class. Daarvoor moeten er twee dingen gebeuren. Ten eerste moet het type van `_metadata` omgezet worden naar de interface -- eenvoudig genoeg. Ten tweede moet de instantiatie van de `MetadataConverter` uit de constructor van de `AssessmentTestPublisher` worden gehaald. Die verantwoordelijkheid delegeren we naar de class die de `AssessmentTestPublisher` instantieert: we gebruiken *dependency injection* (DI):


```cs
public class AssessmentTestPublisher 
{
    private readonly TestContentConverter _testContent;
    private readonly IMetadataConverter _metadata;

    public AssessmentTestPublisher(IMetadataConverter metadata)
    {
        _testContent = new TestContentConverter();
        _metdata = metadata;
    }

    public PublishedTest Publish(AssessmentTest test)
    {
        var testContent = _testContent.Convert(test);
        var metadata = _metdata.Convert(test);
        return new PublishedTest(testContent, metadata);
    }
}
```


## Variaties


De weg is nu vrij om variaties mogelijk te maken. Eerst implementeren we twee varianten van de `IMetadataConverter`:


```cs
public class MetadataConverterX : IMetadataConverter
{
    private XDocument Convert(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard x
    }
}

public class MetadataConverterY : IMetadataConverter
{
    private XDocument Convert(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard y
    }
}
```


Het publiceren van een toets met metadata à la *x* of *y* is nu een kwestie van de `AssessmentTestPublisher` correct instantiëren.


```cs
var x = new AssessmentTestPublisher(new MetadataConverterX());
var y = new AssessmentTestPublisher(new MetadataConverterY());

```


## Krachtig


We hebben ons doel bereikt. We kunnen toetsen publiceren voor verschillende afnameomgevingen zonder onnodige codeduplicatie te hebben geïntroduceerd. Maar belangrijker nog: we hebben dat gedaan zonder een harde koppeling tussen de logica die toetsen publiceert en die metadata converteert. Daarmee houden we de code flexibel en voorkomen we dat beide verantwoordelijkheden met elkaar verknoopt raken.


Compositie is -- zeker in combinatie met DI -- een krachtig middel in objectgeoriënteerd programmeren. Helaas zie ik mijn collega's nog te vaak reflexief grijpen naar overerving, daar waar betere oplossingsrichtingen voorhanden zijn. (Waarmee ik overigens niet wil impliceren dat overerving *nooit* de juiste oplossing is voor een probleem, integendeel. Mijn probleem ligt bij het *gedachteloos* grijpen naar overerving als oplossingsrichting, in plaats van verschillende mogelijkheden af te wegen.) 


Voer jij ook regelmatig interessante discussies met je collega's over de structuur van jullie codebase? Waarover botsen jullie ontwerpintuïties?
