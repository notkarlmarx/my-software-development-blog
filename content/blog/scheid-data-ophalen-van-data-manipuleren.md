---
title: "Scheid data ophalen van data manipuleren"
author: "Karl van Heijster"
date: 2022-07-04T15:15:25+02:00
draft: true
comments: true
tags: ["boeken", "clean code", "mentale modellen", "refactoren", "single-responsibility principe", "testbaarheid", "testen"]
summary: "Het aantal refactoravonturen (met goede of slechte afloop) dat ik heb beleefd is, inmiddels al lang niet meer op één hand te tellen. In de loop der tijd is een terugkerend fenomeen me opgevallen: code waarin het ophalen van data niet wordt gescheiden van het manipuleren ervan. Laten we dat eens wat nader bekijken."
---

Begrijp me niet verkeerd, ik ben dol op het implementeren van nieuwe features. Maar als er één ding is waar mijn softwareontwikkelaarshartje sneller van gaat kloppen, dan is het 't opschonen van bestaande code: variabelen hernoemen, algoritmen vereenvoudigen, verantwoordelijkheden scheiden - oftewel: refactoren. Alles ondersteund door een goed testsuite, uiteraard!


## Het fenomeen


Het aantal refactoravonturen (met goede of slechte afloop) dat ik heb beleefd is, inmiddels al lang niet meer op één hand te tellen. In de loop der tijd is een terugkerend fenomeen me opgevallen: code waarin het ophalen van data niet wordt gescheiden van het manipuleren ervan. 


Denk je bijvoorbeeld een scenario in waarin er een lijst met *resources* wordt opgehaald uit de database. De individuele *resources* worden vervolgens in een `for each`-loop één voor één gemanipuleerd. Ze worden bijvoorbeeld gemapt naar een ander type, of dienen als input om een andere datastructuur op te bouwen. Vaak komt het in dat proces voor dat de data moet worden verrijkt met informatie uit andere bronnen. Dat kan voor alle data gelden, of voor data die aan bepaalde condities voldoet.


De volgende pseudocode geeft het idee aardig weer:


```cs
var result = new List<SomeType>();

// Get resources
var foos = _repository.GetFoos();

foreach (var foo in foos)
{
    // Map resource to new type
    var r = new SomeType 
    {
        Prop1 = foo.Prop1,
        Prop2 = foo.Prop2
    }

    // In case of some condition...
    if (foo.SomeCondition) 
    {
        // ...get some additional information...
        var bars = _repository.GetBars(foo.BarId);

        // ...and add it to the new type
        r.Prop3 = bars;
    }
    result.Add(r);
}

// Further processing...

```


Het hoeft niemand die de titel van deze blog heeft gelezen, te verbazen dat ik geen voorstander ben van dit soort code. Hiermee geconfronteerd, slaat mijn hart een slag over. De linkerhelft duikt teleurgesteld ineen om dit soort structuren, de rechterhelft springt een gat in de lucht omdat ik weer aan het refactoren slaan mag.


## Het probleem


Maar laten we eerst een stapje terugzetten. Wat is het probleem van deze code?


Code die verantwoordelijk is voor het ophalen én manipuleren van data, schendt het *Single-Responsibility Principe* (SRP). Die code kent namelijk twee verantwoordelijkheden: (1) data ophalen, en (2) data manipuleren. 


Nu hoeft dat niet per se een probleem te zijn, zolang je de code nooit aan hoeft te passen. Maar wanneer dat wel gebeurt - en als je een verstokte refactorfanaat in je team hebt zoals ik, *gaat* het gebeuren -, leveren verknoopte verantwoordelijkheden allerlei moeilijkheden op. Het wordt bijvoorbeeld moeiijk om bepaalde functionaliteit naar aparte methods of classes te abstraheren. Die functionaliteit is immers verknoopt met andere verantwoordelijkheden. Een verhuizing zou betekenen: je verhuist ofwel alles, ofwel niets. Maar het hele idee van het abstraheren van bepaalde functionaliteit is nu eenmaal dat het om *bepaalde* functionaliteit gaat!


Om dat soort moeilijkheden verderop in de ontwikkeling van je code base te voorkomen, loont het zich eigenlijk altijd om code zo goed mogelijk te structureren naar het SRP. Maar hoe ver moet je daar in gaan? Want die twee verantwoordelijkheden van de code hierboven kunnen natuurlijk weer uiteenvallen in meerdere deelverantwoordelijkheden. Het ophalen van data kan in de bovenstaande code bijvoorbeeld worden uitgesplitst naar (1a) het ophalen van de `foos` en (1b) het ophalen van de `bars`. En het manipuleren van de data kent ook meerdere stappen: (2a) een nieuw type declareren, (2b) de properties mappen die voor alle objecten gelden, (2c) checken of een bepaalde conditie standhoudt, en (2d) de properties mappen die bij die conditie horen. 


## Wat is één verantwoordelijkheid?


Hoe strikt die deelverantwoordelijkheden gescheiden moeten worden, hangt van een aantal dingen af. Bijvoorbeeld van hun complexiteit. Om de code lees- en onderhoudbaar te houden, kan het zich lonen deze op verschillende plekken - methods, misschien zelfs classes - onder te brengen. 


