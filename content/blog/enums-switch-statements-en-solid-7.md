---
title: "Enums, switch statements en SOLID - deel 7"
author: "Karl van Heijster"
date: 2022-02-19T14:47:43+01:00
draft: true
comments: true
tags: ["clean code", "enums", "leermoment", "open source", "performance", "refactoren", "software ontwikkelaar (rol)", "software ontwikkelen", "SOLID", "waarde"]
summary: "Een eeuwigheid geleden - april vorig jaar - schreef ik een reeks blogs over wat logica die rondom een Enum gebouwd was. Bijna een jaar na dato stel ik de vraag: wat probeerde ik nu eigenlijk te bereiken? - Eigenlijk was mijn *use case* betrekkelijk eenvoudig. Ik wilde wat logica kunnen koppelen aan een Enum-waarde, dat is alles. Sterker nog, die wens is niet alleen eenvoudig, hij is ook ontzettend *generiek*. Dat is een significante observatie. Gezien de generieke aard van het codeerprobleem, is er eigenlijk geen enkele reden waarom *ik* code zou moeten schrijven het probleem op te lossen. "
---

# Slimmere Enums


Een eeuwigheid geleden - april vorig jaar - schreef ik een [reeks blogs](/blog/21/04/enums-switch-statements-en-solid-1/) over een... - hoe zal ik het zeggen...? - over een visueel gehandicapt stuk code dat ik in het wild tegenkwam. Het ging om wat logica die rondom een Enum gebouwd was. Op basis van een bepaalde Enum-waarde, moest de ene of de andere `string` geretourneerd worden.


