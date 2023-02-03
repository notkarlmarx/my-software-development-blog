---
title: "Waarom documentatie belangrijk is"
author: "Karl van Heijster"
date: 2023-02-03T07:45:02+01:00
draft: false
comments: true
tags: ["documentatie", "intentie van code"]
summary: "Er is behoefte aan documentatie. Documentatie voorziet nieuwe ontwikkelaars van een kader, een context waarbinnen ze de code kunnen begrijpen. Het alternatief is: hen zelf een context laten ontwikkelen op basis van de code. Dat is niet alleen veel tijdrovender, het brengt ook het risico met zich mee dat ze zich een onjuist begrip van de code vormen."
---

Documentatie is misschien wel het minst sexy onderwerp in heel softwareontwikkelland allertijden. - Ga maar na: wanneer heb je voor het laatst een boek gelezen over documentatie, of er een cursus over gevolgd, of een tutorial over bekeken? Wanneer heb je voor de laatste keer een praatje over dat onderwerp gevolgd op een conferentie? Wanneer heb je überhaupt voor laatst gezien dat er een praatje over documentatie werd gegeven?


Ontwikkelaars houden niet van documentatie - en dat is begrijpelijk. Niemand is softwareontwikkelaar geworden omdat 'ie het zo leuk vindt om documentatie te schrijven. Sterker nog, het is *terecht* dat ontwikkelaars niet van documentatie houden. De meeste documentatie is intensief om te schrijven - en nog intensiever om te onderhouden -, terwijl het maar weinig toegevoegde waarde oplevert. Bovendien, het resultaat van al die inspanning is vaak moeilijk vindbaar en wordt daarom niet gelezen - en als het wel vindbaar is, wordt het óók niet gelezen, want de documentatie is al verouderd eer de laatste punten en komma's gezet zijn.


## Nieuw aangenomen


Toch geloof ik dat documentatie belangrijk is. Overdenk de volgende situatie bijvoorbeeld eens:


- Je hebt zojuist nieuw aangenomen als softwareontwikkelaar `:D`
- Je vraagt voor documentatie over een intern project `:)`
- Je krijgt als antwoord: "Er is geen documentatie, kijk gewoon naar de code" `:|`
- De code heeft geen comments `:(`
- De variabelenamen bestaan uit afkortingen van drie letters `>:(`
- De meeste bestanden bestaan uit meer dan 2000 regels code `>:'(`


Wat kunnen we van dit verhaal leren?


## "Goede code documenteert zichzelf"


Ten eerste: die kreet, "Goede code documenteert zichzelf" (zie ook [deze blog](/blog/21/12/goede-code-documenteert-zichzelf-niet/))... Begrijp me niet verkeerd, dit drukt een ontzettend wijs inzicht uit, en elke programmeur is moreel verplicht om 'm ten minste één keer in zijn leven gebruikt te hebben in een verhitte discussie. Elke ontwikkelaar zou ernaar moeten streven om zo descriptief mogelijke namen te verzinnen voor elke class, functie en variabele in de code. En de verhoudingen tussen verschillende delen van het systeem moeten logisch zijn. Verantwoordelijkheden moeten goed gescheiden worden, waardoor het makkelijk is om over de code te redeneren. Een goede softwareontwikkelaar is er tot in zijn vezels van overtuigd dat goede code zichzelf documenteert. 


Maar die kreet kan ook iets heel anders betekenen. "Goede code documenteert zichzelf" betekent te vaak ook: "Ik heb geen zin om documentatie te schrijven". Of: "Ik heb geen tijd om documentatie te schrijven." Er ligt dan nog zo'n grote lijst aan features om op te pakken, dat ontwikkelaars allang blij zijn als ze de code werkend hebben gekregen - ze hebben helemaal geen ruimte om tijd te besteden aan "*nice to haves*" als documentatie.[^1]


