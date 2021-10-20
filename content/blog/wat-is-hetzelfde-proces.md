---
title: "Wat is 'hetzelfde proces'?"
author: "Karl van Heijster"
date: 2021-10-18T15:57:08+02:00
draft: true
comments: true
tags: ["communicatie", "informatieanalyse"]
summary: "Hoe verhoudt het proces zich tot de wens van de gebruiker? - En andersom? Is wat *in wezen* hetzelfde proces is, niet *eigenlijk* twee heel verschillende dingen? En hebben gebruikers die erop staan dat "dit echt iets *totaal* anders" is, het wel bij het juiste eind? Die vraag stellen is allesbehalve hem beantwoorden."
---

Schrijven is herschrijven, zegt men ook wel. Met toetsen is het eigenlijk niet anders. Het ontwikkelen van toetsvragen is een kwestie van schrijven, feedback ontvangen, herschrijven, feedback ontvangen, herschrijven - net zolang tot er een goede toetsvraag van de lopende band rolt.


Als toetsen maken je *core business* is, bouw je daar natuurlijk een heel proces omheen. Het ondersteunen van dat proces met software is waar mijn team zich mee bezighoudt.


Het proces kent enkele rollen, bijvoorbeeld[^1] auteurs, redacteurs en reviewers. Die laatste heb je in formele en informele varianten. Maar in wezen vervult elke rol één van de volgende twee verantwoordelijkheden: ofwel men wijzigt de inhoud van toetsvraag, ofwel men beoordeelt zo'n wijziging. Een vraag wordt ofwel geschreven, ofwel bekritiseerd.


## Pingpong


Het stroomdiagram van zo'n proces ziet eruit als een spiraal: een toetsvraag pingpongt constant op en neer tussen de schrijver en de beoordelaar. Of die beoordelaar een collega-auteur is, of een redacteur, of een reviewer is niet eens zo heel belangrijk. Wie naar de stroomdiagrammen van onze organisatie kijkt, zal het vergeven zijn te denken dat het hele proces in essentie maar twee of drie stappen kent.


De opdracht voor de softwareontwikkelaar lijkt daarom heel helder. Er moeten twee dingen gebeuren: er moet een module komen waarin toetsvragen kunnen worden geschreven, en een module waarin iemand feedback kan geven op het geschrevene. 


## Valideren


Toen we met gebruikers gingen praten om onze aannames te valideren, rolde er echter een heel ander beeld uit. Natuurlijk, in essentie klopt het plaatje dat ik hierboven heb beschreven. Maar in de praktijk zijn er toch verschillen. Die komen gauw genoeg aan het licht zodra je wat concrete vragen gaat stellen.


Bijvoorbeeld: stel dat twee mede-auteurs feedback geven op een toetsvraag, mogen zij dan elkaars commentaar zien? - Ja, want het feedbackproces is in deze fase nog informeel. Hoe meer commentaar, hoe beter: de auteurs kunnen alleen maar van elkaar leren! - En twee formele reviewers, mogen die elkaars commentaar zien? - Nee! Want op dat moment is het feedbackproces een formele fase ingegaan, en mogen ze elkaar niet met hun commentaar beïnvloeden.


"Dit is echt iets *totaal* anders!" vinden gebruikers, terwijl wij ons blindstaren op twee identieke feedbackcycli op een whiteboard.


## Context


Context doet er dus toe. Hoewel een proces *in essentie* misschien hetzelfde is, zorgen de concrete omstandigheden voor verschillende behoeften en wensen. Daarom is het ook zo belangrijk om te praten met eindgebruikers, in plaats van alleen af te gaan op abstracte bedrijfsprocessen.


Als softwareontwikkelaar bevind je je in een spagaat. Op macroniveau bouw je enterprise-applicaties om *bedrijfsprocessen* te ondersteunen. Maar op microniveau bouw je software om *gebruikers* te kunnen ondersteunen in hun dagelijkse werkzaamheden. 


Daarom wil je aan de ene kant niet te rigide het bedrijfsproces volgen. Gebruikers kunnen zomaar behoefte blijken te hebben aan iets anders. Maar aan de andere kant wil je niet elke gebruiker alles geven wat zijn of haar leven makkelijker maakt. Want als je dat lang genoeg doet, is er geen bedrijfsproces meer om te volgen.


## Abstract vs. concreet


Je moet constant het midden houden tussen deze twee perspectieven: de abstract essentie aan de ene kant en de concrete praktijk aan de andere. 


Ik geloof niet dat er een makkelijke uitweg is uit deze spagaat - ik heb 'm in elk geval nog niet gevonden. De enige manier om ermee om te kunnen gaan is jezelf te dwingen constant de twee perspectieven tegen elkaar uit te spelen. 


Hoe verhoudt het proces zich tot de wens van de gebruiker? - En andersom? Is wat *in wezen* hetzelfde proces is, niet *eigenlijk* twee heel verschillende dingen? En hebben gebruikers die erop staan dat "dit echt iets *totaal* anders" is, het wel bij het juiste eind? Die vraag stellen is allesbehalve hem beantwoorden. 


Software ontwikkelen is [meer dan code schrijven alleen](/blog/21/06/empathie-met-je-stakeholders/). Het is ook praten, heel veel praten. En constant in het achterhoofd houden: de ogenschijnlijke onmogelijkheid van een (één) antwoord, is het *begin* van een gesprek, en niet het eind. Soms verschilt software ontwikkelen nauweliks van filosofie.


[^1]: Maar niet uitsluitend! Nog ver verwijderd van onze concrete code zwerven platen met "publicisten" en "managers" rond. Als er één ding zeker is in het leven, dan is het wel dat bedrijven hun eigen proces hoe dan ook complexer en complexer maken, en niet altijd ten goede. Wat dat betreft verschillen bedrijven nauwelijks van software.
