---
title: "Enums, Switch Statements en SOLID - Deel 4"
date: 2021-04-26T20:52:07+02:00
draft: true
comments: true
tags: []
summary: ""
---

# Het *Open-closed* principe


[Vorige week](/blog/enums-switch-statements-en-solid-3) refactorde ik [een stuk code](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V01/ClaimsHelper.cs) om meer in lijn te zijn met het [*Dependency inversion* principe](https://en.wikipedia.org/wiki/Dependency_inversion_principle). 


De `ClaimsHelper`, de centrale class in onze oefening, was voor zijn implementatie afhankelijk van de concrete implementaties van drie classes. Ik observeerde dat die drie classes op een hoger abstractieniveau in wezen dezelfde functie vervulden: de claims van een bepaald recht teruggeven. Die functionaliteit kon worden vertaald naar een interface. Dat maakte het mogelijk om de centrale method in onze class, `GetClaimsForUser()`, op te schonen. We konden deze method omschrijven om tegen de interface aan te praten, in plaats van de concrete implementaties. 


Het leverde de volgende code op:


{{< gist notkarlmarx 8cc39148d7b0165c9ad9d58399b7f640 "ClaimsHelper.cs">}}


Helemaal weg zijn de concrete implementaties echter nog niet. De method `GetClaimProvider()` heeft weet van de `Read`-, `Write`- en `DeleteClaimProvider`. 


## Open voor uitbreiding, gesloten voor aanpassing


Wat is het gevolg hiervan? Elke keer als er een nieuwe waarde aan de enum wordt toegevoegd, dan moet `GetClaimProvider()` en dus ook de `ClaimsHelper` worden aangepast. Stel dat we een bewerkingsrechten (`Edit`) toe willen voegen, dan moet de switch-expression in `GetClaimProvider()` worden uitgebreid met een extra conditie. Een ontwikkelaar die dat nalaat krijgt vroeg of laat een `NotSupportedException` om zijn oren.


In de softwareontwikkeling zeggen we dan: de `ClaimsHelper` schendt het *Open-closed* principe. Dit stelt dat software-entiteiten open moeten staan voor uitbreiding, maar gesloten voor aanpassing. Met andere woorden: een wijziging in het ene deel van de code - de `Permissions` - moet niet tot gevolg hebben dat een andere class - de `ClaimsHelper` - moet worden aangepast om te blijven werken.


(Vanuit het *Dependency inversion* principe geredeneerd zouden we zeggen: de class heeft een concrete afhankelijkheid naar `Permissions`. Vanuit het *Single-responsibility* principe: de class heeft de verantwoordelijkheid kennis te nemen van de rechten in de applicatie. De SOLID-principes leggen elk hun eigen accent, maar hangen wel degelijk met elkaar samen.)


## Reflection


Het eerste wat we kunnen doen, is `GetClaimProvider()` verhuizen naar zijn eigen class. Dit is een stap in de goede richting: de `ClaimsHelper` is dan in elk geval niet meer afhankelijk van `Permissions`. Maar het probleem is natuurlijk alleen maar verplaatst. Onze nieuwe class, laten we hem de `ClaimProviderFactory` noemen, is dat namelijk nog steeds wel. Dat is het probleem dat we op moeten zien te lossen.


C# kent gelukkig een handige feature die ons hier uit de brand kan helpen: [Reflection](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/reflection).
