---
title: "Tests als ontwerpmiddel"
author: "Karl van Heijster"
date: 2022-08-04T21:44:33+02:00
draft: true
comments: true
tags: ["clean code", "integratietests", "software architectuur", "test-driven development", "testen", "unit tests"]
summary: "Tests zijn een ontwerpmiddel, een *design tool*. Ze fungeren als indicator voor de kwaliteit van het ontwerp van je code. De vuistregel is even eenvoudig als zag-het-niet-want-het-stond-recht-voor-mijn-neus-vanzelfsprekend: *Is het moeilijk om er een test voor te schrijven? Dan deugt het ontwerp niet!*"
---

> ## TL;DR
>
> Tests zijn een ontwerpmiddel. Tests geven je feedback over de kwaliteit van het ontwerp van je code. De vuistregel luidt: *is het moeilijk om er een test voor te schrijven? Dan deugt het ontwerp niet!*
>
> Alle code valt in vier categorieën in te delen: (1) triviale code, (2) complexe code, (3) domeinsignificante code en (4) overgecompliceerde code. (1) test je niet; voor (2) schrijf je integratietests, voor (3) unittests; (4) refactor je naar (2) en (3) - die je op hun beurt goed test.
>
> Tests achteraf geven uitstekende feedback, maar wie het meest uit tests als ontwerpmiddel wil halen, ontwikkelt middels Test-Driven Development.


Tests zijn een ontwerpmiddel, een *design tool*.


