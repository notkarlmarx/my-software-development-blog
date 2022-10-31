---
title: "Het Single-Responsiblity Principe en mijn keukenkastjes"
author: "Karl van Heijster"
date: 2022-10-31T07:51:25+01:00
draft: false
comments: true
tags: ["beroepsdeformatie", "performance", "single-responsibility principe"]
summary: "Ik vind er wat van dat ik twee verschillende keukenkastjes moet openen voor iets wat in feite één handeling is. Ga maar na: wanneer pak je een koffiekopje? Als je koffie gaat zetten. En wanneer pak je een koffiepad? Als je koffie gaat zetten. Het pakken van een koffiekop gaat altijd gepaard met het pakken van een koffiepad. Het is een atomaire handeling."
---

Ik mag graag een kopje koffie zetten voor mijn vrouw.


Het algoritme voor koffiezetten ziet er ongeveer als volgt uit: 


1. doe water in reservoir;

2. druk op AAN-knop; 

3. pak kopje uit keukenkastje; 

4. zet kopje onder koffiezetapparaat;

5. pak koffiepad uit keukenkastje;

6. doe koffiepad in koffiezetapparaat;

7. als koffiezetapparaat gereed is, druk op KOFFIE ZETTEN-knop; anders wacht tot koffiezetapparaat gereed is;

8. neem koffiekopje en serveer.


In code ziet dat er zo ongeveer zo uit:


```cs
var c = new CoffeeMachine();

c.AddWater();

c.Initialize();

var cup = _kitchenCabinet.GetNewCup();
c.AddCup(cup);

var pad = _kitchenCabinet.GetNewPad();
c.AddPad(pad);

while (!c.Initialized)
{
    Task.Sleep(1000);
}

c.MakeCoffee();

while (!c.Ready)
{
    Task.Sleep(1000);
}

var coffee = c.TakeCoffe();
Serve(coffee);
```


Ik wil het vandaag over stap 3. en 5. hebben. 


## Keukenkastje(s)


Stap 3. en 5. zijn in wezen dezelfde handeling - op een abstractieniveau hoger dan beschreven. Ze zouden om kunnen worden geschreven naar *pak* x *uit keukenkastje* waarbij *x* een variabele is die staat voor een object in het keukenkastje.


```cs
var cup = _kitchenCabinet.GetNew<Cup>();
// ...

var pad = _kitchenCabinet.GetNew<Pad>();
// ...
```


Maar in de praktijk - een abstractieniveau lager dan beschreven, als het ware - zijn stap 3. en 5. best verschillend. In stap 3. worden kopjes gehaald uit het linkerkeukenkastje, en in stap 5. worden koffiepads gehaald uit het rechterkeukenkastje.


```cs
var cup = _kitchenCabinets.Left.GetNew<Cup>();
// ...

var pad = _kitchenCabinets.Richt.GetNew<Pad>();
// ...
```


Ik vind daar wat van.


## Eén handeling


Ik vind er wat van dat ik twee verschillende keukenkastjes moet openen voor iets wat in feite één handeling is. 


Ga maar na: wanneer pak je een koffiekopje? Als je koffie gaat zetten. En wanneer pak je een koffiepad? Als je koffie gaat zetten.


Je pakt nooit een koffiekopje als je niet ook een koffiepad nodig hebt. (Omgekeerd komt overigens wel voor, als je je tweede kop koffie drinkt. Maar het gaat me nu even om de eerste kop.) Het pakken van een koffiekop gaat altijd gepaard met het pakken van een koffiepad. Het is een atomaire handeling: als de ene niet doorgaat, vervalt de andere. Je moet altijd twee deeltaken doen, of geen.


## Bij elkaar


Ik vind dat daar uit volgt dat je de koffiekopjes en de koffiepads dicht bij elkaar zou moeten zetten. Dan kun je ze in één keer pakken.


Je zou stap 3. en 5. in het algoritme tot één terug kunnen brengen. Of: je zou deze taak kunnen paralelliseren. Je hebt immers twee handen, dat zijn genoeg *resources* om een optimalisatieslag door te voeren middels de invoer van wat multitasking.  


```cs
var supplies = _kitchenCabinet.GetCoffeeSupplies();
c.AddCup(supplies.Cup);
c.AddPad(supplies.Pad);
```


Maar zelfs al zou je dat niet doen, dan nog zou je wat performancewinst, bij wijze van spreken, kunnen behalen door beide stappen direct na elkaar uit te voeren.


## Single-Responsibility


De keukenkastjes schenden het Single-Responsibility Principe. De enkele verantwoordelijkheid om de benodigde objecten voor het koffiezetapparaat op te halen, is gedistribueerd over delen van het systeem.


Een opmerkelijke vondst, overigens: in de praktijk zie je het vaker andersom, teveel verantwoordelijkheden in één deel van het systeem. (Hoewel, is het niet vreemd dat je de data-access-, logica en API-laag raakt als je een nieuw endpoint toevoegt?)


Een betere oplossing, een sterker ontwerp zou dus zijn om de koffiekopjes en de koffiepads bij elkaar te zetten.


## Politiek


Ik heb dit de keukenkastjesarchitectuurraad, in de vorm van mijn vrouw, voorgelegd, en het antwoord van de raad was unaniem als volgt: "Karl lieverd, ga effe ergens anders azijnpissen."


Soms is keukenkastjesefficiëntieoptimalisatie net als softwareontwikkelen: meer politiek dan inhoud. Ik zou daar over kunnen azijnpissen, maar zo iemand ben ik niet.
