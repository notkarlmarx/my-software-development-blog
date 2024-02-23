---
title: "Test-Driven Development en YAGNI"
author: "Karl van Heijster"
date: 2024-02-09T12:03:04+01:00
draft: true
comments: true
tags: []
summary: "Vaak werkt het zo: tests maken *x* mogelijk, Test-Driven Development (TDD) tilt *x* naar een volgend niveau. Welnu, het idee van YAGNI -- *You Ain't Gonna Need It* -- veronderstelt tests. TDD tilt het naar een volgend niveau. Tests faciliteren YAGNI, TDD radicaliseert het."
---


Vaak werkt het zo: tests maken *x* mogelijk, [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) tilt *x* naar een volgend niveau.


Welnu, het idee van [YAGNI](/tags/yagni/ "Blogs met de tag 'YAGNI'") -- *You Ain't Gonna Need It* -- [veronderstelt tests] (BLOG). TDD tilt het naar een volgend niveau. Tests faciliteren YAGNI, TDD radicaliseert het.


TDD schrijft voor: *red*-*green*-*refactor*. Schrijf een falende test, schrijf precies genoeg code om die test te laten slagen, en refactor je code daarna. De crux van dit verhaal zit 'm in het "precies genoeg code": dát is YAGNI bij uitstek.


## FizzBuzz