Het kan ook afhangen van de mate waarin die deelverantwoordelijkheden los van elkaar moeten kunnen evolueren. Het is voor de hand liggend dat de manipulatie van data afzonderlijk moet kunnen worden aangepast van het ophalen ervan. Maar datzelfde kan niet per se gezegd worden van de manier waarop de data gemanipuleerd wordt. Het mappen van `foos` en `bars` naar `SomeType` is één actie. Die actie bestaat weliswaar uit deelstappen, maar die deelstappen hebben op zichzelf weinig betekenis. Ze zijn alleen zinvol binnen de context van het overkoepelende algoritme.


Oftewel, als het op het scheiden van de (a)'tjes en de (b)'tjes in de bovenstaande opsomming aankomt, mag je jezelf als ontwikkelaar best wat speelruimte gunnen. Datzelfde vind ik niet opgaan voor het scheiden van de (1)'tjes en de (2)'tjes. Het ophalen van data en het manipuleren ervan zijn mijns inziens zulke ver uit elkaar liggende verantwoordelijkheden, dat deze eigenlijk altijd gescheiden móeten worden.


## Testbaarheid


Wellicht zijn deze overwegingen wat aan de theoretische kant. Ze bieden in elk geval weinig concrete handvaten. Wat complex is, is bijvoorbeeld afhankelijk van het vaardigheidsniveau van de programmeur. En welke deelverantwoordelijkheden bij elkaar horen en welke los van elkaar moeten kunnen evolueren, wil in de loop van een project wel eens overwacht veranderen. 


Een meer praktische leidraad is deze: code moet zodanig gescheiden worden, dat deze eenvoudig te testen is. Sterker nog, één van de belangrijkste redenen om het SRP te respecteren, is omdat dit makkelijk testbare code oplevert - makkelijker testbaar dan wanneer je het niet doet, in elk geval.


