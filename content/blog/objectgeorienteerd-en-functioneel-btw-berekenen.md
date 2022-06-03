---
title: "Objectgeoriënteerd en functioneel BTW berekenen"
author: "Karl van Heijster"
date: 2022-05-28T11:22:38+02:00
draft: true
comments: true
tags: ["boeken", "functioneel programmeren", "objectgeoriënteerd programmeren", "ontwerppatronen", "performance"]
summary: "In het eerste hoofdstuk van Enrico Buonanno's *Functional Programming in C# (Second Edition)* demonstreert de auteur wat functionele features van C# aan de hand van een concreet voorbeeld: het berekenen van de BTW op een (lijst) product(en). Buonanno raadt de lezer aan om dezelfde functionaliteit ook op een objectgeoriënteerde manier te implementeren, om die oplossing te kunnen contrasteren met de zijne. Dus dat is precies wat ik heb gedaan."
---

In het eerste hoofdstuk van [Enrico Buonanno](https://twitter.com/la_yumba)'s [*Functional Programming in C# (Second Edition)*](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition) demonstreert de auteur wat functionele features van C# aan de hand van een concreet voorbeeld: het berekenen van de BTW op een (lijst) product(en). Buonanno raadt de lezer aan om dezelfde functionaliteit ook op een objectgeoriënteerde manier te implementeren, om die oplossing te kunnen contrasteren met de zijne. Dus dat is precies wat ik heb gedaan.


## Aanpak


Het idee is als volgt: stel, je hebt een webwinkel die internationaal goederen verzendt. Je hanteert een vaste prijs voor elk product, en bovenop die prijs komt de BTW van het land waar je de bestelling naartoe verzendt.


Bij het berekenen van BTW, moeten de volgende drie scenario's worden onderkend. 


1. Sommige landen hanteren een uniform BTW-tarief voor elk product. Voor deze landen is het berekenen van de BTW triviaal: je doet de prijs van het product keer het BTW-tarief. Italië en Japan zijn twee voorbeelden van landen waar dit voor geldt.[^1]

2. Andere landen hanteren een ander tarief afhankelijk van het soort product. Er is één (doorgaans lager) tarief voor voedsel, en één tarief voor andere goederen. In zulke gevallen moet je eerst nagaan met wat voor soort product je van doen hebt, voordat je de BTW kunt berekenen. Duitsland is een land met zo'n tarief.

3. Ten slotte zijn er landen waarin de BTW afhankelijk is van de regio. Voor zulke landen moet je eerst nagaan bij welke regio het gekochte product hoort, om het juiste tarief te kunnen bepalen. De Verenigde Staten is een voorbeeld van zo'n land, daar bepalen de staten het tarief. 


Ik ging als volgt te werk. Ik heb eerst Buonanno's oplossing overgenomen ter referentie. Daarna heb ik middels Test-Driven Development (TDD) de verschillende scenario's stuk voor stuk opnieuw gecodeerd in een objectgeoriënteerde stijl.


N.B. Het Engelse equivalent van BTW (belasting toegevoegde waarde) is VAT (*value added tax*). In het vervolg van deze blog zal ik de Engelse afkorting gebruiken, om in lijn te zijn met de code.


## Domeinmodel


Dit is het achterliggende domeinmodel:


{{< gist dotkarl fffbe14591ef1852bf7c8ba6dccd7b2e "Model.cs">}}


In het `Address`-type is het land vastgelegd waar een bestelling naartoe wordt verzonden. Voor de Verenigde Staten geldt dat ook de staat wordt vastgelegd (in het `UsAddress`-type). Dit is om scenario 3 te kunnen ondersteunen.[^2]


Een `Product` bestaat uit een naam en een prijs. Daarnaast heeft dit type een `boolean` die vastlegt of het om voedsel gaat of niet. Dit is om scenario 2 te kunnen ondersteunen.


In een `Order` is de bestelling vastgelegd die naar een bepaald land moet worden verscheept. Om het model eenvoudig te houden, is er uitgegaan van het versimpelde scenario waarin je maar één soort `Product` per keer kan bestellen. De hoeveelheid `Products` is daarentegen wel vrij.


## De functionele oplossing


Dit is Buonanno's oplossing:


{{< gist dotkarl fffbe14591ef1852bf7c8ba6dccd7b2e "FunctionalVatCalculator.cs">}}


Ter contrast, dit is die van mij:


{{< gist dotkarl fffbe14591ef1852bf7c8ba6dccd7b2e "ObjectOrientedVatCalculator.cs">}}


De logica om de VAT te berekenen delegeer ik naar de `ICalculateRate`-implementaties. Hoe die logica er voor elke [*strategy*](https://en.wikipedia.org/wiki/Strategy_pattern) uitziet, kan van de oorspronkelijke oplossing worden afgekeken.


## Wat valt op?


Enkele observaties, in min of meer willekeurige volgorde. 


- De functionele oplossing bevat in totaal minder regels code dan de objectgeoriënteerde. Het is waar, mijn class, in isolatie bekeken, is kleiner, maar ik heb mezelf dan ook de luxe gepermitteerd om wat logica naar andere classes te delegeren. Als je die erbij op zou tellen, dan wint Buonanno's oplossing het qua grootte.

- Eén van de redenen waarom de functionele oplossing zo klein kan blijven, is het gebruik van de [`=>`-syntax](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-operator) om functies te declareren. Dat is mogelijk, omdat elke functie ofwel slechts één regel code bevat, ofwel een [switch expression](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/switch-expression). Zelf maak ik gebruik van de iets meer *verbose* `{`-notatie. Voor een groot deel is dat conventie. Merk op dat ook mijn methods eenvoudig om kunnen worden geschreven naar *oneliners*.

- Geen enkele functie - zowel de functionele als de objectgeoriënteerde - maakt gebruik van method-variabelen; ze berekenen het resultaat en retourneren dat onmiddellijk. In functionele talen is dat heel gebruikelijk om te doen. De objectgeoriënteerde oplossing maakt wel gebruik van class-variabelen, maar ook dat is deels conventie. De `address`- en `order`-parameters zouden in dit geval net zo goed in de method meegegeven kunnen worden, in plaats van [constructor](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/constructors). 

- Als gevolg hiervan kan de functionele oplossing zuiver statisch blijven. De [`static`-modifier](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/static) is op alle niveaus van toepassing: van class tot functie. Ook dat is typisch voor functioneel programmeren. In de objectgeoriënteerde wereld wordt het gebruik van `static` juist veelal afgeraden, omdat dit niet altijd even goed samengaat met het componeren van objecten.[^3] De objectgeoriënteerde oplossing is dan ook niet statisch. (Al zou hij, ook nu weer, eenvoudig om geschreven kunnen worden om wel zo te zijn.)

- De functionele oplossing maakt geen gebruik van een ontwerppatroon. Alle logica zit bij elkaar in één class. De objectgeoriënteerde oplossing hanteert daarentegen het *Strategy*-patroon om de code beheersbaar te houden. Is dat een ontwerpkeuze die inherent is aan het ene of het andere paradigma? Daar ben ik nog niet over uit. Mijn kennis buiten de [objectgeoriënteerde denkwijze](/blog/21/07/objectgeorienteerd-denken/) reikt nog niet ver genoeg om iets over functionele ontwerppatronen te durven zeggen.


Wat valt jou op aan beide oplossingen? Welke heeft je voorkeur? En waarom?


## Benchmarks


Tot zover de esthetische vergelijking. Omdat ik graag grondig ben (en omdat ik de infrastructuur er al voor klaar had staan), heb ik ook wat benchmarks gedraaid om beide oplossingen op performancegebied te kunnen vergelijken.


Als we naar de snelheid kijken, dan zien we dat de functionele oplossing over het algemeen iets sneller is:


|                     Method | Gemiddelde | Foutmarge | Standaardafwijking |
|--------------------------- |-----------:|----------:|-------------------:|
|     CalculateVatFunctional |   234.7 ns |   4.70 ns |           13.33 ns |
| CalculateVatObjectOriented |   295.5 ns |   5.91 ns |            9.02 ns |
<br>


Maar, en dat moet er echt bij gezegd, het gaat hier om een verschil van ongeveer 60 *nano*seconden. En dat is in de echte wereld eenvoudigweg een verwaarloosbaar verschil. Ik zou op basis van deze benchmarks in elk geval niet durven beweren dat functionele oplossingen merkbaar beter zijn in performance dan objectgeoriënteerde.


(Een belangrijke kanttekening daarbij is echter wel dat functionele oplossingen over het algemeen beter paralelliseerbaar zijn dan objectgeoriënteerde. Dat komt doordat functionele oplossingen geen gebruik maken van (muteerbare) variabelen. Daardoor kan het werk eenvoudig over meerdere threads verdeeld worden, zonder dezelfde risico's die objectgeoriënteerde code daarbij loopt.) 


Ook als we naar het gehgeugengebruik kijken, dan zien we dat de functionele oplossing opnieuw punten scoort:


|                     Method |  Gen 0 | Gen 1 | Gen 2 | Allocated |
|--------------------------- |-------:|------:|------:|----------:|
|     CalculateVatFunctional |      - |     - |     - |         - |
| CalculateVatObjectOriented | 0.0820 |     - |     - |     344 B |
<br>


344 bytes zijn echt geen aantallen waar de typische ontwikkelaar zich druk over hoeft te maken, dus in die zin is er niets mis met de objectgeoriënteerde oplossing. Maar eerlijk is eerlijk: de functionele oplossing heeft helemáál geen gebruik hoeven maken van de [*garbage collector*](https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/), en dat is nog iets netter. Het verschil is ook logisch en verklaarbaar, want de functionele aanpak maakt geen gebruik van variabelen waar geheugen voor gereserveerd moet worden.


De conclusie is eenduidig: hoewel beide oplossingen dicht bij elkaar liggen, komt de functionele oplossing op het vlak van performance als winnaar uit de bus.


## Kanttekeningen


Is daarmee alles gezegd over dit experiment? Natuurlijk niet.


Mijn aanpak had een in het oog springend nadeel, en dat is dat ik in mijn nieuwe oplossing wat van Buonanno's functionele oplossing meeneem. Concreet: het gebruik van records voor het model en het gebruik van de `UsAddress`-class. 


Het eerste punt is niet per definitie problematisch. Het model wordt met name gebruikt om enkele testobjecten te kunnen definiëren - en dat gebeurt per test maar één keer. Deze objecten hoeven daarom niet per se muteerbaar te zijn. 


De vraag werpt zich natuurlijk wel op: had ik, als ik van nul af aan was begonnen, ook voor *immutable* objecten gekozen? Dat durf ik niet te zeggen. Een vervolgvraag is dan: als ik de `Product`-class als muteerbaar object zou hebben gedefinieerd, zou ik dan geneigd zijn om een `VatRate`-property of iets dergelijks erop te definiëren? Dat zou mijn eigen oplossing substantieel van die van Buonanno doen verschillen. 


Je kunt je voorstellen dat je de code zodanig implementeert dat het *strategy*-patroon wordt gebruikt op in `Product`-class zelf - een *waarlijk* objectgeoriënteerde oplossing. Ik speel met het idee om in een toekomstige blog zo'n oplossing te schrijven en het experiment opnieuw te doen.


Het tweede punt is minder problematisch, denk ik. Buonanno introduceert de `UsAddress`-class om te kunnen demonstreren dat je een type-check in een `switch expression` kunt gebruiken. Zelf maak ik niet van deze functionaliteit gebruik (hoewel ik mijn oplossing eenvoudig aan zou kunnen passen om dat wel te doen - en het ontwerp er niet per se onder zou leiden). In die zin heeft deze ontwerpkeuze mijn objectgeoriënteerde implementatie dus niet beïnvloed.


## Conclusie


Ik zal geen grootscheepse conclusies presenteren over functionele of objectgeoriënteerde programmeerstijlen - daar is het nog veel te vroeg voor. 


Wat ik wel al durf te concluderen is dit: *Functional Programming in C# (Second Edition)* is een razendinteressant boek dat je op een nieuwe manier naar je code doet kijken. Hoewel ik het boek nog lang niet uitheb, durf ik het nu al aan alle nieuwsgierige C#-ontwikkelaars aan te raden. 


Het is goed om ingesleten patronen van tijd tot tijd tegen het licht te houden en jezelf af te vragen: waarom doe ik het eigenlijk *zo*? Buonanno's boek stimuleert het in slaap gesukkelde ontwerpgedeelte van je ontwikkelaarsbrein met verve.


O, en de code is terug te vinden op [GitHub](https://github.com/dotkarl/RefactorExercises/tree/master/RefactorExercises/VAT) voor de geïnteresseerde lezer.


[^1]: Ik moet je bekennen dat ik helemaal niet weet of wat ik hier zeg daadwerkelijk geldt voor al die landen. Buonanno neemt ze als voorbeeld en ik neem ze over, want ik geloof Buonanno op zijn blauwe ogen.


[^2]: Doorgaans bestaat een adres uit meer dan alleen een land natuurlijk, maar om het voorbeeld zo eenvoudig mogelijk te houden, is hier alleen de noodzakelijke informatie vastgelegd. Buonanno merkt overigens wel op dat je een minimaal `Address` zoals hierboven beschreven zou kunnen hanteren voor specifieke delen van je applicatie, die alleen deze informatie nodig hebben - het deel dat BTW berekent, bijvoorbeeld.


[^3]: Buonanno is overigens niet overtuigd van de rechtvaardigheid van de objectgeoriënteerde afkeer van `static`. Daar wil ik in een latere blog nog op terugkomen!
