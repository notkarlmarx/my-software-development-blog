---
title: "Aantekeningen over requirements - deel 1"
author: "Karl van Heijster"
date: 2023-01-06T10:34:15+01:00
draft: true
comments: true
tags: ["agile ontwikkeling", "boeken", "communicatie", "documentatie", "informatieanalyse", "requirements", "samenwerking"]
summary: "Het moeilijkste onderdeel van softwareontwikkelen is niet *het juist bouwen*, maar *het juiste bouwen*. Vaak zwoegen programmeurs dagenlang op hun code en worstelen testers zich door het resultaat heen, om er pas helemaal op het eind van de ontwikkelcyclus achter te komen dat er iets is gebouwd waar eindgebruikers niet helemaal (of: helemaal niet!) op zaten te wachten. Het scheppen van een juist beeld van wat er gemaakt moet worden  is misschien wel de belangrijkste stap in het ontwikkelen van software - en niet zelden de minst ontwikkelde."
---

Het moeilijkste onderdeel van softwareontwikkelen is niet *het juist bouwen*, maar *het juiste bouwen*. Vaak zwoegen programmeurs dagenlang op hun code en worstelen testers zich door het resultaat heen, om er pas helemaal op het eind van de ontwikkelcyclus achter te komen dat er iets is gebouwd waar eindgebruikers niet helemaal (of: helemaal niet!) op zaten te wachten.


Het scheppen van een juist beeld van wat er gemaakt moet worden, wordt *requirements analysis* (of *requirements engineering* of *elicitation* - kies maar een variant) genoemd. Het is misschien wel de belangrijkste stap in het ontwikkelen van software - en niet zelden de minst ontwikkelde. Om die reden heb ik besloten om wat gedachten over het onderwerp uit te werken.


