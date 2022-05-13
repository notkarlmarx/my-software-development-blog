---
title: "Mijn eerste testgedreven stapjes"
author: "Karl van Heijster"
date: 2022-05-11T11:36:46+02:00
draft: true
comments: true
tags: ["clean code", "eenvoud", "refactoren", "software ontwikkelen", "testcoverage", "test-driven development", "testen", "vertrouwen", "werkplezier"]
summary: "Na niet één, niet twee, niet drie, niet vier, maar vijf blogs over Test-Driven Development had ik ervoor nodig, voordat ik het aandurfde. Maar nu is het dan eindelijk zover: onlangs heb ik mijn eerste testgedreven stapjes gezet in professionele carrière. Een mijlpaal!"
---

Na niet [één](/blog/22/03/agile-en-test-driven-development/), niet [twee](/blog/22/04/een-test-per-keer/), niet [drie](/blog/22/04/to-polyglot-or-not-to-polyglot/), niet [vier](/blog/22/04/legacy-code-en-test-driven-development/), maar [vijf](/blog/22/05/nog-een-reden-om-testgedreven-te-ontwikkelen/) blogs over [Test-Driven Development](/tags/test-driven-development/) (TDD) had ik ervoor nodig, voordat ik het aandurfde. Maar nu is het dan eindelijk zover: onlangs heb ik mijn eerste testgedreven stapjes gezet in professionele carrière. Een mijlpaal!


## Controllers


En ik had een goed [PBI](/tags/product-backlog-items/)'tje ervoor uitgekozen, al zeg ik het zelf: het ontwikkelen van een nieuwe [Web API Controller](https://docs.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-6.0) om toetsen te kunnen opslaan en ophalen. 


