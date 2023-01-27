---
title: "Waarom DRY? Waarom DAMP?"
author: "Karl van Heijster"
date: 2023-01-27T08:29:31+01:00
draft: true
comments: true
tags: ["code lezen", "communicatie", "DRY", "testen", "presenteren"]
summary: "Productiecode optimaliseer je voor onderhoudbaarheid; testcode voor leesbaarheid. Waarom? Omdat de context van productiecode en testcode verschilt. Beide dienen een ander doel, wat verschillende eisen aan de code stelt. Ze opereren in verschillende sferen, zogezegd. "
---

Elke zondag maak ik een ochtendwandeling - [ook weer zo'n nieuwe gewoonte, dit jaar](/blog/23/01/met-atomic-habits-het-nieuwe-jaar-in/). Onder het wandelen oefen ik de presentatie dat ik [in februari](https://www.meetup.com/nimma-codes-meetup-group/events/287692035/) ga geven bij [Nimma.Codes](https://www.nimma.codes/). In de buurt van mijn huis ligt een bedrijventerrein dat op zondagochtend voor mij verlaten genoeg is om niet op te vallen als in zichzelf brabbelende gek. 


De presentatie gaat over tests als documentatie, een onderwerp waar ik op deze blog al vaker over geschreven heb ([hier](/blog/22/09/tests-als-documentatie/), bijvoorbeeld). Het hardop uitspreken van die presentatie is dan ook niet per se om de inhoud ervan nogmaals te overdenken, maar om mijn mond te trainen de juiste dingen op het juiste moment te zeggen. 


Het is wonderlijk om erachter te komen hoe groot de vertaalslag soms kan zijn, van iets wat volslagen helder is in je hoofd naar een enigszins lopende volzin. Het schrijven is natuurlijk een manier om dat begrip concreet te maken. Maar iets op kunnen schrijven en iets uit kunnen spreken zijn twee verschillende dingen, bleek al tijdens mijn eerste wandeling al snel.


## Inzicht


En toch, ondanks dat die wandelingen niet bedoeld zijn om tot inhoudelijke inzichten te komen, is dat wel een welkom bijproduct. Eén van de punten die ik in mijn presentatie maak, is dat je productiecode het principe van DRY moet honoreren - *don't repeat yourself* -, maar dat dit niet per se voor je testcode geldt. Voor je tests geldt DAMP: gebruik *descriptive and meaningful phrases*.


Terwijl ik in mezelf brabbelde, viel me in een ondeelbaar moment in waarom dat het geval is. Het was kennis die zich al langer in mijn hoofd bevond, maar waar ik de woorden nooit eerder voor had gevonden. 


*Productiecode optimaliseer je voor onderhoudbaarheid; testcode voor leesbaarheid.*


Waarom? Omdat de context van productiecode en testcode verschilt. Beide dienen een ander doel, wat verschillende eisen aan de code stelt. Ze opereren in verschillende sferen, zogezegd. 


## Verandering


Productiecode is constant aan verandering onderhevig. Als ontwikkelaar leer je voortdurend nieuwe dingen - denk aan nieuwe *language features* en programmeertechnieken, of nieuwe *libraries* die bepaalde functionaliteit voor je overnemen. Elke ontwikkelaar komt tijdens zijn werk oude code tegen - niet zelden door jezelf geschreven! -, waarvan je denkt: oei, dat moet beter. En in gezonde teams bestaat de ruimte om die verbetering snel door te voeren. Productiecode wordt constant gerefactord.


Je doet ook nieuwe inzichten op over het domein waar je in werkt. Dat wat voorheen één concept leek - uitgeprogrammeerd in één daarmee corresponderend object -, blijkt bij nadere inspectie toch twee verwante maar welonderscheiden ideeën te herbergen. Dus pas je de code aan om dat nieuwe inzicht te weerspiegelen. Je begrip van het domein is geen statisch gegeven - en de code dus ook niet. Productiecode wordt constant verfijnd om nieuwe (of: nieuw ontdekte) requirements te kunnen ondersteunen.


In zo'n context is het essentieel om DRY te honoreren. Als je je code continu aan moet passen, dan wil je dat niet elke keer op twaalf verschillende plekken hoeven doen. Elk concept - elke eenheid aan informatie - dient één plek te hebben in de codebase. Als de code die dat concept representeert om wat voor reden dan ook gewijzigd moet worden, dan moet dat alleen op die ene plek gebeuren.


## Denkwerk


Testcode - althans: goed geschreven testcode - verandert veel minder vaak. [In de tests zijn de specificaties van het systeem gecodeerd](/blog/22/12/tests-zijn-specs/). Die kun je op talloze verschillende manieren implementeren (en als je continu refactort, dan doe je dat ook), zonder dat dat ook maar enige impact heeft op de specificaties *an sich*. De gouden standaard van goede testcode is dan ook: code die niet hoeft te worden aangepast, zelfs al gooi je de implementatie helemaal om. Daarom hoeft testcode ook niet voor onderhoudbaarheid te worden geoptimaliseerd. 


Voor tests geldt: het is belangrijker dat duidelijk is wat de specificatie is, dat de specificatie makkelijk te begrijpen is. Je moet je ogen kunnen laten glijden over een goed geschreven test, en dan precies weten wat er aan de hand is. Het denkwerk van de lezer moet geminimaliseerd worden. Als een test faalt, dan moet in één oogopslag duidelijk zijn welke functionaliteit is omgevallen. 


Een ontwikkelaar die bekend is met de codebase kan daar al vaak uit afleiden waar het probleem zit. En een ontwikkelaar die na elke wijziging de tests aftrapt, weet al waar het probleem zit, namelijk in zijn laatste wijziging. Diegene hoeft alleen maar de test te lezen om erachter te komen wat er aan die wijziging scheelt.


Als je DRY toepast op je test, dan tast je de leesbaarheid van de tests aan. Een lezer zal dan de waarden van verschillende variabelen in zijn hoofd moeten houden, om de test te kunnen begrijpen, of moeten zoeken naar de precieze invulling van een testobject om erachter te komen welke input bij welke output hoort.


In zo'n context kun je je heus wel wat codeduplicatie permitteren. Het is belangrijker dat je snel de oorzaak van een falende test kan achterhalen, dan dat je die test van het ene op het andere moment kunt omschrijven. Dat krijg je voor elkaar met DAMP.


## Duplicatie


Begrijp me niet verkeerd, het is niet zo dat je productiecode geen enkele codeduplicatie mag bevatten, of dat het schrijven van tests uit weinig anders bestaat dan code knippen en plakken. Ik spreek met reden van "optimaliseren", en niet van "coderen überhaupt".


Productiecode mag DRY schenden als twee welonderscheiden concepten *nu nog* dezelfde implementatie kennen, maar verschillen in hun mate van verandering. Je komt die situatie wel vaker tegen bij het ontwerpen van een UI, bijvoorbeeld. Een scherm voor beheerders en een scherm voor eindgebruikers kunnen in de eerste versie van een applicatie nog nagenoeg identiek zijn. Maar beheerders en eindgebruikers hebben heel andere wensen en behoeften. Als je op voorhand al weet dat beide schermen in de tweede versie al uit elkaar gaan lopen, dan kan het geen kwaad om in de eerste versie wat duplicatie te introduceren.


En hoewel productiecode veel vaker verandert dan goed geschreven testcode, volgt daar absoluut niet uit dat je je tests niet hoeft te onderhouden. Integendeel, als je betere manieren vindt om je tests vorm te geven, dan moet je die kans niet laten schieten. Tests verdienen net zo goed zorg en aandacht van ontwikkelaar als productiecode.


## Relevantie


Een testsuite die uit zijn voegen barst van codeduplicatie is een slechte testsuite - geen discussie. Het heet DAMP, en niet WET - en dat is niet voor niets. Je dient alleen codeduplicatie te introduceren in je tests als het hun leesbaarheid ten goede komt.


Je kunt de informatie in je test onderverdelen in ruwweg twee cateogorieën: dat wat belangrijk is voor het begrip van de test, en dat wat noodzakelijk is om de test draaiend te krijgen. Of, anders gezegd: de data en de infrastructuur.


Stel, je hebt een class `C` die een input `I` omzet naar een output `O`. De constructor van `C` vraagt om drie afhankelijkheden: `D1`, `D2` en `D3`. Je zou zo'n test als volgt kunnen schrijven:


```cs
[TestMethod]
public void GivenI_WhenConvertedByC_ThenReturnsO() 
{
    // Arrange
    var d1 = new D1();
    var d2 = new D2();
    var d3 = new D3();
    var sut = new C(d1, d2, d3);
    var i = new I();

    // Act
    var o = sut.Convert(i);

    // Assert
    o.Should().BeOfType<O>();
} 
```


Stel dat ik een stuk of tien tests wil schrijven voor class `C`, waarbij ik steeds een variatie op `I` meegeef als parameter, moet ik dan elke keer opnieuw die afhankelijkheden specificeren en injecteren? Natuurlijk niet! In dit geval zou je wel gek zijn als je hier niet DRY zou hanteren:


```cs
[TestMethod]
public void GivenI_WhenConvertedByC_ThenReturnsO() 
{
    // Arrange
    var i = new I();

    // Act
    var o = GetC().Convert(i);

    // Assert
    o.Should().BeOfType<O>();
} 
```


Maar hoewel ik de instantiatie van `C` weg zou abstraheren naar een *factory*, zou ik datzelfde niet per se doen voor de instantiatie van `I`. Waarom? Omdat de manier waarop `I` geïnstantieerd wordt belangrijk is voor het begrip van de test. Voor `C` geldt dat niet. Ik ben niet geïnteresseerd in de details van hoe die is opgebouwd. Van deze class hoef ik alleen maar aan te nemen dat 'ie correct functioneert.


(Maar let op: als ik `C` verschillende soorten afhankelijkheden mee zou kunnen geven, die het gedrag van de class op een relevante manier beïnvloeden, dan zou ik die afhankelijkheden wél expliciet in mijn tests terug laten komen.)


## DRY tenzij


De crux zit 'm in de manier waarop de code duidelijk maakt wat de test doet. De eerste drie letters van DAMP zijn met zorg gekozen: "*descriptive and meaningful*" - voor het begrip van de test dus. Je dient codeduplicatie in je tests te vermijden, net als bij productiecode - *tenzij* het de leesbaarheid ten goede komt.



Productiecode optimaliseer je voor onderhoudbaarheid: DRY. Testcode optimaliseer je voor leesbaarheid: DAMP, oftewel DRY tenzij.
