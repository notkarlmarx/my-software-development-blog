---
title: "Enums, Switch Statements en SOLID - Deel 4"
date: 2021-05-21T09:07:30+02:00
draft: false
comments: true
tags: ["clean code", "dependency inversion principe", "enums", "open-closed principe", "refactoren", "reflection", "single-responsibility principe", "SOLID", "switch statements"]
summary: "Vorige week refactorde ik een switch statement rondom een enum aan de hand van het *Dependency inversion* principe. Deze week zetten we onze refactorslag voort aan de hand van het de O in SOLID: het *Open-closed* principe. Zo voorkomen we dat we onze code hoeven te herschrijven, elke keer als we onze enum aanpassen."
---

# Het *Open-closed* principe


[Vorige week](/blog/21-05-14-enums-switch-statements-en-solid-3) refactorde ik [een stuk code](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Refactored/V01/ClaimsHelper.cs) om meer in lijn te zijn met het [*Dependency inversion* principe](https://en.wikipedia.org/wiki/Dependency_inversion_principle). 


De `ClaimsHelper`, de centrale class in onze oefening, was voor zijn implementatie afhankelijk van de concrete implementaties van drie classes. Ik observeerde dat die drie classes op een hoger abstractieniveau in wezen dezelfde functie vervulden: de claims van een bepaalde permission teruggeven. 


Die functionaliteit kon worden vertaald naar een interface. Dat maakte het mogelijk om de centrale method in onze class, `GetClaimsForUser()`, op te schonen. We konden deze method omschrijven om tegen de interface aan te praten, in plaats van de concrete implementaties. 


Het leverde de volgende code op:


{{< gist notkarlmarx bedb39a5b877fd1fdbc9508e745e8b4f "ClaimsHelper.cs">}}


Helemaal weg zijn de concrete implementaties echter nog niet. De method `GetClaimProvider()` heeft weet van de `Read`-, `Write`- en `DeleteClaimProvider`. 


## Open voor uitbreiding, gesloten voor aanpassing


Wat is het gevolg hiervan? Elke keer als er een nieuwe waarde aan de enum wordt toegevoegd, dan moet `GetClaimProvider()` en dus ook de `ClaimsHelper` worden aangepast. Stel dat we bewerkingsrechten (`Edit`) toe willen voegen aan onze enum, dan moet de [switch-expression](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/switch-expression) in `GetClaimProvider()` worden uitgebreid met een extra conditie. Een ontwikkelaar die dat nalaat krijgt vroeg of laat een `NotSupportedException` om zijn oren.


In de softwareontwikkeling zeggen we dan: de `ClaimsHelper` schendt het [*Open-closed* principe](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle). Dit stelt dat software-entiteiten open moeten staan voor uitbreiding, maar gesloten voor aanpassing. Met andere woorden: een wijziging in het ene deel van de code - de `Permissions` - moet niet tot gevolg hebben dat een andere class - de `ClaimsHelper` - moet worden aangepast om te blijven werken.


(Vanuit het [*Dependency inversion* principe](/blog/21-05-14-enums-switch-statements-en-solid-3) geredeneerd zouden we zeggen: de class heeft een concrete afhankelijkheid naar `Permissions`. Vanuit het [*Single-responsibility* principe](/blog/21-05-07-enums-switch-statements-en-solid-2): de class heeft de verantwoordelijkheid kennis te nemen van de rechten in de applicatie. De SOLID-principes leggen elk hun eigen accent, maar hangen zoals je ziet wel met elkaar samen.)


## Reflection


Het eerste wat we kunnen doen, is `GetClaimProvider()` verhuizen naar zijn eigen class. Dit is een stap in de goede richting: de `ClaimsHelper` is dan in elk geval niet meer afhankelijk van `Permissions`. 


Maar het probleem is natuurlijk alleen maar verplaatst. Onze nieuwe class, laten we hem de `ClaimProviderFactory` noemen (naar het [factory ontwerppatroon](https://en.wikipedia.org/wiki/Factory_method_pattern)), is dat namelijk nog steeds wel. Dat is het probleem dat we op moeten zien te lossen.


C# kent gelukkig een handige feature die ons hier uit de brand kan helpen: [*Reflection*](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/reflection). Elk object dat je gebruikt of aanmaakt in je code, heeft bepaalde eigenschappen. Deze informatie over het object - de metadata - is in principe gewoon beschikbaar voor jou als ontwikkelaar. In .NET krijg je er toegang toe via het [Type](https://docs.microsoft.com/en-us/dotnet/api/system.type?view=net-5.0) van een object. De classes in de namespace [System.Reflection](https://docs.microsoft.com/en-us/dotnet/api/system.reflection?view=net-5.0) stellen je in staat om de informatie van het Type uit te vragen.


## Een oplossing


Om onze code te laten voldoen aan het *Open-closed* principe, moeten we er middels Reflection achter zien te komen welke classes er allemaal zijn die `IProvideClaims` implementeren. Vervolgens moeten we eracher zien te komen welke van die classes bij welke `Permission` hoort.


De simpelste manier om een `Permission` aan zo'n class te koppelen, is door de interface aan te passen met een [property](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties) van het type `Permission`. Die property moet [static](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/static) zijn, zodat deze uit te vragen is zonder dat we de class in kwestie hoeven te instantiëren.


(Een alternatieve manier om een `Permission` te koppelen aan een ClaimProvider-class is middels het gebruik van [attributen](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/attributes/). Voor het punt dat van deze blog is het echter om het even welke van deze twee oplossingen gekozen wordt.)


{{< gist notkarlmarx 6bffec16a479461005daae78756edf72 "IProvideClaims.cs">}}


De geupdate concrete implementatie laat zich natuurlijk raden:


{{< gist notkarlmarx 6bffec16a479461005daae78756edf72 "ReadClaimProvider.cs">}}


We kunnen nu invulling geven aan onze `ClaimsProviderFactory`:


{{< gist notkarlmarx 6bffec16a479461005daae78756edf72 "ClaimProviderFactory.cs">}}


Zoals je ziet, heeft deze class op geen enkele manier weet van de concrete implementaties van `IProvideClaims`. 


Als de method `GetClaimProvider()` wordt aangeroepen, dan haalt bekijkt deze eerst welke classes er allemaal zijn die de interface implementeren. Vervolgens filtert hij de juiste class uit deze lijst door te kijken naar de property met de naam `Permission`. Als er een class bestaat met zo'n property en deze heeft de juiste waarde, dan creëert de method hier een instantie van en geeft deze terug. Bestaat deze niet, dan wordt er een `NotSupportedException` opgegooid.


De `ClaimsHelper`, ten slotte, ziet er nu als volgt uit:


{{< gist notkarlmarx 6bffec16a479461005daae78756edf72 "ClaimsHelper.cs">}}


We kunnen onze enum nu vrijelijk aanpassen, zonder enige code in de `ClaimsHelper` of de `ClaimProviderFactory` aan te hoeven passen. Het enige wat we moeten doen - als we geen exceptions willen veroorzaken althans - is ervoor zorgen dat we een class toevoegen die `IProvideClaims` implementeert en de nieuwe `Permission` als property opneemt. 


## *What's next?*


Onze code is een stuk makkelijker onderhoudbaar geworden. Maar tegen welke prijs? Reflection is een relatief dure operatie, en onze code maakt er gebruik van, elke keer als deze de foreach-loop in `GetClaimsForUser()` doorloopt. Volgende week bekijken we wat de performance-impact van onze wijzigingen is, en wat we kunnen doen om deze zo klein mogelijk te houden.


Wie tot die tijd graag zelf wil experimenteren, kan de code [via GitHub](https://github.com/notkarlmarx/RefactorExercises/tree/master/RefactorExercises/EnumSwitch/Refactored/V03) binnenhalen.


## Meer in deze reeks

1. [De casus](/blog/21-04-30-enums-switch-statements-en-solid-1)
2. [Het *Single-Responsibility* principe](/blog/21-05-07-enums-switch-statements-en-solid-2)
3. [Het *Dependency inversion* principe](/blog/21-05-14-enums-switch-statements-en-solid-3)
4. **Het *Open-closed* principe**
5. [SOLID en performance](/blog/21-05-28-enums-switch-statements-en-solid-5)
6. Conclusie (binnenkort)
