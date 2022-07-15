---
title: "Wat is jouw mentale model?"
author: "Karl van Heijster"
date: 2022-07-12T11:11:50+02:00
draft: true
comments: true
tags: ["code reviews", "mentaal model", "single-responsibility principe"]
summary: "Eerder schreef ik erover waarom het zo belangrijk is om code die data ophaalt te scheiden van code die data manipuleert. Ik kan me voorstellen dat ik lezers heb die denken: joh, dit zijn toch allemaal open deuren? Misschien hebben die lezers gelijk. Maar aan de andere kant: het aantal keren dat ik code heb kunnen verbeteren door het ophalen en manipuleren van data te scheiden, vertelt een ander verhaal. Misschien loont het zich om daarom kort te reflecteren op een aantal redenen waarom deze goede gewoonte niet stevig verankerd is in het hoofd van elke ontwikkelaar."
---

Eerder schreef ik erover [waarom het zo belangrijk is om code die data ophaalt te scheiden van code die data manipuleert] (LINK). De managementsamenvatting van die blog luidt als volgt:


*Schrijf je code niet zo:*


{{< gist dotkarl eb2b6cc84dd228200ecc277e88bfaded "GetAndMapSimultaneously.cs">}}


*Doe het liever zo:*


{{< gist dotkarl eb2b6cc84dd228200ecc277e88bfaded "GetAndMapSeparated.cs">}}


## Open deuren?


