---
title: "Mijn eerste code review"
author: "Karl van Heijster"
date: 2023-07-07T09:34:10+02:00
draft: true
comments: true
tags: ["boeken", "carrièrepad", "code lezen", "code reviews", "communicatie", "leren", "pull requests", "software ontwikkelen"]
summary: "De tijd maakt alles kapot -- maar nu ben ik nog jong genoeg om me mijn eerste code review te herinneren. Althans, ik herinner me een gevoel -- want de inhoud van het *pull request* ben ik natuurlijk allang kwijt. Het gevoel laat zich denk ik het best omschrijven als hulpeloosheid -- gevolgd door ongemak."
---

De tijd maakt alles kapot -- maar nu ben ik nog jong genoeg om me mijn eerste code review te herinneren.


Althans, ik herinner me een gevoel -- want de inhoud van het *pull request* (PR) ben ik natuurlijk allang kwijt. Het gevoel laat zich denk ik het best omschrijven als hulpeloosheid -- gevolgd door ongemak.


## Hulpeloosheid


Het zal ergens in mijn eerste of tweede week als professioneel softwareontwikkelaar zijn geweest -- en dus mijn negende of tiende week als softwareontwikkelaar. Als je het zo wil noemen, überhaupt, want mijn werkervaring bestond geheel en al uit een acht weken durend bootcamp [programmeren in C#](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/ "'C# programming guide', Microsoft documentatie"). De enige applicatie die ik ooit van binnenuit had gezien, was de demo-applicatie die ik samen met een cursusgenoot gedurende de laatste twee weken had opgetuigd.


Ik ben nooit bijzonder geïnteresseerd geweest in computers, laat staan code. Ik had filosofie gestudeerd en rolde de IT in omdat ik mijn stage op de programma-afdeling van een filmfestival had aangedikt tot "programmeur" (zie [deze blog](/blog/21/07/mijn-loopbaanwending/ "'Mijn loopbaanwending'")). Toen ik een (destijds) acht jaar oude legacy-applicatie van honderdduizenden regels code voor mijn neus kreeg, was dat wel even schrikken. 


Mijn collega's namen stilzwijgend aan dat het grootste struikelblok bestond uit het feit dat deze in voor 95 procent in [Visual Basic](https://learn.microsoft.com/en-us/dotnet/visual-basic/ "'Visual Basic documentation', Microsoft documentatie") was geschreven. Dat was een redelijk naïeve vooronderstelling. Ze schotelden me een PR voor dat in die vijf procent C#-code zat -- daar had ik ervaring mee, dat zou me wel moeten lukken.


Uit meer dan 20, 30 regels code zal het PR niet hebben bestaan. Ik kan me een [`if`-statement](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/selection-statements#the-if-statement "'The if statement', Microsoft documentatie") herinneren, en een extra [method](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods "'Methods (C# Programming Guide)', Microsoft documentatie") in een ander bestand dat onder die conditie werd aangeroepen.


Ik las het `if`-statement, en ik las de code die in dat geval werd aangeroepen. Daarna wist ik niet goed wat ik moest doen, dus las ik nog een keer het `if`-statement, en daarna nog een keer de code die in dat geval werd aangeroepen. Toen controleerde ik of de naam van de method in het ene bestand wel overeenkwam met de naam van de method in het andere bestand. Daarna wist ik echt niet wat ik nog meer kon doen.


Maar zeker genoeg om het PR goed te keuren, voelde ik me niet. Dus liet ik het maar voor wat het was.


## Rol


Deze episode doet me denken aan iets wat ik lang geleden las in een boek van [Jan Bransen](https://www.janbransen.nl/nl/category/blog/), [*Gevormd of Vervormd?*](https://isvw.nl/shop/gevormd-vervormd-jan-bransen/ "Jan Bransen - 'Gevormd of Vervormd?', uitgeverij ISVW"). (Ik heb het boek destijds nog gerecenseerd, [hier zo](https://bazarow.com/recensie/gevormd-of-vervormd-pleidooi-voor-ander-onderwijs/ "'Vervormd onderwijs vervormt leerlingen', Bazarow").) In dit *pleidooi voor ander onderwijs* -- de ondertitel van het boek --, betoogt Bransen dat het huidige onderwijs op verkeerde vooronderstellingen is gebaseerd. 


Onderwijs zou niet moeten draaien om kennisverwerving, maar om het ontwikkelen van zelfvertrouwen. -- Nota bene, kennisverwerving is één manier om zelfvertrouwen te ontwikkelen. Maar het is niet de enige manier. En, en dit is het belangrijke punt: het zou een onderwijsmiddel moeten zijn, niet het uiteindelijke doel. 


Waarom zou onderwijs moeten draaien om de ontwikkeling van zelfvertrouwen? Zodat we in staat zijn om ons te kunnen handhaven in de samenleving in het algemeen en ons werk in het bijzonder. Bransen verpakt dat idee in een dramaturgische metafoor. De wereld is, *dixit* Shakespeare, een toneel, en onderwijs bereidt ons voor om de rollen te kunnen spelen die van ons worden verlangd.


Om de rol van een codereviewer te kunnen spelen, moet je weten wat er van een codereviewer wordt verlangd, hoe een goede code review eruit ziet. Code kunnen lezen, syntactische kennis van een programmeertaal hebben, is een noodzakelijke maar geen voldoende voorwaarde voor het kunnen beoordelen van een PR. -- Dat is waar ik me tijdens mijn eerste code review op stukbeet.


## Ongemak


Goed, dus ik deed niets. Na een tijdje vroeg de schrijver van het PR me: "En, heb je er naar kunnen kijken?" Ik zei: "Ja, ik denk dat het wel goed was." Hij zei: "Nou, keur 'm maar goed dan." En hij keek over mijn schouder mee terwijl ik op die grote groene knop klikte.


Dat was goed, aan de ene kant -- want het bevestigde mijn status als teamlid. Het doopritueel was voltooid: bij dezen mocht ik een mening over de code hebben die door dit team werd geschreven.


Maar aan de andere kant: het voelde niet goed -- want ik had helemaal geen mening over de code die door dit team werd geschreven. Dat gevoel staat me nog het helderst voor de geest. 


-- Maar niet omdat het nou zo'n heftige ervaring was. Eerder omdat ik dat gevoel nog heel vaak heb mogen beleven in mijn carrière als softwareontwikkelaar. Ondanks dat ik steeds meer ervaring opdeed met de syntax van C# (en noodgedwongen ook van Visual Basic), en ondanks dat ik de codebase steeds beter wist te doorgronden, en ondanks dat ik me de principes van softwareontwikkeling steeds meer eigen maakte -- kwam het nog steeds keer op keer voor dat ik PR's goedkeurde zonder dat ik nu echt een mening had over de code.


## Drie vragen


Wat blijkt: het vermogen om code te reviewen is niet iets wat je vanzelf wel ontwikkelt naarmate je langer als softwareontwikkelaar bezig bent. 


Eén van de redenen daarvoor, is dat we als vakgebied nauwelijks aandacht besteden aan het lezen van code. Dat is een punt dat [Felienne Hermans](https://www.felienne.com/) maakt in [*The Programmer's Brain*](https://www.manning.com/books/the-programmers-brain "Felienne Hermans - 'The Programmer's Brain', uitgeverij Manning") (en in [deze video](https://www.youtube.com/watch?v=58LeSsn_nSQ "How to Read Complex Code • Felienne Hermans • YOW! 2021")). Ik schreef er in de context van PR's al eerder over, [hier](/blog/22/08/hoe-review-je-eigenlijk-code/ "'Hoe review je eigenlijk code?'") en [hier](/blog/22/09/test-driven-code-reviews/ "'Test-Driven Code Reviews'").


Een andere reden is dat programmeurs over het algemeen helemaal niet zo goed zijn in het overbrengen van alle informatie die een lezer nodig heeft om een PR goed te kunnen beoordelen. (Zie ook [deze blog](/blog/22/10/pull-requests-als-documentatie/ "'Pull requests als documentatie'").)


In mijn beleving moet een PR antwoord geven op drie vragen:


1. **Waarom bestaat dit PR überhaupt?** Deze informatie kun je het best kwijt in de metadata -- titel en omschrijving -- van een PR. Vaak blijft deze informatie impliciet -- het is onderdeel van de [*tribal knowledge*](https://en.wikipedia.org/wiki/Tribal_knowledge "'Tribal knowledge', Wikipedia") van een team. Maar het expliciet maken van het bestaansrecht van een codewijziging is een uitstekende lakmoesproef. Als dit niet lukt, moet je je afvragen of de wijziging wel de moeite waard is.

2. **Wat doet de code concreet?** Deze informatie kan het best worden vastgelegd middels geautomatiseerde tests. Het doel is de lezer te *vertellen* wat de code doet, niet de lezer dat zelf uit te laten vogelen. Ik heb hier veelvuldig over geschreven (en [gesproken](/talks/altijd-up-to-date-documentatie-met-maximaal-descriptieve-tests/ "'Altijd up to date documentatie met maximaal descriptieve tests'")), onder andere [hier](blog/22/09/tests-als-documentatie/ "'Tests als documentatie'"), [hier](/blog/22/12/tests-zijn-specs/ "'Tests zijn specs'") en [hier](/blog/23/02/waarom-dry-waarom-damp/ "'Waarom DRY? Waarom DAMP?'").

3. **Hoe doet de code dat?** Dit is de daadwerkelijke implementatie -- de code zelf, die in het ideale geval uiteraard [zichzelf documenteert](/blog/21/12/goede-code-documenteert-zichzelf-niet/ "'Goede code documenteert zichzelf (niet)'").


## Duiding


Merk op dat ik geen woord gerept heb over de metadata of tests, toen ik over mijn eerste code review verhaalde. Dat is omdat die simpelweg ontbraken. Die 20, 30 regels code waren alles waar ik het mee moest doen.


Met die kennis is het mogelijk om de gevoelens te duiden die mijn eerste code review bij me losmaakte. Mijn hulpeloosheid kwam voort uit het feit dat ik nog niet het vermogen, het zelfvertrouwen had ontwikkeld om goed en wel de rol van een codereviewer te spelen. Mijn ongemak over het goedkeuren kwam voort uit het feit dat het PR mij als lezer onvoldoende informatie bood om de wijziging goed en wel te kunnen beoordelen.


Dan rest ons nu slechts de taak om heel andere gevoelens bij nieuwe softwareontwikkelaars los te maken, als we hen loslaten op onze PR's.
