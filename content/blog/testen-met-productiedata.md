---
title: "Testen met productiedata"
author: "Karl van Heijster"
date: 2023-02-03T08:30:13+01:00
draft: true
comments: true
tags: ["documentatie", "intentie van code", "testen"]
summary: "Laatst kwam ik een test tegen die checkte of een bepaald object 48 keer voorkwam in een lijst. Het was een hartstikke valide test, verder, daar niet van. Maar hij riep wel de vraag op: waarom 48 keer? Wat was er namelijk gebeurd: de schrijver van de test had wat data van de productieomgeving geplukt en daar een test omheen gebouwd - *et voilà*: hij had bewezen dat de feature werkte als verwacht. Er valt wat op die werkwijze af te dingen, natuurlijk. En omdat ik nu eenmaal ik ben, ga ik dat nu doen."
---

Laatst kwam ik een test tegen die checkte of een bepaald object 48 keer voorkwam in een lijst.


Het was een hartstikke valide test, verder, daar niet van. Maar hij riep wel de vraag op: waarom 48 keer?


Wat was er namelijk gebeurd: de schrijver van de test had wat data van de productieomgeving - liefkozend "*PROD*" genoemd - geplukt en daar een test omheen gebouwd - *et voilà*: hij had bewezen dat de feature werkte als verwacht.


## Voordelen


En eerlijk is eerlijk: die werkwijze heeft zo zijn voordelen. 


De eerste is: snelheid. Door je testdata ergens vandaan te halen, hoef je niet na te denken over hoe die eruitziet. Het scheelt je denkwerk, en het scheelt je tijd. Je bent immers veel minder tijd kwijt aan het handmatig vormgeven van de die data. Alle tijd die je niet daaraan hoeft te besteden, kun je besteden aan het schrijven van een goede test.


Het tweede voordeel: representativiteit. Met de hand geboetseerde testdata brengt een risico met zich mee. Wanneer je testdata te zeer afwijkt van de productiedata, geven je tests een vertekend beeld van de werking van het systeem. Door *PROD* te gebruiken als bron voor je testdata, ben je ervan verzekerd dat je systeem om kan gaan met *the real deal*. 


## Toevallig


Maar er valt wat op die werkwijze af te dingen, natuurlijk. En omdat ik nu eenmaal ik ben, ga ik dat nu doen. Laten we beginnen met het idee dat productiedata je tijdwinst oplevert.


Ik ben er een groot voorstander van tests te zien als documentatie. (Zie met name [deze](/blog/22/09/tests-als-documentatie/), maar ook [deze](/blog/22/06/testen-via-de-voordeur/), [deze](/blog/22/09/test-driven-code-reviews/), [deze](/blog/22/12/over-de-volgorde-van-je-unit-tests/) en [deze](/blog/22/12/tests-zijn-specs/) blog.) Eén van de belangrijkste richtlijnen bij het schrijven van documentatie is: zorg dat deze makkelijk leesbaar is. Immers, moeilijk leesbare documentatie *zal niet gelezen worden*, en verliest zo al haar waarde. Dat is waarom ik eerder schreef: [optimaliseer tests voor leesbaarheid, niet voor onderhoudbaarheid](WAAROM_DRY_WAAROM_DAMP).


Testdata van *PROD* is maar zelden geoptimaliseerd voor leesbaarheid. Zulke data heeft vaak veel toevallige eigenschappen die niet bijdragen aan het begrip van de test. 


Ze bevatten bijvoorbeeld data waar je in je test niets mee doet. "Wat is het probleem?" denk je misschien. "De test leidt daar toch niet onder? Die negeert de data immers!" En dat is waar. Maar de lezer van de test negeert die data niet. Althans, de eerste keer dat 'ie de test leest, negeert 'ie die data niet. Pas nadat de lezer begrepen heeft waar de test om draait, zal deze snappen: "O, ik moet op *dit* deel van de data letten, niet op *dat*!" 


De tijd die je hebt gewonnen met tijdens het schrijven van de test, voeg je toe van de tijd die je besteed aan het lezen van de tests. En omdat code - alle code, ook tests - nu eenmaal vaker worden gelezen dan geschreven, maak je netto verlies.


## Complexiteit


Maar zelfs de data waar je wél iets mee doet, draagt niet per se bij aan het begrip van de test. Ga maar na: moet ik echt 48 objecten in een lijst stoppen, om er zeker van te zijn dat de code goed met lijsten om kan gaan? 


Nee, natuurlijk niet. Om zeker te weten dat je code een lijst goed verwerkt, heb je niet meer dan drie scenario's nodig: een lijst met nul waarden, met één waarde, en een lijst met twee waarden. 0, 1 of veel - daarmee is zijn de testscenario's van een lijst uitputtend beschreven.[^1]


Trouwens, meer dan twee waarden in je lijst stoppen brengt zelfs een risico met zich mee. Want wat als de derde lijstwaarde - of de tiende, of de 47e - een programmeerfout bevat? Hoe groter de lijst, hoe moeilijker het is om de bug te achterhalen. Ook hier geldt weer: alle aanvankelijke tijdwinst gaat verloren aan de complexiteit die je toevoegt.


Wanneer je je testdata uit de *PROD* haalt, dan maak je - bewust of onbewust - een keuze: je kiest voor representativiteit bóven leesbaarheid. Dat kan een valide afweging zijn. Maar dat is het meestal niet.


## Representatief


En trouwens, ook op het representativiteitsargument valt wat af te dingen. Productiedata is representatief voor de data die het systeem zal verwerken, ja, maar daar volgt niet uit dat handgeboetseerde testdata *niet* representatief is. 


De truc is: baseer je bij het construeren van je testdata op productiedata, maar geef je die op zo'n manier vorm dat het de leesbaarheid ten goede komt. Zorg ervoor dat je objecten dezelfde eigenschappen hebben als *the real deal*, maar haal alles weg wat niet bijdraagt aan het begrip van de test.


Een voorbeeld. TypeScript kent, anders dan C#, geen `Guid`-type. De ID's van onze objecten aan de front-end zijn daarom van het type `string`. Ik zie mijn collega's in hun tests die ID's vaak vullen met iets als `'objectId'`. Maar dat is niet representatief voor de data die van de back-end komt - daar zijn de ID's namelijk wél `Guid`s. Dus vul ik de ID's in die tests met een hardgecodeerde unieke identifier: `'cea5b28f-d09f-44c8-bde9-76dfa64a9b7d'`.[^2]


Nu komt het (gelukkig!) nooit - of zeer zelden - voor dat de code aan de front-end breekt als de ID's niet een bepaalde vorm hebben. Maar dat is het punt ook niet. De tests slagen óók met een normale string, maar met een unieke identifier geven ze een representatiever beeld van hoe de code in productie zal werken.


## Investeren


Productiedata is over het algemeen slechte testdata. Maar het is niet zo dat beide niets met elkaar van doen hebben. Productiedata is een uitstekende inspiratiebron voor testdata - maar die data moet wel altijd door de schrijver van een test geoptimaliseerd worden voor het begrip van de test.


Wie de tijd neemt om te investeren in de vormgeving van testdata, krijgt dat dubbel en dwars terugbetaald - in snelheid, leesbaarheid én representativiteit.





[^1]: Let wel: ik heb het hier over *functionele* tests. Bij performancetests is het bijvoorbeeld wél zinvol is om grotere lijsten te gebruiken als testdata.

[^2]: [www.guidgenerator.com](https://www.guidgenerator.com/online-guid-generator.aspx) is mijn grootste vriend bij front-end tests!
