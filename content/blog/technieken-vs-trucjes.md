---
title: "Technieken vs trucjes"
author: "Karl van Heijster"
date: 2024-03-15T09:36:27+01:00
draft: true
comments: true
tags: ["domain-driven design", "functioneel programmeren", "luie programmeur", "refactoren", "software ontwikkelen", "testen", "verantwoordelijkheid"]
summary: "Een goede programmeur is een luie programmeur -- dat is een bekende wijsheid in softwareontwikkelland. Want: een luie programmeur automatiseert oninteressante, repetitieve taken, en creëert op die manier de ruimte om zich bezig te houden met interessante, afwisselende taken. -- Althans, dat is één opvatting van wat het betekent om een luie programmeur te zijn. Maar er zijn nog veel meer manieren om lui te zijn. Vandaag wil ik het hebben over zo'n andere manier. Vandaag wil ik het hebben over de wens, behoefte of neiging om een techniek te reduceren tot een trucje."
---

Een goede programmeur is een [luie programmeur](/tags/luie-programmeur/ "Blogs met de tag 'luie programmeur'") -- dat is een bekende wijsheid in softwareontwikkelland. Want: een luie programmeur automatiseert oninteressante, repetitieve taken, en creëert op die manier de ruimte om zich bezig te houden met interessante, afwisselende taken.


Althans, dat is één opvatting van wat het betekent om een luie programmeur te zijn. Maar er zijn nog veel meer manieren om lui te zijn. (Zie ook [deze blog](/blog/23/05/waar-doe-je-het-voor/ "'Waar doe je het voor?'").) Vandaag wil ik het hebben over zo'n andere manier. Vandaag wil ik het hebben over de wens, behoefte of neiging om een techniek te reduceren tot een trucje.


Wat ik daarmee bedoel? Laat ik drie voorbeelden schetsen, hopelijk wordt dan duidelijk wat ik bedoel.


## "Domain"-Driven "Design"


