---
title: "Semantische bugs"
author: "Karl van Heijster"
date: 2024-07-12T10:06:05+02:00
draft: true
comments: true
tags: ["bugs", "clean code", "falen", "intentie van code", "naamgeving", "professionaliteit", "requirements", "software ontwikkelaar (rol)", "vakmanschap", "verantwoordelijkheid", "werkplezier"]
summary: "Voor een presentatie klooide ik wat variaties op het FizzBuzz-algoritme in elkaar. En ergens in de loop van die codeeroefening stuitte ik op een interessante bug -- hoewel, ik weet niet eens zeker of het wel een bug was. Dus: wat is een bug eigenlijk?"
---

Voor een presentatie klooide ik wat variaties op het [FizzBuzz](https://en.wikipedia.org/wiki/Fizz_buzz "'Fizz buzz', Wikipedia")-algoritme in elkaar. (De broncode is [hier](https://github.com/dotkarl/FizzBuzz "'dotkarl/FizzBuzz', GitHub") te vinden.) En ergens in de loop van die codeeroefening stuitte ik op een interessante bug -- hoewel, ik weet niet eens zeker of het wel een bug was. Dus: wat is een [bug](https://en.wikipedia.org/wiki/Bug_(engineering) "'Bug (engineering)', Wikipedia") eigenlijk?


## Specificaties


-- Een stapje terug. Waar was ik mee bezig? FizzBuzz. Dat is een systeem met lachwekkend eenvoudige specificaties:


> Voor elk geheel getal:
>
> - als deze deelbaar is door 3, retourneer "Fizz";
>
> - als deze deelbaar is door 5, retourneer "Buzz";
>
> - als deze deelbaar is door 3 en 5, retourneer "FizzBuzz";
>
> - anders, retourneer het getal.


## Implementatie #1


Wie naar de specificaties kijkt, ziet de implementatie al haast voor zich. En inderdaad, traditioneel ziet een oplossing voor FizzBuzz er als volgt uit:


```cs
public static string FizzBuzz(int input)
{
    if (IsDivisibleBy3(input) && IsDivisibleBy5(input))
        return "FizzBuzz";
    if (IsDivisibleBy3(input))
        return "Fizz";
    if (IsDivisibleBy5(input))
        return "Buzz";
    return input.ToString();
}
```


## Implementatie #2


Of, als de programmeur in kwestie een liefhebber is van `switch`-expressies:


```cs
public static string FizzBuzz(int input) => input switch
{
    int i when IsDivisibleBy3(i) && IsDivisibleBy5(i) => "FizzBuzz",
    int i when IsDivisibleBy3(i) => "Fizz",
    int i when IsDivisibleBy5(i) => "Buzz",
    _ => input.ToString()
};
```


## Implementatie #3


Of, wanneer de programmeur in kwestie een liefhebber is van [*pipeline-oriented programming*](https://fsharpforfunandprofit.com/pipeline/):


```cs
using static LanguageExt.Prelude;

// ...

public static string FizzBuzz(int input) => Right(input)
    .Bind(FizzBuzzIfDivisibleBy3And5)
    .Bind(BuzzIfDivisibleBy5)
    .Bind(FizzIfDivisibleBy3)
    .Match<string>(
        originalInput => originalInput.ToString(),
        transformedInput => transformedInput);
```


(Deze oplossing is gebaseerd op een implementatie die ik tegenkwam in [dit praatje](https://www.youtube.com/watch?v=ipceTuJlw-M "'Pipeline-oriented programming - Scott Wlaschin - NDC Porto 2023', YouTube") van [Scott Wlaschin](https://scottwlaschin.com/). Anders dan Wlaschin had ik het geduld echter niet om zelf een type te introduceren dat ofwel een `int` ofwel een `string` kon retourneren, daarom maak ik gebruik van de [`Either`-monad](https://louthy.github.io/language-ext/LanguageExt.Core/Monads/Alternative%20Value%20Monads/Either/Either/index.html) uit de [*LanguageExt* library](https://github.com/louthy/language-ext "'language-ext', GitHub") voor C#.)


## Zie je de fout?


Het is in die derde implementatie dat ik die (misschien) bug tegenkwam. Want in mijn oneindige gaarheid had ik de methods `BuzzIfDivisibleBy5` en `FizzIfDivisibleBy3` als volgt geïmplementeerd:


```cs
public static Either<string, int> BuzzIfDivisibleBy3(int input) =>
    IsDivisibleBy5(input) ? "Buzz" : input;

private static Either<string, int> FizzIfDivisibleBy5(int input) =>
    IsDivisibleBy3(input) ? "Fizz" : input;
```


Zie je de fout? -- Ik zag 'm niet. Ik zag 'm heel lang niet.


In de method `BuzzIfDivisibleBy3` check ik of `input` deelbaar is door 5 (`IsDivisbleBy5`), en in `FizzIfDivisibleBy5` check ik of `input` deelbaar is door 3 (`IsDivisbleBy3`). 


Daar klopt natuurlijk helemaal niets van. Want (dacht ik in mijn oneindige gaarheid) `BuzzIfDivisibleBy3` moet checken of `input` deelbaar is door *3*, en `FizzIfDivisibleBy5` zou hetzelfde moeten doen wanneer deze deelbaar is door *5*. Dus ik paste de code aan -- en ineens begonnen er tests te falen.


## Schrödinger


Dat was waarom de fout me nooit opgevallen was: de tests stonden allemaal op groen. Mijn implementatie klopte. -- Maar tegelijkertijd klopte mijn implementatie niet, want de code zei iets heel anders te doen dan het daadwerkelijk deed. (Zie ook [deze blog](WAT_ZEGT_DEZE_CODE "'Wat zegt deze code?'").)


Mijn code bevatte tegelijkertijd wel en niet een bug, leek het: -- [Schrödingers FizzBuzz](https://en.wikipedia.org/wiki/Schr%C3%B6dinger%27s_cat "'Schrödinger's cat', Wikipedia").


Het duurde lachwekkend lang voordat ik de *werkelijke* oorzaak van de bug herkende: de methodnamen klopten niet. `BuzzIfDivisibleBy3` moest `BuzzIfDivisibleBy5` zijn en `FizzIfDivisibleBy5` `FizzIfDivisibleBy3` -- precies zoals ze daadwerkelijk geïmplementeerd waren.


## Bug?


De vraag is nu: bevatte mijn code een bug of niet?


Aan de ene kant: nee, want het gedrag van de code was correct -- het systeem voldeed exact aan de specificaties. Aan de andere kant: ja, want de code bevatte fouten -- verschillende methods zeiden *a* te doen maar deden eigenlijk *b* (en vice versa).


Het is verleidelijk om te zeggen: het is maar net hoe je "bug" definieert. En inderdaad, als we de [Nederlandse Wikipedia](https://nl.wikipedia.org/wiki/Bug_(technologie) "'Bug (technologie)', Wikipedia") erop naslaan, dan lezen we: "Een bug is een fout in een computerprogramma of een website, waardoor het zijn functie niet (geheel) volgens specificaties vervult." -- De zaak is beslist: mijn programmeerfout was geen bug.


## Ongewenst


Maar als we de [Engelse variant](https://en.wikipedia.org/wiki/Bug_(engineering) "'Bug (engineering)', Wikipedia") erbij pakken, dan wordt het beeld wat minder eenduidig: "*In engineering, a bug is a design defect in an engineered system that causes an undesired result.*" -- Wat de vraag oproept: wat is een "*undesired result*" (ongewenst resultaat)?[^1]


Ik zou de verwarrende minuten die ik doormaakte terwijl ik de code probeerde te fixen, wel degelijk als ongewenst willen kenmerken. -- Maar, en daar zit 'm, denk ik, de crux: het was ongewenst *voor mij* als ontwikkelaar. En daarin verschilt deze "bug" van de traditionele bug. In het dagelijks gebruik van die term bedoelen we doorgaans: ongewenst *voor de eindgebruiker*.


En eindgebruikers en ontwikkelaars hebben een heel andere verhouding tot de code. Voor eindgebruikers is de feitelijke code irrelevant, zij zijn primair geïnteresseerd in het gedrag dat die code mogelijk maakt.[^2] Voor ontwikkelaars is de verhouding haast omgedraaid. Zij hebben geen primair belang bij het gedrag van de code, want zij zijn over het algemeen geen gebruiker van het systeem; voor hen is een hoge codekwaliteit van essentieel voor hun productiviteit en werkplezier.


(Hoe kan het dan dat zoveel ontwikkelteams desalniettemin eindeloze hoeveelheden technische schuld produceren? [Robert Martin](http://cleancoder.com/products) legt in [*Clean Craftsmanship*](https://www.pearson.com/en-us/subject-catalog/p/clean-craftsmanship-disciplines-standards-and-ethics/P200000009529/9780136915713) de schuld bij de -- veelal letterlijke -- onvolwassenheid van de ontwikkelpopulatie. [Kent Beck](https://www.kentbeck.com/) zoekt in [*Tidy First?*](https://www.oreilly.com/library/view/tidy-first/9781098151232/) het antwoord in een verstoorde relatie die ontwikkelaars met zichzelf hebben.)


## Semantische bugs


Dus: wat is een bug nu eigenlijk? Ik kwam tot de conclusie dat er -- ten minste -- twee soorten bugs bestaan. 


De eerste variant is de gedragsmatige bug: het systeem gedraagt zich niet zoals gewenst. Dit is een bug vanuit het perspectief van een gebruiker van het systeem. Het is een bug in de traditionele zin van het woord.


De tweede variant is de semantische bug: de code vertelt een onwaarheid, drukt iets uit wat niet in lijn is met de feiten. Dit is een bug vanuit het perspectief van de onderhouder van het systeem. Het is een fenomeen waar, voor zover ik weet, nog geen geaccepteerde term voor is. Het zal veelal worden aangeduid als "technische schuld"[^3] -- of, waarschijnlijker: "*shit code*".


Als [softwareprofessionals](/tags/professionaliteit/ "Blogs met de tag 'professionaliteit'") laten we daarmee een kans liggen. We laten de kans liggen om woorden te geven -- en daarmee in kaart te brengen -- aan de manieren waarop we ons eigen werk vaak zo moeilijk maken. En door die taal te formuleren, schetsen we voor onszelf een beeld van hoe we ons werk beter zouden kunnen doen. 


We volgen de juiste weg door paden te identificeren die we dienen te vermijden. Semantische bugs zijn niet gewoon *shit code* waar we nu eenmaal mee moeten leven -- we zijn het aan onszelf en onze stakeholders verplicht onze code ook op dit vlak bugvrij te maken en houden.


[^1]: Het artikel zelf geeft overigens als volgt antwoord op die vraag: "*The undesirable result can be classified and described* many *ways including: intermittent, transient, glitch, crash or hang. -- Since desirability is subjective, what is considered undesirable to one may be considered desirable to another; even a useful feature.*"

[^2]: Het is te kort door de bocht om te stellen dat eindgebruikers *alleen* geïnteresseerd zijn in het gedrag. Wanneer hun wensen veranderen en de code aangepast moet worden, is het voor hen een onacceptabel te horen dat een ogenschijnlijk eenvoudige nieuwe feature maanden op zich laat wachten door alle technische schuld. Secundair zijn eindgebruikers wel degelijk in codekwaliteit geïnteresseerd.

[^3]: Waarbij er voor het gemak vanuit wordt gegaan dat technische schuld altijd een negatieve term is. Maar, zoals [Kevlin Henney](https://kevlinhenney.medium.com/ "Kevlin Henney @ Medium") onder andere in [dit praatje](https://www.youtube.com/watch?v=9iLxR1h2208 "'Technical Neglect - Kevlin Henney - NDC London 2024', YouTube") fantastisch uiteenzet: daarmee wordt het hele punt van de metafoor gemist. Zie ook [deze blog](/blog/21/11/bewuste-technische-schuld/ "'Bewuste technische schuld'").
