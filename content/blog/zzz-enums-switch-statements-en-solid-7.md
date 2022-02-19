---
title: "Enums, switch statements en SOLID - deel 7"
author: "Karl van Heijster"
date: 2022-02-19T14:47:43+01:00
draft: true
comments: true
tags: []
summary: ""
---

# Slimmere enums

Een eeuwigheid geleden - april vorig jaar - schreef ik een reeks blogs over een - hoe zal ik het zeggen...? - over een nogal lelijk stuk code dat ik in het wild tegenkwam. Het ging om wat logica die rondom een Enum gebouwd was. Op basis van een bepaalde Enum-waarde, moest de ene of de andere `string` geretourneerd worden.


In niet twee, niet drie, niet vier maar in zes (!) blogs refactorde ik dat stuk code aan de hand van de SOLID-principes, totdat ik iets had wat onderhoudbaar én performant was.


Het doel van die blogs was tweeledig. Ten eerste wilde ik het lelijke stuk code tot presentabele proporties op kunnen schonen. Ten tweede was het een mooie gelegenheid om de SOLID-principes toe te kunnen passen op een afgebakend stukje code. 


Wat het tweede doel betreft, kan ik mijn blogs nog steeds als een geslaagde onderneming opvatten. Het eerste punt is problematischer. Want hoewel ik uiteindelijk inderdaad uitkwam op onderhoudbare, performante code, introduceerde ik met mijn oplossing ook een hoop complexiteit. 

\- Is het, bijna een jaar na dato, nog steeds vol te houden dat Reflection en Singletones nodig zijn om een stukje logica aan een Enum te kunnen koppelen?


De vraag stellen is hem beantwoorden. Maar om het antwoord uit te werken, loont het zich deze video van Nick Chapsas te bekijken:


{{<youtube id="CEZ6cF8eoeg" title="How to write smarter enums in C#" >}}
<br>


Mijn *use case* is eigenlijk betrekkelijk eenvoudig: ik wil wat logica kunnen koppelen aan een Enum-waarde. Sterker nog, hij is niet alleen eenvoudig, hij is ook ontzettend *generiek*.


Dat is een significante observatie. Gezien de generieke aard van het codeerprobleem, is er eigenlijk geen enkele reden waarom *ik* code zou moeten schrijven het probleem op te lossen. Als professioneel softwareontwikkelaar is het mijn taak om *business*-problemen op te lossen met code. 


Natuurlijk, een onderdeel daarvan is algemene codeproblemen oplossen. Maar code is een middel, geen doel op zich. Als ik een businessprobleem op kan lossen zonder daar zelf code voor te hoeven schrijven, dan verdient dat de voorkeur.


Dus waarom zou ik Reflection en Singletons gebruiken om code te kunnen koppelen aan een Enum, als er ook een stukje opensource software bestaat die dit probleem voor mij oplost? Want, getuige Chapsas' video, bestaat dat: *SmartEnum* is een NuGet package dat je in staat stelt om logica te koppelen aan bepaalde Enum-waarden.


Ik zal niet uitleggen hoe dat er in code uitziet, daarvoor kun je de bovenstaande video bekijken of de documentatie doorpluizen. De code in de context van mijn oorspronkelijke probleem kan ik wel delen, die ziet er zo uit: 


...


Ik heb ook de boel gebenchmarkt om te zien of er performancewinst is behaald met deze oplossing - en ja hoor:


|              Method |        Mean |       Error |      StdDev |      Median | Ratio | RatioSD | Rank |  Gen 0 | Gen 1 | Gen 2 | Allocated |
|-------------------- |------------:|------------:|------------:|------------:|------:|--------:|-----:|-------:|------:|------:|----------:|
| GetClaimsForUserV07 |    403.1 ns |    47.98 ns |   141.47 ns |    471.4 ns |  0.36 |    0.14 |    1 | 0.2446 |     - |     - |      1 KB |
| GetClaimsForUserV00 |    860.6 ns |    14.92 ns |    23.23 ns |    855.7 ns |  1.00 |    0.00 |    2 | 0.2842 |     - |     - |   1.16 KB |
| GetClaimsForUserV01 |    884.7 ns |    17.68 ns |    34.06 ns |    885.1 ns |  1.04 |    0.05 |    3 | 0.2842 |     - |     - |   1.16 KB |
| GetClaimsForUserV02 |    916.1 ns |    18.22 ns |    40.75 ns |    908.9 ns |  1.05 |    0.04 |    4 | 0.3014 |     - |     - |   1.23 KB |
| GetClaimsForUserV06 |    997.2 ns |    18.88 ns |    44.13 ns |    997.8 ns |  1.16 |    0.07 |    5 | 0.3014 |     - |     - |   1.23 KB |
| GetClaimsForUserV05 |  5,114.2 ns |   652.18 ns | 1,922.98 ns |  5,894.1 ns |  7.37 |    0.88 |    6 | 0.4692 |     - |     - |   1.92 KB |
| GetClaimsForUserV04 |  5,213.8 ns |   702.33 ns | 2,070.84 ns |  4,521.9 ns |  8.00 |    1.36 |    6 | 0.4654 |     - |     - |   1.92 KB |
| GetClaimsForUserV03 | 12,741.5 ns | 1,386.58 ns | 4,088.36 ns | 14,377.7 ns |  8.39 |    0.73 |    7 | 0.7935 |     - |     - |   3.26 KB |


Deze optie is twee keer zo snel als de oorspronkelijke oplossingsrichting!


De code is eenvoudiger én sneller. De les is duidelijk: gebruik de kracht van opensource voor algemene codeerproblemen. Iedereen wint, zo simpel is het.


## Meer in deze reeks

1. [De casus](/blog/21/04/enums-switch-statements-en-solid-1)
2. [Het *Single-Responsibility* principe](/blog/21/05/enums-switch-statements-en-solid-2)
3. [Het *Dependency inversion* principe](/blog/21/05/enums-switch-statements-en-solid-3)
4. [Het *Open-closed* principe](/blog/21/05/enums-switch-statements-en-solid-4)
5. [SOLID en performance](/blog/21/05/enums-switch-statements-en-solid-5)
6. [Conclusie](/blog/21/06/enums-switch-statements-en-solid-6)
7. **Slimmere Enums**