Het is belangrijk om je als ontwikkelaar bewust te zijn van dat verschil. Als je zegt dat goede code zichzelf documenteert, propageer je dan een hoge standaard als het om descriptieve code gaat, of creëer je een sluippad om onder het schrijven van documentatie uit te komen?


## Behoefte


De tweede les is veel simpeler nog: er is behoefte aan documentatie. Documentatie voorziet nieuwe ontwikkelaars van een kader, een context waarbinnen ze de code kunnen begrijpen. Het alternatief is: hen zelf een context laten ontwikkelen op basis van de code. Dat is niet alleen veel tijdrovender, het brengt ook het risico met zich mee dat ze zich een onjuist begrip van de code vormen.


Maar het zijn niet alleen nieuwe ontwikkelaars die geholpen zijn bij documentatie. Denk aan iets eenvoudigs als een [code review](/tags/code-reviews/). Wanneer je de code van een ander bekijkt, dan helpt documentatie je om sneller een beeld te vormen van de voor- en nadelen van een gekozen oplossingsrichting. Sterker nog, het helpt je om snel te kunnen beoordelen of het probleem dat de code oplost, überhaupt een probleem was. (Zie ook [deze](/blog/22/09/test-driven-code-reviews/) en [deze](/blog/22/10/pull-requests-als-documentatie/) blog.)


En wat te denken van jezelf, als je aan het ontwikkelen bent? Zonder documentatie zou je geen enkele nieuwe feature kunnen bouwen - hoe zou je immers weten wat er gevraagd wordt? Het is waar dat binnen Agile ontwikkelprocessen de voorkeur wordt gegeven aan gesprekken boven uitgebreide documentatie, maar het kan toch verdomd handig zijn als je na een gesprek met een domeinexpert wat punten op papier hebt gezet die je werkgeheugen tijdens het programmeren kunnen ontzien. 


## Geen traditionele documentatie


Als documentatie zo belangrijk is, moeten we morgen dan allemaal weer teruggaan naar het schrijven van uitgebreide lappen tekst met specificaties? Nee, absoluut niet. Dat is immers precies waar documentatie aan zijn slechte naam kwam.


Die slechte naam is veelal het gevolg van een verkeerde vorm van documentatie voor het verkeerde onderwerp. Geschreven documenten zijn geschikt voor informatie die niet snel verandert. Visiedocumenten, bijvoorbeeld, die beschrijven wat het beoogde doel is van een applicatie. Of architectuurplaten die beschrijven welke applicaties onderlinge afhankelijkheden naar elkaar hebben (of behoren te hebben). Of verslaglegging van de rationale achter een architecturele keuze. Traditionele documentatie is geschikt voor onderwerpen die een relatief grote afstand hebben tot de broncode.


Als je eenmaal dichter bij de implementatiedetails komt te zitten, verliest traditionele documentatie haar waarde. Code verandert constant, en traditionele documentatie *in sync* houden met dat constant veranderend landschap, brengt kosten met zich mee die niet opwegen tegen de baten. 


Naarmate je dichter op de code komt te zitten, zul je op een andere manier moeten documenteren. Architectuurplaten die de verhoudingen tussen verschillende classes (of clusters van classes, gegroepeerd per namespace) kun je bijvoorbeeld beter met bepaalde tooling genereren uit de broncode. En functionele documentatie - de functionele specificaties, de beschrijving van wat een applicatie *doet* -, leg je vast met descriptieve tests.


De vraag die je je moet stellen is niet *of* je documenteert, maar *hoe*. Wie daar meer over wil weten, kan ik overigens van harte [*Living Documentation*](https://www.oreilly.com/library/view/living-documentation-continuous/9780134689418/) aanraden van [Cyrille Martraire](http://cyrille.martraire.com/).


[^1]: Maar vraag jezelf af: waar is de aanname (!) dat documentatie "nice *to have*" is, op gebaseerd? De vraag wordt nog prangender wanneer drukke softwareteams ook dingen als tests als "*nice to have*" gaan zien.
