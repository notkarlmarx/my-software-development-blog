---
title: "Tests als vangnet"
author: "Karl van Heijster"
date: 2022-09-23T08:29:41+02:00
draft: false
comments: true
tags: ["clean code", "end to end tests", "integratietests", "ontwerppatronen", "refactoren", "testen", "teststrategie", "unit tests"]
summary: "Tests zijn een vangnet. Elke keer dat je code aanraakt - en dat doe je continu -, dan speel je een balanceeract. Als je code blijft functioneren zoals bedoeld, blijf je op het koord. Zo niet, dan val je. En als je valt, heb je een keus: te pletter vallen, of opgevangen worden door een vangnet. Tests zijn je vangnet, je afgrond is - ontevreden ontwikkelaars, stakeholders, eindgebruikers."
---

> ## TL;DR
>
> Goede code wordt constant gerefactord. Tests dienen als vangnet bij het refactoren van code.
>
> Om deze functie optimaal te kunnen vervullen, moet de testsuite zodanig worden ontworpen dat deze de interface van code test, en niet de implementatie.
>
> Een consequentie hiervan is dat je softwarearchitectuur je teststrategie bepaalt. Eenvoudige CRUD-applicaties zullen meer *End to end*- en integratietests kennen. De testsuite van complexere applicaties met een grotere focus op businesslogica, zal vooral uit unittests bestaan. 


Sommige mensen zeggen: tests zijn de steigers die je helpen een gebouw te doen verrijzen. - Alleen breek je ze nooit af.


Het is een uitvloeisel van de metafoor van een software ontwikkelen als projectontwikkelen: - een junior softwareontwikkelaar als constructiemedewerker, de senior als ingenieur.[^1]


Ik zeg liever: tests zijn een vangnet. Elke keer dat je code aanraakt - en dat doe je continu -, dan speel je een balanceeract. Als je code blijft functioneren zoals bedoeld, blijf je op het koord. Zo niet, dan val je. 


En als je valt, heb je een keus: te pletter vallen, of opgevangen worden door een vangnet. Tests zijn je vangnet, je afgrond is - ontevreden ontwikkelaars, stakeholders, eindgebruikers.


## Refactoren


Goede code heeft een korte halfwaardetijd. 


Dat klinkt als een tegenintuïtieve opmerking, ik weet het. Zou goede code niet tegen de tand des tijds bestand moeten zijn? - Nee, want die code is geschreven met de kennis van *dat* moment. Met het verstrijken van de tijd dienen zich onvermijdelijk nieuwe inzichten aan. (En trouwens, ook de snelle veranderingen in het IT-landschap doen elke hoop op de eeuwigheidswaarde van je code teniet.)


Goede code absorbeert die inzichten zo snel en gemakkelijk mogelijk. De best mogelijke codebase is niet een codebase die perfect ontworpen is - het is een codebase die constant wordt aangepast om tegemoet te komen aan nieuwe inzichten. Continue refactoring is het ultieme teken van gezonde code, onderhouden door een goed functionerend team.


En dat is onmogelijk zonder een goede testsuite. - Dat is geen hyperbool. Refactoren zonder tests is een riskante onderneming, dat weet elke ontwikkelaar. Zonder vangnet worden ontwikkelaars terughoudend om te refactoren. 


Het gevolg laat zich raden: de code begint eerst te stinken en vervolgens te rotten. Nieuwe features worden *ad hoc* geïmplementeerd om de bestaande functionaliteit niet per ongeluk om te gooien. Met elke dag die verstrijkt, wordt de codebase moeilijker onderhoudbaar.


Zonder steigers is het niet mogelijk een goed gestructureerd gebouw te doen verrijzen. Zonder vangnet denk je wel twee keer na voordat je gaat koorddansen.


## Een ontwerp


Maar het hebben van een testsuite alléén is niet voldoende om continu te kunnen refactoren. Niet elke testsuite is immers ontworpen op zo'n manier dat het deze taak optimaal vervult. Integendeel, het is mogelijk - makkelijk, zelfs - om een testsuite te ontwerpen die het refactoren eerder belemmert dan bevordert.


