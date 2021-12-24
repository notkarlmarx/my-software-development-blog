---
title: "Dertig seconden winst in twee commits"
author: "Karl van Heijster"
date: 2021-12-24T12:05:59+01:00
draft: false
comments: true
tags: ["IEnumerable", "intentie van code", "leermoment", "performance", "productieverstoring", "software ontwikkelen"]
summary: "Eén enkele commit was voldoende om de latency van een cruciale call naar onze back-end te verlengen van minder dan één seconde naar twintig tot dertig (!) seconden. Wat was er in hemelsnaam gebeurd?"
---

Eén enkele commit was voldoende om de [latency](https://en.wikipedia.org/wiki/Latency_(engineering)) van een cruciale call naar onze back-end te verlengen van minder dan één seconde naar twintig tot dertig (!) seconden.


{{<figure src="https://i.imgur.com/ji79f6l.gif" alt="Wauw!" width="300">}}


Wat was er in hemelsnaam gebeurd?


## Migratie


Oké, ten eerste was het, eerlijk gezegd, niet alléén die commit. We migreerden onze gebruikers van een door het team onderhouden [Azure Active Directory](https://azure.microsoft.com/nl-nl/services/active-directory/) (AAD) naar die van de organisatie. 


We hadden daar twee redenen voor. Ten eerste zorgde onze applicatiespecifieke AAD voor dubbele administratie. Gebruikers bestonden zowel in de onze als die van de organisatie. Er waren dus twee bronnen van waarheid. Het zorgde voor onduidelijkheid wie er en dienst is en wie niet, en dat is problematisch. 


Ten tweede bezorgde het beheer van gebruikers in onze Productie-omgeving ons veel onderhoudslast. Iedereen was het er over eens dat dat niet de verantwoordelijkheid van het ontwikkelteam zou moeten zijn. 


## Kwijt


De migratie verliep relatief vlekkeloos, in die zin dat we geen enkele gebruiker kwijtraakten.


Dat wil zeggen, we raakten wel enkele gebruikers kwijt, maar dat bleek te zijn omdat onze call naar de [Microsoft Graph API](https://docs.microsoft.com/en-us/graph/use-the-api) alleen de eerste pagina aan gebruikers ophaalde. Dat was bij onze eigen AAD geen probleem, want die was klein genoeg om maar één pagina te hebben. 
 
 
Maar die van de organisatie telde er vijf. En omdat we op maar vijftien gebruikers-ID's tegelijkertijd konden query'en, ging onze code uit van een hack die eerst alle gebruikers ophaalde om daarna pas filtering toe te passen.


Dus ja, bij elke van de hierboven genoemde cruciale call spraken wij vijf keer de Microsoft Graph Api aan. Wat blijkt: dat is dus niet raadzaam voor de performance.


## Caching


We breidden als een gek onze [caching](https://nl.wikipedia.org/wiki/Cache_(tijdelijk_geheugen)) uit en gingen meteen naar Productie. Commit #1. En inderdaad: de latency verminderde aanzienlijk.


Van twintig tot dertig seconden, naar [zeven seconden](https://www.youtube.com/watch?v=wqCpjFMvz-k). [Wauw!](https://i.imgur.com/ji79f6l.gif)


Ik weet niet of je ooit in een applicatie hebt moeten werken waar bijna elke muisklik gepaard gaat met een laadscherm van zeven seconden, maar ik kan je verzekeren dat dat niet prettig werken is. Prettiger dan een laadscherm van twintig tot dertig seconden, natuurlijk, dat is waar. Maar dat is een beetje alsof je zegt dat het prettiger is je hand te verliezen dan je hand en je voet en een been en je oog.


Wat ik bedoel te zeggen is: de situatie was nog steeds onacceptabel.


## De oorzaak


We hebben een uur lang met de debugger door de code gestapt. Alles zag er goed uit, totdat onze [Controller](https://docs.microsoft.com/en-us/aspnet/mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs) het resultaat van de call daadwerkelijk retourneerde. Zeven seconden vertraging.


Wat bleek nu uiteindelijk: ergens in de code werd de informatie uit de Graph API doorgegeven als een [`IEnumerable`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerable?view=net-6.0). Op zich niets geks: onze code zit vol `IEnumerables`. Sterker nog, ik programmeer al jaren vrijwel elke verzameling uit als `IEnumerable`, tenzij het niet anders kan. 


De [interface](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/interfaces) verlangt namelijk het minst van de concrete implementatie. Het stelt de code in staat om [`Arrays`](https://docs.microsoft.com/en-us/dotnet/api/system.array?view=net-6.0), [`Lists`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=net-6.0), [`Collections`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.objectmodel.collection-1?view=net-6.0) zonder problemen met elkaar uit te wisselen. En de [*deferred execution*](https://docs.microsoft.com/en-us/dotnet/standard/linq/deferred-execution-example) die de interace mogelijk maakt, heb ik altijd als één van de grote voordelen ervan ervaren.


## *Deferred execution*


Maar precies dat zorgde hier voor het probleem. *Deferred execution* wil zeggen dat bepaalde code pas wordt uitgevoerd op het moment dat deze nodig is. In dit geval: wanneer de Controller het resultaat van de call retourneerde. 


Onze code haalde eerst alle gebruikers binnen via de Graph API, zoals verwacht. Maar zodra de call zijn eindpunt bereikte, zorgde de *deferred execution* ervoor dat er alsnog een call naar de Graph API gemaakt werd om de informatie van een gebruiker op te halen. In een [*for each*-loop](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/statements/iteration-statements).


Dus: per gebruiker. Per gebruiker, vijf calls naar de Graph API om alle gebruikers op te halen; dan pas filteren aan onze kant. En dat, in het slechtste geval, vijfentwintig keer achter elkaar. [Wauw!](https://i.imgur.com/ji79f6l.gif)


## Lijst


Zelden zorgde zo'n simpele oplossing voor zoveel performancewinst: we voegden op één plek een [`.ToList()`](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.tolist?view=net-6.0) toe. Commit #2. En de latency kromp als sneeuw voor de zon, van zeven seconden, terug naar onder de oorspronkelijke één.


Zelden ben ik zo hard op de neus gedrukt over de impact van mijn programmeerkeuzes op de performance van een applicatie. `IEnumerable` is een prachtige, eenvoudige interface, ik ben er dol op. Maar hij is allesbehalve zaligmakend.


## Alternatief


In dit geval was een `IReadOnlyList` gepaster geweest. Het zou deze de intentie van de code veel beter hebben weergegeven. Het is immers niet de bedoeling dat iemand in de code de lijst van gebruikers nog aan gaat passen. (Ook hier geldt: één bron van waarheid!)


En over de performancewinst van het gebruik van `IReadOnlyList` ten opzichte van `IEnumerable` hoef ik denk ik niet uit te wijden. De les is hard maar waardevol: denk goed na over het type verzameling die je method retourneert. 


Het zou je zomaar zes, zeven seconden kunnen schelen.
