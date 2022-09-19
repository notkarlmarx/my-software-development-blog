---
title: "Tests als documentatie"
author: "Karl van Heijster"
date: 2022-09-19T07:53:25+02:00
draft: false
comments: true
tags: ["clean code", "documentatie", "intentie van code", "testen"]
summary: "Tests zijn een vorm van documentatie. Ze leggen vast hoe een deel van je codebase zich hoort te gedragen. Maar ook: hoe je dat deel van de codebase gebruikt - wat je nodig hebt om het *system under test* te instantiëren, het gedrag van z'n methods etc.. Wie de tests leest, weet hoe de code gebruikt dient te worden. - Althans, dat is de ideale wereld."
---

> ## TL;DR
>
> Tests zijn een vorm van documentatie. Wil documentatie waardevol zijn, dan moet deze makkelijk te raadplegen zijn. Goede tests zijn daarom geoptimaliseerd voor descriptiviteit. 
>
> 1. Ze hebben consistente en eenduidige namen door het hanteren van de *Given_When_Then*-conventie.
>
> 2. Ze leggen nadruk op relevante variabelen door toepassing van DAMP: *Descriptive And Meaningful Phrases*.
>
> 3. Ze abstraheren irrelevante variabelen door het gebruik van *factory*-methods, *Object Mothers* of *Test Builders*.


Tests zijn een vorm van documentatie.


Tests leggen vast hoe een deel van je codebase zich hoort te gedragen.


