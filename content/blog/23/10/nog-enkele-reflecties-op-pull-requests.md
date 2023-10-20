---
title: "Nog enkele reflecties op pull requests"
author: "Karl van Heijster"
date: 2023-10-20T11:21:09+02:00
draft: false
comments: true
tags: ["code lezen", "code reviews", "leermoment", "presenteren", "pull requests", "professionaliteit", "pull requests"]
summary: "Onlangs hield ik een praatje op het werk over de edele kunst van het pull request. Het gesprek dat naar aanleiding daarvan ontstond, vond ik erg waardevol. Het geven van een goede presentatie werkt in bepaalde zin net als software ontwikkelen: je maakt een eerste versie, legt die voor aan een groep mensen, en gebruikt hun feedback om een betere tweede versie te ontwikkelen."
---

Onlangs hield ik een praatje op het werk over [de edele kunst van het pull request](/talks/de-edele-kunst-van-het-pull-request/) (PR). Het gesprek dat naar aanleiding daarvan ontstond, vond ik erg waardevol. Het geven van een goede presentatie werkt in bepaalde zin net als software ontwikkelen: je maakt een eerste versie, legt die voor aan een groep mensen, en gebruikt hun feedback om een betere tweede versie te ontwikkelen.


Het centrale punt van mijn presentatie luidt als volgt. Om een codewijziging goed te kunnen beoordelen, moet je jezelf drie vragen stellen: 1. waarom bestaat deze wijziging überhaupt? -- 2. wat doet de gewijzigde code? -- en 3. hoe doet de code dat? Een goed geschreven PR geeft antwoord op alle drie de vragen -- in respectievelijk de omschrijving, de geautomatiseerde tests en de gewijzigde code zelf. (Dit punt zet ik uitgebreider uiteen in [deze blog](/blog/23/09/drie-vragen-die-elk-pull-request-moet-beantwoorden/ "'Drie vragen die elk pull request moet beantwoorden'").)


De hoe-vraag beantwoordt elk PR als het ware gratis en voor niets. Als er geen codewijziging zou zijn, zou er immers geen PR aangemaakt (hoeven) worden. De eerste twee vragen zijn interessanter. Veel PR's laten het als oefening aan de lezer te achterhalen waarom de wijziging noodzakelijk is en wat de code precies doet. In mijn presentatie besteedde ik daarom vooral veel aandacht aan het waarom en het wat.


## Schrift of gesprek?


De volgende vraag is terecht: waarom moeten deze vragen allemaal in het PR zelf, in tekst, beantwoord worden? Zou je ze niet ook -- of misschien zelfs beter -- in een gesprek toe kunnen lichten?


Hoewel mijn presentatie over PR's gaat, zal ik nooit beweren dat het PR de enige manier is om de drie vragen te beantwoorden. 


