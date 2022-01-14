---
title: "De leercurve van Angulartests beklimmen - Deel 1"
author: "Karl van Heijster"
date: 2022-01-14T08:14:35+01:00
draft: true
comments: true
tags: ["angular", "clean code", "end to end tests", "leermoment", "software ontwikkelen", "technische schuld", "testen", "unit tests", "web development"]
summary: "Niet lang nadat we Angular als front end-framework besloten te gebruiken, maakten we de keuze de unit tests te laten voor wat het was. We waren heus wel overtuigd van het belang ervan, dat was het probleem niet, maar de stijle leercurve van Angulars tests verleidde ons daar niet naar te handelen. Toch lieten we het testen van de front end niet helemaal schieten. Onze tester had zich verdiept in *end to end* testframework Selenium, en het team wilde graag geloven dat dit een acceptabel alternatief was voor het schrijven van front end tests. En eerlijk is eerlijk, een tijdlang werkte deze aanpak behoorlijk. Maar uiteindelijk dwong de werkelijkheid ons toch die beslissing te herzien."
---

# Van *end to end* naar unit tests


Ik weet niet hoe het met jullie zit, maar mijn team en ik, wij vonden de leercurve van [testen in Angular](https://angular.io/guide/testing) aan de stijle kant. 


Om dat te kunnen begrijpen, moet je weten dat mijn team en ik een stel .NET-ontwikkelaars zijn, die zich door schade en schande het [unit testen in dat framework](https://docs.microsoft.com/en-us/dotnet/core/testing/) eigen hebben gemaakt - we hebben een ononderhoudbaar *legacy*-applicatie om het te bewijzen.


## Woorden en daden


Het volwassen worden van het team bestond uit twee delen: ten eerste het belang van unit tests inzien, en ten tweede daarnaar handelen. De eerste stap lijkt misschien triviaal, maar is dat niet. Er bestonden en bestaan wel degelijk teams die zich met man en macht verzetten tegen de noodzaak van testen, al krimpt hun aantal. Toch is dit deel eigenlijk het makkelijkst. Een gemiddelde ontwikkelaar anno 2022 zal het belang van testen in woord onderschrijven.


Daar naar handelen is een ander verhaal. Ten eerste bestaat er een druk vanuit stakeholders om nieuwe features zo snel mogelijk te releasen. Deze externe druk maakt het voor ontwikkelaars verleidelijk om de tests te laten voor wat het is, en hun code zonder automatische tests richting de [*main branch*](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) terug te sturen. 


Dit wordt nog verergerd door een interne druk: veel ontwikkelaars vinden het schrijven van unit tests een vervelend klusje. Eerlijk gezegd is dat niet helemaal onterecht. De meeste ontwikkelaars schrijven de logica eerst, en daarna pas de tests. Dit haalt het denkwerk - en dus de uitdaging - weg uit het schrijven van tests. Bovendien wordt deze stap dan bewust of onbewust als nutteloos ervaren, omdat de ontwikkelaar al handmatig heeft geverifieerd dat de logica doet wat het moet doen.[^1]


## Een alternatief?


Ik denk dat deze achtergrond relevant is voor de beslissing die we maakten, niet lang nadat we Angular als front end-framework besloten te gebruiken: we lieten de unit tests voor wat het was. We waren heus wel overtuigd van het belang van unit tests, dat was het probleem niet, maar de stijle leercurve van Angulars tests verleidde ons daar niet naar te handelen.


Toch lieten we het testen van de front end - gelukkig! - niet helemaal schieten. Onze tester had zich verdiept in *end to end* (E2E) testframework [Selenium](https://www.selenium.dev/), en het team wilde graag geloven dat dit een acceptabel alternatief was voor het schrijven van front end tests.


En eerlijk is eerlijk, een tijdlang werkte deze aanpak behoorlijk. Maar uiteindelijk dwong de werkelijkheid ons toch die beslissing te herzien. E2E-tests sloten eenvoudigweg niet goed genoeg aan bij wat we van onze front-end-tests verlangden.


## Een goede unit test


Goed, wat verlangt een ontwikkelaar dan van een unit test? Het doel van een unit test is om een ontwikkelaar snel feedback te geven over de gevolgen van zijn aanpassing. 


Zulke tests hebben daarom idealiter de volgende eigenschappen[^2]: 


1. **Ze zijn snel.** Het liefst trap je je unit test elke keer af als je een codewijziging hebt doorgevoerd. Zo weet je onmiddellijk of je wijziging een deel van de bestaande functionaliteit heeft omgegooid of niet. Wanneer het te lang duurt om op de resultaten van een test te wachten, zal een ontwikkelaar ze niet gebruiken. Daarmee verliezen ze hun informatieve waarde tijdens de ontwikkelcyclus.

2. **Ze zijn informatief over de plek van het defect.** Een unit test moet op zijn minst een hint geven over de plek waar de nieuw geïntroduceerde fout optreedt. Dat stelt de ontwikkelaar in staat om het probleem snel op te lossen. Wanneer een unit test dit nalaat, introduceert deze inefficiëntie in de ontwikkelcyclus, doordat de ontwikkelaar na elke wijziging van context moet wisselen om op zoek te gaan naar de oorzaak van de fout. 

3. **Ze zijn deterministisch**. Dat wil zoveel zeggen als: gegeven dezelfde input, geeft de test altijd dezelfde uitkomst. Tests die om voor de test irrelevante redenen falen of slagen, zullen uiteindelijk door ontwikkelaars genegeerd worden. Hun onbetrouwbaarheid zorgt dat ze hun informatieve waarde tijdens de ontwikkelcyclus verliezen. 


## E2E-tests als unit tests


Het klinkt als een open deur, natuurlijk, maar E2E-tests zijn geen goede unit tests.


1. **Ze zijn langzaam.** Doordat E2E-tests niet één stukje code testen, maar een volledige applicatie inclusief alle afhankelijkheden, hebben ze er langer voor nodig om te draaien. Zo lang, dat een ontwikkelaar ze niet tijdens de ontwikkelcyclus zal inzetten, maar hooguit na het afronden van zijn werkzaamheden.

2. **Ze signaleren alleen *dat* er iets mis is.** Maar *wat*, dat is veelal een open vraag. Doordat ze zo langzaam zijn, wordt er een drempel opgeworpen om al teveel E2E-tests te schrijven. Dat zorgt er voor dat de tests grofmaziger van aard worden. En dat zorgt er, ten slotte, weer voor dat de tests weinig inzicht bieden over de oorzaak van een defect.

3. **Ze zijn nondeterministisch.** E2E-tests kunnen om allerlei redenen falen die niets met wijzigingen in de logica te maken hebben: denk aan een slechte verbinding of een afhankelijkheid. Dat is op zich waardevolle informatie, maar niet om erachter te komen of je logica een bug heeft geïntroduceerd of niet. Hun nondeterministische aard zorgt ervoor dat ze het liefst door ontwikkelaars genegeerd worden, totdat het niet anders kan.


Let wel, hiermee is niet gezegd dat E2E-tests geen waarde hebben. Ze zijn een uitstekende aanvulling op unit tests. Maar een vervanging? Nee, daarvoor zijn ze bepaald niet geschikt.


## Een keuze


Het team werd dus voor een keuze gesteld. Gaan we door met het exclusieve gebruik van Selenium om de front end te testen, met alle gebreken van dien, of gaan we er werk van maken om de front end daadwerkelijk te *unit*testen? (Er was nog een derde optie, namelijk het testen van de front end helemaal te laten schieten. Maar die kon op geen enkele steun rekenen in het team. We staan immers voor de waarde van tests!)


Uit het feit dat deze blog nog doorgaat na deze alinea, kun je vast en zeker wel raden welke keus het team gemaakt heeft. De daaropvolgende keuze in de beslissingsboom was deze: gaan we ons in het zweet werken om Angulars steile leercurve te beklimmen, of bekijken we of er een manier is waarop we het testen voor ons kunnen vergemakkelijken? Daar gaat de volgende blog in deze reeks over.


## Meer in deze reeks

1. **Van *end to end* naar unit tests**

2. Van integratie- naar unit tests [volgt binnenkort]

3. ...? [volgt binnenkort]


[^1]: [Test-driven development](https://nl.wikipedia.org/wiki/Test-driven_development) is een manier om met precies die twee problemen om te gaan. Helaas is die praktijk nog niet bij ons in het team - mezelf incluis - ingesleten. Het is interessant om in de toekomst te onderzoeken wat ons tegenhoudt deze manier van software ontwikkelen eigen te maken.


[^2]: Waarschijnlijk vergeet ik er nog een paar. Geïnteresseerde lezers verwijs ik door naar [*Unit Testing*](https://www.manning.com/books/unit-testing) van Vladimir Khorikov en de essays over testen in [*Software Engineering at Google*](https://www.oreilly.com/library/view/software-engineering-at/9781492082781/). Beide boeken bevatten uitstekende uiteenzettingen over de vereisten allerhande soorten geautomatiseerde tests. Niet voor niets kregen ze allebei een plekje in mijn [top 5 beste boeken die ik in 2021 las](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/)!