\- O, niet mijn eigen gedachten, hoor - maak je geen zorgen. Het volgende is gebaseerd op de aantekeningen die ik maakte tijdens het lezen van [*Software Development Pearls*](https://www.informit.com/store/software-development-pearls-lessons-from-fifty-years-9780137487776) van [Karl Wiegers](https://www.karlwiegers.com/). (Zie ook [deze blog](ATOMIC_HABITS).) Wiegers heeft meer dan vijftig jaar ervaring in het vak en heeft zijn hoofd al een stuk vaker aan de requirementssteen gestoten dan ik.


Deze blog beslaat het eerste deel van het eerste deel van Wiegers' boek, te weten de eerste acht van zestien lessen over de praktijk van requirements engineering. De volgende acht komen in een volgende blog aan bod.


**I.**


Het belang van requirements is moeilijk te overschatten. Het achterhalen van de juiste requirements is essentieel voor het succes van een project.[^1] De oorzaak van mislukte softwareprojecten ligt vaak bij een gebrekkige vorm van requirements engineering.


Stakeholders zijn je informatiebron voor het achterhalen van requirements. Helaas bestaan deze niet netjes geordend in hun hoofden. Om de juiste requirements te achterhalen, moet je *doorlopend* met stakeholders praten. Ze moeten regelmatig beschikbaar zijn voor verhelderingsvragen. Het uitvragen van requirements kost veel tijd - voor jou en de stakeholders.


Hun managers moeten het dus goed vinden dat ze een groot deel van hun tijd besteden aan het project. Als dat nog niet het geval is, probeer hen dan te overtuigen. De beste manier om iemand te overtuigen is, zoals altijd: laten zien wat het oplevert. Voor ons betekent dat: werkende software *die doet wat de stakeholders nodig hebben*.


Zorg dat je dichtbij je stakeholders zit. Dit verbetert de communicatie, zowel in kwantiteit als in kwaliteit. Hoe toegankelijker je stakeholders zijn, hoe meer je met hen zult praten. En "praten" is een toverwoord hier. Hoe belangrijk geschreven communicatie ook is, bij het ontdekken van requirements gaat er niets boven een gesprek, waarin je regelmatig kunt nagaan of je op dezelfde golflengte zit, en doorvragen wanneer dat niet het geval is.


Probeer eens om een dag dicht in de buurt van (één van) je stakeholder(s) te zitten, en kijk wat er gebeurt. 


**II.**


Het doel van het formuleren van requirements is het kweken en cultiveren van gedeeld begrip - tussen stakeholders en het ontwikkelteam. Al het resultaat van requirementsanalyse - documenten, indexkaarten etc. - dient dit ene doel.


Een visiestatement kan helpen om de hoog over verwachtingen te verhelderen. Je kunt hiervoor het volgende sjabloon gebruiken: 


> **For** [target customers]
>
> **Who** [statement of the business need or opportunity]
>
> **The** [name of the product or project]
>
> **Is** [type of product or project]
>
> **That** [major product capabilities; core benefits it will provide; compelling reason to by the product or undertake the project]
>
> **Unlike** [current business reality or alternative products]
>
> **Our product** [concise summary of the major advantages of this product over the current reality or the competition]


Vertaald naar het Nederlands, en in de context van deze blog, zou zo'n visiestatement er als volgt uit kunnen zien:


> **Voor** Karl, **die** een middel nodig heeft om zijn inzichten over zijn vakgebied vast te leggen, **is** *dotkarl*, een wekelijks blog, **dat** wat hem dwingt om zijn gedachten concreet te formuleren en vast te leggen in een doorzoekbaar formaat. **In tegenstelling tot** een Word-bestandje op zijn computer, biedt ***dotkarl*** hem de mogelijkheid zijn gedachten eenvoudig met de buitenwereld te delen.


Merk op dat dit visiestatement is geschreven met mezelf als *target customer*. Dat is in lijn met hoe ik mijn blog zie. Zou ik grotere ambities hebben, dan zou ik ook een visiestatement kunnen schrijven die bijvoorbeeld de Nederlandse softwareontwikkelgemeenschap als meewerkend voorwerp. - Het statement is bedoeld om je expliciet na te laten denken over dit soort afwegingen.


**III.**


Ken je je stakeholders? - Ken je ál je stakeholders? Dat wil zeggen: zowel de directe gebruikers (de mensen die ermee werken) als de indirecte (bijvoorbeeld hun managers, die een productiviteitsboost verwachten dankzij je app)? In welke groepen zou je je stakeholders in kunnen delen?


Weet je wat je ze willen? Weet je wat ze nodig hebben van jou? Willen ze bijvoorbeeld alleen geïnformeerd worden? Of hebben ze behoefte aan intensiever contact? Weet je hoe betrokken elke groep stakeholders is? Hangt hun leven af van het succes van dit project, of vinden ze alles wel best? En hoeveel invloed hebben ze?


Probeer een antwoord op deze vragen te formuleren voor elke groep stakeholders. Dit stelt je in staat om bewuste, geïnformeerde keuzes te maken, bijvoorbeeld over wie je op welk moment waarbij betrekt.


**IV.**


Als je requirements verzamelt, focus je dan niet op features. Dit leidt vaak tot de implementatie van functionaliteit die zelden (of zelfs nooit!) wordt gebruikt.


Focus je in plaats daarvan op de gebruiker. - Wat is zijn/haar doel? Welke taken moet of wil hij/zij voltooien? - Dit zorgt ervoor dat je focust op het probleem dat opgelost dient te worden, in plaats van een voorgestelde oplossing. 


Focussen op de oplossing onttrekt de vraag aan het zicht: "Is dit de *juiste* oplossing?" Om die te kunnen beantwoorden, moet je eerst weten wat het probleem is.


[*User stories*](https://agilescrumgroup.nl/wat-is-een-user-story/) zijn hiervoor een geschikt middel. Deze hebben de volgende vorm: "Als [stakeholder] wil ik [dat dit ontwikkeld wordt] zodat [dit probleem wordt opgelost]." Maar kijk uit: het is makkelijk om *feature* requirements op te schrijven in een *user story*-sjabloon.


Een alternatief voor een *user story* is een [*job story*](https://jtbd.info/replacing-the-user-story-with-the-job-story-af7cdee10c27): "In [deze situatie], wil ik [deze taak uitvoeren], zodat ik [deze uitkomst kan bewerkstelligen]."


Begin met een hoog over overzicht van wat er moet gebeuren. Dit maakt het makkelijker om te prioriteren dan wanneer je met de details begint.


**V.**


Requirements verzamelen is een iteratief proces. Je zal nooit in één keer alle requirements goed krijgen. Dit is ook een van de redenen waarom je doorlopend met je stakeholders in gesprek moet blijven. Menselijke communicatie is niet lineair. Je zult steeds meer inzichten opdoen naarmate je meer gesprekken voert, die hun invloed hebben op de manier waarop je de requirements formuleert en prioriteert.


Zorg eerst voor een overzicht van alle *user stories*. Prioriteer ze daarna. Werk de belangrijkste uit. Prioriteer opnieuw wanneer nodig. Tijdens deze bezigheid zullen sommige *user stories* afvallen, en er zullen nieuwe *user stories* verschijnen. Dit is normaal - al kan het regelmatig enorm frustrerend zijn.


Het helpt vaak om verschillende weergaven te hebben van de requirements. Vul de *user stories* aan met diagrammen, testcases, ontwerpschetsen en prototypes. Deze technieken zullen je stakeholders op een andere manier prikkelen, waardoor gaten in je begrip naar de oppervlakte kunnen komen.


**VI.**


Agile requirements verschillen niet fundamenteel van de requirements in traditionele projecten. In allebei de gevallen dienen ze hetzelfde doel: alle betrokkenen hun werk op een juiste manier te laten doen. Voor ontwikkelaars betekent dat: het juiste ontwikkelen. Voor stakeholders: op basis van het ontwikkelde hun werk zo goed mogelijk uitvoeren. Of je je requirements giet in een uitgebreid specificatiedocument of noteert op indexkaarten, aangevuld met doorlopende communicatie, is een implementatiedetail.


Er zijn wel wat verschillen qua rollen en verantwoordelijkheden tussen beide benaderingen. In agile projecten, beslissen ontwikkelaars (niet analysten!) of een requirement voldoende is uitgewerkt om ermee aan de slag te kunnen gaan. De rol van businessanalysten verschuift van eenmalige specificatie naar doorlopend heronderhandelen met stakeholders over de scope van de komende iteraties.


**VII.**


Agile methodlogieën leggen het zwaartepunt op communicatie boven geschreven documenten. Dat is niet onterecht: de agile filosofie zag het levenslicht in een tijd waarin softwareontwikkeling werd geplaagd door een overdaad aan documentatie.


Maar geschreven documenten hebben wel degelijk voordelen boven gesproken communicatie. Het schrift is duurzamer dan het woord. Vertrouwen op louter je geheugen is riskant. Wanneer je iets vergeet, dan zul je je stakeholder aan moeten schieten met een vraag die hij of zij al eerder heeft beantwoord. Dat is een kostbaar proces. Het kost zowel de analyst als de stakeholder tijd en moeite, en zorgt waarschijnlijk voor een hoop frustratie bij de laatste.


Schrijf daarom de inzichten op die je opdoet tijdens het verzamelen van requirements. Het is eenvoudiger en goedkoper om die documentatie terug te lezen, dan de inzichten opnieuw te ontdekken.


Dat betekent uiteraard niet dat het als analyst je taak is om een berg aan papier te produceren. Documenteer je inzichten op een gepast niveau van detail. Zorg dat je voldoende informatie ter beschikking hebt om de belangrijkste inzichten terug te kunnen halen. Elke keer als je een stakeholder uitvraagt, wil je *nieuwe* inzichten opdoen, niet terughalen wat jullie de vorige keer hebben besproken.


De vraag is, natuurlijk: hoe documenteer je dat wat je leert op een duurzame manier?


**VIII.**


Softwareontwikkeling is deels techniek en deels communicatie. Requirements engineering is daarentegen 100% communicatie. Het werk van een businessanalyst bestaat grotendeels uit gesprekken met een groot aantal stakeholders, waaronder domeinexperts en ontwikkelaars, eindgebruikers en projectmanagers. 


Al die groepen hebben andere informatie nodig om hun werk te kunnen doen. Ze hebben verschillende informatiebehoeften als het aankomt op bijvoorbeeld de reikwijdte en de mate van detail van de specifiecaties.


Je zou, al probeer je het nog zo hard, nooit een enkel requirementsdocument kunnen schrijven dat tegemoet komt aan de behoeften van al je stakeholders. Je moet de manier waarop je de informatie weergeeft elke keer opnieuw toesnijden op je publiek.


Daaruit volgt dat requirements veel verschillende vormen aan kan nemen. Requirements kunnen worden weergegeven in natuurlijke taal, maar ook in testcases en visualisaties. Deze methoden vullen elkaar aan. 


Vertrouw op sjablonen en standaarden wanneer mogelijk. Dit reduceert de cognitieve belasting voor je publiek, en stelt ze in staat om zich te richten op dat wat belangrijk is: de inhoud.


## Meer in deze reeks


1. **Aantekeningen over requirements - deel 1**

2. Aantekeningen over requirements - deel 2 [binnenkort]


[^1]: Is "project" de juiste term om onze bezigheden als softwareontwikkelaar te duiden? [Kevlin Henny](http://kevlin.tel/) en [Sander Hoogendoorn](https://sanderhoogendoorn.com/) spreken in [dit gesprek](https://www.youtube.com/watch?v=JAl3QFae_dE) liever van "producten". Projecten hebben een einddatum; softwareproducten kunnen daarentegen in principe oneindig doorontwikkeld worden.
