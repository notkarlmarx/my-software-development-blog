---
title: "Objectgeoriënteerd en functioneel BTW berekenen - Revisited"
author: "Karl van Heijster"
date: 2022-06-24T11:26:45+02:00
draft: true
comments: true
tags: ["boeken", "functioneel programmeren", "objectgeoriënteerd programmeren", "performance"]
summary: "Ik plaatste een tijd geleden wat kanttekeningen bij mijn aanpak Enrico Buonanno's uitdaging om een objectgeoriënteerde BTW-calculator te schrijven. Zo zette ik mijn vraagtekens bij het feit dat ik zijn oorspronkelijke model één op één overnam. Die keuze bracht met ertoe een aparte `VatCalculator`-class te definiëren. En hoewel die objectgeoriënteerd was opgezet, viel deze makkelijk om te schrijven naar een functionele variant. De vraag wierp zich op: hoe objectgeoriënteerd is die oplossing? Is de vergelijking daarmee wel eerlijk? Hoe zou een \"echt\" objectgeoriënteerde oplossing eruit zien?"
---

[Een tijd terug] (LINK) schreef ik over het demoproject waarmee [Enrico Buonanno](https://twitter.com/la_yumba) de lezer van [*Functional Programming in C# (Second Edition)*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition) bekend maakt met het concept van functioneel programmeren in C#. 


Het demoproject berekent voor verschillende landen het BTW-tarief van een bestelling. Het doet dat op basis van de nettoprijs en de in die landen geldende regels. (De Engelse term voor BTW is VAT, *value added tax*. In het vervolg van deze blog zal ik die term hanteren.)


In de herhaling is hier Buonanno's oplossing: 


{{< gist dotkarl fffbe14591ef1852bf7c8ba6dccd7b2e "FunctionalVatCalculator.cs">}}


Buonanno daagde zijn lezers uit zelf een oplossing te bedenken in objectgeoriënteerde stijl. Ik schreef een op het [*strategy*-patroon](https://en.wikipedia.org/wiki/Strategy_pattern) gebaseerde `VatCalculator` en vergeleek die - op esthetiek en performance - met de oorspronkelijke. Nu kun je twisten over welke oplossing de mooiste is, maar Buonanno's functionele oplossing won het qua snelheid en geheugengebruik overtuigend van mijn eigen versie.


## Versie 2.0


Ik plaatste echter wat kanttekeningen bij mijn aanpak van het probleem. Zo zette ik mijn vraagtekens bij het feit dat ik Buonanno's oorspronkelijke model één op één overnam. Die keuze bracht met ertoe een aparte `VatCalculator`-class te definiëren. En hoewel die objectgeoriënteerd was opgezet, viel deze makkelijk om te schrijven naar een functionele variant. De vraag wierp zich op: hoe objectgeoriënteerd is die oplossing? Is de vergelijking daarmee wel eerlijk?


Hoe zou een "echt" objectgeoriënteerde oplossing eruit zien? Die zou het berekenen van de BTW de verantwoordelijkheid maken van één van de objecten in het domeinmodel. Buonanno's oplossing berekent de VAT op basis van een `Order` en een `Address`. Het ligt voor de hand om de verantwoordelijkheid bij één van die twee classes te leggen. Omdat een adres intuïtief weinig met VAT te maken heeft, wat mij betreft, heb ik de logica in de `Order`-class stopt:


{{< gist dotkarl fffbe14591ef1852bf7c8ba6dccd7b2e "ectOrientedVatCalculatorV2.cs">}}


De logica is identiek aan mijn eerdere oplossing, met als enige verschil dat de `GermanRate` nu een `Product` accepteert als parameter, in plaats van een `Order`. De reden waarom laat zich raden: `Order` is onderdeel van het oude model, waar deze class nu juist de vervanger van is. Bovendien heeft de class alleen het `Product` nodig om de VAT te kunnen berekenen.


Op esthetisch vlak heb ik weinig toe te voegen ten opzichte van [wat ik de vorige keer daarover heb gezegd] (LINK). Maar ik ben wel benieuwd: is deze opzet een vooruitgang ten opzichte van de vorige? Welke oplossing heeft je voorkeur, de functionele of de (nieuwe) objectgeoriënteerde? En vooral: waarom? 


## Benchmarks


Dan: de performance. Ik heb opnieuw wat [benchmarks](https://benchmarkdotnet.org/articles/overview.html) gedraaid om de oplossingen met elkaar te kunnen vergelijken. Allereerst de snelheid:


|                       Method | Gemiddelde | Foutmarge | Standaardafwijking | 
|----------------------------- |-----------:|----------:|-------------------:|
|       CalculateVatFunctional |   222.9 ns |   2.57 ns |            2.28 ns |
| CalculateVatObjectOrientedV2 |   281.6 ns |   2.49 ns |            2.08 ns |
| CalculateVatObjectOrientedV1 |   299.2 ns |   8.07 ns |           23.81 ns |


De nieuwe objectgeoriënteerde versie blijkt iets sneller dan de oorspronkelijke, al is het verschil marginaal. Bedenk: het gaat hier om nanoseconden, dus in de praktijk is er geen verschil merkbaar. Wat wel opvalt, is dat de foutmarge en de standaardafwijking een stuk groter zijn bij de oorspronkelijke objectgeoriënteerde dan bij de andere twee. Ik kreeg een waarschuwing dat deze method een [multimodale distibutie](https://en.wikipedia.org/wiki/Multimodal_distribution) had. Ik acht het niet onwaarschijnlijk dat het daar iets mee te maken heeft.


Feit blijft echter: de objectgeoriënteerde oplossingen blijven beide achter bij de functionele. Ook hier geldt weer: het verschil is niet dusdanig groot dat het in de praktijk gevolgen zal hebben, maar het verschil is er wel degelijk en het is significant. Toch weer een puntje voor het functionele paradigma.


En ook qua geheugengebruik wint de functionele oplossing opnieuw:


|                       Method |  Gen 0 | Gen 1 | Gen 2 | Allocated |
|----------------------------- |-------:|------:|------:|----------:|
|       CalculateVatFunctional |      - |     - |     - |         - |
| CalculateVatObjectOrientedV2 | 0.0820 |     - |     - |     344 B |
| CalculateVatObjectOrientedV1 | 0.0820 |     - |     - |     344 B |


Beide objectgeoriënteerde oplossingen hebben hetzelfde geheugengebruik, en dat is ook te verwachten, want het is dezelfde code.


## En nu?


Oké, en nu? Dat weet ik eerlijk gezegd ook niet precies. Misschien is het antwoord wel: helemaal niets. Mag een man ook gewoon 'n keertje een bescheiden vrijdagochtendexperimentje uitvoeren, en dat was dat? 


Nou ja. Ja. Van mij wel, in elk geval. O, en voor de geïnteresseerde collega-experimentator: [de code is op GitHub te vinden](https://github.com/dotkarl/RefactorExercises).
