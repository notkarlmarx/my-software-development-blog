---
title: "Tests zijn specs"
author: "Karl van Heijster"
date: 2022-11-11T11:02:04+01:00
draft: true
comments: true
tags: ["communicatie", "documentatie", "samenwerking", "testen", "unit tests"]
summary: "Kleine (of liever: te kleine) tests geven weinig informatie over de werking van het systeem. Ze verlangen van de lezer om op de hoogte te zijn van implementatiedetails, en verliezen zo het grote geheel uit het zicht. Voor grotere unittests gaat die beperking niet op. Zulke tests doen geen aannames over de interne werking van het systeem. Ze beschrijven slechts de buitenkant ervan: wat de gebruiker - hoe we die dan ook mogen definiëren - invoert en wat deze terugkrijgt. Het gevolg daarvan is *dat je tests leesbaar worden voor niet-ontwikkelaars*."
---

Aan het eind van de dag - en aan het begin ook, trouwens - ben ik maar een mens, en daarom luister ik graag naar alles en iedereen die me bevestigt in een mening die ik toch al had. Het deed me - met mijn geschiedenis van blogs over testen via de voordeur ([hier](/blog/22/06/testen-via-de-voordeur/), maar ook [hier](/blog/22/09/tests-als-vangnet/) en [hier](/blog/22/11/wat-is-een-unit/)) - dan ook deugd om [Peter Schuler](https://www.linkedin.com/in/peterschuler/) te horen spreken over grotere unittests tijdens een online bijeenkomst van [Tech Excellence](https://www.meetup.com/techexcellence/):


{{<youtube id="D5YSQkNFu_E" title="Bigger Unit Tests are Better (Peter Schuler)" >}}
<br>


Schuler en ik zitten op één lijn wat betreft de nadelen van een *mockist* visie op testen (ik schreef er [hier](/blog/22/11/wat-is-een-unit/) en [hier](/blog/22/02/de-leercurve-van-angulartests-beklimmen-deel-3/) over). Het voorbeeld dat hij gebruikt om de absurditeit ervan te illustreren vond ik erg sterk. 


## Schroeven en bouten


Stel, je hebt een bout en een schroef. Hoe zou je op een *mockist* manier testen of deze op elkaar passen? 


Je zou - individueel van elkaar, uiteraard - kunnen verifiëren dat de groeven van de schroef en de bout bepaalde afmetingen hebben, en in een aparte validatiestap (handmatig?) verifiëren dat deze overeenkomen. - Dit is wat je doet wanneer je twee componenten in isolatie van elkaar test.


Of! of! of! - je zou ook een wassen schroef respectievelijk bout kunnen maken, en verifiëren of deze inderdaad op de bout respectievelijk schroef past. - Dit is wat je doet als je een *mock* gebruikt.


Maar wat je ook zou kunnen doen is: de bout om de schroef proberen te schroeven. Een sneller en eenvoudiger manier om een antwoord te krijgen op je oorspronkelijke vraag bestaat er niet. - De conclusie is dan ook glashelder: test niet dogmatisch alles in isolatie.


## Leesbaar


Maar Schuler maakt nog een ander interessant punt. Hij merkt op dat (te) kleine tests weinig informatie geven over de werking van het systeem. Ze verlangen van de lezer om op de hoogte te zijn van implementatiedetails, en verliezen zo het grote geheel uit het zicht.


Voor grotere unittests - *front door tests* zou ik ze noemen, ontleend aan het [fantastische](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/) [*Software Engineering at Google*](https://www.oreilly.com/library/view/software-engineering-at/9781492082781/) - gaat die beperking niet op. Zulke tests doen geen aannames over de interne werking van het systeem. Ze beschrijven slechts de buitenkant ervan: wat de gebruiker - hoe we die dan ook mogen definiëren - invoert en wat deze terugkrijgt.


Het gevolg daarvan is *dat je tests leesbaar worden voor niet-ontwikkelaars*.[^1] Dat betekent natuurlijk niet elke man of vrouw die je van de straat plukt, je test zal begrijpen. Maar een business analist of een domeinexpert (die niet onmiddellijk terugdeinst van wat code) weet, met de juiste scope, wel chocola van je test te maken.


## Communicatiemiddel


Waarom is het belangrijk voor een analist of domeinexpert om je test te kunnen lezen? - Omdat dit je in staat stelt om hen concrete scenario's voor te leggen, zonder dat je het systeem op hoeft te starten en in een bepaalde conditie hoeft te brengen. Vragen hoeven niet meer *in abstracto* te worden besproken, of pas te worden beslecht na een moeizaam handmatig proces. 


Het enige wat je hoeft te doen, is de analist of domeinexpert je test voor te leggen, en ze de simpele vraag te stellen: "Heb ik deze requirement zo goed begrepen?" 


Je hebt je tests ontkoppeld van technische implementatiedetails. Je tests specificeren wat het systeem doet voor een eindgebruiker. Ze zijn daarmee een communicatiemiddel geworden, een levend specificatiedocument dat altijd *in sync* is met je code. - Ben ik de enige die dat ontzettend cool vindt klinken? 


[^1]: Aangenomen dat je je voldoende hebt bekommerd om de leesbaarheid van je tests, uiteraard! Ik schreef er [hier](/blog/22/09/tests-als-documentatie/) over. 
