---
title: "Revert!"
author: "Karl van Heijster"
date: 2023-11-10T08:13:42+01:00
draft: false
comments: true
tags: ["falen", "integratietests", "leermoment", "software ontwikkelen", "testen"]
summary: "Drie dagen hebben we de boel lopen te debuggen. Bij elke nieuwe wijziging leken we verder te zakken in een onverklaarbaar moeras van verborgen afhankelijkheden. Op een gegeven moment was ik het zat. Ik zei: \"Ik ga de boel terugdraaien.\" (Mijn collega, verslagen, zag al zijn harde werk voor zijn ogen in vlammen opgaan.) \"Niet alles, maar wel alles in die ene class. En dan ga ik je wijziging één voor één opnieuw toepassen, net zolang totdat er tests falen.\""
---

Ook je testcode verdient liefde. Unit- en integratietests dien je van tijd tot tijd te refactoren, bijvoorbeeld als je nieuwe inzichten op hebt gedaan over [hun leesbaarheid](/blog/22/01/hoe-droog-wil-je-je-test-hebben/ "'Hoe droog wil je je test hebben?'") of [de manier waarop je ze het best kunt structureren](/blog/22/12/over-de-volgorde-van-je-unit-tests/ "'Over de volgorde van je unit tests'").


Niet lang geleden nam een collega de taak op zich om onze integratietests onder handen te nemen -- de tests die het gedrag van onze API [documenteerden](/blog/22/09/tests-als-documentatie/ "'Tests als documentatie'"). De opzet die we voor die tests gekozen hadden, piepte en kraakte aan alle kanten. Alle tests erfden van een baseclass met daarin een `HttpClient` en wat *helper methods* die de interactie daarmee vergemakkelijkten.


## Onwerkbaar