Er was een tijd dat de back-end van onze applicatie bestond uit [drie horizontale lagen](https://martinfowler.com/bliki/PresentationDomainDataLayering.html "'Presentation Domain Data Layering', Martin Fowler"): een presentatielaag, een domeinlaag, en een datalaag.[^1] De eerste was de API voor onze front-end, in de tweede zit alle logica verstopt, en in de derde spreken we de database aan -- dat is het idee.


Concreet betekende dat: in de presentatielaag vonden we Controllers, in de domeinlaag Services en in de datalaag Repositories. We hadden zulke classes voor elk object in ons domeinmodel: een `ItemsController`, `ItemsService`, `ItemsRepository`; een `AssessmentTestsController`, `AssessmentTestsService`, `AssessmentTestsRepository`, etc..


Nu ik erop terugkijk, klinkt die opzet beschamend simplistisch. Maar op het moment dat we aan het ontwikkelen waren, dachten we oprecht dat we [Domain-Driven Design](/tags/domain-driven-design/ "Blogs met de tag 'domain-driven design'") (DDD) aan het doen waren. De code gebruikte immers dezelfde taal als onze stakeholder: *items*, *assessment tests* -- en we gebruikten de patronen die [Eric Evans](https://www.domainlanguage.com/) in [zijn boek](https://www.oreilly.com/library/view/domain-driven-design-tackling/0321125215/ "'Domain-Driven Design: Tackling Complexity in the Heart of Software', Eric Evans") noemde: *services*, *repositories*.


Natuurlijk hadden we geen van allen dat boek daadwerkelijk gelezen. We hadden de woorden gehoord die hij gebruikte, en we namen die woorden over zonder echt te snappen wat 
ze betekenden. We hadden Evans' rijke inzichten platgeslagen tot een simpel trucje: *elk domeinobject moet zijn eigen* service *en zijn eigen* repository *hebben*.


Natuurlijk leverde dat problemen op. Want de objecten in ons domeinmodel hingen met elkaar samen: *items* zijn onderdeel van een *assessment test*. Dat betekende dat de `AssessmentTestsService` ook een afhankelijkheid naar de `ItemsRepository` moest hebben. Maar toen we die lijn van redeneren doortrokken, kwamen we uit op een punt waarop bijna elke *service* een afhankelijkheid had op bijna elke *repository*.


In plaats van de oorzaak van onze modelleerproblemen te doorgronden, probeerden we de oplossing te zoeken in de introductie van een nieuw trucje: *een* service *mag alleen een afhankelijkheid hebben naar de* repository *van zijn "eigen" object, en voor elk ander object moesten ze maar bij de daarmee corresponderende* service *zijn.* Dus de `AssessmentTestsService` had een afhankelijkheid naar de `AssessmentTestsRepository` en naar de `ItemsService` (en naar de *zus*, en naar de *zo*...) -- en we waren heel tevreden met onszelf.


Maar het probleem hadden we niet opgelost. Want een goed systeem ontwerp je niet door een reeks trucjes toe te passen. Een goed systeem ontwerp je door *na te denken* -- niet één keer, helemaal aan het begin van het project, maar continu. Dat is een les die we op de harde manier hebben geleerd.


## Matroesjka


Een ander voorbeeld. Onlangs refactorde ik een deel van onze codebase -- een betrekkelijk ondoorgrondelijk deel. De code was geschreven zonder gebruik te maken van [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) en (daarom) ontzettend moeilijk om te testen. (Ik schreef [hier](/blog/23/04/tijdreis/ "'Tijdreis'") al eens eerder over dit stuk code.) 


Maar refactoren zonder vangnet van tests is onverantwoord, en daarom was ik een goede dag bezig met het opzetten van [karakterisatietests](https://en.wikipedia.org/wiki/Characterization_test "'Characterization test', Wikipedia") waarin ik vastlegde wat het huidige gedrag van de code was. Om ze werkend te krijgen moest ik [zipbestanden](https://en.wikipedia.org/wiki/ZIP_(file_format) "'ZIP (file format)', Wikipedia") (!) vol [XML](https://nl.wikipedia.org/wiki/Extensible_Markup_Language "'Extensible Markup Language', Wikipedia") als inputparameters mee moest geven -- het was een feest.


Hoe dan ook, op een gegeven moment had ik de code redelijk onder controle. Maar er zat me iets dwars aan de resultaten die ik terugkreeg van de tests. In de code kwam ik veelal de volgende soort constructies tegen:


```cs
public ServiceResult<SomeObject> DoSomething(SomeObject o)
{
    try
    {
        // Update SomeObject o...

        return ServiceResult.Success(o);
    }
    catch(Exception ex)
    {
        o.SetError(ex.Message);
        return ServiceResult.Error(o, ex.Message);
    }
}
```


Twee dingen zaten me niet lekker. De eerste is dat het object dat als input-parameter mee wordt gegeven aan deze method, in de method zelf wordt aangepast. Sinds ik me meer in het [functionele programmeerparadigma](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'") ben gaan verdiepen, maak ik liever gebruik van [*immutable*](/tags/immutability/ "Blogs met de tag 'immutability'") datastructuren. Dat zorgt ervoor dat ik nooit verrast wordt over het feit dat de *state* van een object zonder dat ik het wist in een of andere method is aangepast -- zoals hier gebeurt.


Maar wat ik nog veel verwarrender vond, is het feit dat er in het geval van een *exception* zowel een foutmelding op `SomeObject` zelf werd gezet, als op het `ServiceResult`-object dat als een wrapper om `SomeObject` heen werd gezet. Wat was het idee daar achter?


Het antwoord is: er zat geen idee achter. Wat erachter zat, was een trucje: *wrap het resultaat van de aanroep op een* service *altijd in een `ServiceResult`.*


Maar wat de schrijver van deze code niet door leek te hebben gehad, was dat `SomeObject` *zelf* al als een soort *result*-object fungeerde. Het object zelf gaf namelijk al aan of er fouten waren opgetreden bij het updaten van diens *state*. Dit was één van de dingen die de code zo nodeloos ondoorgrondelijk maakte: *result*-objecten die als matroesjkapoppetjes in *result*-objecten worden gestopt.


En het ergste was: deze toegevoegde complexiteit had geen enkele toegevoegde waarde. Want toen ik de aanroepende code van dit soort functies bekeek, bleek er geen gebruik te worden gemaakt van de informatie in het `ServiceResult`. De aanroepende code dook meteen op `SomeObject` en haalde daar zijn foutinformatie uit. Het trucje was blind toegepast.


Dat was, naar omstandigheden, goed nieuws. Want het betekende dat ik `ServiceResult` weg kon halen zonder al te veel code te hoeven herschrijven. Maar het zou natuurlijk beter zijn geweest als het `ServiceResult` überhaupt nooit op deze plek was geïntroduceerd. 


## Testscope


Een laatste voorbeeld. Onlangs presenteerde ik op [DomCode](https://www.meetup.com/domcode/) over [tests als vorm van documentatie](/talks/altijd-up-to-date-documentatie-met-maximaal-descriptieve-tests/ "'Altijd up to date documentatie met maximaal descriptieve tests'"). Eén van de onderwerpen die ik in dat praatje behandelde, was de vraag naar de juiste testscope.


Eén mogelijke testscope is: test elke publieke method van elke class in isolatie. Maar dat heeft tot gevolg dat je je tests koppelt aan de implementatiedetails van je code. Elke codewijziging zal met falende tests gepaard gaan. Bovendien kunnen dit soort tests niet als documentatie dienen, omdat ze op een te laag abstractieniveau zijn geschreven. Ze zijn alleen begrijpelijk voor mensen die de werking van de code al snappen. Maak niet een testclass aan voor elke class in je codebase -- dat is een trucje!


Een andere mogelijkheid is: test het systeem als geheel. Maar dat heeft weer zijn eigen set nadelen. Je tests zullen er langzaam van worden, zo langzaam dat je ze niet als feedbackmechanisme kan gebruiken tijdens het ontwikkelen. En waarschijnlijk zullen ze instabiel worden, omdat het aantal variabelen enorm toeneemt met een grotere testscope. 


De juiste scope zit ergens tussen die twee extremen in. Maar waar precies, dat is onmogelijk op voorhand te zeggen. Dat is afhankelijk van de codebase en het domein. Het bepalen van de juiste testscope is een balanceeract, en bepaald geen makkelijke. De enige manier om deze te kunnen bepalen, is door op je tests te blijven itereren.


Na afloop kwam één van de toehoorders naar me toe met wat vragen over dit onderwerp. Ik probeerde ze naar eer en geweten te beantwoorden, maar ik moest hem bekennen dat ik niet een definitieve oplossing had voor zijn probleem. Teleurgesteld concludeerde hij: "Nu ben ik nog steeds geen stap verder."


Pas later besefte ik waar de bron van zijn teleurstelling in zat. -- Hij was op zoek naar een trucje. Hij was op zoek naar een eenvoudige regel die hij altijd, zonder na te hoeven denken, kon toepassen en die hem fantastische tests op zou leveren. Maar ik had geen trucje voor hem in de aanbieding. Ik had alleen maar richtlijnen die hem, als hij ze zorgvuldig toepaste, dichter bij een ideaal konden brengen.


## Les


*Er bestaan geen trucjes in softwareontwikkeling.* Wat wel bestaat, is bepaalde technieken die ons kunnen helpen in ons proces. DDD, *result*-objecten en testabstractie zijn daar voorbeelden van. Het zijn gereedschappen die we kunnen gebruiken om kwalitatief hoogwaardige software op te leveren.


Het verschil tussen een trucje en een techniek, is dat de eerste zonder nadenken kan worden toegepast, daar waar de tweede om ons oordeelsvermogen vraagt. Technieken helpen (!) ons bij het doorgronden van een probleem of bij het formuleren van een oplossing. Maar wij zijn nog steeds *zelf* verantwoordelijk voor dat wat we met hulp van die technieken bewerkstelligen.


Wie software probeert te reduceren tot de toepassing van een reeks trucjes, zal steevast teleurgesteld raken. Want de werkelijkheid van softwareontwikkeling is te weerbarstig om zich te laten reduceren tot trucjes.


En bovendien, een probleem écht doorgronden en oplossen is toch veel leuker dan het blind toepassen van een trucje?
  

[^1]: Op dit moment bevinden we ons in het proces de applicatie om te vormen naar een [*vertical slice architecture*](https://www.jimmybogard.com/vertical-slice-architecture/ "'Vertical Slice Architecture', Jimmy Bogard").