Ik hoor jullie denken: hij gaat het over [Test-Driven Development](https://en.wikipedia.org/wiki/Test-driven_development) (TDD) hebben. 


Dat klopt.


Maar ik ga het niet alléén over TDD hebben. Ook tests die *after the fact* zijn geschreven kunnen prima fungeren als indicator voor de kwaliteit van het ontwerp van je code. De vuistregel is even eenvoudig als zag-het-niet-want-het-stond-recht-voor-mijn-neus-vanzelfsprekend: *Is het moeilijk om er een test voor te schrijven? Dan deugt het ontwerp niet!*


## Twee assen, vier kwadranten


Dat kan ik uitleggen aan de hand van een concept dat ik al eens eerder heb behandeld ([hier](/blog/21/08/moet-je-dit-willen-testen/)). Stel je twee assen voor[^1]: de verticale geeft de algoritmische complexiteit en domeinsignificantie aan, de horizontale de complexiteit van de code, gemeten in het aantal classes waarmee de code interacteert. Alle in je codebase valt aan de hand van die assen in vier kwadranten te plotten:


|                                |                             |                             |
|:------------------------------:|-----------------------------|-----------------------------|
|                                | Domeinmodel, algoritmen (3) | Overgecompliceerde code (4) |
| **Domeinsignficantie&#8593;**  | Triviale code (1)           | Controllers (2)             |
|                                | **Complexiteit&#8594;**     |                             |
<br>


Code die weinig complex is en weinig domeinsignificantie heeft, en met weinig andere classes interacteert, is triviaal (1), e.g. getters en setters op een bepaald object. 


\- Deze code is de moeite van het testen niet waard.


Weinig complexe code die met veel classes interacteert, noemt Khorikov *controllers* (2). Dit zijn classes wiens doel het is om de samenwerking van bepaalde objecten (met hoge complexiteit of domeinsignificantie) te orchestreren. Denk aan services die data ophalen om ze vervolgens aan een [message bus](https://www.enterpriseintegrationpatterns.com/MessageBus.html) door te spelen. 


\- Deze code dient te worden geïntegratietest.


Complexe en/of domeinsignificante code die met weinig classes interacteert (3). De algoritmische complexiteit en/of domeinsignificantie maken het bestaan van deze tests essentieel, en hun lage complexiteit zorgen ervoor dat deze eenvoudig geschreven kunnen worden. Denk aan de objecten in je [*Domain Model*](https://martinfowler.com/eaaCatalog/domainModel.html) hebt gedefinieerd, en die door heel de codebase gebruikt worden.


\- Hier schrijf je unittests voor. Je *system under test* is makkelijk te instantiëren. Je voert het verschillende waarden voor elke parameter om het gedrag vast te leggen - en verifiëren. Deze tests testen puur en alleen [*businesslogica*](https://en.wikipedia.org/wiki/Business_logic). ((2) is daarentegen een test van, zou je kunnen zeggen, de [*applicatielogica*](https://en.wiktionary.org/wiki/application_logic).)


## Complex en domeinsignificant


Wat overblijft is complexe, domeinsignificante code die met veel classes interacteert (4). 


\- Deze code is te complex om goed en wel te kunnen testen. Unittests voor deze code hebben veel afhankelijkheden naar mocks. Daardoor zijn ze fragiel. Integratietests verhullen de logica die getest wordt. Bovendien, ze duren zo lang dat ze de [*developer flow*](https://stackoverflow.blog/2018/09/10/developer-flow-state-and-its-impact-on-productivity/) verstoren. Ontwikkelaars draaien ze aan het eind van hun proces - en komen er dan pas achter als hun code bugs bevat. Tests voor dit soort code zijn moeilijk te schrijven, en, eenmaal geschreven, moeilijk onderhoudbaar.


Je moet deze code niet testen. Je moet deze code uitsplitsen. De businesslogica refactor je naar domeinsignificante unittests. De applicatielogica werk je om naar controllers, wier gedrag is geverifieerd middels integratietests.


## Signaal


De complexe tests waren een signaal: deze code is niet goed ontworpen, hij schendt het [Single-Responsibility Principe](https://en.wikipedia.org/wiki/Single-responsibility_principle) (SRP). Goed ontworpen methods, classes, modules bevatten businesslogica - en alleen maar businesslogica -, of ze coördineren de businesslogica. (Zie ook [deze blog] (LINK naar Scheid data ophalen van...).)


Andersom werkt het ook: als tests zich haast vanzelfsprekend laten schrijven, dan is dat een teken dat de code goed is opgezet. Ook testcode can *clean* zijn - in de zin dat ze het [*principle of least surprise*](https://en.wikipedia.org/wiki/Principle_of_least_astonishment) respecteren. En ironisch genoeg houden ze de productiecode daar net zo *clean* mee.


## Het bruggetje[^2]


En dan kom ik toch bij TDD uit. Want wat is de eenvoudigste manier om vanzelfsprekende tests te schrijven? - Door eerst een test te schrijven, en dan de implementatie. Dan weer een test, dan weer wat implementatie.


Hoewel, dat is niet *precies* de cirkel van TDD. Die ziet er, in mijn beleving, zo uit: 


1. **Je denkt na**, wat wil je dat de code doet? 

2. **Je schrijft een zo simpel mogelijke test.** - Let op: je hoeft niet onmiddellijk voor het goud te gaan. Begin met de simpelste features - de triviale features, haast. En bouw van daaruit systematisch uit naar complexere gevallen. TDD werkt alleen incrementeel. Wie met de complexe features begint implementeert code op de "traditionele" manier (bij gebrek aan een beter woord), maar dan voorafgegaan door één test.

3. **Je laat deze zo simpel mogelijk slagen.** Denk nog niet na over de optimale implementatie van de code. Je eerste prioriteit is de zojuist geschreven (falende) test naar groen te krijgen. Er is een tijd van implementeren, en een tijd van je code opschonen.

4. **Schoon je code op.** Refactoren is een op zichzelf staande stap in het proces van een softwareontwikkelaar. Wie tegelijkertijd features implementeert en de bestaande code refactort, schendt het SRP - ik bedoel: de variant van het SRP die in onze gedragscode is vastgelegd. (We hebben nog een gedragscode, maar die zouden we wel moeten hebben, en daar zou een variant van het SRP een rol in moeten hebben.)

5. **Ga terug naar 1.**


[TDD is een ontwerpdiscipline] (LINK). Hoewel tests achteraf je een indicatie geven van het ontwerp van je code, functioneren ze op hun best wanneer ze tijdens het ontwikkelen actief worden gebruikt. Tests zijn je blauwdrukken - je werkt een stuk beter gefocust met een plan.


## Perspectief


Als je TDD't heb je niet alleen tests - hoewel dat op zichzelf al waardevol genoeg is. Je verandert daarmee ook het perspectief waarmee je code schrijft. (zie ook [deze blog](/blog/22/05/nog-een-reden-om-testgedreven-te-ontwikkelen/).)


Wie "traditioneel" codeert, benadert zijn code vanuit het perspectief van de ontwikkelaar. Dit zal, als je niet uitkijkt (zelfs als je goed onderlegd bent in ontwerppatronen *en niet uitkijkt*), zijn effect hebben op de code die je niet schrijft. De interface van je classes zal een weerspiegeling zijn van de implementatie. Je schrijft [*leaky abstractions*](https://en.wikipedia.org/wiki/Leaky_abstraction). 


\- Nogmaals: als je niet uitkijkt.


## Gebruiker


Maar wie TDD't, heeft dat probleem niet. Je denkt éérst nadenkt over dat wat je code behoort te doen - en hoe een gebruiker van die code dat voor elkaar wil krijgen. Ik zeg dat heel bewust: "*wil* krijgen". Want een gebruiker - een softwareontwikkelaar; jij, bijvoorbeeld, over twee maanden! - *wil* niet eerst zes dependencies injecteren voordat 'ie het ene object kan mappen naar het andere. Die wil een method aanroepen, een object meegeven en een ander object daarvoor terugkrijgen.


(Hoor je al de test zichzelf al schrijven?)


De uitkomst van dat denkproces leg je vast in een test. Een zo simpel mogelijke test. Die test wordt niet gehinderd door enig implementatiedetail. Die test is vanzelfsprekendsprekend. 


Je weet hoe die tests eruitzien. Het is een unittest voor domeinobjecten, het is een integratietest voor controllers.


\- En je implementatie van die test is zo simpel mogelijk. - Je schrijft geen overgecompliceerde code - want je let op. Daar hebben de tests je toe gedwongen. Je schrijft pas nieuwe functionaliteit nadat je een nieuwe test hebt geschreven. Zo lang dat niet het geval is, refactor je.



## Kracht


Tests zijn een ontwerpmiddel, een *design tool*. Dat is een perspectief op tests dat makkelijk te vergeten valt - wanneer je door het modderige ontwerp van *legacy code* heen baggert - of wanneer je zonder vangnet aan een refactorslag begint - of wanneer je een test schrijft om aan de minimale coverage te komen.


Het belang van grondig geteste, goed ontworpen code is moeilijk te overschatten. Robert "*Uncle Bob*" Martin windt er in [*Clean Craftmanship: Disciplines, Standards, and Ethics*](https://www.oreilly.com/library/view/clean-craftsmanship-disciplines/9780136915805/) geen doekjes om. (Nota bene: de helft (!) van dat boek is aan testen gewijd is. - *De helft!* En dat terwijl het, aan de subtitel te zien, toch genoeg stof om te overdenken bevat!) Hij schrijft:


> Is TDD really a prerequisite to professionalism? Am I really suggesting that you can’t be a professional software developer unless you practice TDD?
>
>
> Yes, I think that’s true. Or rather, it is becoming true.


Een ontwikkelaar die op de toekomst voorbereid wil zijn, kan TDD maar beter omarmen - en de kracht van tests als ontwerpmiddel ten volle benutten.


## Meer in deze reeks


1. [Tests als documentatie] (LINK)
2. [Tests als vangnet] (LINK)
3. **Tests als ontwerpmiddel** 


[^1]: De volgende ideeën ontleen ik aan [Vladimir Khorikovs](https://enterprisecraftsmanship.com/) [*Unit Testing: Principles, Practices, and Patterns*](https://www.manning.com/books/unit-testing), een [aanrader](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/)!

[^2]: *[Of: de rotonde - Red.]*