In de loop van de tijd was het aantal *helpers* in die class tot onwerkbare proporties gegroeid. Die methods -- en die `HttpClient` -- waren, dankzij de manier waarop het [`ClassInitializeAttribute`](https://learn.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2013/ms245248(v=vs.120) "'ClassInitializeAttribute Class', Microsoft documentatie") in [MSTest](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-mstest "'Unit testing C# with MSTest and .NET', Microsoft documentatie") werkt, noodgedwongen [`static`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/static "'static (C# Reference)'"). Dat is me altijd een doorn in het oog geweest.[^1]


Maar vooral het gebruik van overerving is me in de loop der jaren steeds meer tegen gaan staan. Door gedeelde functionaliteit in een baseclass te stoppen, verberg je belangrijke informatie voor de lezer van de code. Om de flow van een programma te kunnen gebruiken, zul je continu heen en weer moeten springen tussen verschillende classes. Het gevolg is dat de correcte werking van een programma voor een oppervlakkige -- of onervaren of haastige of vermoeide -- lezer het gevolg lijkt van magie. Wie te sterk leunt op overerving als middel om code te hergebruiken, levert in op leesbaarheid en begrijpelijkheid.


Waarmee ik niet wil impliceren dat overerving altijd slecht is. Maar vaak is er een beter alternatief beschikbaar. Het is niet voor niets zo dat de spreuk "[composition over inheritance](https://en.wikipedia.org/wiki/Composition_over_inheritance "'Composition over inheritance', Wikipedia")" zijn eigen Wikipediapagina heeft, en "inheritance over composition" niet.


## Opdracht


Goed, dus die collega van mij, die had zichzelf de opdracht gesteld om een eind te maken aan die lelijke de baseclass in onze integratietestsuite. En dus deed hij wat elke goede ontwikkelaar doet: hij maakte zichzelf een voorstelling van hoe de code er in de nieuwe situatie uit zou moeten zien, en begon driftig zaken te verplaatsen. 


En we hebben wel een paar honderd integratietesten, dus je kunt je voorstellen dat er flink wat te verplaatsen viel.


Terwijl hij aan het verplaatsen was, vielen hem nog wel een paar dingetjes meer op die wat hem betreft beter konden. Dus deed hij wat elke goede ontwikkelaar doet: hij liet de code netter achter dan hij 'm aangetroffen had. Hij werkte duplicatie weg, versimpelde de testinitialisatie, plaatste met elkaar samenhangende operaties achter een eenvoudige façade.


Hoezeer ik ook mag hameren op het feit dat testcode net zo belangrijk is als productiecode, er sluipt toch altijd meer technische schuld in dat deel van de codebase dan je denkt.


Hij was er een goeie dag of anderhalf mee bezig, maar daarna was de code om door een ringetje te halen.


## Probleem


Er was alleen één probleem: het werkte niet. Althans, het werkte wel, maar toch beduidend minder goed dan voorheen. Tests die gisteren nog slaagden, faalden ineens. Behalve als je ze nog een keer aftrapte, dan deden ze het ineens weer wel.


De tests waren van elkaar afhankelijk geworden -- maar waarom, dat was een raadsel. Wie de code las -- en we hebben samen hele grote delen van die nieuwe code doorgekeken --, zag een heleboel prachtig van elkaar gescheiden, atomaire brokjes (test)functionaliteit. Maar zelden heb ik meegemaakt dat code zó bedrieglijk was. We zagen ons geconfronteerd met eenvoudige, verzorgde code die op sublieme wijze fouten onder de motorkap voor ons verborg.


Drie dagen hebben we de boel lopen te debuggen.


Bij elke nieuwe wijziging leken we verder te zakken in een onverklaarbaar moeras van verborgen afhankelijkheden.


## Terugdraaien


Op een gegeven moment was ik het zat. Ik zei: "Ik ga de boel terugdraaien." (Mijn collega, verslagen, zag al zijn harde werk voor zijn ogen in vlammen opgaan.) "Niet alles, maar wel alles in die ene class. En dan ga ik je wijziging één voor één opnieuw toepassen, net zolang totdat de tests falen."


Ik draaide de wijziging terug, moest de baseclass herstellen, gooide daar alles uit weg wat niet meer gebruikt werd, en trapte de tests af. Alles groen. Ik paste één method aan, trapte de tests af. Alles groen. Paste een tweede method aan, trapte de tests af. Alles groen.


Op een gegeven moment had ik alle methods uit de baseclass vervangen, alles was nog steeds groen. Daar zat 't 'm dus niet in. Ik verwijderde de dode code en richtte me op de volgende wijziging. De voorheen gedupliceerde code verving ik door een method call: alles bleef groen. De testinitialisatie dan. Ik kopieerde zijn oplossing en plakte 'm over de bestaande code heen, trapte de tests af -- rood.


Drie dagen intensief debuggen was teruggebracht tot een halfuurtje domme arbeid: code wijzigen en testen, code wijzigen en testen.


## Les #1


Er zitten twee lessen in dit verhaal, een positieve en een negatieve.


De negatieve luidt als volgt: neem tijdens het programmeren geen grote stappen. Want dit is waar mijn collega de mist in was gegaan. Hij had een heleboel code gewijzigd, en valideerde zijn wijzigingen pas nadat hij deze op tientallen plekken in de code door had gevoerd. Toen bleek dat zijn tests faalden, had hij geen idee meer welke van de honderden regels gewijzigde code de fout(en) herbergde.


Vervolgens deed hij wat elke ontwikkelaar instinctief doet in zo'n situatie: hij haalde zijn debugger tevoorschijn. Maar dat is alsof je met een microscoop een crimineel op probeert te sporen. Het instrument is veel te precies voor het doel dat je ermee wil bereiken. Daarmee is niet gezegd dat je de oorzaak van het probleem er niet mee kunt vinden, maar wel dat dat eerder een kwestie van geluk zal zijn dan wat anders.


Ik neem het mijn collega niet kwalijk. Zelf ben ik tientallen, honderden keren in dezelfde val getrapt. De truc is een stap terug te doen en je bewust te worden van het feit dat je *werkwijze*, en niet je code, de eigenlijke oorzaak is van het probleem.


-- Moeilijk te doorgronden bugs zijn geen technisch probleem. Het is een probleem dat voortkomt uit je manier van werken.


## Les #2


De positieve les luidt: programmeren doe je het best in zo klein mogelijke stappen. Na elke stap valideer je dat je wijziging niets heeft gebroken. Zo nee, leg deze wijziging dan vast. We gebruiken tegenwoordig allemaal [Git](https://git-scm.com/), dus in de praktijk betekent dat: *commit* je wijziging. -- Dit is het minst interessante onderdeel van de les.


Interessanter is wat er gebeurt als je wijziging je tests breekt. De eerste ingeving van elke programmeur zal zijn: de problematische code te willen repareren. Je begint de code driftig aan te passen. Dan run je de tests nog een keer. Als deze nog steeds falen, dan doe je de volgende wijziging. Als de tests nog steeds falen, dan haal je de debugger tevoorschijn.


Voordat je het weet heb je een enorme berg code geschreven, en als je pech hebt, dan zijn je tests nog steeds rood. Je bent opnieuw in dezelfde val gestapt: je hebt te grote stappen genomen.


Een betere oplossing is dit: draai je wijziging terug. De wijziging is klein, dus daar mis je niets aan. *Revert* en vraag je af: wat heb ik geleerd van deze mislukte poging? Probeer het met je nieuwe inzicht nog eens opnieuw.


Klinkt dat inefficiënt? Ik kan je [*The Mikado Method*](https://mikadomethod.info/) aanraden.


[^1]: De manier waarop [XUnit](https://xunit.net/) het initialiseren van variabelen op class-niveau aanpakt, is wat dat betreft een stuk eleganter: daar gebruikt het framework simpelweg de constructor voor. Voor een vergelijking tussen [NUnit](https://nunit.org/), XUnit en MSTest, [klik hier](https://www.lambdatest.com/blog/nunit-vs-xunit-vs-mstest/ "'NUnit vs. XUnit vs. MSTest: Comparing Unit Testing Frameworks In C#', LambdaTest").
