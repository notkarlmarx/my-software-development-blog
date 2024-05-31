---
title: "Een goede ontwikkelaar begrijpt eerst het probleem"
author: "Karl van Heijster"
date: 2024-05-31T12:24:03+02:00
draft: true
comments: true
tags: ["software ontwikkelaar (rol)", "vakmanschap", "verantwoordelijkheid", "waarde"]
summary: "Een softwareontwikkelaar is niet *iemand die code schrijft*. Iemand die slechts dat doet, kan ondanks al zijn inspanningen van geen enkele toegevoegde waarde zijn. Want uiteindelijk gaat het niet om de code. Het gaat niet om de code, zelfs niet als die code precies doet wat er gevraagd wordt. -- Software ontwikkelen gaat om het oplossen van problemen."
---

Onlangs zijn enkele teamgenoten en ik een boekenclub begonnen -- de start van een nieuwe junior ontwikkelaar vormde een ideale aanleiding. We lezen [Robert C. Martins]((https://en.wikipedia.org/wiki/Robert_C._Martin)) [*Clean Craftsmanship*](https://www.pearson.com/en-us/subject-catalog/p/clean-craftsmanship-disciplines-standards-and-ethics/P200000009529/9780136915713). Dat bleek een ideale aanleiding voor de meer ervaren softwareontwikkelaars om herinneringen op te halen aan alle ellende die komt kijken bij het in de wind slaan van Martins inzichten.


Het ontbreken van unittests zorgt ervoor dat ontwikkelaars bang worden de code te wijzigen. Het gevolg is dat ze aanpassingen aan de code doen die het veiligst zijn op de korte termijn, en niet het beste voor de code. Continu refactoren is uit den boze: de kans het systeem om zeep te helpen is te groot. Wijzigingen aan de codestructuur worden uitgesteld totdat het niet anders kan, en dan zijn ze des te complexer omdat feature op feature is gestapeld -- en helpen vervolgens inderdaad het systeem om zeep.


Maar het zijn niet alleen technische vaardigheden die de senioren voorheen ontbeerden. Een collega merkte op: "Eén van de dingen die we tegenwoordig beter doen, is dat we niet overal meer ja op zeggen. We bouwen niet zomaar meer wat er gevraagd wordt." 


## Code schrijven


Dat wijst op een fundamenteel punt over wat het betekent softwareontwikkelaar te zijn. Want wat mijn collega implciet zegt, is: nu ik erop terugkijk, concludeer ik dat software ontwikkelen *niet* betekent dat je wacht op een codeeropdracht en die vervolgens voltooit.


Dat is hoe hij (net als de rest van zijn team) zijn werk misschien vroeger zag. En het is hoe veel programmeurs hun werk nog steeds zien -- je kunt ze herkennen aan klaagzangen over constant wijzigende requirements en stakeholders die heel de tijd van mening veranderen. 


Zulke ontwikkelaars zien hun werk als het schrijven van code -- en ze verwachten dat anderen hen vertellen wat hun code moet doen. Ze redeneren: het is de taak van die anderen om een oplossing te verzinnen voor een probleem, het is mijn taak die oplossing in code om te zetten.


Zij zijn in hun ogen niet verantwoordelijk voor het begrijpen van het probleem, misschien zijn ze niet eens verantwoordelijk voor het bedenken van de oplossing. Ze zijn slechts verantwoordelijk voor het schrijven van code.


## Problemen oplossen


Maar een softwareontwikkelaar is niet *iemand die code schrijft*. Iemand die slechts dat doet, kan ondanks al zijn inspanningen van geen enkele toegevoegde waarde zijn. Want uiteindelijk gaat het niet om de code. Het gaat niet om de code, zelfs niet als die code precies doet wat er gevraagd wordt. (Merk op dat dit net zozeer geldt voor de lelijke, slecht gestructureerde en ongeteste code die mijn collega's vroeger schreven, als voor de mooie, doorlopend gerefactorde en geteste code die ze vandaag de dag opleveren.)


Waar gaat het dan wel om? Software ontwikkelen gaat om het oplossen van problemen. Specifieker: het oplossen van *businessproblemen*. (Wanneer software ontwikkelen te vaak gaat over het oplossen van *codeerproblemen*, dan is dat een teken dat je betere code moet schrijven.) De waarde van een ontwikkelaar is af te lezen van de mate waarin deze die problemen oplost.


Code die het probleem niet (of nauwelijks) oplost, blijft waardeloze code, zelfs al is ze door een expert geschreven.


## Begrijpen


Om een probleem op te kunnen lossen, moet je eerst het probleem begrijpen. De kwaliteit van een oplossing is één op één gecorreleerd aan de mate waarin het probleem is begrepen. Een halfbegrepen probleem leidt tot een halfbakken oplossing -- zo simpel is het.


Het is als softwareontwikkelaar nooit je taak te bouwen wat er gevraagd wordt *omdat* het je gevraagd wordt. Wie programmeert wat er gevraagd wordt, codeert een oplossing zonder het probleem goed te hebben doorgrond. Maar dat betekent niet dat je nooit mee hoeft te gaan in een voorgestelde oplossingsrichting. Het gaat erom waarom je erin meegaat. Heb je het probleem zelf doorgrond, en ben je tot de conclusie gekomen dat de stakeholder (of businessanalist) op de best mogelijke oplossing is gestuit? Schroom dan niet die oplossing in code te vatten. 


Meestal verloopt het proces van software ontwikkelen echter heel anders. Wanneer je gevraagd wordt een bepaalde oplossing te bouwen, dien je er eerst achter te komen welk probleem daarmee opgelost wordt. Vervolgens dien je erachter te komen waarom dat probleem een probleem is. Dat zet je vaak op het spoor van een onderliggende vraag of wens. En die wens is vaak beter op een andere manier op te lossen, soms zelfs een eenvoudiger manier -- soms zelfs zonder ook maar één regel code te hoeven schrijven. 


Een goede ontwikkelaar codeert niet zomaar een voorgestelde oplossing. Een goede ontwikkelaar begrijpt eerst het probleem.