Hoe zou zo'n testsuite eruit zien, denk je?


Stel, je codeert een nieuwe class, `a`. Daar moet je tests voor hebben, natuurlijk. Dus je definieert een class `aTest`. Logisch, toch? 


\- Oké, stel je hebt ook een class `b`. `b` heeft een afhankelijkheid naar `c` en `c` heeft er een naar `d`. Welke testclasses definieer je allemaal? Laten we achteraan beginnen. `dTest` schrijft zichzelf haast. Om `cTest` te kunnen schrijven, hebben we zowel een afhankelijkheid naar `c` als `d` nodig. Oké, geen probleem. En om `bTest` te kunnen schrijven, hebben we `b`, `c` en `d` nodig.


## Problemen


Probeer eens een afhankelijkheidsdiagram te tekenen van het ontwerp van deze testsuite. (Nota bene, óók testcode is ontworpen code!) Hoe overzichtelijk is dat overzicht? Kun je wegwijs worden uit het aantal pijlen? - Bedenk dat we hier nog maar een eenvoudige hiërarchie gedefinieerd hebben! Hoe zou dit ontwerp schalen naar complexere structuren?


Maar de complexiteit is niet eens het grootste probleem. Want wat gebeurt er wanneer je je code besluit te refactoren? Als je `a` omgooit, niet zoveel gelukkig. Maar wat als `d` eraan moet geloven? Zo'n wijziging heeft invloed op `dTest` én `bTest` en `cTest`. Een wijziging in de productiecode zal gepaard gaan met een wijziging in de testcode.


Waarom? Omdat de productie- en de testcode te sterk aan elkaar gekoppeld zijn. - Inderdaad, niet alleen in de wereld van productiecode levert *strong coupling* problemen op; dat geldt net zo zeer voor de verhouding tussen productiecode en haar tests. 


Een andere manier om dit te verwoorden is: de tests testen de implementatie, niet het interface. Maar de implementatie is precies dat deel van de code dat een korte halfwaardetijd heeft. 


## Oplossing


De oplossing laat zich raden: ontkoppel de tests van je productiecode. Anders gezegd: test niet de implementatie, maar de interface. Of: test niet via de achterdeur, maar [via de voordeur](/blog/22/06/testen-via-de-voordeur/). 


Kies een logisch *entry point*. Zorg dat je ver genoeg van het metaal verwijderd bent om moeiteloos te kunnen refactoren, maar niet zo ver dat een wijziging in het gedrag van de code in geen enkele test meer boven komt drijven.


Merk op dat er een verschil is tussen het aantal regels code dat je test raakt, en het aantal regels code dat je *test*. Je test kan honderden regels code hebben uitgevoerd vóórdat je bij die ene regel aankomt waar het je om gaat. Dat is geen probleem (zolang het geen al te grote impact heeft op de snelheid van de tests!). De voordelen van deze opzet wegen ruimschoots op tegen het aanvankelijk tegenintuïtieve karakter ervan.


## Voorbeeld


