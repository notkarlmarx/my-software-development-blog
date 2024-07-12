---
title: "Imperatieve Options?"
author: "Karl van Heijster"
date: 2024-07-12T07:55:29+02:00
draft: false
comments: true
tags: ["clean code", "code reviews", "declaratieve code", "eenvoud", "eerlijke functies", "imperatieve code", "intentie van code", "functioneel programmeren", "leermoment", "monads", "options", "procedureel programmeren", "refactoren", "samenwerking"]
summary: "Ik gebruik Options graag, ze voorkomen een hoop foutmeldingen. Maar, belangrijker nog, ze maken mijn code expressiever en eleganter. Of liever: ze hebben de potentie dat te doen. Laatst kwam ik tijdens een codereview een functie tegen, waarop mijn primaire reactie was: dit *moet* anders. -- Maar waarom?"
---

Ik heb hier vaker geschreven over [functioneel programmeren](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'") met [*monads*](/blog/22/12/wat-is-een-monad/ "'Wat is een monad?'") in het algemeen en [Options](/tags/options/ "Blogs met de tag 'options'") in het bijzonder. 


Wat is een Option, vraag je? Een Option is een doosje met twee mogelijke waarden: *iets* of *niets*. Je mag als ontwikkelaar iets in het doosje stoppen -- of niet, natuurlijk. Vervolgens geef je het doosje door van de ene functie in je codebase naar de andere. Als die functie iets met de waarde in het doosje wil doen, dan moet die altijd twee scenario's afhandelen: het scenario waarin er inderdaad iets in het doosje zit, of het scenario waarin dat niet het geval is.


## Met veilige groet


Neem de volgende code:


```cs
private static string Greet(User user) =>
    $"Hello, {user.FirstName}!";
```


Deze code is eenvoudig -- zo eenvoudig, dat er weinig aan te verprutsen valt. Dat zou je denken, althans, maar schijn bedriegt. De code is *te* eenvoudig, bijvoorbeeld in dit scenario:


```cs
var user = userRepository.GetById(42);
var greeting = Greet(user);
Console.WriteLine(greeting);
```


Wat gebeurt er wanneer de gebruiker met ID `42` niet gevonden kan worden? Dan retourneert de `GetById`-method `null`. En die `null` wordt rechtstreeks onze `Greet`-method ingeduwd. En wanneer die `.FirstName` aan probeert te roepen op dat lege object, dan resulteert dat in een [`NullReferenceException`](https://learn.microsoft.com/en-us/dotnet/api/system.nullreferenceexception?view=net-8.0 "'NullReferenceException Class', Microsoft documentatie"). Oeps!


We zouden dit scenario af kunnen handelen door in `Greet` eerst op `null` te checken. Maar dat is een foutgevoelige strategie. Wat als een programmeur dit vergeet? Veiliger is om de mogelijkheid van de afwezigheid van een gebruiker te coderen in de signatuur van de functie zelf. In plaats van de gebruiker rechtstreeks mee te geven aan de functie, geven we een doosje mee waar mogelijk een gebruiker in zit. Als de functie iets met de inhoud van dat doosje wil, dan moet zowel de aan- als afwezigheid van zo'n gebruiker expliciet worden afgehandeld: 


```cs
private static string Greet(Option<User> user) => 
    user.Match(u => $"Hello, {u.FirstName}!",
        () => "I'm sorry, I didn't get your name...");
```


Ik gebruik Options graag, ze voorkomen een hoop foutmeldingen. -- Maar, belangrijker nog, ze maken mijn code expressiever en eleganter.


## Elegant?


Of liever: ze hebben de potentie dat te doen. Laatst kwam ik tijdens een code review[^1] een functie tegen, die er ongeveer als volgt uitzag:


```cs
private static Option<Transformed> Transform(Option<SomeType> someType)
{
    Option<Transformed> result = None;
    someType.IfSome(st => 
    {
        if (SomeCondition(st))
        {
            result = new Transformed
            {
                Foo = someType.Foo,
                Bar = someType.Bar
            };
        }
    });
    return result;
}
```


Mijn primaire reactie op de code was: dit *moet* anders. -- Maar waarom? 


Is de code veilig? Ja, want het gebruik van de Option voorkomt een `NullReferenceException`. -- Is de code expressief? Ja, in die zin dat de signatuur van de functie duidelijk aangeeft wat de code beoogt. 


-- Maar is de code elegant? Nou... nee. De code oogt als klassieke procedurele of objectgeoriënteerde code. Sterker nog, de code is overduidelijk *geschreven* als klassieke procedurele code -- maar dan met een `IfSome` erin verwerkt, gevolgd door een `Action<SomeType>`, daar waar je normaliter een eenvoudige `if (someType is null)` zou verwachten. Je zou kunnen beargumenteren dat het gebruik van de Option de code hier zelfs minder leesbaar maakt, zeker voor junior ontwikkelaars of ervaren ontwikkelaars die nog niet eerder met *monads* gewerkt hebben.


## Oneerlijk


Het probleem van deze code is: het maakt gebruik van een functioneel construct, de Option, maar zondigt tegelijkertijd tegen verschillende functionele principes. Het gevolg is verwarring voor zowel functioneel- als objectgeoriënteerde lezers van de code.


Waar gaat het mis, vanuit functioneel standpunt gezien? Het begint met de `Action<T>`. Deze wordt gebruikt om een waarde toe te kunnen wijzen aan een variabele die *buiten* die method gedefinieerd wordt: een klassiek voorbeeld van een neveneffect.


[De method communiceert niet eerlijk](/blog/22/07/wat-zijn-eerlijke-functies/ "'Wat zijn eerlijke functies?'") over haar intentie. De signatuur van de actie is namelijk als volgt: `SomeType -> void`. (Dit is wat het type `Action<SomeType>` *de facto* uitdrukt.) Maar wat er feitelijk wordt bewerkstelligt heeft de volgende vorm: `SomeType -> Option<Transformed>`.


## Als...


Een tweede probleem ontstaat met het `if`-statement. Typische functionele code bevat geen statements, louter expressies.[^2] Statements zijn imperatief. Ze lezen als instructies aan de computer: *doe nu dit*. Expressies zijn declaratief. Ze produceren waarden. Ze lezen als een samenvatting naar de lezer: *zus levert zo op*.


De schrijver van de bovenstaande functie wilde dat `SomeType` alleen zou worden omgezet naar `Transformed` *als* er aan een bepaalde conditie werd voldaan. Maar hij wist zo gauw niet hoe hij dat binnen het functionele paradigma voor elkaar moest krijgen, en viel daarom terug op de overbekende manier van onderscheidingen maken.


Maar het `if`-statement is de bron van veel programmeerfouten. Want naarmate het aantal `if`-statements toeneemt, explodeert het aantal paden dat de code kan doorlopen en wordt de code steeds ondoorgrondelijker. Ik ben niet tegen het gebruik van `if` per se, maar het loont zich om na te denken over alternatieven.


## LINQ


Want er zijn alternatieven voor handen. De beoogde functionaliteit kan met hulp van wat standaard [LINQ](https://learn.microsoft.com/en-us/dotnet/csharp/linq/ "'Language Integrated Query (LINQ)', Microsoft documentatie") heel leesbaar worden uitgeschreven:


```cs
private static Option<Transformed> Transform(Option<SomeType> someType) =>
    someType
        .Where(SomeCondition)
        .Select(st => new Transformed 
        {
            Foo = st.Foo,
            Bar = st.Bar
        });
```


De code communiceert hetzelfde als de oorspronkelijke poging: als `SomeType` aan een bepaalde conditie voldoet, zet deze dan om naar `Transformed`. Maar het gaat me om *hoe* die boodschap wordt gecommuniceerd: eenvoudig, elegant -- delcaratief.


## Declaratief vs. imperatief


En in dat laatste zit het 'm nu precies. Functionele code is eenvoudig en elegant omdat deze declaratief is. En procedurele of objectgeoriënteerde kan complex en plomp zijn omdat ze imperatief is. De ene leest als een verhaal, de andere als een set instructies voor een computer.


Ga maar na. De imperatieve variant leest van boven naar beneden als volgt. "Declareer een variabele `result` van het type `Option<Transformed>` en laat deze initeel leeg. Ga na of parameter `someType` niet `None` is. Als dat het geval is, kijk dan of de waarde van `someType` aan conditie `SomeCondition` voldoet. Als dat het geval is, creëer dan een object `Transformed` en wijs dit aan `result` toe. Retourneer vervolgens `result`."


De declaratieve variant: "Wanneer parameter `someType` aan conditie `SomeCondition` voldoet, maak er dan een `Transformed` van." (-- Je vergeet haast dat je met een `Option<T>` van doen hebt, omdat deze informatie vervat wordt in het gebruik van `.Where` en `.Select`. Automatisch worden je ogen geleid naar de functies die daarin worden meegegeven, en die gaan uit van gewrapte object. Bovendien hoef je je niet druk te maken om de vraag wat er gebeurt wanneer `someType` `None` is; dat wordt automatisch voor je afgehandeld.)


Declaratieve code is over het algemeen leesbaarder dan imperatieve code.


## Les


Toch is de les die ik uit deze code review haalde niet: schrijf voortaan alleen maar declaratieve code. Nee, de les is eerder: denk goed na over wat het betekent voor een team wanneer je functionele (i.e. declaratieve) programmeertechnieken introduceert in een traditioneel objectgeoriënteerde (i.e. imperatieve) omgeving. (Zie ook [deze blog](/blog/24/02/callback-hell/ "'Callback hell'").)


Functioneel programmeren vraagt niet alleen een andere manier van programmeren dan objectgeoriënteerd programmeren, het vraagt om een andere manier van *denken*. -- Is het team bereid om zich die nieuwe manier van denken eigen te maken? Zijn ze zich überhaupt bewust van het feit dat ze dat zullen moeten doen? En is er ruimte om hen daarin te begeleiden?


Softwareontwikkeling is een ten diepste sociale aangelegenheid. Hoe plezierig het ook is om mooiere code te schrijven dankzij nieuwe technieken, je mag nooit uit het oog verliezen dat er ook andere mensen voor nodig zijn om die code te kunnen blijven onderhouden.


[^1]: Het was toevallig (of niet) dezelfde code review die me ertoe aanzette [deze blog](/blog/24/05/functioneel-denken-een-praktijkvoorbeeld/ "'Functioneel denken: een praktijkvoorbeeld'") te schrijven.

[^2]: Zie [deze blog](https://fsharpforfunandprofit.com/posts/expressions-vs-statements/ "'Expressions vs. statements: Why expressions are safer and make better building blocks', F# for Fun and Profit") van [Scott Wlaschin](https://scottwlaschin.com/) voor een uiteenzetting over het verschil tussen die twee. Op het moment van schrijven lees ik zijn [*Domain Modeling Made Functional*](https://pragprog.com/titles/swdddf/domain-modeling-made-functional/) -- een aanrader! Zie [deze blog](/blog/23/01/eerlijke-domeinmodellen/ "'Eerlijke domeinmodellen'") voor een inleiding in de ideeën uit dat boek.
