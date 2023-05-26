---
title: "Het is niet jouw verantwoordelijkheid een onmogelijke deadline te halen"
author: "Karl van Heijster"
date: 2023-05-26T08:07:26+02:00
draft: false
comments: true
tags: ["druk", "falen", "procesverbetering", "professionaliteit", "shift left", "verantwoordelijkheid"]
summary: "Er gebeurt iets wonderlijks wanneer je tegen een ontwikkelteam zegt dat die en die feature een deadline heeft: ze gaan hun best doen om die deadline te halen. Dat is een nobel streven, natuurlijk. Maar het is ook een gevaarlijk gegeven. Want niet elke deadline voor elke feature is even realistisch. Een team dat, ongeacht de haalbaarheid, gaat rennen om die deadline te halen, werkt zichzelf - en haar stakeholders - in de nesten."
---

Er gebeurt iets wonderlijks wanneer je tegen een ontwikkelteam zegt dat die en die feature een deadline heeft: ze gaan hun best doen om die deadline te halen.


Dat is een nobel streven, natuurlijk. Maar het is ook een gevaarlijk gegeven. Want niet elke deadline voor elke feature is even realistisch. Een team dat, ongeacht de haalbaarheid, gaat rennen om die deadline te halen, werkt zichzelf - en haar stakeholders - in de nesten.


## Uitgekauwd


Het gevaar is - in mijn ervaring - het grootst wanneer de feature al helemaal uitgekauwd is, en de deadline belangrijk. De stakeholders zijn verliefd geworden op het idee van bepaalde functionaliteit, en hebben zichzelf ervan overtuigd dat elk facet ervan absoluut noodzakelijk is. Tegelijkertijd laat de deadline geen ruimte voor fouten of nieuwe inzichten.


Er lijkt voor het team niets anders op te zitten dan zich strak aan de planning te houden, te ploeteren desnoods. Dan gebeurt het volgende: men gaat bezuinigen op kwaliteit. Het team implementeert functionaliteit die in de praktijk minder goed werkt dan op papier. Teamleden snijden hoeken af als het op codekwaliteit aankomt. Ze laten de unittests voorlopig maar even voor wat het is. 


Uiteraard beloven ze zichzelf die rommel later op te zullen ruimen. -- Maar later dient zich een nieuwe feature aan, helemaal uitgekauwd, met een belangrijke deadline. Het gevolg laat zich raden.


Er zijn maar weinig ontwikkelaars die zich hier niet schuldig aan hebben gemaakt -- ik ook niet.


## Verantwoordelijkheid


Waar gaat het mis? Op een heleboel vlakken, waarschijnlijk, afhankelijk van de organisatie. Maar een constante factor is de verantwoordelijkheid die een ontwikkelteam op zich neemt -- misschien bewust, maar waarschijnlijk onbewust.


Als een manager het team beveelt: "Bouw die en die feature vóór die en die deadline", dan hoort het team te zeggen: "Joh, laat ons eerst even kijken hoe haalbaar het is." Als de manager tegenwerpt: "Daar hebben we geen tijd voor, we moeten meteen beginnen met bouwen", dan hoort een team te zeggen: "Welke onderdelen van deze feature zijn een absolute must, en welke kunnen we eventueel laten vallen?" Als de manager antwoordt: "Alles is belangrijk", dan hoort een team te zeggen: "Oké, begin je stakeholders dan maar vast op een teleurstelling voor te bereiden."


Maar in plaats daarvan zeggen teams vaak: "Oké, we gaan ons best doen." -- Op dat moment nemen ze een verantwoordelijkheid op zich. Ze nemen de verantwoordelijkheid op zich om een deadline te halen waarvan ze sterk vermoeden -- lees: al heel goed weten -- dat ze die waarschijnlijk gaan missen. 


En, belangrijker nog, ze hebben de manager ontheven van zijn verantwoordelijkheid. Sterker nog, ze hebben hem ontheven van zijn belangrijkste taak: het project managen. De manager heeft die verantwoordelijkheid overgedragen aan het team. En het team vult deze in op de enige manier die ze kennen: met code. -- Brakke, ranzige, ongeteste code, om precies te zijn.


## Single-Responsibility Principe


Het [Single-Responsiblity Principe](/tags/single-responsibility-principe/ "Blogs met de tag 'Single-Responsibility Principe'") (SRP) is, als je het mij vraagt, het belangrijkste principe dat een softwareontwikkelaar consequent moet hanteren in zijn carrière. Want het principe geldt niet alleen voor zijn code.


Een ontwikkelaar moet zich bewust zijn van zijn ultieme verantwoordelijkheid: het opleveren van kwalitatief hoogwaardige code die waarde levert voor zijn of haar opdrachtgever. Wanneer je functionaliteit implementeert die in de praktijk niet blijkt te werken, verzaak je die verantwoordelijkheid. Wanneer je hoeken afsnijdt in de code, verzaak je die verantwoordelijkheid. Wanneer je het verzuimt om je code te unittesten... -- je snapt het idee.


Wanneer je de verantwoordelijkheid op je neemt een project te managen ten koste van het opleveren van nette, foutloze code, dan handel je onverantwoord. Je verzuimt je eigen verantwoordelijkheid -- en die van je manager.


Daarmee is niet gezegd dat dat verantwoordelijkheidsgevoel uit een slechte bron ontspringt. Integendeel, de meeste ontwikkelaars die ik ken, willen niets liever dan hun stakeholders zo goed mogelijk bedienen. Maar ze houden zichzelf en die stakeholders voor de gek wanneer ze een deadline boven kwaliteit stellen. De weg naar een *big ball of mud* is geplaveid met goede bedoelingen.


## Nee verkopen


Hoe zouden ontwikkelaars dan moeten handelen? Ze moeten *nee* verkopen. Als een manager aan komt zetten met een onmogelijke deadline, dan zeggen ze: "Dat is niet haalbaar" -- en ze houden voet bij stuk. Elke consessie op kwaliteit wijzen ze resoluut van de hand. "Nee, we gaan geen half werk leveren. We gaan geen slechte code schrijven. We gaan het testen niet overslaan."


Natuurlijk kun je je manager wel tegemoet komen: "Dit en dat kunnen we wél opleveren vóór de deadline." Als hij tegenwerpt: "Maar daar hebben we niks aan als we de rest niet meenemen!", dan moet de conclusie zijn: "Dan doen we het niet."


Zo'n antwoord zal je niet altijd in dank afgenomen worden. Maar *guess what*: dat geldt ook voor buggy software die maar de helft doet van wat het belooft. Door nee te verkopen kom je dus op precies hetzelfd eindpunt uit -- maar zonder alle verspilling van tijd en geld en gefrustreerde eindgebruikers die het alternatief met zich meebrengt. 


Het is beter de pijn van een gemiste deadline naar voren te halen -- opnieuw: [*shift left*](/tags/shift-left/ "Blogs met de tag 'shift left'") -- door een onhaalbaar plan meteen af te schieten, dan 'm Sprint na Sprint uit te spreiden en dán te concluderen dat het hele idee vanaf het begin gedoemd was.


Het is niet jouw verantwoordelijkheid een onmogelijke deadline te halen. Het is jouw verantwoordelijkheid goede software te ontwikkelen. En daarom is het jouw verantwoordelijkheid om onhaalbare plannen af te schieten. Het is vervolgens de verantwoordelijkheid van je manager om de onvermijdelijke teleurstelling bij stakeholders te verzachten en -- met jouw hulp -- een nieuw, haalbaar plan op te stellen. 


Er gebeurt iets wonderlijks wanneer je op die manier software ontwikkelt.