Als ik een PR tegenkom waarvan de omschrijving onduidelijk is of zelfs ontbreekt, dan zal ik niet als een dictator eisen dat al mijn vragen schriftelijk in het PR beantwoord worden. Onduidelijkheden kun je prima in een gesprek ophelderen. (Nadeel daarvan is wel dat een volgende ontwikkelaar met dezelfde vragen bij de schrijver van het PR aan kan komen zetten. Maar omdat PR's over het algemeen niet keer op keer herlezen worden, is dat een risico dat ik bereid ben te nemen.)


De wat-vraag, daar ik strenger in: deze *moet* wat mij betreft met tests worden beantwoord. Daar zijn twee redenen voor. Ten eerste *bewijzen* tests dat de code zich op een bepaalde manier gedraagt. Een ontwikkelaar zul je daarentegen op z'n blauwe ogen moeten vertrouwen. -- Nu is het niet zo dat ik mijn collega's niet vertrouw, maar het is wel zo dat ik weet dat ze feilbaar zijn, en dat de code anders kan functioneren dan ze zelf denken, zeker als het complexe *edge cases* betreft.


Belangrijker nog -- en dat is het tweede punt -- is het feit dat geautomatiseerde tests de kwaliteit van de code op een duurzame manier borgen. Een gesprek kan problemen rondom de werking boven water brengen, maar het zorgt er niet voor dat deze over een maand niet opnieuw de kop op steken. Een gesprek vervliegt zodra het voorbij is -- tests bewijzen hun waarde lang nadat ze geschreven zijn.


## Log?


De volgende vraag hangt met de eerste samen: introduceer ik geen log proces met de eisen die ik aan PR's stel? Daar waar ontwikkelaars voorheen alleen "gewoon" de code konden wijzigen, verlang ik nu van hen dat ze de context van hun wijzigingen expliciet maken én alles met tests dekken. Rem ik daarmee de ontwikkelsnelheid af?


Mijn antwoord daarop klinkt misschien lomp. Desalniettemin: als je voorheen weg kwam met -- in mijn ogen -- half werk, dan *voelt* het misschien als nodeloos vertragend wanneer er ineens van je wordt verlangd de hele klus te klaren. Maar dat gevoel is precies dat -- een gevoel, en niet meer. Goed geschreven PR's verhogen zelfs de ontwikkelsnelheid.


Als je een PR inschiet zonder in de omschrijving te zetten wat het bestaansrecht van deze wijziging is, dan bespaar je als schrijver van het PR tijd. Maar het zal de lezer van het PR extra tijd kosten -- tijd die diegene zal moeten besteden aan het helder krijgen van de context van de wijziging. Netto is de tijdwinst negatief. De lezer zal er langer mee bezig zijn de waarom-vraag te beantwoorden dan de schrijver -- want de schrijver weet die context op het moment van schrijven al, en kan deze dus makkelijker produceren dan de lezer.[^1] 


Bovendien zou ik nooit van de schrijver verlangen een heel verhaal over die context te schrijven. Twee zinnen is in de meeste gevallen meer dan genoeg. De lezer is immers, dankzij [Stand-ups](/tags/daily-standup/ "Blogs met de tag 'daily standup'") en [Refinements](/tags/product-backlog-refinement/ "Blogs met de tag 'product backlog refinement'"), al bekend met de context. Het enige wat de schrijver moet bieden, is een manier om het waarom terug naar de voorgrond te halen, niet een voor leken geschreven introductie in het probleemdomein.


## Professioneel


Dan: de tests. De eis je code te documenteren met tests is slechts veeleisend voor ontwikkelaars die het schrijven van tests niet in hun werkwijze hebben opgenomen. Maar dat zijn -- *excusez le mot* -- geen professionele ontwikkelaars.[^2] 


Wie tests achterwege laat, zal achter de feiten aanlopen. Alle ontwikkeltijd zal uiteindelijk op worden geslokt door het fixen van bugs, in plaats van het toevoegen van waarde door middel van nieuwe features. Het is belangrijk om je beseffen: je werkgever betaalt je niet om bugs te fixen -- bugs zijn problemen die je *zelf* veroorzaakt hebt.


De beste manier om tests te integreren in je werkwijze, is door aan [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) te doen. Wie begint met een test, formuleert voor zichzelf een antwoord op de vraag wat de code doet. Pas daarna zal diegene zich richten op de vraag hoe deze dat doet. TDD is, zou je kunnen zeggen, een manier om jezelf in de schoenen van de codereviewer te plaatsen -- om eerst een lezer van de code te zijn, voordat je er de schrijver van wordt. 


Voor ontwikkelaars die TDD'en, is wat ik voorstel geen log proces. Het enige wat mijn manier van PR's schrijven van hun verlangt, is dat ze in de beschrijving bondig de informatie delen die ze toch al tot hun beschikking hebben.


## Pull requests of pair programming?


Ook de derde vraag hangt met de eerste samen. Veel van de problemen die PR's oplossen, zou je ook met [pair programming](/tags/pair-programming/ "Blogs met de tag 'pair programming'") op kunnen lossen. (Ik zette dit standpunt eerder uiteen in [deze blog](/blog/23/01/wel-code-reviews-geen-pull-requests/ "'Wel code reviews, geen pull requests'")) Verliezen mijn opmerkingen over goede PR's niet al hun waarde zodra je PR's loslaat?


Dat is geen onterechte opmerking, maar het is er één die het eigenljke doel van de presentatie mist. De belangrijke vraag is niet: *hoe schrijf ik goede PR's?* De belangrijke vraag is dit: *wat is er allemaal voor nodig om code goed te kunnen beoordelen?* -- En die vraag is net zo relevant voor softwareontwikkelaars die samen [*trunk based* ontwikkelen](/blog/23/09/doe-je-wel-echt-aan-continuous-integration/ "'Doe je wel écht aan continuous integration?'") als voor ontwikkelaars wier proces GitFlow met PR's volgt.


Ik geef toe: zelf heb ik bijgedragen aan die verwarring door mijn presentatie *De edele kunst van het pull request* te noemen. Maar PR's zijn wat mij betreft slechts een *framing device*, een ingang die ik koos omdat het voor veel ontwikkelaars het moment vormt waarop hen uitdrukkelijk gevraagd wordt code te beoordelen.


Maar code beoordelen is net zo belangrijk wanneer je in een voor jouw onbekend deel van de code aan de slag gaat, of wanneer je een bug fixt of een nieuwe feature implementeert. En in al die gevallen is dat een kwestie van het kunnen formuleren van een antwoord op de drie bovengenoemde vragen.


Mijn presentatie was en is in eerste instantie een poging de vraag naar het beoordelen van code te verhelderen. Het is een in wezen filosofische excercitie: een poging woorden te geven aan iets dat elke ontwikkelaar elke dag onbewust doet. Dat het betere PR's oplevert -- en dat het dat doet, daar ben ik van overtuigd --, is eigenlijk alleen maar mooi meegenomen.


[^1]: Het alternatief is dat de codereviewer minder tijd besteed aan het achterhalen van het waarom, wat op termijn een daling in de kwaliteit van de code met zich mee zal brengen. Het resultaat is hetzelfde: de tijdwinst is netto negatief.


[^2]: De context waarin ik die uitspraak doe is belangrijk, natuurlijk. Ik heb het over productiecode die ontwikkeld is in een professionele context. Wanneer hobbyprojecten of *proofs of concept* niet door tests worden gedekt, dan is dat uiteraard een niet problematisch.
