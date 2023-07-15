---
title: "Mijn eerste code review"
author: "Karl van Heijster"
date: 2023-07-07T09:34:10+02:00
draft: true
comments: true
tags: ["boeken", "carrièrepad", "code lezen", "code reviews", "communicatie", "leren", "pull requests", "software ontwikkelen"]
summary: "De tijd maakt alles kapot -- maar nu ben ik nog jong genoeg om me mijn eerste code review te herinneren. Althans, ik herinner me een gevoel -- want de inhoud van het *pull request* ben ik natuurlijk allang kwijt. Het gevoel laat zich denk ik het best omschrijven als een vorm van hulpeloosheid -- gevolgd door ongemak."
---

De tijd maakt alles kapot -- maar nu ben ik nog jong genoeg om me mijn eerste code review te herinneren.


Althans, ik herinner me een gevoel -- want de inhoud van het *pull request* (PR) ben ik natuurlijk allang kwijt. Het gevoel laat zich denk ik het best omschrijven als een vorm van hulpeloosheid -- gevolgd door ongemak.


## Hulpeloosheid


Het zal ergens in mijn eerste of tweede week als professioneel softwareontwikkelaar zijn geweest -- en dus mijn negende of tiende week als softwareontwikkelaar *tout court*. Als je het zo wil noemen, überhaupt, want mijn werkervaring bestond geheel en al uit een acht weken durend bootcamp [programmeren in C#](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/ "'C# programming guide', Microsoft documentatie"). 


Ik ben nooit bijzonder geïnteresseerd geweest in computers, laat staan code. Ik had filosofie gestudeerd en rolde de IT in omdat ik mijn stage op de programma-afdeling van een filmfestival had aangedikt tot "programmeur" (zie [deze blog](/blog/21/07/mijn-loopbaanwending/ "'Mijn loopbaanwending'")).


De enige applicatie die ik ooit van binnenuit had gezien, was de demo-applicatie die ik samen met een cursusgenoot uit de grond had gestampt, drie of vier weken eerder. Mijn cursusgenoot en ik, wij deden niet aan PR's of codereviews, wij waren allang blij als onze code geen compilerfouten bevatte. 


Toen ik vervolgens een (op dat moment) acht jaar oude legacy-applicatie van honderdduizenden regels code voor mijn neus kreeg, was dat wel even schrikken. 


## Als, dan


Mijn collega's namen stilzwijgend aan dat mijn grootste struikelblok bestond uit het feit dat deze in voor 95 procent in [Visual Basic](https://learn.microsoft.com/en-us/dotnet/visual-basic/ "'Visual Basic documentation', Microsoft documentatie") was geschreven. (Dat is op zichzelf een interessant gegeven. Namen ze -- onjuist -- aan dat het lezen van code hoofdzakelijk bestaat uit het begrijpen van syntax?) Ze schotelden me een PR voor dat in die vijf procent C#-code zat. Daar had ik ervaring mee, immers, dus dat zou me wel moeten lukken.


Uit meer dan 20, 30 regels code zal het PR niet hebben bestaan. Ik kan me een [`if`-statement](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/selection-statements#the-if-statement "'The if statement', Microsoft documentatie") herinneren, en een extra [method](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods "'Methods (C# Programming Guide)', Microsoft documentatie") in een andere class die onder die conditie werd aangeroepen.


Ik las het `if`-statement, en ik las de code die in dat geval uit werd gevoerd. Daarna wist ik niet goed wat ik moest doen, dus las ik nog een keer het `if`-statement, en daarna nog een keer de code die in dat geval werd uitgevoerd. Toen controleerde ik of de naam van de method in het ene bestand wel overeenkwam met de naam van de method in het andere bestand. Dat deed het. 


Daarna wist ik echt niet wat ik nog meer kon doen. Maar zeker genoeg om het PR goed te keuren, voelde ik me niet. Dus liet ik het maar voor wat het was.


## Kennis


Deze episode doet me denken aan iets wat ik lang geleden las in een boek van [Jan Bransen](https://www.janbransen.nl/nl/category/blog/), [*Gevormd of Vervormd?*](https://isvw.nl/shop/gevormd-vervormd-jan-bransen/ "Jan Bransen - 'Gevormd of Vervormd?', uitgeverij ISVW"). (Ik heb het boek destijds nog gerecenseerd, [hier zo](https://bazarow.com/recensie/gevormd-of-vervormd-pleidooi-voor-ander-onderwijs/ "'Vervormd onderwijs vervormt leerlingen', Bazarow").) In dit *pleidooi voor ander onderwijs* -- de ondertitel van het boek --, betoogt Bransen dat onze huidige manier van scholen op verkeerde vooronderstellingen is gebaseerd. 


Het huidige onderwijs draait om kennisverwerving. Leerlingen worden gezien als vaten die vol dienen te worden gestopt met informatie. Pas als ze die informatie hebben opgenomen, kunnen ze de wijde wereld intrekken om deze toe te passen. 


Opleidingen veronderstellen dat het leven uit twee welonderscheiden fasen bestaat: een leerfase en een leeffase. De eerste is eerder theoretisch of cognitief, de tweede praktisch of toegepast. En je kunt (of mag?) pas aan de tweede fase beginnen als de eerste is afgerond.


## Zelfvertrouwen


Bransen stelt daar een alternatieve visie tegenover. Onderwijs zou niet moeten draaien om kennisverwerving, maar om het ontwikkelen van zelfvertrouwen. -- Nota bene, kennisverwerving is één manier om zelfvertrouwen te ontwikkelen. Maar het is niet de enige manier. En, en dit is het belangrijke punt: het zou een middel moeten zijn in het onderricht, niet het uiteindelijke doel. 


Waarom zou onderwijs moeten draaien om de ontwikkeling van zelfvertrouwen? Zodat we in staat zijn om ons te kunnen handhaven in de samenleving in het algemeen en ons werk in het bijzonder. Bransen verpakt dat idee in een dramaturgische metafoor. [De wereld is, *dixit* Shakespeare, een toneel](https://en.wikipedia.org/wiki/All_the_world%27s_a_stage "'All the world's a stage', Wikipedia"), en onderwijs bereidt ons voor om de rollen te kunnen spelen die de wereld van ons verlangt.


Om de rol van een codereviewer te kunnen spelen, moet je weten wat er van een codereviewer wordt verlangd, hoe een goede code review eruit ziet. Code kunnen lezen, syntactische kennis van een programmeertaal hebben, is een noodzakelijke maar geen voldoende voorwaarde voor het kunnen beoordelen van een PR. -- Dat is waar ik me tijdens mijn eerste code review op stukbeet.


## Ongemak


Goed, dus ik deed niets. Na een tijdje vroeg de schrijver van het PR me: "En, heb je er naar kunnen kijken?" Ik zei: "Ja, ik denk dat het wel goed was." Hij zei: "Nou, keur 'm maar goed dan." En hij keek over mijn schouder mee terwijl ik op die grote groene knop klikte.


Ergens was dat goed -- want het bevestigde mijn status als teamlid. Het doopritueel was voltooid: bij dezen mocht ik een mening over de code hebben die door dit team werd geschreven. Ik had de rol van codereviewer gespeeld en dat betekende dat ik deze rol ook mocht spelen.


("Spelen" is een treffende term in deze context. Ik *was* nog geen codereviewer, ik had er slechts een gespeeld, gesimuleerd. Zoals kinderen die gezinnetje spelen, simuleren vader en moeder te zijn.)


Dat ik nog steeds niet wist wat er allemaal bij die rol kwam kijken, was geen bezwaar. Hoe een codereviewer zijn rol ook invult, één ding staat vast: zijn performance eindigt met een druk op een knop -- *Approve* of *Reject*. (Of *Waiting for Author* -- de werkelijkheid is altijd weerbarstiger dan de theorie.) Ik had in elk geval *dat* mogen ervaren.


Maar aan de andere kant was duidelijk dat ik nog een lange weg te gaan had, want ik kon niet onder woorden brengen hoe ik tot dat slotakkoord was gekomen. -- Kun jij dat wel?