In niet twee, niet drie, niet vier maar in zes (!) blogs refactorde ik dat stuk code aan de hand van de [SOLID-principes](https://en.wikipedia.org/wiki/SOLID), totdat ik iets had wat onderhoudbaar én performant was.


## Twee doelen


Het doel van die blogs was tweeledig. Ten eerste wilde ik het lelijke stuk code tot presentabele proporties op kunnen schonen. Ten tweede was het een mooie gelegenheid om de SOLID-principes toe te kunnen passen op een afgebakend stukje code. 


Wat het tweede doel betreft, kan ik mijn blogs nog steeds als een geslaagde onderneming opvatten. Het is als ontwikkelaar verleidelijk om je te concentreren op nieuwe technieken en features, en de basisvaardigheden te laten versloffen. Alle tijd die je besteedt aan een oefening in het schrijven van schone code is de moeite waard. 


Het eerste punt is problematischer. Want hoewel ik uiteindelijk inderdaad uitkwam op onderhoudbare, performante code, introduceerde ik met mijn oplossing ook een hoop complexiteit. 


\- Is het, bijna een jaar na dato, nog steeds vol te houden dat er een interface, een stuk of wat implementaties, een singleton (en Reflection als de lijm tussen al die elementen) voor nodig is om een stukje logica aan een Enum te kunnen koppelen?


Stel, je zou het onderstaande stukken code in het wild tegenkomen...:


{{< gist dotkarl 6bffec16a479461005daae78756edf72 "ClaimsHelper.cs">}}


{{< gist dotkarl a5571b15998ff4b86de84d368152ff0b "ClaimProviderFactoryV06.cs">}}


...zou je dan roepen: "Ah, duidelijk!" - of iets verzuchten over, eh, een visuele handicap? - De vraag stellen is hem beantwoorden, natuurlijk. 


## Wat wil ik?


Dus: terug naar de tekentafel. Wat probeerde ik nu eigenlijk te bereiken? - Eigenlijk is mijn *use case* betrekkelijk eenvoudig. Ik wil wat logica kunnen koppelen aan een Enum-waarde, dat is alles. Sterker nog, die wens is niet alleen eenvoudig, hij is ook ontzettend *generiek*.


Dat is een significante observatie. Gezien de generieke aard van het codeerprobleem, is er eigenlijk geen enkele reden waarom *ik* code zou moeten schrijven het probleem op te lossen. 


## Mijn taak


Dat klinkt misschien tegenintuïtief. Als softwareontwikkelaar is het toch bij uitstek jouw taak om codeproblemen op te lossen, generiek of niet? We doen de hele dag toch niet anders?


Ja en nee. Ja, professionele softwareontwikkelaars lossen problemen op met code. Welke problemen? In eerste instantie: *business*problemen. En pas in tweede instantie codeproblemen - problemen die ontstaan door de gekozen oplossing voor het businessprobleem.


Maar het is belangrijk om in het achterhoofd te houden (en dit is de "nee"): code is een doel, geen middel. Als ik een businessprobleem op kan lossen zonder daar zelf code voor te hoeven schrijven, heeft dat dan niet de voorkeur? 


Waarom zou ik interfaces en singletons en Reflection gebruiken om code te kunnen koppelen aan een Enum, als er ook een stukje opensource software bestaat die dit probleem voor mij oplost? - Door de oplossing zelf te coderen, haal ik me codeproblemen op de hals die ik kan vermijden door de code uit te besteden.


## De oplossing


De vraag wordt dan: *kan ik dit probleem uitbesteden?* En het antwoord is een volmondig "Ja!", leerde ik dankzij de onderstaande video van [Nick Chapsas](https://nickchapsas.com/):


{{<youtube id="CEZ6cF8eoeg" title="How to write smarter enums in C#" >}}
<br>


De oplossing bevindt zich in het gebruik van de [*SmartEnum*](https://github.com/ardalis/SmartEnum). Dat is een NuGet package dat je in staat stelt om logica te koppelen aan bepaalde Enum-waarden.


Ik zal niet stap voor stap uitleggen hoe dat er in code uitziet, daarvoor kun je de bovenstaande video bekijken of de [documentatie](https://github.com/ardalis/SmartEnum#usage) doorpluizen. 


In plaats daarvan zal ik het eindresultaat presenteren. Alle code die ik in de oorspronkelijke zes blogs heb opgetuigd, kan dankzij *SmartEnums* gereduceerd worden tot deze drie classes:


{{< gist dotkarl 512416c55a313961ed5e9322744c1c60 "SmartPermission.cs">}}

{{< gist dotkarl 512416c55a313961ed5e9322744c1c60 "SmartUser.cs">}}

{{< gist dotkarl 512416c55a313961ed5e9322744c1c60 "ClaimsHelper.cs">}}


Er is geen `ClaimProviderFactory` meer nodig: alle code om de logica te koppelen aan een Enum-waarde wordt afgehandeld door de `SmartPermission`, die via een property `Claim` de juiste string gekoppeld heeft.[^1] 


## Performance


Ik heb ook de boel gebenchmarkt om te zien of er performancewinst is behaald met deze oplossing. En ja hoor:


|              Method |        Gem. |   Foutmarge | Standaarddev. | Mediaan |
|-------------------- |------------:|------------:|------------:|------------:|
| [GetClaimsForUserV07](https://github.com/dotkarl/RefactorExercises/tree/master/RefactorExercises/EnumSwitch/Refactored/V07) |    403.1 ns |    47.98 ns |   141.47 ns |    471.4 ns | 
| [GetClaimsForUserV00](https://github.com/dotkarl/RefactorExercises/tree/master/RefactorExercises/EnumSwitch/Original) |    860.6 ns |    14.92 ns |    23.23 ns |    855.7 ns | 
| [GetClaimsForUserV01](https://github.com/dotkarl/RefactorExercises/tree/master/RefactorExercises/EnumSwitch/Refactored/V01) |    884.7 ns |    17.68 ns |    34.06 ns |    885.1 ns | 
| [GetClaimsForUserV02](https://github.com/dotkarl/RefactorExercises/tree/master/RefactorExercises/EnumSwitch/Refactored/V02) |    916.1 ns |    18.22 ns |    40.75 ns |    908.9 ns | 
| [GetClaimsForUserV06](https://github.com/dotkarl/RefactorExercises/tree/master/RefactorExercises/EnumSwitch/Refactored/V06) |    997.2 ns |    18.88 ns |    44.13 ns |    997.8 ns | 
| [GetClaimsForUserV05](https://github.com/dotkarl/RefactorExercises/tree/master/RefactorExercises/EnumSwitch/Refactored/V05) |  5,114.2 ns |   652.18 ns | 1,922.98 ns |  5,894.1 ns | 
| [GetClaimsForUserV04](https://github.com/dotkarl/RefactorExercises/tree/master/RefactorExercises/EnumSwitch/Refactored/V04) |  5,213.8 ns |   702.33 ns | 2,070.84 ns |  4,521.9 ns | 
| [GetClaimsForUserV03](https://github.com/dotkarl/RefactorExercises/tree/master/RefactorExercises/EnumSwitch/Refactored/V03) | 12,741.5 ns | 1,386.58 ns | 4,088.36 ns | 14,377.7 ns | 


Deze optie is twee keer zo snel als de *oorspronkelijke* oplossingsrichting, laat staan mijn refactorpogingen!


## Les


Dit is precies waarom IT-managers graag dingen als "*Buy before build!*" roepen. De kans dat iemand een betere oplossing heeft bedacht voor een algemeen programmeerprobleem, is ontzettend groot. De kans dat een heuse community aan opensource-developers een betere oplossing heeft, is nagenoeg 1.


De implicaties daarvan voor wat het betekent om een goede softwareontwikkelaar te zijn, zijn nauwelijks te overschatten. *Het gaat er niet (meer?) om wie de beste code kan schrijven.* Een ontwikkelaar die de beste oplossing kan vinden op het web, wint het van een vaardige programmeur, makkelijk. 


De code die ik schrijf met *SmartEnum* is eenvoudiger én sneller. De les is duidelijk: gebruik de kracht van opensource voor algemene codeerproblemen. Iedereen wint, zo simpel is het.


## Meer in deze reeks

1. [De casus](/blog/21/04/enums-switch-statements-en-solid-1)
2. [Het *Single-Responsibility* principe](/blog/21/05/enums-switch-statements-en-solid-2)
3. [Het *Dependency inversion* principe](/blog/21/05/enums-switch-statements-en-solid-3)
4. [Het *Open-closed* principe](/blog/21/05/enums-switch-statements-en-solid-4)
5. [SOLID en performance](/blog/21/05/enums-switch-statements-en-solid-5)
6. [Conclusie](/blog/21/06/enums-switch-statements-en-solid-6)
7. **Slimmere Enums**


[^1]: Ik heb de oplossing bewust zo simpel mogelijk gehouden. De oorspronkelijke Enum had bijvoorbeeld een [`FlagsAttribute`](https://docs.microsoft.com/en-us/dotnet/api/system.flagsattribute?view=net-6.0) om het opslaan in de database te vergemakkelijken. Flags worden kort ook [ondersteund door *SmartEnum*](https://github.com/ardalis/SmartEnum#smartflagenum), maar zijn buiten beschouwing gelaten omdat ze niet voor het punt van deze blog relevant zijn.