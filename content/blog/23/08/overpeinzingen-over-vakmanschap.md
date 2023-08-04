---
title: "Overpeinzingen (over vakmanschap)"
author: "Karl van Heijster"
date: 2023-08-04T11:34:13+02:00
draft: false
comments: true
tags: ["boeken", "filosofie", "professionaliteit", "software ontwikkelaar (rol)", "stakeholders", "technische schuld", "testen", "vakmanschap", "verantwoordelijkheid"]
summary: "\"Ziet u niet hoe vaklieden, hoewel zij tot op zekere hoogte bereid zijn om hun opdrachtgever tegemoet te komen, zich niet kunnen veroorloven af te wijken van de voorschriften van hun vak? Is het niet verbazingwekkend en teleurstellend tegelijk dat bij een architect en een geneesheer de grondbeginselen van hun vak meer gerespecteerd worden dan bij de rede bij de doorsneemens, terwijl het juist de rede is die hij met de goden gemeen heeft?\""
---

In zijn [*Overpeinzingen*](https://www.ankh-hermes.nl/boek/overpeinzingen/ "Marcus Aurelius - 'Overpenzingen', uitgeverij AhnkHermes") overpeinst [Marcus Aurelius](https://plato.stanford.edu/entries/marcus-aurelius/): 


> "Ziet u niet hoe vaklieden, hoewel zij tot op zekere hoogte bereid zijn om hun opdrachtgever tegemoet te komen, zich niet kunnen veroorloven af te wijken van de voorschriften van hun vak? Is het niet verbazingwekkend en teleurstellend tegelijk dat bij een architect en een geneesheer de grondbeginselen van hun vak meer gerespecteerd worden dan bij de rede bij de doorsneemens, terwijl het juist de rede is die hij met de goden gemeen heeft?"


Het is een interessante passage -- filosofisch bezien, maar ook in relatie tot softwareontwikkeling.


## Voorschriften


Het eerste wat opvalt, is dat de filosoof het uitoefenen van een vak koppelt aan volgen van voorschriften en het respecteren van grondbeginselen.


Wat zouden de grondbeginsel van softwareontwikkeling kunnen zijn? -- Daar zijn meerdere antwoorden op mogelijk. De volgende lijst is allesbehalve uitputtend[^1]:


- Software is nooit een doel op zich, het dient altijd een ander doel. Om waarde te kunnen leveren, dient het het juiste te doen. Software moet functioneel correct zijn.

- Software wordt maar zelden door één persoon ontwikkeld. Samenwerking tussen ontwikkelaars is een essentieel onderdeel van het proces. Vanuit een communicatieve invalshoek, dient code zelfverklarend te zijn. Alle code communiceert een boodschap -- goede code communiceert die helder en eenduidig.

- De laatste twee punten komen concreet samen in de praktijk van [geautomatiseerde tests](/tags/testen/ "Blogs met de tag 'testen'"). Deze bewijzen functionele correctheid en communiceren het bedoelde gedrag naar andere ontwikkelaars. Alle software die langer dan een paar dagen dient te leven, moet worden gedekt door tests.

- Vanuit een technische invalshoek bezien, dient software de [SOLID](https://en.wikipedia.org/wiki/SOLID)-principes te honoreren.[^2] Componenten -- of dat nu functies, classes, of modules zijn -- moeten [*highly* cohesive*](https://en.wikipedia.org/wiki/Coupling_(computer_programming)) en [*loosely coupled*](https://en.wikipedia.org/wiki/Loose_coupling) zijn. 

- Software dient zo eenvoudig mogelijk te zijn. Afkortingen [KISS](https://en.wikipedia.org/wiki/KISS_principle) -- Keep It Simple, Stupid! -- en [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it) -- You Ain't Gonna Need It -- communiceren dat idee in een pakkende slogan.


-- Welke grondbeginselen of voorschriften zou je nog meer kunnen bedenken?


## Afwijken


Voorschriften zijn er om nageleefd te worden -- dat is waarom het voorschriften zijn. 


Een goede vakman (1) kent de grondbeginselen van zijn vakgebied, (2) brengt deze in de praktijk door de daaruit voortvloeiende voorschriften te volgen, en (3) houdt deze hoog, ook als zijn opdrachtgever hem onder druk zet daar van af te wijken.


Het is op dit laatste punt waar het vakgebied softwareontwikkeling nog veel te leren heeft, denk ik. Ik kan niet meer op één hand tellen hoe vaak ik collega's heb horen bekennen dat ze hoeken hebben afgesneden in de code om aan de wensen van hun stakeholders tegemoet te komen. Ze hebben functionaliteit ingebouwd waarvan ze weten dat deze niets toevoegt, ze hebben genoegen genomen met spaghetticode omdat ze zichzelf voorlogen dat die code toch niet meer gewijzigd hoefde te worden, of ze hebben de tests overgeslagen om een deadline te halen.


En -- hij die zonder zonde is, werpe de eerste steen -- datzelfde geldt voor mij net zozeer. Niemands vakmanschap overleeft volledig ongeschonden de barse praktijk van software ontwikkelen. -- En dat is ook niet erg, zo lang er maar van die ervaringen geleerd wordt. Eén van de redenen waarom ik zo op tests hamer (in [deze blog](/blog/23/04/tijdreis/ "'Tijdreis'"), bijvoorbeeld), is omdat ik heb ervaren wat het is om zonder tests te moeten ontwikkelen -- en daar wil ik niet naar terug.


## Pragmatisme


Het [stoïcisme](https://plato.stanford.edu/entries/stoicism/) is een pragmatische filosofie -- dat is één van de redenen waarom deze vandaag de dag nog steeds zo aansprekend is --, en dat blijkt ook uit Marcus Aurelius' citaat. Dogmatiek past een vakman niet. Hij moet bereid zijn *tot op zekere hoogte* tegemoet te komen aan de wensen van zijn opdrachtgever.


In ons vakgebied uit dat zich in het opnemen van -- [bewuste](/blog/21/11/bewuste-technische-schuld/, "'Bewuste technische schuld'")! -- [technische schuld](/tags/technische-schuld/ "Blogs met de tag 'technische schuld'"). 


Wie nu een schuld op zich neemt, doet dat met de verwachting dat hij hiermee de mogelijkheden schept om deze later terug te kunnen betalen. Een deadline kan zó belangrijk zijn dat het verstandig is om *nu* wat minder strak vast te houden aan enkele voorschriften. Als de deadline eenmaal is gehaald -- en er bijvoorbeeld een grote order binnen is gehaald --, dan kan de daaruit voortvloeiende winst gebruikt worden om de schuld af te betalen.


En die schuld wordt afbetaald *met rente*. Het is altijd eenvoudiger om kwaliteit van te voren in te bouwen, dan om deze achteraf nog toe te voegen. Maar kwaliteit kan tijd kosten -- op de korte termijn althans -- en die tijd heb je niet altijd. 


Wie een schuld aangaat zonder plan om deze terug te betalen, handelt onverantwoordelijk. Het is aan ons als vakmensen om onze opdrachtgever op dat eenvoudige gegeven te wijzen. Zo lang er een realistisch plan bestaat om technische schuld terug te betalen, kunnen we hem tegemoet komen. Als dat er niet is, dan dient een vakman op te komen voor zijn beroepseer.


## Het goede leven


Dat gezegd hebbend, natuurlijk ging het Marcus Aurelius in het bovenstaand citaat niet om vakmanschap -- van architecten, geneesheren, softwareontwikkelaars --, toen hij die passage schreef. Hij had een veel grootser thema op het oog. Het ging hem om leiden (en lijden) van het goede leven -- hoe een vakman te zijn in het leven, zogezegd.


Ook daar kunnen we over peinzen -- maar dat is, vrees ik, voor een volgende keer.


[^1]: Voor een gestructureerder en uitgebreider overzicht, zie [*Clean Craftmanship*](https://www.pearson.com/store/p/clean-craftsmanship-disciplines-standards-and-ethics/P200000009529/9780136915713) -- die titel is geen toeval -- van [Robert "*Uncle Bob*" Martin](http://cleancoder.com/products).

[^2]: Zie met name [deze blog](/blog/21/04/enums-switch-statements-en-solid-1/ "'Enums, switch statements en SOLID - deel 1'"), maar [ik heb vaker over SOLID geschreven](/tags/solid/ "Blogs met de tag 'SOLID'").