Een voorbeeld. De applicatie van mijn team draait om de constructie van toetsen. Toetsen bestaan uit toetsvragen ([*items*](http://www.imsproject.org/spec/qti/v3p0/impl#h.77l136x98r3)). Zo'n vraag bestaat uit enkele onderdelen of bouwblokken. Een inleidende tekst, bijvoorbeeld, al dan niet met een afbeelding; de eigenlijke vraag, en het interactietype dat erbij hoort (een antwoordveld, enkele meerkeuzemogelijkheden etc.).


De applicatie kent de functionaliteit om items uit onze database om te zetten naar een [QTI-representatie](http://www.imsproject.org/spec/qti/v3p0/impl#abstract). QTI is een internationale standaard voor het uitwisselen van toetsvragen. Elk bouwblok van het item kent zijn eigen soort QTI: de inleidende tekst, de afbeelding, het interatietype.


Het spreekt, hoop ik, voor zich dat de QTI-generator voor elk blok van de vraag zijn eigen class kent (een `TextQtiGenerator`, `ImageQtiGenerator` etc.). En elke generator kent zijn eigen tests. Maar die tests nemen niet de individuele generator als *entry point*. Dus niet[^2]:


```cs
[TestMethod]
public void TextQtiGenerator_GeneratesTextBlockQti_PreservesText() 
{
    var textBlock = new TextBlock("Test");
    var generator = new TextQtiGenerator();
    var result = generator.GetQti(textBlock);
    result.Text.Should().Be("Test");
}
```


Maar:


```cs
[TestMethod]
public void ItemQtiGenerator_GeneratesTextBlockQti_PreservesText() 
{
    var item = new ItemBuilder()
        .WithBlock(new TextBlock("Test"))
        .Build();
    var generator = new ItemQtiGenerator();
    var result = generator.GetQti(item);
    GetBlock<TextBlock>(result).Text.Should().Be("Test");
}
```


(De test maakt gebruik van het [*Test Builder*-patroon](https://canro91.github.io/2021/04/26/CreateTestValuesWithBuilders/) om de code leesbaar te houden. `GetBlock` is een helper method die de lezer de details van het opvragen van het juiste stukje QTI bespaart. Zie ook [deze blog](/blog/22/09/tests-als-documentatie/).)


Deze opzet stelt het team in staat om moeiteloos alles wat zich achter de interface van de `ItemQtiGenerator` bevindt te refactoren, zonder de tests aan te hoeven passen. De generators van de inviduele onderdelen kunnen naar harteloos gesplitst worden, of juist samengevoegd, of worden voorzien van [*special cases*](https://martinfowler.com/eaaCatalog/specialCase.html) zonder dat er maar één regel testcode hoeft te worden aangepast.


## Scope


Wat is een logisch *entry point* voor je tests? - Dat hangt ervan af. Er bestaan verschillende vuistregels voor het kiezen van de scope van je tests.


Eén vuistregel is bijvoorbeeld: wordt de code op verschillende plekken in de applicatie (of over applicaties heen) gebruikt? Dan moet deze geunittest worden. Is de code specifiek voor een bepaalde module? Test die code dan als onderdeel van de module. - De hierboven genoemde `TextBlockGenerator` valt in die laatste categorie en hoeft daarom niet in isolatie getest te worden.


Een andere vuistregel luidt: test code via hetzelfde pad als een gebruiker van de code. Maar wat is een gebruiker van je code? Hier kun je meerdere gevallen onderscheiden. 


Als je een helper class schrijft die door de hele applicatie wordt gebruikt, dan ben jij als ontwikkelaar zelf de gebruiker. Hetzelfde geldt voor een object in een [rijk domeinmodel](https://martinfowler.com/eaaCatalog/domainModel.html). Om er zeker van te zijn dat deze objecten zich gedragen zoals je zou verwachten, moet je deze unittesten. Hun veelvuldig gebruik in de codebase maakt het noodzakelijk vrij dicht op het metaal te gaan zitten. Een fout in deze code heeft immers grote gevolgen.


Je zou "gebruiker" ook kunnen lezen als "eindgebruiker". Als je een eenvoudige CRUD-applicatie hebt met een Web-API als back-end, dan is het niet onlogisch om je applicatie via die ingang te testen. Zeker als de applicatie weinig complexe logica kent, kunnen integratietests uitstekend als vangnet fungeren. 


## Architectuur en teststrategie


[Vlad Khononov](https://vladikk.com/) tilt dit idee nog een stap verder in [*Learning Domain-Driven Design*](https://www.oreilly.com/library/view/learning-domain-driven-design/9781098100124/). Zijn standpunt laat zich samenvatten als: je softwarearchitectuur bepaalt je teststrategie. (Ik schreef er eerder over, [hier](/blog/22/07/zelfs-de-testpiramide-is-niet-meer-heilig/).)


Applicaties die zijn opgezet volgens het [*Transaction Script*-patroon](https://martinfowler.com/eaaCatalog/transactionScript.html) bestaan uit weinig meer dan lijm tussen externe componenten, zoals [databases](https://nl.wikipedia.org/wiki/Database) of een [servicebus](https://nl.wikipedia.org/wiki/Enterprise_service_bus). Unittests zijn een slechte match voor zulke relatief eenvoudige applicaties met weinig businesslogica. De testsuite van zo'n applicatie zal daarom vooral uit *End to end* (*E2E*)-tests bestaan. 


Andere applicaties zijn veel meer gericht op het in code vastleggen van businessregels. Zulke applicaties zullen veelal gebruik maken van een [domeinmodel](https://martinfowler.com/eaaCatalog/domainModel.html). Objecten uit dat model zijn geisoleerd van infrastructurele delen van de code en worden door de hele codebase gebruikt. Daarom zal de testsuite van dat soort applicaties veel unittests kennen.


Een middenweg wordt gevormd door applicaties die gebruik maken van het [*Active Record*-patroon](https://www.martinfowler.com/eaaCatalog/activeRecord.html). Je zou een *active record* kunnen zien als een domeinobject dat tevens verantwoordelijk is voor zijn eigen persistentie. Het heeft zowel domeinlogica als infrastructurele verantwoordelijkheden. De testsuite van dit soort applicaties zal daarom veel integratietests kennen.


De softwarearchitectuur bepaalt de teststrategie. Welke soort tests je voornamelijk zal schrijven, is afhankelijk van het ontwerppatroon dat je kiest. Samengevat:


|       Ontwerppatroon |   Teststrategie |     Soort testpiramide | 
|---------------------:|----------------:|-----------------------:|
|       *Domain Model* |       Unittests | Klassieke testpiramide |
|      *Active Record* | Integratietests |            Testdiamant |
| *Transaction Script* |     *E2E*-tests |    Omgekeerde piramide |
<br>


## Kanttekeningen


Wat kanttekeningen bij het verhaal hierboven. 


1. Ik zeg niet dat de teststrategie *alleen* uit de ene of de andere soort tests zal bestaan. Uit het feit dat je een eenvoudige CRUD-applicatie schrijft, volgt niet dat je nooit meer unittests hoeft te schrijven. Zie het meer als een richtlijn om te bepalen hoe je een zo efficiënt mogelijk vangnet kan opzetten voor bij het ontwikkelen. 

2. Besef je dat delen van je applicatie meer of minder businesslogica kunnen bevatten, en dus andere teststrategieën kunnen verlangen. Mijn team unittest de hierboven genoemde QTI-functionaliteit, maar het opslaan en opvragen van *items* wordt getest middels integratie- en *E2E*-tests.

3. Ook dit zijn vuistregels. Wees niet bang om af te wijken van dit schema wanneer de situatie daar om vraagt, bijvoorbeeld als er sprake is van wettelijke verplichtingen. Wees je alleen bewust van het feit dat de test in dat geval niet per se als vangnet fungeert. 


## Makkelijk aanpassen


Software heet niet voor niets *soft*ware. Het definiërende kenmerk van software is dat het makkelijk aangepast kan worden. Maar zulke aanpassingen kunnen alleen veilig worden gemaakt wanneer er een goede testsuite aanwezig is die ontwikkelaars het vertrouwen geeft dat hun refactorslagen geen bestaande functionaliteiten omver werpen. 


Anders gezegd: ontwikkelaars zouden idealiter hun code moeten kunnen verbouwen zonder dat er ook maar één test faalt. Dan vervullen de tests optimaal hun functie als vangnet.


Om dat voor elkaar te krijgen, moet de testsuite op een bepaalde manier ontworpen worden. De tests moeten de interface van de code testen, en niet de implementatie. Test dus niet blind elke publieke method op elke class! Test via de voordeur, niet de achterdeur. Kies een geschikt *entry point* voor je tests, neem het liefst dezelfde route als een gebruiker van je code. 


De extra moeite die je steekt in het ontwerp van je testcode betaalt zich dubbel en dwars terug als hulpmiddel bij het ontwikkelen.


## Meer in deze reeks


1. [Tests als documentatie](/blog/22/09/tests-als-documentatie/)
2. **Tests als vangnet**
3. [Tests als ontwerpmiddel](/blog/22/09/tests-als-ontwerpmiddel/)


[^1]: Ik schreef hier per ongeluk: "*ingenieus*" - en dat is natuurlijk ook waar!

[^2]: Wat volgt is pseudocode om het punt duidelijk te maken.