Een korte opfriscursus: een Controller is een class die een endpoint definieert op een Web API. Als je de [REST-standaard](https://en.wikipedia.org/wiki/Representational_state_transfer) hanteert - zoals tegenwoordig gebruikelijk is -, dan betekent dat dat je de URL vastlegt waarop bepaalde data benaderbaar is. Die data wordt vastgelegd in een object en kan via diverse [HTTP-verbs](https://restfulapi.net/http-methods/) worden gemanipuleerd. Een object kan bijvoorbeeld worden opgehaald ([GET](https://restfulapi.net/http-methods/#get)), toegevoegd ([POST](https://restfulapi.net/http-methods/#post)), geüpdate ([PUT](https://restfulapi.net/http-methods/#put)) of verwijderd ([DELETE](https://restfulapi.net/http-methods/#delete)).[^1]


De applicatie waar mijn team aan werkt, is al een tijd in ontwikkeling, en kent daarom al diverse Controllers via welke diverse andere objecten benaderbaar zijn. Een voordeel van het uitkiezen van uitgerekend deze feature om mijn TDD-vaardigheden mee te ontwikkelen, was dat ik de implementatie eigenlijk zó af kon kijken van de Controllers die we al hadden. Daardoor kon ik er zeker van zijn niet vast te lopen.


De uitdaging was daarom niet zozeer: hoe geef ik vorm aan dit stuk code? De vraag was veeleer: welke tests moet ik schrijven om de functionaliteit te ondersteunen die we in de andere Controllers al hebben?


Ik zal de lezer in het vervolg van deze blog niet vervelen met de precieze details van elke test. Ik zal beschrijven wat de test voor mij controleert, en de code laten zien die ik schreef om die test te laten slagen.


## Eerste test


Eerste test: als ik een toets POST, dan moet ik een 201 Created terugkrijgen. Oké, geen probleem. 


```csharp
[HttpPost]
[ProducesResponseType((int)HttpStatusCode.Created)]
public async Task<ActionResult<Guid>> AddAssessmentTest([FromBody] AssessmentTest assessmentTest)
{
    return Created(null, null);
}
```


Maar wacht! denk je misschien. Als ik een toets POST, dan moet ik 'm toch opslaan in de database, zodat ik 'm straks terug kan halen? Dat is immers de hele bedoeling van dingen POSTen naar een Web API: ze persisteren in een database! 


\- En dat klopt, wat je zegt. Maar dat is niet wat de test van mij vraagt. De test vraagt van me om een 201 Created terug te geven - niet om de toets daadwerkelijk op te slaan. Die test volgt nog.


Onthoudt: wie testgedreven ontwikkelt, implementeert altijd eerst de simpelst mogelijke code om de test te laten slagen. Het opruimen van de code komt pas in een later stadium. - Dat kan direct na het laten slagen van de test zijn. Máár, zoals we zullen zien, dat hoeft niet altijd.


## Tweede, derde en vierde test


Tweede test: als ik een toets opsla, dan moet ik in die 201 het Id terugkrijgen van de nieuw aangemaakte resource. Simpel:


```csharp
[HttpPost]
[ProducesResponseType((int)HttpStatusCode.Created)]
public async Task<ActionResult<Guid>> AddAssessmentTest([FromBody] AssessmentTest assessmentTest)
{
    return Created(null, Guid.NewGuid());
}
```


Is het al tijd om aan het refactoren te slaan? Laten we de volgende test nog even afwachten.


Derde test: als ik een toets met een bepaald Id op probeer te halen, dan moet ik een 200 OK terug krijgen. Ja hoor:


```csharp
[HttpGet("id/{assessmentTestId}")]
[ProducesResponseType((int)HttpStatusCode.OK)]
public async Task<ActionResult<AssessmentTest>> GetAssessmentTest(Guid assessmentTestId)
{
    return Ok();
}
```


Dit is een prima moment om even een stapje terug te doen. We hebben nu een GET-endpoint. Dat maakt het voor de hand liggend om onze eerdere POST-method ietwat te refactoren om hiervan gebruik te maken. We hebben nu immers een locatie om mee terug te geven, in plaats van die vreselijke `null` die we nu in die `Created`-method stoppen.


Vierde test: als ik een toets opsla, dan wil ik de locatie terugkrijgen waarop ik die toets kan terugvinden.


```csharp
[HttpPost]
[ProducesResponseType((int)HttpStatusCode.Created)]
public async Task<ActionResult<Guid>> AddAssessmentTest([FromBody] AssessmentTest assessmentTest)
{
    var assessmentTestId = Guid.NewGuid();
    return CreatedAtAction(
        nameof(GetAssessmentTest),
        new
        {
            assessmentTestId = assessmentTestId.ToString()
        },
        assessmentTestId);
}
```


Jaha, jij dacht natuurlijk: die jongen gaat nu eindelijk een toets opslaan. Nou, nee hoor! De refactorslag is tot het minimale beperkt gebleven. De implementatie is er eigenlijk nog steeds eentje van lik-me-vestje.


## Vijfde en zesde test


Vijfde test: als ik een toets met een bepaald Id op probeer te halen, dan moet ik een toets-object terugkrijgen met dat Id. Doen we:


```csharp
[HttpGet("id/{assessmentTestId}")]
[ProducesResponseType((int)HttpStatusCode.OK)]
public async Task<ActionResult<AssessmentTest>> GetAssessmentTest(Guid assessmentTestId)
{
    var assessmentTest = new AssessmentTest { Id = assessmentTestId };
    return Ok(assessmentTest);
}
```


Zesde test: als ik een niet-bestaande toets op probeer te halen, dan moet ik een 404 NotFound terugkrijgen.


\ - Nu komen we ergens! Ga eens na, dat is interessant: ik kon wel vijf tests schrijven die gingen over het opslaan en ophalen van toetsen, vóórdat ik logica hoefde te schrijven die de toetsen daadwerkelijk opsloeg of ophaalde!


Dit is het moment waarop de logica die daarvoor nodig is, niet meer binnen één eenvoudige Controller-method past. Ik definieer een interface in de Service-laag, wiens implementatie uiteindelijk een database aan zal roepen. Voor nu is het echter voldoende als die Service gebruik maakt van in memory-objecten - maar die details laat ik buiten beschouwing. De Controller ziet er als volgt uit:


```csharp
private readonly IAssessmentTestService _assessmentTestService;

public AssessmentTestController(IAssessmentTestService assessmentTestService)
{
    _assessmentTestService = assessmentTestService;
}

[HttpGet("id/{assessmentTestId}")]
[ProducesResponseType((int)HttpStatusCode.OK)]
[ProducesResponseType((int)HttpStatusCode.NotFound)]
public async Task<ActionResult<AssessmentTest>> GetAssessmentTest(Guid assessmentTestId)
{
    var assessmentTest = await _assessmentTestService.GetAssessmentTestAsync(assessmentTestId);
    return Ok(assessmentTest);
}

[HttpPost]
[ProducesResponseType((int)HttpStatusCode.Created)]
public async Task<ActionResult<Guid>> AddAssessmentTest([FromBody] AssessmentTest assessmentTest)
{
    var assessmentTestId = await _assessmentTestService.AddAssessmentTestAsync(assessmentTest);
    return CreatedAtAction(
    nameof(GetAssessmentTest),
    new
    {
        assessmentTestId = assessmentTestId.ToString()
    },
    assessmentTestId);
}
```


## Code coverage


Ik geef toe: bovenstaande is haast op het pedante af, zo streng was ik in het toevoegen van tests vóór ik nieuwe functionaliteit schreef. Maar die pedanterie is met een reden. Hoe strenger je testgedreven ontwikkelt, hoe zekerder je ervan bent dat je code geen bugs bevat. Je schrijft namelijk alleen - als je wil: *echt alleen* - nieuwe code als er een test is die valideert dat die doet wat het moet doen.


Dat is waarom je [red-green-refactort](https://www.codecademy.com/article/tdd-red-green-refactor). TDD kent drie welonderscheiden stappen, om je te dwingen een zo eenvoudig mogelijk implementatie als uitgangspunt te nemen. Je weet zeker dat je geen onnodige complexiteit introduceert. (Zie ook [deze blog](/blog/22/03/agile-en-test-driven-development/).) De complexiteit komt pas als de volgende test erom vraagt. 


TDD is de enige manier waarop het voor jou als ontwikkelaar mogelijk is om in de buurt van honderd procent code coverage te komen. - Niet dat het onmogelijk is om achteraf tests te schrijven die alle functionaliteit afdekt, maar geestdodend is het wel. Dat is wat ik het meest meeneem van mijn eerste stapjes in de wereld van TDD: het is de beste manier om het schrijven van hoogwaardige tests te verheffen van geestdodend naar... - bij gebrek aan een beter woord: *leuk!* 


[^1]: Dit zijn de standaard methods die in je elke RESTful API kunt aanroepen voor elk object. Maar een Controller is niet gekoppeld aan de REST-standaard. Het is ook mogelijk om *custom* operaties te definiëren, die meestal gebruik maken van de GET en POST verbs. Een uitstekend boek hierover is overigens [*API Design Patterns*](https://www.manning.com/books/api-design-patterns) van [JJ Geewax](https://www.geewax.org/).
