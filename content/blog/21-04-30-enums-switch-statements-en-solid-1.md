---
title: "Enums, Switch Statements en SOLID - Deel 1"
date: 2021-04-20T18:59:08+02:00
draft: false
comments: true
tags: ["clean code", "dependency inversion principe", "enums", "interface segregatie principe", "liskov substitutie principe", "open-closed principe", "refactoren", "single-responsibility principe", "SOLID", "switch statements"]
---

# De casus


Onlangs stuitte ik op een stuk code dat ik de dagen erop maar niet uit mijn hoofd kreeg. Ik ben er nog niet helemaal over uit of dat tekenend is voor mijn passie voor en/of professionaliteit als softwareontwikkelaar, of voor mijn langzame aftakeling gedurende de coronacrisis.


Laten we positief blijven en van het eerste uitgaan.


## De code


Het ging om een [switch statement](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/switch) rond een [enum](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/enum). Dit is denk ik een patroon dat elke ontwikkelaar wel ergens op een onbewaakt moment geïmplementeerd heeft. Sterker nog, als ik me het goed herinner was ik zelf verantwoordelijk voor de oorspronkelijke implementatie van dat patroon in de [class](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes) in kwestie.


Ik zou het patroon met veel woorden uit kunnen leggen, maar de onderstaande code snippet - een versimpelde versie van de code die ik in het wild tegenkwam - illustreert de boel denk ik heel aardig:


{{< gist notkarlmarx c8d96422d63e6cd7165e19a4fb243886 "ClaimsHelper.cs">}}


Waar hebben we hier mee te maken? Deze class, de `ClaimsHelper`, kent één method: `GetClaimsForUser()`. Deze bekijkt welke rechten (`Permissions`) een gebruiker (`User`) allemaal heeft, en geeft voor elk recht een string-representatie (claim) terug. Deze wordt als nieuwe regel toegevoegd aan een string met wat inleidende tekst.


Stel dat een gebruiker met als Id `1` alleen leesrechten heeft. Dan zou de output van deze method de volgende string zijn:


```
User '1' has the following claims:
- User can Read entries
```


Stel dat een gebruiker met als Id `2` zowel lees-, schrijf- en verwijderrechten heeft, dan zou de output als volgt zijn:


```
User '2' has the following claims:
- User can Read entries
- User can Write entries
- User can Delete entries
```


Eenvoudig genoeg, dunkt me. Waarom bleef deze code dan door mijn hoofd spoken?


## SOLID


Om dat te kunnen snappen, moet je iets weten over [SOLID](https://en.wikipedia.org/wiki/SOLID). De letters in SOLID staan elk voor een ontwerpprincipe voor [objectgeörienteerde](https://en.wikipedia.org/wiki/Object-oriented_programming) code. Door deze principes te volgen, schrijf je als het ware automatisch code die makkelijker te onderhouden is. Afwijken is dus op eigen risico!


De principes zijn als volgt:


- Het ***Single-responsibility* principe**: een software-entiteit moet maar één reden hebben om te worden aangepast. Met andere woorden: elke software-entiteit moet precies één verantwoordelijkheid hebben.

- Het ***Open-closed* principe**: software-entiteiten moeten open staan voor uitbreiding, maar gesloten zijn voor aanpassing. Met andere woorden: een wijziging van de ene class moet niet tot gevolg hebben dat een andere class moet worden aangepast om te blijven werken.

- Het **Liskov substitutie principe**: objecten in een programma zouden vervangbaar moeten zijn door instanties van hun subtypes zonder dat de juiste werking van het programma beïnvloed wordt.

- Het **Interface segregatie principe**: het hebben van veel cliënt-specifieke interfaces valt te verkiezen boven het hebben van één algemene interface. Met andere woorden: een class zou nooit verplicht moeten zijn bepaalde methods te moeten implementeren als gevolg van de implementatie van een interface, als hij deze eigenlijk niet nodig heeft.

- Het ***Dependency inversion* principe**: wees afhankelijk van abstracties (bijvoorbeeld interfaces, maar ook baseclasses), niet van concrete implementaties.


Om kort te gaan: het bovenstaande stuk code voldoet niet aan de meeste van de SOLID-principes. (En daar waar ze er wel aan voldoet, is dat omdat het principe eigenlijk niet of nog niet van toepassing is.)


Kun je de manieren in kaart brengen waarop de `ClaimsHelper` niet aan SOLID-principes voldoet?


## *What's next?*


Welnu, dit opmerken is één ding. Het probleem verhelpen, dat is een heel ander verhaal. 


De komende weken zal ik het bovenstaande stuk code stapsgewijs [refactoren](https://en.wikipedia.org/wiki/Code_refactoring) in een poging de code wat netter en beter uitbreidbaar te maken. Gedurende de refactorslag zullen drie van de vijf SOLID-principes voorbij komen, die hopelijk meteen hun waarde zullen bewijzen.


Wie nog niet helemaal overtuigd is van de waarde van SOLID, of wie er graag meer over zou willen leren, kan ik de [video's van Tim Corey](https://www.youtube.com/channel/UC-ptWR16ITQyYOglXyQmpzw) aanraden. Deze, over het *single responsibility* principe is een goed begin:
{{<youtube id="5RwhyZnVRS8" title="Design Patterns: Single Responsibility Principle Explained Practically in C# (The S in SOLID)" >}}


De code is [via GitHub](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Original/ClaimsHelper.cs) te bekijken en binnen te halen. Wees niet bang om zelf met de class te spelen en te bekijken hoe je 'm wat meer in lijn met de SOLID-principes kan brengen!


## Meer in deze reeks

1. **De casus**
2. Het *Single-Responsibility* principe (binnenkort)
3. Het *Dependency inversion* principe (binnenkort)
4. Het *Open-closed* principe (binnenkort)
5. SOLID en performance (binnenkort)
6. Conclusie (binnenkort)