Ga maar na. Stel, je zou het algoritme willen testen die `foos` en `bars` mapt naar `SomeType`, zoals geschetst in de code hierboven. Op dit moment kun je die code niet testen zonder gebruik te maken van de `repository` - wat dat ook moge zijn. Als dat een interface is, zul je een mock moeten specificeren die *the real deal* simuleert. Dat is wat ongemak voor jou als ontwikkelaar - en wat extra testcode om te onderhouden -, maar op zich overkomelijk. Als het echter een concrete implementatie is - *foei!* -, dan heb je een groter probleem. De code is dan namelijk niet in isolatie te testen. Het testen van het algoritme houdt automatisch ook het testen van de [Repository](https://dotnettutorials.net/lesson/repository-design-pattern-csharp/) in, en dat houdt het testen van de database in. 


Denk je eens in wat er allemaal voor nodig is om die tests aan de gang te krijgen! Je moet een database opzetten en inrichten en deze vullen met testdata, en dat allemaal vóórdat je kunt beginnen aan dat waar het je eigenlijk om gaat: het algoritme testen. Bovendien zal het je tests erg langzaam maken, waardoor je ontwikkelcyclus vertraagd zal worden. Elke keer als je de tests aftrapt, zul je even moeten wachten, wat je als ontwikkelaar uit je *flow* haalt, en je productiviteit vermindert.


## De scheiding


Het goede nieuws is: je *hoeft* je verantwoordelijkheden niet met elkaar te verknopen. In de meeste gevallen is het vrij eenvoudig om het ophalen van data te scheiden van het manipuleren ervan. Maar het vraagt wel wat bewustzijn van je als ontwikkelaar. De bovenstaande code kan bijvoorbeeld worden omgeschreven naar iets als dit:


```cs
var foos = _repository.GetFoos();
// Get bars for foos where SomeCondition applies,
// based on the foo's BarId
var bars = _repository.GetBars(
    foos.Where(f => f.SomeCondition)
        .Select(f => f.BarId));

var result = new List<SomeType>();
foreach (var foo in foos)
{
    // Map resource to new type
    var r = new SomeType 
    {
        Prop1 = foo.Prop1,
        Prop2 = foo.Prop2,
        // If available, get some additional information
        // and add it to the new type
        Prop3 = bars.FirstOrDefault(b => b.Id == foo.BarId);
    }
    result.Add(r);
}

// Further processing...
```


De code om de data op te halen, is nu helemaal losgetrokken van de mappingcode. En je ziet: de code is er meteen een stuk eenvoudiger op geworden ook! De check op `SomeCondition` is uit het algoritme verdwenen, bijvoorbeeld. Dat komt doordat deze in wezen gekoppeld was aan de vraag of we de data op moesten halen of niet. Het `if`-statement kon worden omgeschreven naar een `Where`-clausule. 


Hierdoor hoeven we in het algoritme zelf alleen maar de corresponderende `bar` in de al opgehaalde lijst te vinden - of `null` terug te geven wanneer deze niet gevonden kan worden, en de property daarom effectief niet zetten.


Maar de voordelen eindigen nog niet daar. Onze aanvankelijke refactorslag heeft ons in staat gesteld om de `foreach`-loop te kunnen abstraheren naar een nieuwe method. Laten we 'm `ToSomeType` noemen:


```cs
public static IEnumerable<SomeType> ToSomeType(IEnumerable<Foo> foos, IEnumerable<Bar> bars)
{
    foreach (var foo in foos)
    {
        // Map resource to new type
        var r = new SomeType 
        {
            Prop1 = foo.Prop1,
            Prop2 = foo.Prop2
        }

        // If available, get some additional information
        // and add it to the new type
        r.Prop3 = bars.FirstOrDefault(b => b.Id == foo.BarId);
        yield return r;
    }
}
```


Het mooie is nu: deze method valt in isolatie te testen. Het enige wat je moet doen, is wat `foos` en wat `bars` specificeren in je test, en deze meegeven aan die nieuwe method. De volgende test geeft een indruk:


```cs
[TestMethod]
public void OneFooWithCorrespondingBar_WhenMappedToSomeType_ReturnsSomeTypeWithBar()
{
    // Arrange
    var foo = new Foo { BarId = 1 };
    var bar = new Bar { Id = 1 };
    var foos = new [] { foo };
    var bars = new [] { bar };

    // Act
    var someType = ToSomeType(foos, bars).First();

    // Assert
    Assert.IsNotNull(someType.Prop3);
}
```


Nu weet ik niet hoe het met jou zit, maar als ik moest kiezen tussen een complete database opzetten of wat objecten definiëren aan het begin van mijn test - nou, dan wist ik het wel! 


## Waarom scheiden we code niet?


Ik kan me voorstellen dat ik lezers heb die denken: joh, dit zijn toch allemaal open deuren? En misschien hebben ze daar gelijk in - maar het aantal keren dat ik code heb kunnen verbeteren door het ophalen en manipuleren van data te scheiden, vertelt toch een ander verhaal. Misschien loont het zich om daarom kort te reflecteren op een aantal redenen waarom dit niet stevig verankerd is in het hoofd van elke ontwikkelaar.


Een eerste mogelijkheid zou kunnen zijn: gebrek aan kennis. Misschien is niet elke ontwikkelaar zich even bewust van de problemen die schendingen van het SRP opleveren, verderop in de ontwikkelcyclus. Deze blog zou een bijdrage kunnen leveren aan een verhoging van het bewustzijn op dat gebied.


Misschien is het ook: druk van buitenaf. Veel stakeholders van softwareprojecten zijn over het algemeen in de eerste instantie geïnteresseerd in nieuwe features. Voor codekwaliteit interesseren ze zich in mindere mate - en meestal pas als het te laat is. (Dat is overigens geen steek onder water naar stakeholders toe. Het is helemaal niet hun taak zich om codekwaliteit te bemoeien; dat is die van jou als ontwikkelaar!) Het is denkbaar dat ontwikkelaars de hete adem van stakeholders in hun nek voelen, en daarom genoegen nemen met code die werkt, in plaats van code die geweldig is opgezet. Lieg niet: ik geloof dat iedereen zich hier wel eens aan heeft bezondigt.


## Mentale modellen


Een derde mogelijkheid ontleen ik aan [Felienne Hermans](https://www.felienne.com/)' bespreking van [mentale modellen](https://en.wikipedia.org/wiki/Mental_model) in [*The Programmer's Brain*](https://www.felienne.com/). Misschien zien sommige ontwikkelaars het probleem van deze specifieke schending van het SRP niet, omdat hun mentale representatie van wat de code doet, dat niet toelaat.


Kijk nog eens naar de code waar ik deze blog mee begon. Met welke analogie zou je die code kunnen beschrijven? Ik zou me een ontwikkelaar voor kunnen stellen, die het als volgt zou omschrijven: *Ik verzamel alle spullen in deze doos (*`repository.GetFoos()`*), en als ze van mij zijn (*`if (foo.SomeCondition)`*), dan pak ik een rode sticker uit die doos (*`repository.GetBars()`*) en plak die erop.* (En omdat ik mezelf nu eenmaal ben, stel ik me voor dat die ontwikkelaar in een pijnlijke scheiding ligt.)


Wat impliceert die analogie over de code hierboven? Wie een doos doorzoekt, gaat niet eerst een keer alle spullen door om te kijken hoeveel rode stickers 'ie nodig heeft, om daarna nog een keer aan de gang te gaan om zijn spullen te beplakken. Het is in dat geval veel gemakkelijker om de rode sticker te pakken, zodra je één van je spullen tegenkomt.


De crux zit 'm in het feit dat de ontwikkelaar denkt dat het ophalen van de `bars` een eenvoudige operatie is, net als het pakken van een rode sticker. Maar precies op dat punt wijkt het mentale model af van de werkelijkheid. 


Want het ophalen van data uit een database is een relatief zware operatie, die beter gevangen wordt door de volgende analogie: *Ik verzamel alle spullen in deze doos, en als ze van mij zijn, dan ga ik naar de supermarkt om een rode sticker te halen en erop te plakken.* Een ontwikkelaar die zo redeneert, denkt wel twee keer na voordat 'ie data ophalen en data manipuleren met elkaar verknoopt!
