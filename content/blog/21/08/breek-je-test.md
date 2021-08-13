---
title: "Breek Je Test"
author: "Karl van Heijster"
date: 2021-08-13T07:20:45+02:00
draft: false
comments: true
tags: ["boeken", "leermoment", "refactoren", "testen"]
summary: "In Martin Fowlers *Refactoring* vond ik een interessante programmeertip: *breek je test.* Ja, dat lees je goed."
---

In [Martin Fowlers](https://martinfowler.com/) [*Refactoring*](https://martinfowler.com/books/refactoring.html) vond ik een interessante programmeertip: *breek je test.*


Ja, dat lees je goed.


## Wanneer je test hoort te falen


Maar tests horen toch juist te slagen? Ja. Maar ook: nee. 


Tests horen te slagen *in 99,9% van de gevallen*. 99,9% van de tijd geeft een falende test aan dat er iets mis is met je code. 


Dit is ook precies waarom je een goede [testcoverage](https://en.wikipedia.org/wiki/Code_coverage) wil hebben. Je schrijft geen tests omdat je code zo ingewikkeld is dat je anders niet snapt wat hij doet. Je schrijft tests omdat je wil weten wanneer je nieuwe code bestaande functionaliteiten omver werpt.


In 0,1% van de tijd *hoort* je test te falen. Dat is de keer dat je nagaat of hij daadwerkelijk test wat hij zou moeten testen.


Dat een test dat doet, is geen triviaal gegeven. Programmeren is moeilijk, en zeker wanneer je vermoeid bent (bijvoorbeeld omdat je al [uren achtereen](/blog/21/07/stoor-me-niet-ik-zit-in-the-zone) tests aan het schrijven bent... toch?!) wil je het nogal eens over het hoofd zien wanneer een test niet doet wat hij moet doen. In dat geval slaagt de test vanwege een bijwerking van de conditie die je probeert te testen. Of erger: hij slaagt ongeacht die condities!


## De casus


Onlangs kwam ik op moeizame wijze achter de wijsheid van Fowlers tip.


De applicatie waaar mijn team en ik aan werken, bestaat uit een [Angular](https://angular.io/) [front-end](https://en.wikipedia.org/wiki/Front_end_and_back_end), die middels [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) communiceert met een [ASP.NET Web API](https://dotnet.microsoft.com/apps/aspnet/apis). 


In code is zo'n API niet meer dan een aantal [Controller](https://docs.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-5.0#controllerbase-class)-classes met wat methods die corresponderen met [HTTP-verbs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods). Denk aan `GET` voor het ophalen van data en `POST` voor het opslaan ervan.


Een controller zou er zo uit kunnen zien:


```c#
[HttpGet("api/resource")]
public void ActionResult<IEnumerable<Resource>> SearchResource([FromQuery] SearchRequest request)
{
    var resources = _service.Search(request);
    return Ok(resources);
}
```


In het attribuut boven de method, staat het HTTP-verb gespecificeerd, plus (een deel van) de [URL](https://en.wikipedia.org/wiki/URL) waar je naar moet navigeren om de method aan te roepen. De method zelf kent één parameter, die wordt samengesteld uit datgene wat in de [querystring](https://en.wikipedia.org/wiki/Query_string) wordt meegegeven.

Stel dat het `SearchRequest`-object een property `KeyWords` bevat:

```c#
public class SearchRequest
{
    public string KeyWords { get; set; }

    // Other properties...
}
```

In dat geval zou je een RESTful call naar onze API kunnen maken door naar de volgende URL te navigeren: `.../api/resource?keywords=puppies`. (Op de drie puntjes zou de [*base URL*](https://swagger.io/docs/specification/api-host-and-base-path/) komen te staan. Voor deze website is dat bijvoorbeeld `www.karlvanheijster.com`.) Deze URL geeft je, als het goed is, alle resources terug die over puppy's gaan.


## De test


Onze code base kent integratietests die precies dit doen. Ze roepen een bepaalde URL aan, al dan niet met een querystring, om te valideren dat de endpoints de juiste objecten teruggeven.


Naar goede gewoonte slaagden al deze tests. En naar minder goede (?) gewoonte faalde er één toen ik onze testcases in het kader van onderhoudbaarheid refactorde. 


De test in kwestie was onderdeel van een reeks querystringtests. Vóór mijn refactorslag, werden de URLs en querystrings in elke test afzonderlijk uitgecodeerd. Ik schreef een helpermethod die dat werk voor mij afhandelde, zodat ik de URL en querystrings maar op één plek hoefde bij te houden.


Wat bleek nu: die ene test probeerde resources op te halen door de volgende URL aan te roepen:`.../api/resource?keyword=puppies`. Hij is geslaagd als hij iets terugkrijgt. Zie je waar de fout zit? 


In de querystring wordt een `keyword` (enkelvoud) meegegeven, in plaats van `keywords` (meervoud). 


Het gevolg is dat ASP.NET de querystring niet kan serialiseren naar het `SearchRequest`. Wie de test debugt, komt erachter dat `KeyWords` *null* is. Het gevolg daarvan is dat het endpoint alle resources teruggeeft, in plaats van alleen de resources die over puppy's gaan. En het gevolg dáárvan is dat de test altijd slaagt.


En hij is blijven slagen, lang nadat de puppy's een eerdere refactorslag waren gesneuveld. Er waren helemaal geen resources die over puppy's gaan!


## De les


Ik zal de hand in eigen boezem steken, want de kans is groot dat *ik* degene ben die eerder de puppy's uit de test heeft gerefactord. Had ik destijds de test proberen te breken door een keyword in de querystring te zetten waarvan ik wist dat deze geen resultaten op zou leveren, dan was het me opgevallen dat de test niet deed wat hij moest doen.


Maar ik ben niet te streng voor mezelf, want ik heb lange tijd geloofd dat tests 100% van de tijd horen te slagen. Dankzij Martin Fowler weet ik nu beter.
