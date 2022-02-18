---
title: "De leercurve van Angulartests beklimmen - Deel 2"
author: "Karl van Heijster"
date: 2022-02-04T07:48:39+01:00
draft: false
comments: true
tags: ["angular", "clean code", "integratietests", "leermoment", "ontwerppatronen", "single-responsibility principe", "software ontwikkelen", "technische schuld", "testen", "unit tests", "web development"]
summary: "In een vorige blog beschreef ik de keuze van mijn team om de front end van onze Angular-applicatie te testen via *end to end*-tests - en waarom we daar uiteindelijk op terugkwamen. Nu we besloten hadden inderdaad te willen (nee, *moeten*) unit testen, doemde er een nieuwe keuze op in de beslisboom: gaan we ons in het zweet werken om Angulars steile leercurve te beklimmen, of bekijken we of er een manier is waarop we het testen voor ons kunnen vergemakkelijken?"
---

# Van integratie- naar unit tests


In een [vorige blog](/blog/22/01/de-leercurve-van-angulartests-beklimmen-deel-1/) beschreef ik de keuze van mijn team om de front end van onze Angular-applicatie te testen via *end to end*-tests - en waarom we daar uiteindelijk op terugkwamen. Nu we besloten hadden inderdaad te willen (nee, *moeten*) unit testen, doemde er een nieuwe keuze op in de beslisboom: gaan we ons in het zweet werken om Angulars steile leercurve te beklimmen, of bekijken we of er een manier is waarop we het testen voor ons kunnen vergemakkelijken?


Omdat programmeurs nu eenmaal lui zijn, kozen we voor de tweede optie. Maar voordat we de uitkomsten van dat onderzoek bekijken, loont het zich te bekijken *waarom* we de leercurve van de Angulartests nu precies zo stijl vonden.


## .NET vs. Angular


Het zou [de vloek van kennis](https://en.wikipedia.org/wiki/Curse_of_knowledge) kunnen zijn, maar in mijn beleving is [unit testen in .NET](https://docs.microsoft.com/en-us/visualstudio/test/walkthrough-creating-and-running-unit-tests-for-managed-code?view=vs-2022) betrekkelijk eenvoudig. De conventionele wijsheid is dat een test uit drie delen bestaat, vereeuwigd in het [AAA-patroon](https://medium.com/@pjbgf/title-testing-code-ocd-and-the-aaa-pattern-df453975ab80):


1. **Arrange**. In deze fase van het testen instantieer je de class die je wil testen en haar afhankelijkheden. (Zie ook [deze blog](/blog/21/09/droger-tests-met-factory-methods/).)

2. **Act**. In deze fase roep je de method aan die je wil testen.[^1]

3. **Assert**. In deze fase ga je na of de aanroep in de vorige fase het effect heeft gehad dat je beoogde.


Een eenvoudige test (die overigens geen gebruik maakt van Microsofts eigen [Assert class](https://docs.microsoft.com/en-us/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert?view=visualstudiosdk-2022), maar van het fantastische [FluentAssertions](https://fluentassertions.com/)) ziet er bijvoorbeeld zo uit:


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "DotNETExampleTests.cs">}}


Hoe ziet een doodgewone Angulartest eruit? Ik pluk een codevoorbeeld uit [hun eigen documentatie](https://angular.io/guide/testing-components-basics):


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "welcome.component.spec.ts">}}


De eigenlijke test (op regel 14 t/m 16), die de *Act*- en *Assert*-fase op één regel plaatst, is betrekkelijk eenvoudig. 