Ik kan me voorstellen dat ik lezers heb die denken: joh, dit zijn toch allemaal open deuren? Elke ontwikkelaar die ooit zijdelings iets van het [*Single-Responsibility Principe*](https://en.wikipedia.org/wiki/Single-responsibility_principle) (SRP)[^1] heeft meegekregen, weet toch dat je code niet twee dingen tegelijkertijd moet doen?


Misschien hebben die lezers gelijk. Maar aan de andere kant: het aantal keren dat ik code heb kunnen verbeteren door het ophalen en manipuleren van data te scheiden, vertelt een ander verhaal. Misschien loont het zich om daarom kort te reflecteren op een aantal redenen waarom deze goede gewoonte niet stevig verankerd is in het hoofd van elke ontwikkelaar.


## Waarom we niet scheiden


Een eerste mogelijkheid zou kunnen zijn: gebrek aan kennis. Misschien is niet elke ontwikkelaar zich even bewust van de problemen die schendingen van het SRP opleveren, verderop in de ontwikkelcyclus.  en [Deze](/blog/scheid-data-ophalen-van-data-manipuleren/) (en [deze](/blog/21/05/enums-switch-statements-en-solid-2/)) blog zou een bijdrage kunnen leveren aan een verhoging van het bewustzijn op dat gebied.


Misschien is het ook: druk van buitenaf. Veel stakeholders van softwareprojecten zijn over het algemeen in de eerste instantie geïnteresseerd in nieuwe features. Voor codekwaliteit interesseren ze zich in mindere mate - en meestal pas als het te laat is.[^2] Het is denkbaar dat ontwikkelaars de hete adem van stakeholders in hun nek voelen, en daarom genoegen nemen met code die werkt - of liever: *louter* werkt -, in plaats van code die geweldig is opgezet. 


Lieg niet: ik geloof dat iedereen zich hier wel eens aan heeft bezondigt. Eén van de grootste uitdagingen waar de programmeerwereld voor staat is het ontwikkelen van een professionele ethos die een ontwikkelteam in staat stelt om nee te zeggen tegen ongeduldige stakeholders. [Robert "*Uncle Bob*" Martin](http://cleancoder.com/) heeft daar uitgebreid over geschreven in [*The Clean Coder*](https://www.pearson.com/us/higher-education/program/Martin-Clean-Coder-The-A-Code-of-Conduct-for-Professional-Programmers/PGM8366.html) en [*Clean Craftmanship*](https://www.pearson.com/us/higher-education/program/Martin-Clean-Craftsmanship-Disciplines-Standards-and-Ethics/PGM2931928.html) - maar dat is niet waar ik het in deze blog over wil hebben. 


## Mentale modellen


Een derde mogelijkheid ontleen ik aan [Felienne Hermans](https://www.felienne.com/)' bespreking van [mentale modellen](https://en.wikipedia.org/wiki/Mental_model) in [*The Programmer's Brain*](https://www.felienne.com/). Misschien zien sommige ontwikkelaars het probleem van deze specifieke schending van het SRP niet, omdat hun mentale representatie van wat de code doet, dat niet toelaat.


Hermans' hanteert de volgende definitie van mentale modellen: een mentaal model creëert een abstractie in je [werkgeheugen](https://en.wikipedia.org/wiki/Working_memory) dat je kunt gebruiken in je redenering over een bepaald probleem. Wanneer we werken met het bestandsysteem van een computer, denken we bijvoorbeeld aan een groep bestanden een map. Maar in het echt is er natuurlijk geen sprake van bestanden en mappen die op een harde schijf zijn opgeslagen. Het mentale model van bestanden-in-mappen is een handige fictie die we kunnen gebruiken wanneer we ons afvragen waar we een bepaald bestand ook alweer hebben opgeslagen.


## Een analogie


Kijk nog eens naar de code waar ik deze blog mee begon. Als jij een samenvatting van deze code zou moeten geven, hoe zou die er dan uitzien? Met welke analogie zou je die code kunnen beschrijven? Welk verhaal vertel je over de code?


Ik zou me een ontwikkelaar voor kunnen stellen, die het als volgt zou omschrijven: 


> Ik verzamel alle spullen in deze doos (`repository.GetFoos()`), en als ze van mij zijn (`if (foo.SomeCondition)`), dan pak ik een rode sticker uit die doos (`repository.GetBars()`) en plak die erop (`r.Prop3 = bars`).


(En omdat ik mezelf nu eenmaal ben, stel ik me voor dat die ontwikkelaar in een pijnlijke scheiding ligt.)


# Implicaties


Wat impliceert die analogie over de code hierboven? Wie een doos doorzoekt, gaat niet eerst een keer alle spullen door om te kijken hoeveel rode stickers 'ie nodig heeft, om daarna nog een keer aan de gang te gaan om zijn spullen te beplakken. Het is in dat geval veel gemakkelijker om de rode sticker te pakken, zodra je één van je spullen tegenkomt.


De crux zit 'm in het feit dat de ontwikkelaar denkt dat het ophalen van de `bars` een eenvoudige operatie is, net als het pakken van een rode sticker. Maar precies op dat punt wijkt het mentale model af van de werkelijkheid. Want het ophalen van data uit een database is een relatief zware operatie.


## Een betere analogie


En dat wordt beter gevangen door de volgende analogie:


> Ik verzamel alle spullen in deze doos (`repository.GetFoos()`), en als ze van mij zijn (`if (foo.SomeCondition)`), dan ga ik naar de supermarkt om een rode sticker te halen (`repository.GetBars()`) en erop te plakken (`r.Prop3 = bars`). 


Een ontwikkelaar die zo redeneert, denkt wel twee keer na voordat 'ie data ophalen en data manipuleren met elkaar verknoopt! Zo'n ontwikkelaar zal éérst de doos met spullen doorlopen om te kijken hoeveel stickers hij nodig heeft, en pas als 'ie dát weet, naar de supermarkt vertrekken - en hij zal zijn code dan ook zodanig (her)schrijven.


## De werkelijkheid


Merk op dat die tweede - betere - analogie in belangrijke mate van de werkelijkheid afwijkt. Het verzamelen van spullen uit een doos en het gaan naar de supermarkt zijn in werkelijkheid twee totaal verschillende zaken. In de code, daarentegen, maken de acties die door die gebeurtenissen worden gerepresenteerd allebei gebruik van de `repository` om data op te halen. Zou die overeenkomst niet door het mentale model moeten worden gerespecteerd?


Het antwoord is: dat hangt ervan af wat het doel is van het mentale model. In dit geval wilde ik met deze analogie alleen maar duidelijk maken dat `repository.GetBars()` een zware operatie is, die je niet graag in een `for`-loop onderbrengt. Het klopt dat je datzelfde niet moet willen doen met `repository.GetFoos()`, maar omdat de oorspronkelijke code dat toch al niet deed, hoefde de analogie dat deel van de werkelijkheid niet getrouw na te bootsen.


Onthoud: een mentaal model is een abstractie. Als zodanig is het geen probleem als je niet-relevante delen van het werkelijke versluiert. De problemen ontstaan pas wanneer de abstractie relevante delen verkeerd weergeeft. En die discrepantie tussen model en werkelijkheid kan behoorlijk subtiel zijn.


## Hoe ontdek je verschillen?


De vraag is: hoe kom je erachter dat je mentale model afwijkt van de werkelijkheid? Om dat te kunnen achterhalen, moet je eerst weten (1) dát je een mentaal model hanteert, (2) dat deze af kan (en mag!) wijken van de werkelijkheid, en (3) dat het achterhalen van die discrepantie geen triviale taak is. Dat is de boodschap van deze blog.


Maar ik beken, ik heb geen pasklaar antwoord op die vraag. Het beste antwoord dat ik tot nu toe heb gevonden is: open zijn over hoe je code leest. Dat is de reden waarom ik tijdens *code reviews* veelal hardop nadenk over de code die ik tegenkom. (Zie ook [deze blog](/blog/22/01/code-reviews-als-leermiddel/).) 


Die openheid geeft de mogelijkheid tot een (drie)dubbel inzicht. Wanneer uit mijn commentaar blijkt dat mijn mentale model niet in lijn is met die van de schrijver van de code, dan betekent dat dat óf mijn model, óf dat van hem (of haar) gecorrigeerd moet worden - of dat we er allebei op relevante delen naast blijken te zitten. 


Onjuist mentale modellen kunnen lang blijven sluimeren. De beste manier om ze te corrigeren, is ze uit het domein van het mentale te trekken, de buitenwereld in.



[^1]: Het SRP is de eerste van de [SOLID-principes](https://en.wikipedia.org/wiki/SOLID) - en wat mij betreft de belangrijkste. Mijn eerdere blogs over dit onderwerp zijn [hier](/tags/single-responsibility-principe/) terug te lezen.


[^2]: Dat is overigens geen steek onder water naar stakeholders toe. Het is helemaal niet hun taak zich om codekwaliteit te bemoeien; dat is die van jou als ontwikkelaar!
