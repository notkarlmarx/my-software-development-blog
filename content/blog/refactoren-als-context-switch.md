---
title: "Refactoren als context switch"
author: "Karl van Heijster"
date: 2023-04-28T09:54:48+02:00
draft: true
comments: true
tags: ["context switch", "refactoren", "software ontwikkelen", "test-driven development"]
summary: "*Context switching* heeft een slechte naam in softwareontwikkelland en dat is niet helemaal onterecht. Het is enorm vervelend als je nét lekker aan het programmeren bent - om vervolgens weggeroepen te worden voor een snelle vraag of ellenlange vergadering (die ook een e-mail had kunnen zijn). Op dat moment raak je alle informatie kwijt die je in je hoofd hebt opgebouwd om een probleem te kunnen tackelen, en mag je opnieuw beginnen. Maar dat is maar de helft van het verhaal."
---

*Context switching* heeft een slechte naam in softwareontwikkelland en dat is niet helemaal onterecht. Het is enorm vervelend als je nét lekker aan het programmeren bent - om vervolgens weggeroepen te worden voor een snelle vraag of ellenlange vergadering (die ook een e-mail had kunnen zijn). Op dat moment raak je alle informatie kwijt die je in je hoofd hebt opgebouwd om een probleem te kunnen tackelen, en mag je opnieuw beginnen.[^1]


Maar dat is maar de helft van het verhaal. Elke ontwikkelaar kan bevestigen dat *context switches* ook kunnen helpen bij het oplossen van een probleem. Een probleem dat aan het eind van de dag onmogelijk leek, blijkt na een goede nachtrust doodeenvoudig. En wie al de hele ochtend naar zijn scherm aan het staren is, doet er goed aan een middagwandeling te maken. 


Soms moet je je hoofd even legen voordat je verder kunt. De *context switch* stelt je onderbewuste in staat het probleem op te lossen waar je met je volle bewustzijn niet uitkwam.


## Uitdaging


Laatst had ik mezelf in een netelige hoek geprogrammeerd. Ik was bezig met code die een XML-bestand importeert en omzet naar ons interne datamodel. De uitdaging was natuurlijk: de XML en het datamodel konden niet één op één naar elkaar worden gemapt. 


Wat in de XML een lijst met mogelijke waarden was, moest in ons datamodel worden omgezet naar een lijst van alle mogelijke combinaties van die waarden. Oftewel: `(A|B)&(C|D)` moest worden omgezet naar: `(A&C)|(A&D)|(B&C)|(B&D)`.


Hoe je dat probleem oplost, is nu niet van belang. Wat nu van belang is, is dat ik een tijd lang compleet vastzat.


Als ik [mijn eigen woorden](/blog/22/06/mijn-eerste-testgedreven-stapjes/) moet geloven (en dat doe ik), praktiseer ik nu ongeveer een jaar [Test-Driven Development](/tags/test-driven-development/) (TDD). Dus begon ik met een test. Eerst een eenvoudig geval, daarna een complexer variant: `A`, `A&B`, `(A|B)&C`... 


Maar met `(A|B)&(C|D)` worstelde ik. Wat ik ook probeerde, het resultaat was steevast een enorme puinhoop die voor logica door moest gaan - en mijn test bleef rood.


## Refactor


Dus besloot ik uit het probleem te stappen. Ik besloot dat ik nu in de TDD-cyclus van [*red-green-refactor*](/blog/22/03/agile-en-test-driven-development/) nu even niet in *red* moest zitten. Ik besloot van context te switchen: terug naar refactor.


Ik wijzigde wat variabelenamen, splitste enkele methods op - de gebruikelijke opruimacties. Op een gegeven moment viel me de gedachte in: waarom ben ik eigenlijk direct op die XML (in de vorm van een [`XElement`](https://learn.microsoft.com/en-us/dotnet/api/system.xml.linq.xelement?view=net-7.0)) aan het werken? Waarom voer ik deze berekening niet uit op een [DTO](https://en.wikipedia.org/wiki/Data_transfer_object)'tje? 


Dus ik keek welke objecten ik uit de XML plukte, en maakte een object aan met al die elementen. En alle code die direct op de XML werkte, kopieerde ik naar dat object. Daarna paste ik de oorspronkelijke code aan - [stapje voor stapje, één method per keer](/blog/22/08/twee-stijlen-van-refactoren/) - om de DTO te gebruiken in plaats van de XML. Toen ik daarmee klaar was, kon ik alle code die op de XML werkte, uit de oorspronkelijke class verwijderen.


## Voorwaarts


Waar stond ik nu? Ik was een uur verder en had nog precies evenveel groene tests als voorheen. Maar: waar ik oorspronkelijk één class had van krap tweehonderd regels code, had ik er nu twee van elk ruim honderd regels code. 


Dat klinkt misschien als stilstand - achteruitgang, zelfs. Maar het was eigenlijk een gigantische stap voorwaarts. Gedurende de eerste drie tests had ik niet eens doorgehad dat mijn oorspronkelijke code eigenlijk twee verantwoordelijkheden had: (1) de benodigde informatie uit de XML plukken, en (2) deze transformeren naar het interne datamodel.


Nu ik de verantwoordelijkheden had gescheiden, hoefde ik voor de volgende test mijn aandacht nog maar op de helft van het aantal regels code te richten. Ik hoefde me alleen nog druk te maken over de omzetting van de DTO naar het datamodel. De andere helft, die de XML omzet naar een DTO, kon ik met een gerust hart vergeten. 


Mijn refactorslag had de code dusdanig versimpeld, dat de volgende stap een stuk dichterbij was gekomen. 


## Leegmaken


\- Merk op: dit is de standaardreden waarom een groene test door een refactorslag moet worden gevolgd. Maar er was ook nog iets anders gebeurd. De refactorslag had mijn hoofd leeggemaakt.


Een bepaald probleem had een tijd lang al mijn aandacht opgeëist: hoe zet ik deze XML om naar een datamodel dat heel anders in elkaar zit? De refactorslag deed me focussen op een ander, eenvoudiger probleem: hoe zet ik deze XML om naar een datamodel dat er heel dicht tegenaan zit?


Het eenvoudige probleem hield mijn bewustzijn bezig - maar niet zo stevig dat ik geen enkele hersencapaciteit meer overhield. Mijn onderbewuste kon broeden op het grotere probleem. En inderdaad: toen ik de refactorslag achter de rug had en een kop thee ging zetten, was het volslagen helder wat ik moest doen om de test te doen slagen.


Ik had alleen nog een antwoord op [Stack Overflow](https://stackoverflow.com/questions/64955703/how-to-get-a-cartesian-product-of-a-list-containing-lists) om het voor elkaar te krijgen.


[^1]: Fun fact: direct na het schrijven van deze alinea werd ik weggeroepen door een collega voor een snelle vraag. Goed, waar was ik gebleven?