Helaas kan dat niet gezegd worden van de *Arrange*-fase die eraan voorafgaat (regel 1 t/m 12).[^2] Een `TestBed` heeft de verantwoordelijkheid om een module te configureren door een `WelcomeComponent` aan te leveren, samen met een [gemockte](https://en.wikipedia.org/wiki/Mock_object) afhankelijkheid. Het resultaat van deze operatie wordt toegeschreven aan twee properties die in de daadwerkelijke test worden gebruikt. (De declaratie van deze properties is niet weergegeven.)


## Unit- of integratietest?


Vanwaar deze complexiteit? Waarom niet gewoon (?) een nieuwe `WelcomeComponent` instantiëren en er een (al dan niet gemockte) `UserService` aan doorspelen?


Dat is omdat de unit tests in Angular eigenlijk helemaal geen unit tests zijn, maar integratietests. Componenten in Angular bestaan uit ten minste twee delen: een deel presentatie in de vorm HTML, en een deel business- of applicatielogica in de vorm van TypeScript. De bovenstaande test test niet ófwel de presentatie ófwel de logica. Het test de component als geheel.


Het is met name deze versmelting van presentatie en logica die testen in Angular bemoeilijkt. (Al helpt de praktijk van structureel vertrouwen ook mocks ook niet mee.) Het maakt de *Arrange*-fase ingewikkelder, maar moedigt bovendien ook aan om logica en presentatiecode te vermengen. Zo wordt het verleidelijk om code te schrijven die het [Single-Responsibility Principe](https://en.wikipedia.org/wiki/Single-responsibility_principle) (SRP) schendt, wat ook de testbaarheid niet ten goede komt.


## Services boven componenten


Het Angular-team lijkt zich dat ook te hebben beseft. Dat is waarom hun testdocumentatie steeds nadruk is gaan leggen op het [testen van services](https://angular.io/guide/testing-services), in plaats componenten. Services zijn immers classes à la C#, die zich louter met logica bezig (zouden moeten) houden. Ze kunnen dus op dezelfde manier worden getest.


(Overigens, componenten zijn net zozeer classes en kunnen in principe dus op dezelfde manier getest worden; zie [deze blog](https://www.forbes.com/sites/forbesdigitalgroup/2020/04/21/how-to-make-your-angular-unit-tests-25x-faster/) van [Zach Shuffield](https://www.linkedin.com/in/zach-shuffield-0a00a5aa/). Dit lost de schending van het SRP echter niet op. De opzet van de tests is dus eenvoudiger, maar de winst blijft beperkt als de code niet testbaar is opgezet. Shuffield prijst deze opzet overigens aan als manier om Angulartests 2,5 keer sneller te maken, wat mijns inziens eerder bijzaak is.) 


Dat is dan ook de uiteindelijke route die we hebben genomen om onze leercurve voor het testen in Angular te verkleinen. We hebben de logica verplaatst van de componenten naar diverse services. De services kregen op hun beurt hun eigen tests. Ze zouden er zo uit kunnen zien:


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "welcome.service.spec.ts">}}


En de componenten? Hebben die geen tests nodig? Nou ja, *it depends* (natúúrlijk!). Als de componenten, ondanks onze refactorslag, nog steeds een aanzienlijke hoeveelheid presentatielogica blijken te bevatten, dan kan het verstandig zijn om ze op de oorspronkelijke manier te testen. 


Maar idealiter voorkom je die situatie. In onze nieuwe opzet zouden componenten alleen maar verantwoordelijk moeten zijn voor het aan de HTML doorspelen van data die ze uit de services krijgen. Met andere woorden: componenten moeten [Humble Objects](https://martinfowler.com/bliki/HumbleObject.html) worden - én blijven. Een Humble Object is een object dat zó simpel is dat testen eigenlijk zonde van je tijd is. 


## Het eind?


Is dat het eind van het verhaal? Is ons team enthousiast aan de slag gegaan om vereenvoudigde Angulartests te schrijven?


Nee, niet helemaal helaas. Waarom niet? Dat leg ik in een volgende blog uit.


## Meer in deze reeks

1. [Van *end to end* naar unit tests](/blog/22/01/de-leercurve-van-angulartests-beklimmen-deel-1/)

2. **Van integratie- naar unit tests**

3. [Zijn deze tests onderhoudbaar?](/blog/22/02/de-leercurve-van-angulartests-beklimmen-deel-3/)

4. [Droger Angulartests met factory classes](/blog/22/02/de-leercurve-van-angulartests-beklimmen-deel-4/)


[^1]: Strikt genomen wil je geen *methods* testen, maar *gedrag*. Het gedrag is de abstractie waar je in geïnteresseerd bent, de method is de implementatie daarvan. Voor onze uiteenzetting van hoe een unit test er in .NET uitziet, is dat verschil echter niet van belang.


[^2]: Deze fase is in een aparte method geplaatst, `beforeEach`, die het mogelijk maakt om deze set up-logica één keer te definiëren voor meerdere tests. In principe zou je deze code ook in de body van de test zelf kunnen plaatsen, zodat de test qua vorm wat meer op de .NET-test lijkt. Ik heb de opzet van de oorspronkelijke code gehandhaafd, omdat dit de gebruikelijke manier is om het te doen in Angular.
