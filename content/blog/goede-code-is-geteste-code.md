---
title: "Goede code is geteste code"
author: "Karl van Heijster"
date: 2024-05-18T21:45:44+02:00
draft: true
comments: true
tags: ["agile ontwikkeling", "clean code", "kwaliteitsattributen", "test-driven development", "testen"]
summary: "Goede code is geteste code. Het is testbare code, zeker -- en er zijn tests die het bewijzen. Als er geen tests zijn, dan is het geen goede code. -- De vraag hier is natuurlijk: wat is goede code, wat betekent \"goede code\"? Is het code die doet wat het moet doen? Die netjes gestructureerd is? Die er goed uitziet?"
---

# I


Goede code is geteste code. Het is testbare code, zeker -- en er zijn tests die het bewijzen. Als er geen tests zijn, dan is het geen goede code. -- De vraag hier is natuurlijk: wat is goede code, wat betekent "goede code"? Is het code die doet wat het moet doen? Die netjes gestructureerd is? Die er goed uitziet? 


Op al die vragen: ja. Maar de functionele en esthetische kwaliteiten van code zijn niet doorslaggevend voor haar kwaliteit. Doorslaggevend is: de mate waarin de code aanpasbaar is. Eenvoudig aanpasbare code doet wat het moet doen (en blijft dat doen -- daar kom ik nog op terug), is netjes gestructureerd en ziet er goed uit (is eenvoudig te lezen, voelt alsof het zo moet zijn). -- De vraag is hier: wat maakt de code eenvoudig aanpasbaar?


Het antwoord op die vraag is: tests. Tests vertellen ons: je zit op de juiste weg -- of: *stuur bij!!* Dat betekent dat als ontwikkelaars naar hun tests luisteren -- en deze bij elke codewijziging op groen houden -- ze altijd op het juist pad blijven. Dat [vangnet](/blog/22/09/tests-als-vangnet/ "'Tests als vangnet'") maakt onze code eenvoudig aanpasbaar. Het is wat onze software *soft* maakt.


Goede code is veilig aanpasbare code. Code is veilig aanpasbaar als deze gedekt wordt door geautomatiseerde tests. Goede code is geteste code. (En de grap is: geteste code kan een grotere mate van chaos en lelijkheid verdragen. Want geteste code is eenvoudig te refactoren (*aan te passen*) om gestructureerder en mooier te worden. -- En daarom is er relatief weinig chaotische en lelijke geteste code.)


## II


[Robert *uncle Bob* Martin](https://en.wikipedia.org/wiki/Robert_C._Martin) vergelijkt [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) in [*Clean Craftsmanship*](https://www.pearson.com/en-us/subject-catalog/p/clean-craftsmanship-disciplines-standards-and-ethics/P200000009529/9780136915713) met het [dubbel boekhoudsysteem](https://nl.wikipedia.org/wiki/Dubbel_boekhouden "'Dubbel boekhouden', Wikipedia"). 


Binnen dat systeem wordt elke transactie op zijn minst op twee verschillende manieren geadministreerd. Elke transactie heeft zijn plaats aan de credit- én debetkant van een grootboekrekening. Worden beide kanten bij elkaar opgeteld, dan is het resultaat 0 -- altijd een eeuwig, en als dat niet zo is, dan weten we dat we een fout moeten hebben gemaakt. 


Net zo dient elke gedraging in onze code tweemaal te worden vastgelegd: één keer in de productiecode en één keer in de testcode. Wanneer elke gedragswijziging van de code wordt voorafgegaan door een (dan nog falende) test, dan weten we zeker, wanneer alle tests slagen, dat de code precies doet wat het moet doen. En als er een test faalt, dan weten we dat we een fout hebben gemaakt.


Het is niet voldoende om *enkele* tests te hebben -- net zoals het niet voldoende is om *sommige* transacties aan de credit- en debetkant te boeken. Code die *deels* is getest, is beter dan code die *niet* is getest. Maar goede code -- écht goede code -- is volledig getest. En de beste manier om dat voor elkaar te krijgen is door middel van TDD.


## III


Goede code is aanpasbare code *omdat code aangepast moet worden*. Code is niet statisch, rigide, dood. Code is dynamisch, flexibel, levend. Code bestaat niet buiten ruimte en tijd, code reageert op haar omgeving -- en *moet* daar ook op reageren, wil het overleven. Code is nooit af.


Code moet veranderen omdat het ecosysteem verandert waarin het opereert. Vanuit technisch oogpunt betekent dat: afhankelijkheden raken *out of date*, bijvoorbeeld omdat ze beveiligingslekken bevatten. Vanuit economisch oogpunt: de wensen van haar eindgebruikers veranderen, ze vragen om nieuwe features. Vanuit procedureel oogpunt: wij als ontwikkelaars doen nieuwe inzichten op over het probleemdomein -- dat is de kern van [Agile ontwikkelen](/tags/agile-ontwikkeling/ "Blogs met de tag 'agile ontwikkeling'"). 


Code wordt maar heel even gecreëerd -- en daarna heel lang onderhouden. Dat onderhoud gebeurt door een team ontwikkelaars van vlees en bloed. Willen die ontwikkelaars hun werk goed kunnen doen, dan moeten ze adequaat kunnen reageren op veranderingen in hun omgeving. En dat kunnen ze alleen met hulp van veiligheidsmechanismen -- want ontwikkelaars zijn ook maar mensen.


Testen behoort tot de kern van softwareontwikkeling.
