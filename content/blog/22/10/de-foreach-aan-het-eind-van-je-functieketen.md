---
title: "De ForEach aan het eind van je functieketen"
author: "Karl van Heijster"
date: 2022-10-21T07:08:15+02:00
draft: false
comments: true
tags: ["functioneel programmeren", "functiepuurheid", "single-responsibility principe"]
summary: "Het idee dat een functie altijd een waarde retourneert, is erg krachtig. Zo zorgt het ervoor dat je eenvoudige tests voor je functies kunt schrijven. Helaas is de werkelijkheid weerbarstig, en is het retourneren van een waarde niet altijd voldoende. Soms moet code neveneffecten bewerkstelligen. Denk bijvoorbeeld aan het wegschrijven van bepaalde data naar een tekst- of zipbestand. Het resultaat van zulke code kan niet in een teruggegeven waarde worden gevangen."
---

Het zal voor sommigen misschien als een verrassing komen, maar binnen de wereld van het functioneel programmeren zijn ze dol op functies. [Wat zijn functies](/blog/22/07/wat-zijn-eerlijke-functies/), vraag je? Je zou functies kunnen zien als vertaaltabellen van de ene waarde naar de andere: je stopt er *a* en en krijgt er *b* voor terug. 


Dit zie je bijvoorbeeld ook terug in de signatuur van de diverse [`Funcs`](https://learn.microsoft.com/en-us/dotnet/api/system.func-1?view=net-7.0) in [C#](https://learn.microsoft.com/en-us/dotnet/csharp/): `Func<TResult>`, `Func<T, TResult>`, `Func<T1, T2, TResult>` etc. In het eerste geval ontvangt de functie geen parameters, in het tweede geval één en en het derde geval twee. Elke `Func` geeft een waarde terug.


## Kracht en beperking


Het idee dat een functie altijd een waarde retourneert, is erg krachtig. Zo zorgt het ervoor dat je eenvoudige tests voor je functies kunt schrijven. Anders dan bij sommige objectgeoriënteerde code, hoef je na de aanroep van een bepaalde method niet in de data van een object te lopen wroeten om te zien of de operatie geslaagd is. Het resultaat van een een functie is altijd glashelder: dat wat de functie retourneert.


Helaas is de werkelijkheid weerbarstig, en is het retourneren van een waarde niet altijd voldoende. Soms moet code neveneffecten bewerkstelligen. Denk bijvoorbeeld aan het wegschrijven van bepaalde data naar een tekst- of zipbestand. Het resultaat van zulke code kan niet in een teruggegeven waarde worden gevangen.


(Natuurlijk zou je om deze beperking heen kunnen proberen te werken, bijvoorbeeld door `true` terug te geven als de operatie geslaagd is. Maar de werkelijke vraag is niet: *geeft de functie `true` of `false` terug?* - het is: *is mijn data correct weggeschreven naar een tekst- of zipbestand?* Een goede test van deze functionaliteit moet voorbij de teruggegeven waarde kijken.)


## Puur en onpuur


Een functie die een waarde retourneert op basis van zijn inputvariabelen *en niks anders*, wordt een pure functie genoemd. Elke functie die gebruik maakt van anderssoortige variabelen of die een neveneffect bewerkstelligt, is onpuur. Om die functie te doorgronden, moet je als het ware buiten de code van de functie zelf treden.


Voor het uitvoeren van onpure operaties bestaat een aparte method binnen het functionele paradigma.[^1] Met `ForEach` voer je een actie uit op de binnenste waarden van een bepaalde container. Je zou de method kunnen zien als het [onpure](https://thesharperdev.com/pure-v-impure-functions/) broertje van de `Map`-functie waar ik [eerder](/blog/22/10/wat-is-een-functor/) over schreef.


## Scheiding


Het is niet per ongeluk dat er twee verschillende methods bestaan om voor pure en onpure operaties. Het is een *best practice* om dit soort zaken zoveel mogelijk te scheiden. Pure logica is namelijk eenvoudiger om over te redeneren. Hoe meer je zulke logica "vervuilt" met neveneffecten, hoe moeilijker doorgrondbaar deze wordt. 


Schrijf je code dus liever niet zo:


```cs
var opt = Some("John");
opt.ForEach(name => 
    Console.WriteLine($"Hello, {name}!"));
```


In de lambda-functie die de `ForEach` als parameter neemt, worden twee acties uitgevoerd. De binnenste waarde van de [Option](/blog/22/08/spelen-met-options/) wordt zowel getransformeerd (van `"John"` naar `"Hello, John"`) als weggeschreven naar de console. De eerste is een pure functie, de tweede een onpure.


Het is beter deze code zo te schrijven:


```cs
var opt = Some("John");
opt.Map(name => $"Hello, {name}")
   .ForEach(Console.WriteLine);
```


## Het eind


Deze manier van je code opzetten heeft interessante consequenties. 


Het zorgt er ten eerste voor dat de `ForEach` altijd aan het eind van een (potentieel heel lange) keten van pure functies komt. Na de `ForEach` is het over met de functionele pret: er wordt geen waarde meer teruggegeven die kan worden gemanipuleerd. Het neveneffect is het enige wat overblijft.


Code in de `ForEach` focust zich nog maar op één ding: het neveneffect bewerkstelligen. Het is een zo klein mogelijk stukje functionaliteit, scherp gescheiden van alle puur functionele code.


We hebben de pure en onpure code in de voorbeelden hierboven op methodniveau gescheiden - maar waarom daar stoppen? Code die neveneffecten produceert moet zijn eigen, geïsoleerde plek in de codebase hebben. Slechts één module mag zich met neveneffecten bezig houden (naar een database schrijven, zip-bestanden maken), de rest is zuiver functioneel.


Zo helpt een scherpe scheiding van pure en onpure functies - een variant op het [Single-Responsibility Principe](/tags/single-responsibility-principe/) - bij het schrijven van optimaal testbare code.


[^1]: Merk op dat ik hier van een *method* spreek, en niet van een *functie*!