Laten we de bekende [FizzBuzz](https://codingdojo.org/kata/FizzBuzz/ "'FizzBuzz', Coding Dojo") [kata](https://nl.wikipedia.org/wiki/Kata "'Kata', Wikipedia")[^1] nemen om dit te illustreren. In deze kata word je gevraagd om een systeem te implementeren met eenvoudige requirements. Het systeem accepteert een `integer` als input, en retourneert een `string` als output. In de meeste gevallen zal de output de `string`-representatie van de input zijn: `1` staat tot `"1"`, `2` tot `"2"`, enzovoort. Er zijn drie afwijkingen van deze regel. Een getal dat deelbaar is door 3, retourneert `"Fizz"`; een getal dat deelbaar is door 5 retourneert `"Buzz"`, en een getal dat deelbaar is door 3 én 5 retourneert `"FizzBuzz"`.


Het doel van de kata is niet de juiste logica te schrijven -- dat is een triviale opgave. Het doel van de kata is de juiste logica te schrijven *door middel van TDD*. Dus dat is wat we gaan doen.


## Compileerfout


FizzBuzz begint met een falende... -- nee, niet eens met een falende test, niet in de conventionele zin van het woord in elk geval. FizzBuzz begint met een compileerfout:


```cs
[TestMethod]
public void Test()
{
    var result = FizzBuzz(1);
}
```


We roepen een method `FizzBuzz` aan, maar er bestaat nog helemaal geen method `FizzBuzz`. We bevinden ons nu in fase *red*. -- Die observatie vertelt ons iets over het wezen van deze fase. Een test die zich in *red* bevindt, is niet per se een test die bewijst dat het systeem een fout in de logica bevat. Het kan net zo goed betekenen: de afwezigheid van een systeem, of een deel van het systeem, om te testen. 


Een test bevindt zich in *red* als deze faalt *om wat voor reden dan ook*.


Ons onmiddellike doel is om de test naar *green* te krijgen. Dat wil zeggen: de compileerfout verhelpen.


```cs
[TestMethod]
public void Test()
{
    var result = FizzBuzz(1);
}

public string FizzBuzz(int input)
{
    return string.Empty;
}
```


Merk op: we schrijven precies genoeg code om de compileerfout te verhelpen *en geen regel meer*.


## Test #1


Pas daarna gaan we verder met de test:



```cs
[TestMethod]
public void Test()
{
    var result = FizzBuzz(1);
    result.Should().Be("1");
}

// ...
```


Deze test faalt, omdat `FizzBuzz` een lege `string` teruggeeft, en niet `"1"`. We bevinden ons weer in *red*. Het is tijd om ons opnieuw op de implementatie te richten: 


```cs
// ...

public string FizzBuzz(int input)
{
    return "1";
}
```


We schrijven de code die nodig is om de test te laten slagen *en geen regel meer*.


Natuurlijk: het is absurd om een hard gecodeerde waarde terug te geven in `FizzBuzz`. We weten toch dat deze implementatie niet lang stand zal houden? Waarom zouden we onze tijd besteden aan deze ongein? Omdat: we *nu* nog niet meer code nodig hebben.


## Test #2


Laten we een tweede test toevoegen, en de implementatie aanpassen om deze te laten slagen:


```cs
[DataTestMethod]
[DataRow(1, "1")]
[DataRow(2, "2")]
public void Test(int input, string output)
{
    var result = FizzBuzz(input);
    result.Should().Be(output);
}

public string FizzBuzz(int input)
{
    return input.ToString();
}
```


Opnieuw: je weet heus wel dat de code die je schrijft de volgende test niet zal overleven -- dat is het punt niet. Het punt is: op dit moment is het nog niet nodig dat je code meer doet dan dit. Dit is programmeren op z'n YAGNI in zijn meest pure vorm -- en het is aanvankelijk verwarrend en ongemakkelijk en voelt inefficiënt, dat is allemaal waar.


## Test #3 & #4


Maar we blijven dat idee nastreven in de volgende test, en de implementatie is opnieuw stuitend triviaal:


```cs
[DataTestMethod]
[DataRow(1, "1")]
[DataRow(2, "2")]
[DataRow(3, "Fizz")]
public void Test(int input, string output)
{
    var result = FizzBuzz(input);
    result.Should().Be(output);
}

public string FizzBuzz(int input)
{
    if (input == 3)
    {
        return "Fizz";
    }
    return input.ToString();
}
```


En misschien is de implementatie van de vierde test wel net zo stuitend:


```cs
[DataTestMethod]
[DataRow(1, "1")]
[DataRow(2, "2")]
[DataRow(3, "Fizz")]
[DataRow(6, "Fizz")]
public void Test(int input, string output)
{
    var result = FizzBuzz(input);
    result.Should().Be(output);
}

public string FizzBuzz(int input)
{
    if (input == 3 || input == 6)
    {
        return "Fizz";
    }
    return input.ToString();
}
```


## Test #5


Maar tegen de tijd dat we het scenario toe gaan voegen om de `9` om te zetten naar `"Fizz"`, moeten we ons afvragen of dit niet handiger kan. En dat blijkt ook te kunnen:


```cs
// ...

public string FizzBuzz(int input)
{
    if (input % 3 == 0)
    {
        return "Fizz";
    }
    return input.ToString();
}
```


Nu we ons veilig in *green* bevinden, kunnen we de boel zelfs een beetje opschonen. We kunnen de code, ondersteund door ons [vangnet](/blog/22/09/tests-als-vangnet/ "'Tests als vangnet'") van tests, veilig refactoren:


```cs
// ...

public string FizzBuzz(int input)
{
    if (IsDivisibleBy3(input))
    {
        return "Fizz";
    }
    return input.ToString();
}

private bool IsDivisibleBy3(int input) =>
    input % 3 == 0
```


Het is niet het doel van deze blog deze complete kata uit te spellen. De rest van de implementatie -- van zowel de logica als de tests -- laat ik over als oefening aan de lezer. Ik vertrouw erop dat het idee nu wel duidelijk zal zijn, en hoop dat het verband tussen TDD en YAGNI voldoende is aangetoond.


## Moeilijkheid


Maar voor sommige lezers zal de vraag blijven knagen: waarom zou ik ervoor kiezen om mijn code op zo'n (ogenschijnlijk) gruwelijk inefficiënte manier te schrijven? 


Ik heb sympathie voor het gevoel dat TDD -- zeker in de context van FizzBuzz -- vreselijk omslachtig aanvoelt. Maar dat gevoel is gestoeld op het idee dat de kata bedoeld is om de juiste logica te produceren, en dat idee is onjuist. Het punt van de kata is om een proces van programmeren te oefenen, om TDD in de vingers te krijgen -- de logica die het uiteindelijk oplevert is van ondergeschikt belang.


De moeilijkheid van de kata zit 'm in het feit dat het probleemdomein zo eenvoudig is dat het verleidelijk wordt de principes van TDD los te laten. Het is verleidelijk om de oplossing van het gestelde probleem in één vloeiende beweging uit je vingers te laten vloeien. Een ontwikkelaar die niet geoefend is in de kunst van TDD zal constant met zichzelf in strijd zijn om niet meer code te schrijven dan nodig is. Maar onthoud: *You Ain't Gonna Need It... just yet*.


## Inefficiënt?


TDD voelt misschien inefficiënt, maar dat is het niet. Dat is het niet, omdat het proces ervoor zorgt dat je nooit onbedoeld code schrijft die je niet had hoeven schrijven. Als er geen test is die je noodzaakt bepaalde code te schrijven, is er geen reden om die code te schrijven.


Het effect daarvan is: je codebase zal nooit code bevatten die niet gedekt is door tests. Dat reduceert het aantal bugs in de code aanzienlijk. 


Bovendien zal de werking van de code altijd goed [gedocumenteerd](/blog/22/09/tests-als-documentatie/ "'Tests als documentatie'") zijn. Wie TDD't -- écht TDD't, en wie dus het idee van YAGNI volledig geïnternaliseerd heeft --, zal altijd naar de tests kunnen wijzen en zeggen: *dit* is wat de code doet *en meer ook niet*. Zelfs de helderste, duidelijkst gestructureerde code ter wereld kan die belofte niet waarmaken.


Klinkt dat inefficiënt? Ik dacht het niet!
