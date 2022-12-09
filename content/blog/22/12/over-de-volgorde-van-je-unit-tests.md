---
title: "Over de volgorde van je unit tests"
author: "Karl van Heijster"
date: 2022-12-09T07:47:44+01:00
draft: false
comments: true
tags: ["clean code", "code lezen", "documentatie", "intentie van code", "testen", "unit tests"]
summary: "Maakt het uit in welke volgorde je unit tests staan? - Nee. Tests slechts een middel om de werking van het systeem te valideren. Het maakt niet uit in welke volgorde de tests worden afgetrapt, als ze maar allemaal slagen. (Of liever: als ze maar op het juiste moment falen.) Dat is een mogelijk antwoord. - In een praatje van Kevlin Henney vond ik een ander antwoord."
---

Maakt het uit in welke volgorde je unit tests staan? 


Nee. Tests slechts een middel om de werking van het systeem te valideren. Het maakt niet uit in welke volgorde de tests worden afgetrapt[^1], als ze maar allemaal slagen. (Of liever: als ze maar op het juiste moment falen.) - Dat is een mogelijk antwoord.


In het onderstaande praatje van [Kevlin Henney](http://kevlin.tel/) vond ik een ander antwoord.


{{<youtube id="MWsk1h8pv2Q" title="Structure and Interpretation of Test Cases • Kevlin Henney • GOTO 2022" >}}
<br>


Ja, de volgorde van je unit tests is belangrijk. Want een ontwikkelaar zal je tests raadplegen om de werking van de code te proberen te begrijpen. [Tests zijn een vorm van documentatie](/blog/22/09/tests-als-documentatie/), behandel hen dus als zodanig.


## Van eenvoudig naar complex


Een ontwikkelaar zal naar alle waarschijnlijkheid beginnen bij de eerste test in je testclass - want zo zitten mensen, lezers nu eenmaal in elkaar. Ze lezen van boven naar beneden.


Als de eerste test een obscure *edge case* behandelt, dan legt dat onmiddellijk een hoge cognitieve druk op de lezer. Van hem of haar wordt verlangd een geavanceerd scenario te begrijpen, zonder dat de basis daarvoor éérst is gelegd. En dat zal het begrip niet ten goede komen.


De eerste les wat betreft de volgordelijkheid van unit tests, moge dus duidelijk zijn: *begin met de eenvoudige tests, en werk langzaam omhoog naar steeds complexere scenario's.* 


Neem je lezer bij de hand. Elke test bouwt voort op de vorige.


Bouw na het schrijven van elke test een reflectiemoment in: "Lezer, begrijp je wat hier gebeurt? Ja? Stel nu dat we *hier* op gaan variëren..." - En vraag je onder het schrijven regelmatig af: bestaat er tussen deze en de volgende test een tussenscenario, bij wijze van spreken, die mijn lezer meer inzicht geeft in het complexer scenario?


## Groepering


De tweede les wat betreft de volgordelijkheid van unit tests, volgt uit het voorgaande: *groepeer je tests zodanig dat ze een conceptuele eenheid vormen.*


Als de tests in je testclass eerst functionaliteit *a* testen, en dan *b*, dan weer *a* en daarna *c*, dan raakt de lezer al snel de draad kwijt. Groepeer functionaliteiten *a*, *b* en *c*. Zet dat wat bij elkaar hoort dicht bij elkaar.


Gebruik hiervoor geneste classes. (Dit is een tip van Henney waar ik van opveerde.) Je kunt de geneste classes gebruiken om bepaalde onderdelen van een feature te testen. 


```cs
public class FeatureTests
{
    [TestClass]
    public class SubFeatureATests
    {
        // ...
    }

    [TestClass]
    public class SubFeatureBTests
    {
        // ...
    }
}
```


Wat ook kan, is de feature te verdelen in een *happy path* en *sad paths*. 


```cs
public class FeatureTests
{
    [TestClass]
    public class HappyPathTests
    {
        // ...
    }

    [TestClass]
    public class SadPathATests
    {
        // ...
    }

    [TestClass]
    public class SadPathBTests 
    {
        // ...
    }
}
```


Die nesting helpt jou als schrijver van de tests om je op één ding te focussen. Het helpt je om in beeld te brengen welke aspecten je allemaal wil testen, en geeft je inzicht in het de vraag of je bepaalde aspecten voldoende hebt behandeld of niet. Een geneste class met maar één test is doorgaans een teken dat je je code maar oppervlakkig hebt doorlopen. Welke scenario's kun je nog meer verzinnen?


Tegelijkertijd helpt het de lezer om snel een overzicht te krijgen van de manier waarop je testclass gestructureerd is. Het helpt om de subfeatures in kaart te brengen - als je de boel zo hebt ingericht - of om eenvoudig een overzicht te krijgen van hoe de code idealiter werkt - en wat er gebeurt wanneer je daarvan afwijkt.


## Leesbaarheid


Tests zijn een validatiemechanisme - maar ze hebben de potentie om meer te zijn dan dat. Dit zijn twee eenvoudige manieren om tests te transformeren tot toegankelijke documentatie voor ontwikkelaars.


[Robert "uncle Bob" Martin](http://cleancoder.com/products) schreef al in [*Clean Code*](https://www.oreilly.com/library/view/clean-code-a/9780136083238/) dat het aller-, aller-, allerbelangrijkste aan je testsuite haar leesbaarheid is. Dankzij de tips van Henney komt dat ideaal nu een stapje dichterbij.


[^1]: Aangenomen dat er geen onderlinge afhankelijkheden zijn, althans!