Tests leggen vast hoe je dat deel van de codebase gebruikt: wat je nodig hebt om het [*system under test*](https://en.wikipedia.org/wiki/System_under_test) (SUT) te instantiëren, het gedrag van z'n methods etc..


Wie de tests leest, weet hoe de code gebruikt dient te worden. - Althans, dat is de ideale wereld.


## Descriptief


Om het gebruik van de code te documenteren, moet het voor een lezer begrijpelijk zijn wat er gebeurt. - Sterker nog: het moet *makkelijk* zijn om te begrijpen wat er gebeurt: welke variabelen zijn relevant? - waarom krijg ik dit resultaat? - waarin verschilt deze test van de vorige?


Tests moeten descriptief zijn (tests zijn immers ook code!). Ze moeten [helder en welonderscheiden](https://nl.wikipedia.org/wiki/Cirkelredenering_van_Descartes) hun boodschap communiceren. Ze zijn er om ontwikkelaars te helpen.


Want als ontwikkelaars code breken, zijn de tests hun eerste leidraad bij het vinden van het probleem. Een ontwikkelaar die zo'n falende test voor zijn neus toveren, moet denken: *ja, logisch.* Hij moet denken: *het is logisch dat* die *wijziging* deze *test om zeep helpt.*


## Waarom


Dat verhoogt de ontwikkelproductiviteit aanzienlijk. Elke minuut die niet aan debuggen hoeft te worden besteed, is gewonnen.


Maar ontwikkelcapaciteit is niet de enige reden waarom tests descriptief moeten zijn.


Wil documentatie - elke vorm van documentatie; ook tests - ontwikkelaars helpen, dan moet deze wel gelezen worden. Documentatie die niet gelezen wordt, is waardeloos. (- Niemand leest de handleiding; dat doe jij ook niet bij je nieuwe stofzuiger!) 


Als je gelezen wil worden, moet je het aantrekkelijk maken gelezen te worden. Tests moeten ontwikkelaars een prettige tijd geven door hen te helpen - te leiden - in hun ontwikkelwerkzaamheden. - En als je een prettige ervaring met tests hebt, ben je ook meer geneigd deze goed te onderhouden. 


## Naamgeving


Hoe maak je tests descriptief? Dat begint bij de naamgeving.


Allereerst wil je dat je naamgeving consistent is. Als een lezer weet wat hij kan verwachten, verlicht dat zijn cognitieve druk. Hij kan op eerdere ervaringen vertrouwen, in plaats van alles opnieuw zelf uit te hoeven vogelen. Dat geeft 'm meer gelegenheid om zich op de inhoud te richten.


Wat de inhoud van die test is, moet van de titel afgelezen kunnen worden. `Feature_6839()` is geen descriptieve naam. (- Maar gelukkig zou jij nooit zulke namen gebruiken... toch?) `Bug_12056()` ook niet. `GetItem_Successfully()` is al wat beter - al laat het aan de lezer om te raden waar dat succes in bestaat.


## Given_When_Then


`GetItemEndpoint_ReceivesIdRequest_ReturnsItemWithThatId()` is - wat aan de lange kant, maar toch ook behoorlijk eenduidig. Wie die titel leest, weet precies wat 'ie kan verwachten van de test.


De ontwikkelaar die deze test voor zijn neus krijgt, moet wel denken: *ja, logisch.*


De bovenstaande naamgeving volgt het [*Given_When_Then*-patroon](https://en.wikipedia.org/wiki/Given-When-Then). Het eerste deel (*Given*) beschrijft de conditie die je test, het tweede deel (*When*) de operatie die je uitvoert, en het derde deel (*Then*) de uitkomst van die operatie. 


De naamgeving volgt eigenlijk het adagium van [*Arrange, Act, Assert*](https://docs.microsoft.com/en-us/visualstudio/test/unit-test-basics?view=vs-2022#write-your-tests). Dat betekent dat de naam van de test je een beknopt overzicht geeft van wat je in de test aan zult treffen. Samen geven ze een compleet beeld van waar de test uit bestaat.


Wie die naamgevingsconventie volgt, krijgt daar gratis de gewilde consistentie bij. 


## Relevantie


Een descriptieve test maakt de relevante variabelen expliciet (en abstraheert al het overbodige - maar daar kom ik zo op). Het moet voor een lezer duidelijk zijn wat de werkzame onderdelen in de vergelijking zijn. Je kunt het ook zo zien: een descriptieve test is een verhaal - focus je dus op de hoofdpersonen en niet op de figuranten. (- Onze tests zijn geen postmoderne fictie!) 


Neem de volgende test[^1]:


```cs
[TestMethod]
public void Navigator_GoesToAlbumPage_NavigatesToAlbumsUrl() 
{
    var baseUrl = "http://photos.user.com/";
    var nav = new Navigator(baseUrl);
    nav.GoToAlbumPage();
    nav.GetCurrentUrl().Should().Be(baseUrl + "/albums");
}
```


Duidelijk genoeg, toch? - En wat als ik nu vertel dat deze code een bug bevat?


De test faalt namelijk, omdat het `"http://photos.user.com//albums"` als resultaat verwacht. Oeps!


Wat scheelt er aan deze test? - Hij legt te weinig nadruk op de relevante variabelen - in dit geval: de output. Het gebruik van logica verhult het verwachte gedrag van de code, zodanig zelfs, dat een bug eenvoudig onder de radar vliegt.


## Niet DRY, maar DAMP


Deze versie is duidelijker:


```cs
[TestMethod]
public void Navigator_GoesToAlbumPage_NavigatesToAlbumsUrl() 
{
    var nav = new Navigator("http://photos.user.com/");
    nav.GoToAlbumPage();
    nav.GetCurrentUrl().Should().Be("http://photos.user.com/albums");
}
```


Het is waar, bovenstaande bevat wat codeduplicatie - de test is minder [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). 


Maar schone tests (*clean test code*) zijn niet hetzelfde als schone productiecode (*clean production code*), hun logica is anders. Tests kunnen juist descriptiever worden van codeduplicatie - zeker als het om de outputs gaat. Ze hoeven niet zo DRY te zijn. Ze mogen DAMP zijn, dat wil zeggen: bestaan uit *Descriptive And Meaningful Phrases*.


## Abstractie


"Nadruk op het relevante leggen" wil ik ook zeggen: het irrelevante abstraheren, verbergen voor de lezer. 


Stel je een test voor, een muur van code. Aan het begin regel na regel complexe *set up*-logica die het SUT in de juiste staat brengt. (Objecten die geïnstantieerd worden, vervolgens als afhankelijkheid geinjecteerd worden; methods die drie keer worden aangeroepen om de data in gereedheid te brengen; een property die wordt gewijzigd...)


Dan, uiteindelijk: een commentaarregel `//Act` en daaronder een method. Gevolgd door een (DAMP, uiteraard!) *Assert*-sectie. Ga nu maar na: welk deel van die *set up*-logica had het uiteindelijke resultaat nu tot gevolg?


Het probleem van zo'n test is dat deze de lezer overlaadt met informatie. De ontwikkelaar ziet de bomen door het bos niet meer. Alle relevante onderdelen zijn aanwezig - maar ook alle irrelvante. De test is een roman die aan de lopende band uitweidt, die niet kan kiezen tussen haar hoofdpersonages en figuranten.


## Factories


Dit probleem kan voorkomen worden met het gebruik van *factories*. (Ik zeg bewust niet: het [*Factory*-patroon](https://en.wikipedia.org/wiki/Factory_method_pattern). Want het idee hierachter is breder dan dat - of, ook mogelijk: er is niet één *Factory*-patroon.) Een *factory* is een method of class die verantwoordelijk is voor het instantiëren van een object.


*Factories* zijn ideaal om complexe *set up*-logica te verhullen voor de lezer van een test. - Maar, nota bene, alléén voor zover die logica irrelevant is om de test te begrijpen. *Factories* die relevante informatie abstraheren, hinderen het begrip van een test net zozeer als overdadige informatie.


De eenvoudigste implementatie daarvan is: een *factory*-method in de test-class. Deze instantieert het SUT met de juiste defaultwaarden - en accepteert parameters daar waar relevante variabelen in het spel zijn. (Zie ook [deze blog](/blog/21/09/droger-tests-met-factory-methods/).) 


Een bijkomend voordeel van deze aanpak is dat je tests er minder fragiel van worden. Wanneer de constructor van je SUT wijzigt, hoef je dit maar op één plek in je testcode aan te passen - en je tests slagen weer. 


```cs
[TestMethod]
public void Factory() 
{
    var sut = GetSutWithComplexSetUpLogic();
    sut.DoSomething("Relevant variable");
    sut.SomethingDone.Should().BeTrue();
}

private static SystemUnderTest GetSutWithComplexSetUpLogic()
{
    var sut = new SystemUnderTest();

    // Complex set up logic
    // ...

    return sut;
}
```


Wat ook regelmatig voorkomt, is dat verschillende tests (al dan niet met verschillende SUTs) dezelfde soort objecten verwachten om te functioneren. Dat is een uitgelezen gelegenheid om het [*Object Mother*-patroon](https://martinfowler.com/bliki/ObjectMother.html). Dit is een static class die ervoor verantwoordelijk is om deze objecten te instantiëren. De class kan uit verschillende methods bestaan, die elk een aangepaste versie van het object instantiëren.


```cs
[TestMethod]
public void ObjectMotherFoo() 
{
    var oFoo = ObjectMother.GetObjectWithFoo();
    var sut = GetSutWithComplexSetUpLogic();
    sut.DoSomething(oFoo);
    sut.SomethingDone.Should().BeTrue();
}

[TestMethod]
public void ObjectMotherBar() 
{
    var oBar = ObjectMother.GetObjectWithBar();
    var sut = GetSutWithComplexSetUpLogic();
    sut.DoSomething(oBar);
    sut.SomethingDone.Should().BeFalse();
}
```


Wanneer *Object Mothers* niet meer voldoen - wanneer het aantal variaties uit de klauwen begint te lopen, bijvoorbeeld - kun je het grove geschut van stal halen: [*Test Builders*](https://arleypadua.medium.com/builder-pattern-applied-to-testing-60e009c427c6). Ik zal hier niet uitweiden over de details, ik zal alleen maar zeggen: - ik vind het er altijd erg cool uitzien in mijn testcode:


```cs
[TestMethod]
public void TestBuilder() 
{
    var obj = new TestObjectBuilder()
        .WithId(1)
        .WithName("Foo")
        .WithProperty(new PropertyBuilder()
            .WithName("Property1"))
        .Build();
    var sut = GetSutWithComplexSetUpLogic();
    sut.DoSomething(obj);
    sut.SomethingDone.Should().BeTrue();
}
```


*Test Builders* zijn ideaal om irrelevante details te abstraheren en zo de maximale nadruk op de relevante variabelen te leggen. In het bovenstaande voorbeeld zou je bijvoorbeeld, aangenomen dat `"Property1"` de relevante variabele is, de `TestObjectBuilder` standaardwaarden mee kunnen geven voor het `Id` (`1`) en de `Name` (`"Foo"`). De aandacht van de lezer komt zo automatisch te liggen bij datgene wat voor de test het meest relevant is.


## Waardevol


Tests zijn net zo'n waardevol deel van je codebase als je productiecode. Tests informeren ontwikkelaars over het gebruik van bepaalde delen van de code. Dat is handig voor nieuwe ontwikkelaars - maar ook voor jou, als je na maanden afwezigheid opnieuw in een stoffig deel van de codebase moet duiken.


Ze verdienen daarom net zoveel aandacht als productiecode - maar daarom niet per se dezelfde aandacht. Goede testcode is geoptimaliseerd voor descriptiviteit. Elke test moet eenvoudig te doorgronden zijn voor de lezer. Let daarom goed op de naamgeving, en op welke informatie je toont en welke je achterwege laat.


Elke test vertelt een verhaal. En uiteindelijk is een spannend verhaal - een verhaal dat je wíl lezen - de beste vorm van documentatie.


## Meer in deze reeks


1. **Tests als documentatie**
2. Tests als vangnet [binnenkort]
3. Tests als ontwerpmiddel [binnenkort]


[^1]: Een aangepaste versie van voorbeeld besprak ik eerder [deze blog](/blog/22/01/hoe-droog-wil-je-je-test-hebben/); de oorspronkelijke referentie is [*Unit Testing*](https://www.oreilly.com/library/view/software-engineering-at/9781492082781/ch12.html) van [Erik Kuefler](https://www.linkedin.com/in/erikkuefler/), hoofdstuk 12 van het [fantastische](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/) [*Software Engineering at Google*](https://www.oreilly.com/library/view/software-engineering-at/9781492082781/)). De test maakt overigens gebruik van het eveneens fantastische [Fluent Assertions](https://fluentassertions.com/).
