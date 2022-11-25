---
title: "Wel code reviews, geen pull requests"
author: "Karl van Heijster"
date: 2022-11-25T09:22:26+01:00
draft: true
comments: true
tags: ["code reviews", "procesverbetering", "pull requests", "samenwerking", "shift left", "sprint retrospective"]
summary: "Tijdens een Sprint Retrospective zei ik: \"Ik heb het gevoel dat het te lang duurt voordat onze *pull requests* (PR's) worden gecodereviewd. Hebben andere mensen datzelfde idee?\" Ja, ze hadden hetzelfde idee. We spraken af: als je merkt dat er niets met je PR gedaan wordt, trek dan iemand even aan de jas. Als PR's te lang open blijven staan, dan moet je actief een reviewer erbij betrekken. Het is een oplossing die vooralsnog goed genoeg werkt. Maar hij laat een belangrijke oorzaak - misschien wel dé belangrijkste oorzaak - van het probleem in stand: het bestaan van PR's überhaupt."
---

Tijdens een Sprint Retrospective zei ik: "Ik heb het gevoel dat het te lang duurt voordat onze *pull requests* (PR's) worden gecodereviewd. Hebben andere mensen datzelfde idee?" Ja, ze hadden hetzelfde idee. 


De gevolgen lieten zich raden. Ontwikkelaars willen terecht niet zitten duimendraaien tot hun PR goedgekeurd is. Dus borduren ze in bij het oppakken van hun volgende taak voort op de *branch* van het openstaande PR. Uiteindelijk komt daar commentaar op. In het beste geval, levert dat wat minieme wijzigingen op, die weinig invloed hebben op hun nieuwe code. - Maar in het slechtste geval komt het commentaar met zulke ingrijpende verbetervoorstellen, dat die nieuwe code eigenlijk onmiddellijk weer de prullenbak in kan.


## Oorzaken


Het team was heus doordrongen van de noodzaak om code zo snel mogelijk door het codereviewproces te loodsen (zonder op de kwaliteit te beknibbelen, natuurlijk!). Waarom bleven de PR's dan zo lang open staan?


Eén collega zei: ik word tegenwoordig zoveel in vergaderingen getrokken, dat het voor mij onmogelijk wordt om voldoende ononderbroken tijd vrij te maken om de code te kunnen bekijken. Een andere collega verklaarde dat hij al zijn tijd al kwijt was aan zijn eigen programmeerwerkzaamheden, om daarna dan nog andermans code te bekijken was gewoon te vermoeiend. Een derde collega zei niets, maar hij dacht waarschijnlijk wat de meeste programmeurs denken: ik vond code schrijven heel leuk - code lezen een stuk minder.


We spraken af: als je merkt dat er niets met je PR gedaan wordt, trek dan iemand even aan de jas. Als PR's te lang open blijven staan, dan moet je actief een reviewer erbij betrekken.


## Belangrijkst


Het is een oplossing die vooralsnog goed genoeg werkt. Maar hij laat een belangrijke oorzaak - misschien wel dé belangrijkste oorzaak - van het probleem in stand: het bestaan van PR's überhaupt.


Dave Farley legt het in de onderstaande video heel netjes uit:


{{<youtube id="UQrlEXU6RM8" title="Why Pull Requests Are a Bad Idea • Dave Farley • GOTO 2022">}}
<br>


Lang verhaal kort: codereviews zijn ontzettend belangrijk - PR's niet per se. 


Codereviews zijn belangrijk, omdat twee meer weten dan één. De codereviewer kan een oplossingsrichting voorstellen waar de codeur niet aan gedacht heeft. Daarnaast dient de codereviewer als check: jij snapt de code misschien wel, maar snapt iemand anders 'm ook? Codereviews zijn een essentieel middel om de kwaliteit van de code op peil te houden. Het is *altijd* een goed idee om twee paar ogen over de code te hebben laten gaan.


## Beslispunt


PR's zijn minder belangrijk. Deze zijn oorspronkelijk in het leven geroepen voor open source-projecten waarbij de onderhouder van de code niet per se één op één contact had met degene die een wijziging wil maken in de code base. In zo'n context is het belangrijk om een expliciet beslispunt in te bouwen: sta ik deze wijziging toe, of wijs ik 'm af?


Maar de context van een teamproject is totaal anders. Hier is het wel mogelijk om één op één contact te hebben met de maker van de wijziging. En daar volgt uit: je moet codereviewen, maar niet per se middels PR's.


## Pair programming


De vraag wordt dan: wanneer codereview je dan wél? En het antwoord is: niet aan het eind van het proces - maar doorlopend. Je gaat er naast zitten, en je kijkt met iemand mee, denkt hard op na, doet verbetervoorstellen terwijl de code wordt geschreven. (En je wisselt die rol af met het schrijven van code, natuurlijk, want niemand houdt van iemand die alléén maar kritiek heeft.) Met andere woorden: je programmeert in paren - *pair programming*.


Dat idee is niet nieuw. Al aan het begin van het jaar hoorde ik [de mannen van Codurance hun bedenkingen uiten over codereviews](https://www.youtube.com/watch?v=Q0oKYyBIKVE). Alle voordelen daarvan - betere kwaliteit, maar ook kennisdeling op het technische én domeininhoudelijke vlak - zouden met *pair programming* kunnen worden afgevangen, zonder de nadelen van traditionele codereviews.


Maar, zoals zo vaak, valt het kwartje pas als je er eigenhandig hinder van ondervindt.


De komende tijd heb ik mezelf dus voorgenomen vaker te *pair programmen* met mijn collega's. Zal ik na verloop van tijd niet meer terug willen naar solocodeersessies, afgesloten met een kritische codereview? We zullen het merken!
