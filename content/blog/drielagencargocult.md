---
title: "Drielagencargocult"
author: "Karl van Heijster"
date: 2024-11-15T09:55:24+01:00
draft: true
comments: true
tags: ["aannames", "intentie van code", "software ontwikkelen"]
summary: "Goede abstracties worden niet *bedacht*. Goede abstracties worden *ontdekt*. Ze vinden pas het levenslicht als reactie op een concrete vraag van de codebase. Softwareontwikkeling is in wezen een empirische aangelegenheid."
---

Het klassieke model om software te structureren is door een applicatie onder te verdelen in een *user interface*-, logica- en datalaag.[^1] Dat levert applicaties op waarbij elke handeling doorgaans door ten minste drie classes wordt afgehandeld: een `Controller`, een `Service` en een `Repository`. -- En inderdaad, diezelfde onderverdeling vond zijn weg naar een klein projectje dat mijn team onlangs oppakte. 


Het doel van dat project was een flinterdunne applicatie te ontwikkelen die diende als lijm tussen ons eigen systeem en de systemen van enkele externe partijen. Deze proxy deed in wezen niets anders dan HTTP-requests uit onze applicatie interpreteren, en op basis daarvan informatie ophalen uit de juiste externe web-API.


De proxy had een `Controller` en enkele `Services` -- één voor elk extern systeem. Tot zover prima -- en toen kwam de derde abstractie om de hoek zetten: een `ExternalApiService`. Dat was een abstractie om de [`HttpClient`](https://learn.microsoft.com/en-us/dotnet/api/system.net.http.httpclient?view=net-8.0 "'HttpClient Class', Microsoft documentatie") uit de [`System.Net.Http`-namespace](https://learn.microsoft.com/en-us/dotnet/api/system.net.http?view=net-8.0 "'System.Net.Http Namespace', Microsoft documentatie").


## Twee delen


Om precies was het een abstractie om *twee* `HttpClients` -- één met automatische *redirects* en één zonder. Want het ene externe systeem gaf ons alle informatie die we nodig hadden in de header van een HTTP-response die de `HttpClient` zonder verdere configuratie ongemerkt zou hebben ingeslikt, en het andere niet. Het gevolg was dat de methods op de `ExternalApiService` die onder water gebruik maakten *redirects* louter en alleen door de ene service werden gebruikt. En de methods die onder water gebruik maakten van de ongeconfigureerde `HttpClient` werden gebruikt door de andere service. 


De abstractie viel uiteen in twee welonderscheiden delen, die afhankelijk waren van een implementatiedetail. Om te weten welke method in de `ExternalApiService` je aan moest roepen, moest je weet hebben van welke `HttpClient` er onder water gebruikt werd. Dat druist tegen het hele idee van abstractie in. De abstractie *verborg* juist de informatie die een gebruiker nodig had om het juiste resultaat te bereiken.


Erger nog: de abstractie *abstraheerde niet*. De input parameters waren precies dezelfde als die op `HttpClient` en de transformatie van het resultaat ervan was tegelijkertijd specifiek toegesneden op de aanroepende partij, en triviaal genoeg om door die partij zelf af te kunnen handelen.


## Aanname


Waar ging het mis? -- De abstractie werd bedacht *voordat* de code werd geschreven. Hij berustte op een aanname -- de aanname dat er überhaupt een derde abstractie *moest* zijn. De `ExternalApiService` was het resultaat van een [cargocult](https://en.wikipedia.org/wiki/Cargo_cult "'Cargo cult', Wikipedia") die ten onrechte meent dat elke applicatie drie lagen moet hebben.


Het hele idee van de proxy was om HTTP requests te maken naar externe systemen. `HttpClient` biedt al alles wat ervoor nodig is om dat voor elkaar te krijgen. De noodzaak voor een abstractielaag daaromheen ontbrak -- dat blijkt ook uit het feit dat de code van de abstractie weinig interessants te berde bracht.


Goede abstracties worden niet *bedacht*. Goede abstracties worden *ontdekt*. (Zie ook [deze blog](/blog/23/12/codefluisteren/ "'Codefluisteren'").) Ze vinden pas het levenslicht als reactie op een concrete vraag van de codebase. Softwareontwikkeling is in wezen een empirische aangelegenheid.


[^1]: Maar voor een kritische benadering van dat idee, dat voortkomt uit een inmiddels verouderde drang naar kennissilo's, zie [dit praatje](https://www.youtube.com/watch?v=WPCrGYjrJ1Y "'The Most Dangerous Phrase • Daniel Terhorst-North • GOTO 2023', YouTube") van [Daniel Terhorst-North](https://dannorth.net/).
