---
title: "Stap voor stap software testen"
author: "Karl van Heijster"
date: 2021-09-24T11:23:32+02:00
draft: true
comments: true
tags: ["agile ontwikkeling", "boeken", "recensies", "samenwerking", "software ontwikkelen", "testen"]
summary: "Software testen is een vak apart. Veel ontwikkelaars hebben wel een schetsmatige notie van hoe een goede test eruit dient te zien, maar ontberen een gedegen theoretisch fundament. Zulke ontwikkelaars zouden er goed aan doen om *Essentials of Software Testing* van Ralf Bierig, Stephen Brown, Edgar Galván en Joe Timoney te lezen."
---

Waarom testen we software? Een belangrijke reden is om te controleren dat deze werkt zoals bedoeld. Een nog belangrijker reden is om te blijven controleren dat deze werkt zoals bedoeld. In een snel veranderende wereld, waar het [refactoren](https://nl.wikipedia.org/wiki/Refactoren) van bestaande code aan de orde van de dag is, en er constant nieuwe [features](https://en.wikipedia.org/wiki/Software_feature) aan [applicaties](https://nl.wikipedia.org/wiki/Applicatie) worden toegevoegd, zijn geautomatiseerde tests de enige duurzame manier om de kwaliteit van software te waarborgen.


Dat is een les die veel softwareontwikkelaars met pijn en moeite hebben geleerd. Lang werd testen gezien als de verantwoordelijkheid van testers. Deze mochten helemaal aan het eind van de softwareontwikkelketen nagaan of datgene wat de ontwikkelaars opgeleverd hadden, überhaupt wel werkte. Met de opkomst van [*Agile*](https://nl.wikipedia.org/wiki/Agile-softwareontwikkeling) methoden zoals [Scrum](https://nl.wikipedia.org/wiki/Scrum_(softwareontwikkelmethode)) en [Lean](https://nl.wikipedia.org/wiki/Lean-softwareontwikkeling) worden ontwikkelaars en testers gedwongen nauw samen te werken. Ze zouden elkaars werk inmiddels zelfs praktisch over moeten kunnen nemen.


## Fundament


De praktijk is echter, zoals altijd, weerbarstiger. Software testen is een vak apart. Veel ontwikkelaars hebben wel een schetsmatige notie van hoe een goede test eruit dient te zien, maar ontberen een gedegen theoretisch fundament. Zulke ontwikkelaars zouden er goed aan doen om [*Essentials of Software Testing*](https://www.cambridge.org/highereducation/books/essentials-of-software-testing/5BEA8B9CB2E001E014CE0FDD7F41F3E9#overview) van [Ralf Bierig](https://bierig.net/), [Stephen Brown](https://www.linkedin.com/in/stephen-brown-a5586a8/), [Edgar Galván](https://ie.linkedin.com/in/edgar-galvan-8661a298) en [Joe Timoney](https://www.linkedin.com/in/joe-timoney-65345a4) te lezen. 


Anders dan veel ontwikkelaars gefocuste inleidingen, beginnen deze heren niet onmiddellijk met het schrijven van [unit tests](https://nl.wikipedia.org/wiki/Unittesten). De auteurs hanteren een nauwgezet stappenplan. Hoe test je software? Dat begint met analyse, het in kaart brengen van testwaarden en het opstellen van test cases. Pas nadat deze geverifieerd zijn, worden de tests daadwerkelijk geschreven. Het is belangrijk om te beseffen dat dat stappenplan een conceptuele constructie is. De auteurs benadrukken dat sommige stappen in de praktijk impliciet blijven. (En dat is maar goed ook, want anders zou een tester meer bezig zijn met documentatie schrijven dan testen!)


## Black box


Vervolgens behandelen de auteurs verschillende teststrategieën, elk uitgelegd aan de hand van het stappenplan. Ze beginnen eenvoudig, met [*equivalence partitions*](https://en.wikipedia.org/wiki/Equivalence_partitioning) en [*boundary value analysis*](https://en.wikipedia.org/wiki/Boundary-value_analysis). Bij de eerste test je met behulp van representatieve waarden een bepaalde functionaliteit, en bij de tweede doe je hetzelfde met grenswaarden. Zulke tests worden [*black box*-tests](https://nl.wikipedia.org/wiki/Blackboxtest) genoemd, omdat ze kunnen worden geschreven op basis van de [specificatie](https://en.wikipedia.org/wiki/Software_requirements_specification) alleen, zonder de daadwerkelijke [implementatie](https://nl.wikipedia.org/wiki/Implementatie#Implementatie_van_software) in code mee te hoeven nemen.


Stel, je hebt een eenvoudige methode die aangeeft of een getal hoger is dan 100. De input van die methode is een getal, de output een waarde *waar* of *onwaar*. Iemand die aan de hand van *equivalence partitions* test, werkt twee scenario’s uit: één met een input van 50 (en verwachte waarde *onwaar*) en één met een input van 150 (en verwachte waarde *waar*). Het idee is dat die waarden equivalent zijn aan alle andere waarden boven en onder de honderd. Iemand die aan de hand van *boundary value analysis* werkt, schrijft tests voor de getallen 99 (*onwaar*) en 100 (*waar*). Dit omdat er bij die grenswaarden vaak fouten in de code sluipen.


## Voor- en nadelen


Helaas voor de ontwikkelaar - en gelukkig voor de eindgebruiker! - is software meestal niet zo eenvoudig, waardoor het noodzakelijk wordt [*white box*-tests](https://nl.wikipedia.org/wiki/Whiteboxtest) te ontwikkelen. Dit zijn tests die uitgaan van de specificatie én de implementatie. In het geval van [*statement coverage*](https://en.wikipedia.org/wiki/Code_coverage) wordt tijdens het ontwikkelen van de tests nagegaan hoeveel regels code daadwerkelijk afgetest worden. Sterkere varianten daarvan zijn *branch coverage* en *all paths coverage*.


De auteurs illustreren al deze strategieën aan de hand van één eenvoudig voorbeeld. Door steeds nieuwe bugs in de code te introduceren, leggen ze bloot welke soort fouten elke strategie weet te onthullen, en vooral ook welke niet. Hierdoor ontstaat een goed overzicht van de voor- en nadelen van elke manier van testen. Dat stelt ontwikkelaars in staat om een grondiger afweging te maken in de manier waarop ze code testen. Hoewel het standaardvoorbeeld in de vorm van een unit test is gegoten, zijn alle teststrategieën net zo goed van toepassing op [integratie](https://nl.wikipedia.org/wiki/Integratietest)- en [applicatietesten](https://nl.wikipedia.org/wiki/Systeemtest). 


## Koppelvlak


Het is deze opzet die de lezer prikkelt na te denken of zijn eigen tests. Maar de auteurs laten een kans liggen om de lezer te prikkelen na te denken over de code die getest wordt. Ontwikkelaars en testers werken steeds inniger samen. Dit noodzaakt de eerste om code op te leveren die makkelijk te testen is voor de tweede. Sterker nog, vaak is de ontwikkelaar ook degene die de unit- en integratietests schrijft, dus het is in zijn eigen belang om na te denken over de [testbaarheid](https://en.wikipedia.org/wiki/Software_testability) van code.


Hoewel ze het onderwerp af en toe zijdelings aansnijden, blijft het koppelvlak van code en tests onderbelicht. Wie *Essentials of Software Testing* leest, zou het vergeven zijn te denken dat dat twee gescheiden wereld zijn en blijven. Theoretisch is dat misschien het geval, maar de praktijk is, zoals altijd, weerbarstiger. Gelukkig maar.


*Deze recensie verscheen oorspronkelijk op [De Leesclub van Alles](https://deleesclubvanalles.nl/).*
