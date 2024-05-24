---
title: "Functioneel denken: een praktijkvoorbeeld"
author: "Karl van Heijster"
date: 2024-03-22T07:51:53+01:00
draft: true
comments: true
tags: ["declaratief programmeren", "eenvoud", "functioneel programmeren", "imperatief programmeren", "refactoren", "software ontwikkelen"]
summary: "Onlangs hielp ik een collega een moeilijk volgbare berg code te reduceren tot enkele eenvoudig leesbare regels. Door onze oorspronkelijke, imperatieve redeneertrant van ons af te werpen, en deze te vervangen door een declaratieve stijl, reduceerden we het netelige origineel tot een elegante functionele oplossing. -- Het was een schoolvoorbeeld van de kracht van functioneel denken."
---

Onlangs hielp ik een collega een moeilijk volgbare berg code te reduceren tot enkele eenvoudig leesbare regels. Door onze oorspronkelijke, [imperatieve](https://en.wikipedia.org/wiki/Imperative_programming "'Imperative programming', Wikipedia") redeneertrant van ons af te werpen, en deze te vervangen door een [declaratieve](https://en.wikipedia.org/wiki/Declarative_programming "'Declarative programming', Wikipedia") stijl, reduceerden we het netelige origineel tot een elegante functionele oplossing. -- Het was een schoolvoorbeeld van de kracht van functioneel denken.


## Zoeken


Eerst: wat context. Sinds kort maakt onze codebase gebruik van [Azure AI Search](https://azure.microsoft.com/en-us/products/ai-services/ai-search/ "'Azure AI Search', Microsoft"). In plaats van rechtstreeks onze database te doorzoeken, plaatsen we voor elk object in ons domeinmodel de relevante informatie in een zoekindex een doorzoeken deze. 


Eén van de voordelen die ons dat oplevert, is een flexibiliteit die we nu nog regelmatig missen. Ons domeinmodel bestaat namelijk uit een boel objecten die principieel los van elkaar staan maar wel een associatie met elkaar hebben. Gebruikers willen een object, *a*, kunnen vinden door te zoeken op de kenmerken van het met *a* geassocieerde object *b*. AI Search stelt ons daartoe in staat zonder die objecten met elkaar te verweven in onze eigen code.


## Tool


Dat klinkt mooi, maar om ons doel te bereiken moeten we *a* en *b* natuurlijk wel aan elkaar gekoppeld in de zoekindex zien te plaatsen. Een collega van me had daarom een tooltje gecodeerd dat onze database leegtrok en op basis daarvan de juiste informatie in de zoekindex plaatste. En inderdaad: als je de tool startte, dan zag je voor je ogen de index bijgewerkt worden.


De flow van de tool zat ongeveer als volgt in elkaar. Eerst werd er een lijst opgehaald met de ID's van met elkaar gecorreleerde objecten. Daarna werd een lijst van *a* opgehaald en omgezet naar de juiste representatie voor de zoekindex. Vervolgens werd een lijst van *b* opgehaald en omgezet naar de juiste representatie. En die werd daarna samengevoegd aan de representatie van *a*.


Dat wil zeggen, als er een associatie tussen beide bestond. Want het kon ook voorkomen dat er geen enkele *b* met *a* correspondeerde. Dus om die associatie goed en wel te kunnen leggen, werd er voor elke geconverteerde *a* gekeken of er een *b* mee correspondeerde, en zo ja, dan werd die geconverteerde *b* aan de nieuwe representatie van *a* toegevoegd.


Daarna werd dit complete plaatje richting de index gestuurd.


## Problemen


-- Althans, als alles goed ging. Want ik vroeg 'm: "Wat als *a* niet gevonden kan worden?" Hij zei: "Dat zou in principe niet voor mogen komen." Dus ik vroeg: "Maar wat als het wel gebeurt?" En hij gaf toe: "Dat weet ik eigenlijk niet precies." En dus keken we samen nog eens naar zijn code.


We constateerden: als *a* niet gevonden kon worden, dan verdween deze -- ongemerkt, eigenlijk -- uit beeld. Nu zou dit in principe niet voor moeten mogen komen, dus we hoefden het proces er niet om af te kappen. Maar we zouden zo'n fout eigenlijk wel moeten loggen. Dus vergeleken we, nadat de index was bijgewerkt, de lijst met ID's met de lijst aan gecreëerde representaties. En als deze afweek, dan logden we de ID's van de objecten die niet konden worden gevonden.


Maar dat was niet het enige probleem. Want wat als er tijdens het omzetten naar de juiste representatie iets misging, en er een [*exception*](https://learn.microsoft.com/en-us/dotnet/standard/exceptions/ "'Handling and throwing exceptions in .NET', Microsoft documentatie") werd opgegooid? "Dan..." mijn collega dacht er een paar seconden over na, "dan stopt 'ie helemaal met waar 'ie mee bezig is."


Opnieuw: dit zou in principe niet voor mogen komen. Maar: wat als het wel zo was? Dan zouden we die fout toch op z'n minst willen loggen. En we zouden willen dat de objecten die geen fout opleverden, alsnog goed zouden worden afgehandeld. Om dat voor elkaar te krijgen, introduceerde mijn collega een `Dictionary<Guid, Exception>`, die hij bijwerkte elke keer als een object een fout opgooide. 


En helemaal aan het eind van de rit, dan moest er gecheckt worden of er inderdaad *exceptions* aan dat ding waren toegevoegd. En de foutmeldingen die daaruit voortkwamen moesten dan worden toegevoegd aan de foutmeldingen voor de objecten die we niet hadden kunnen vinden, zodat we beide konden loggen.


## Complex


Mijn collega is een prima ontwikkelaar. Als hij iets werkend wil krijgen, dan zorgt hij er hoe dan ook voor dat 'ie het werkend krijgt. Maar de code die het opleverde, was naar mijn smaak wel erg complex. Te complex. Nodeloos complex, om eerlijk te zijn. 


Als lezer moest je constant heen en weer pingpongen om te kunnen volgen wat er gebeurde. Eerst werd object *a* geconverteerd naar een nieuwe representatie, maar die representatie was nog niet de uiteindelijke variant, want de representatie van *b* moest daar vervolgens nog aan worden toegevoegd, als deze bestond tenminste; en de foutconditie van niet-aanwezige objecten werd aan het eind geaddresseerd, maar foutcondities bij het omzetten van naar de nieuwe representatie hadden een onmiddellijk effect, zij het dat de afhandeling pas plaatsvond ná die andere foutconditie. 


Het was erg veel -- veel om in je hoofd te kunnen houden, maar ook: heel veel code.


## Declaratief


Waarom was deze code zo complex? Het had verschillende oorzaken, naar mijn idee. Ten eerste -- excuses, ik haal mijn stokpaardje weer even van stal -- had mijn collega de oorspronkelijke code zonder [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) ontwikkeld. Daardoor had hij zichzelf niet in staat gesteld om de code continu eenvoudig te refactoren. En dat had tot gevolg dat hij functionaliteit op functionaliteit had gestapeld, zonder het ontwerp van zijn code aan te passen aan nieuwe inzichten. Zo werd de flow met elke nieuwe toevoeging iets complexer.


Maar de tweede, voor deze blog relevantere, observatie is dat zijn code werd gekenmerkt door een hoogst imperatieve stijl. Die stijl kenmerkt zich doordat een ontwikkelaar nauwgezet uitschrijft *hoe* een bepaald probleem moet worden opgelost. *Doe eerst dit, en doe dit op die manier, en doe daarna dat, en doe dat op deze manier* -- dat is hoe dit soort code leest.


Deze stijl van programmeren geeft de ontwikkelaar veel controle in de manier waarop een probleem wordt opgelost. Maar het geeft de ontwikkelaar ook veel mogelijkheden om suboptimale oplossingsrichtingen uit te programmeren. En dat zal onvermijdelijk gebeuren, als de code niet continu wordt gerefactord.


## Hoe dan?


Wat is het alternatief? Hoe zouden we deze code anders op kunnen zetten? Dat is een vraag waar ik een hele ochtend mijn hoofd over brak. Maar toen ik de oplossing eenmaal gevonden had, werd de code eenvoudig en elegant. Ik vond een oplossing in het [functionele](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'") [programmeerparadigma](/tags/paradigmas// "Blogs met de tag 'paradigma's'"). Maar daarvoor moest ik de manier waarop we het probleem benaderden veranderen.


Ik zette enkele overwegingen op papier:


- De oorspronkelijke implementatie zette eerst *a* om en dan *b* en voegde beide daarna samen. Dat zat me niet lekker. Mijn intuïtie zei me: *a* en *b* horen bij elkaar -- ze leveren samen één resultaat op -- en horen dus samen om te worden gezet. Dus ik moest *a* en *b* (wanneer aanwezig) verenigen in één object.

- Gegeven de lijst met ID's, kon object *a* gevonden worden of niet. Als *a* gevonden werd, dan moest deze samen met *b* (wanneer aanwezig) worden omgezet. Als deze niet gevonden kon worden, dan moest er een foutmelding worden gelogd.

- Gegeven de aanwezigheid van *a*, is er een mogelijkheid dat er een *b* met dit object is geassocieerd. Zo ja, dan moet *b* samen met *a* worden omgezet naar de nieuwe representatie. Zo nee, dan is de conversie van alleen *a* volledig.

- Gegeven de aanwezigheid van *a* en *b*, konden beide succesvol worden geconverteerd naar een nieuwe representatie of niet. Als deze succesvol was, dan zou de conversiefunctie de representatie moeten retourneren. Zo niet, dan zou deze een foutmelding moeten teruggeven om te loggen.


Door deze dingen voor mezelf uit te spellen, werden de contouren van een functionele oplossing zichtbaar. 


## Opdracht


De opdracht was: bundel de relevante informatie in een datastructuur en transformeer deze -- ofwel naar de nieuwe representatie, ofwel naar een foutmelding. Het probleem was voor mijn ogen van gedaante veranderd. Worstelingen rondom de *control flow* van een programma werden vervangen door vragen rondom datatransformatie.


Zoals altijd in de wereld van functioneel programmeren is het probleem gereduceerd tot: een input en een output, en meer niet. Het enige wat mij restte was de uit te schrijven op welke output moest volgen op welke input.


## DTO


De code zag er, toen ik er eenmaal mee klaar was, als volgt uit. Allereerst introduceerde ik een [*data transfer object*](https://en.wikipedia.org/wiki/Data_transfer_object "'Data transfer object', Wikipedia") (DTO) dat alle informatie bezat dat ik nodig had:


```cs
private record AB(A a, Option<B> b);

private class IndexDto()
{
    public Guid Id { get; private set; }
    public Option<AB> AB { get; private set; }
}
```


Record `AB` communiceert: `A` en `B` horen bij elkaar. Bij elke `A` *kan* een `B` horen. Dat er ook geen associatie tussen beide kan zijn, wordt gecommuniceerd door `B` in een `Option<T>` te wrappen. Daarmee zeggen we in feite: we verwachten sowieso een `A`, maar `B` mag ook afwezig zijn. (Ik heb meermaals over Options geschreven, waaronder [hier](/blog/22/07/wat-zijn-eerlijke-functies/ "'Wat zijn eerlijke functies?'"), [hier](/blog/22/08/spelen-met-options/ "'Spelen met Options'") en [hier](/blog/22/12/wat-is-een-monad/ "'Wat is een monad?'").)


Class `IndexDto` communiceert: bij elk `Id` *kan* een `AB` horen, een associatie tussen deze objecten. Maar het zou ook kunnen dat we geen `A` kunnen vinden gegeven een bepaald Id. In dat geval is `AB` afwezig.


## Instantiatie


Om de `IndexDto` te vullen, haal ik eerst alle `A`'s en `B`'s op. 


Daarna vul ik de `IndexDto` met de juiste data. Daarvoor maak ik gebruik van een eenvoudige functie `FirstOrNone`, die hetzelfde werkt als [`FirstOrDefault`](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.firstordefault "'Enumerable.FirstOrDefault Method', Microsoft documentatie") maar die `None` retourneert in plaats van `null`. 


```cs
private async Task Convert(IEnumerable<(Guid a, Guid b)> ids)
{
    var listOfA = await _aRepository.Get(ids.Select(i => i.a));
    var listOfB = await _bRepository.Get(ids.Select(i => i.b));
    var dtos = ids.Select(i => new IndexDto(i, listOfA, listOfB));

    // ...
}

// ...

private class IndexDto(
    (Guid a, Guid b) ids,
    IEnumerable<A> listOfA,
    IEnumerable<B> listOfB)
{
    public Guid Id { get; } = ids.a;
    public Option<AB> AB { get; } = listOfA
        .FirstOrNone(a => a.Id == ids.a)
        .Select(a => new AB(a, listOfB.FirstOrNone(b => b.Id == ids.b)));
}
```


## Transformatie


Nu we een DTO hebben met daarin alle informatie die we nodig hebben, hoeven de data alleen nog maar te transformeren naar het verwachte resultaat. In de succesconditie is dat een, laten we zeggen, `IndexRepresentation`. In de foutconditie is dat een `string` met daarin de foutmelding. De code is relatief eenvoudig:


```cs
private IEnumerable<Either<string, IndexRepresentation>> TryConvertDtos(
    IEnumerable<IndexDto> dtos) =>
    dtos.Select(TryConvertIfPresent);

private Either<string, IndexRepresentation> TryConvertIfPresent(
    IndexDto dto) =>
    dto.AB.Match(ab => TryConvert(ab.A, ab.B),
        () => $"Could not find A with Id '{dto.Id}'");

private Either<string, IndexRepresentation> TryConvert(
    A a, B b) =>
    Try(() => Convert(a, b)).ToEither(ex => ex.Message);

private IndexRepresentation Convert(A a, Option<B> b)
{
    // Transformation logic, could throw Exception
}
```


Wanneer we deze code lezen, dan lezen we eigenlijk de overwegingen die ik hierboven neerpende. Als deze er geen `A` gevonden kon worden, retourneer dan een foutmelding (`"Could not find A with Id..."`). Als deze wel gevonden is, probeer deze dan te converteren. 


Die conversie kan *exceptions* opgooien, daarom wordt deze gewrapt in de `Try`-functie. Deze retourneert een `Try<IndexRepresentation>`, wat je zou kunnen lezen als: `Either<Exception, IndexRepresentation>`. Dat type moeten we omzetten naar het type dat we verwachten, namelijk een `Either<string, IndexRepresentation`>. Dat doen we met de `ToEither`-functie, waarin we het bericht van de *exception* teruggeven.


## Conclusie


De totale oplossing ziet er ongeveer als volgt uit (waarbij ik mezelf wat dichterlijke vrijheid veroorloof in hoe het resultaat wordt afgehandeld):


```cs
private async Task Convert(IEnumerable<(Guid a, Guid b)> ids)
{
    var listOfA = await _aRepository.Get(ids.Select(i => i.a));
    var listOfB = await _bRepository.Get(ids.Select(i => i.b));
    var dtos = ids.Select(i => new IndexDto(i, listOfA, listOfB));
    var result = TryConvert(dtos);
    result.ToList().ForEach(either => either.Match(
        indexRepresentation => _search.Index(indexRepresentation),
        error => _logger.LogError(error)));
}

private IEnumerable<Either<string, IndexRepresentation>> TryConvertDtos(
    IEnumerable<IndexDto> dtos) => dtos.Select(ConvertIfPresent);

private Either<string, IndexRepresentation> TryConvertIfPresent(
    IndexDto dto) =>
    dto.AB.Match(ab => TryConvert(ab.A, ab.B),
        () => $"Could not find A with Id '{dto.Id}'");

private Either<string, IndexRepresentation> TryConvert(
    A a, B b) =>
    Try(() => Convert(a, b)).ToEither(ex => ex.Message);

private IndexRepresentation Convert(A a, Option<B> b)
{
    // Transformation logic, could throw Exception
}

private record AB(A a, Option<B> b);

private class IndexDto(
    (Guid a, Guid b) ids,
    IEnumerable<A> listOfA,
    IEnumerable<B> listOfB)
{
    public Guid Id { get; } = ids.a;
    public Option<AB> AB { get; } = listOfA
        .FirstOrNone(a => a.Id == ids.a)
        .Select(a => new AB(a, listOfB.FirstOrNone(b => b.Id == ids.b)));
}
```


Valt er nog genoeg te verbeteren aan deze oplossing? Ongetwijfeld -- want ook ik ben nog steeds lerende als het over functioneel programmeren in C# gaat. Maar wat ik wel durf te stellen, is dat deze oplossing een stuk eenvoudiger is dan de oorspronkelijke. 


Dat heeft twee redenen. De eerste is dat de code in een declaratieve stijl is geschreven. In plaats van in detail te specificeren *hoe* de code een probleem op dient te lossen, vertelt deze nu vooral *wat* er wordt gedaan: `TryConvertDtos`, `TryConvertIfPresent`, `TryConvert`, `Convert`. De precieze implementatiedetails zijn minder interessant. Waar het om gaat is wat er in de functie gaat en wat je ervoor terugkrijgt.


De tweede reden voor de gevonden eenvoud komt voort uit het feit dat het probleem opnieuw is bekeken vanuit een functionele bril. De opdracht wordt dan: de juiste datatypen vinden om mee te werken. In plaats van direct met `A` en `B` te werken en deze later samen te voegen, blijkt het veel eenvoudiger ze in een vroeg stadium te verenigen in een nieuwe type. Wanneer dit soort typen eenmaal gevonden zijn, is het een kwestie van de juiste transformaties op het juiste moment door te voeren. 


Wie een probleem kan terugbrengen tot een reeks datatransformaties, houdt zijn code simpel en elegant. Daarin zit de kracht van functioneel denken. 
