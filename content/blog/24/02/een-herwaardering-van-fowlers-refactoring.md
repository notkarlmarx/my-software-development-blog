---
title: "Een herwaardering van Fowlers Refactoring"
author: "Karl van Heijster"
date: 2024-02-02T08:25:54+01:00
draft: false
comments: true
tags: ["boeken", "refactoren", "software ontwikkelaar (rol)"]
summary: "Martin Fowlers *Refactoring* is een klassieker in het genre -- en baanbrekend voor zijn tijd. Boeken over het ontwerp van nieuwe software bestaan al zo lang als dat software bestaat. Maar het idee dat je bestaande code *aan kon passen* -- niet als noodzakelijk kwaad, maar als essentiële vaardigheid van elke programmeur --, dat was ongekend. -- En toch was ik teleurgesteld toen ik het boek uitlas, drie jaar geleden."
---

[Martin Fowlers](https://martinfowler.com/) [*Refactoring: Improving the Design of Existing Code*](https://martinfowler.com/books/refactoring.html) is een klassieker in het genre -- en baanbrekend voor zijn tijd. Boeken over het ontwerp van nieuwe software bestaan al zo lang als dat software bestaat. Maar het idee dat je bestaande code *aan kon passen* -- niet als noodzakelijk kwaad, maar als essentiële vaardigheid van elke programmeur --, dat was ongekend.


## Teleurgesteld


En toch was ik teleurgesteld toen ik het boek uitlas, drie jaar geleden.[^1] Een eerste bron van teleurstelling zit 'm in de ondertitel ervan -- of liever, mijn interpretatie ervan: *Improving the Design of Existing Code*. Ik las *Refactoring* met de verwachting dat het boek me iets zou leren over het ontwerpen van code. Ik verwachtte dat ik, als ik het boek eenmaal uit zou hebben, een beter idee zou hebben van hoe goede code eruit zou zien.


Maar dat is niet wat *Refactoring* biedt. Fowler houdt zich niet bezig met de inhoudelijke vraag of het ene ontwerp beter is dan het andere. Hij biedt "slechts" de technieken om een ontwerp te verbeteren, gegeven het feit dat een beter ontwerp voorhanden is. Hij zegt niet: pas *die* techniek in *deze* gevallen toe, en *deze* techniek en *die* gevallen. Het zou ook onzinnig zijn om dat te proberen, besef ik nu. Want of een ontwerp goed in elkaar steekt, hangt af van de context, en de context is voor geen twee projecten hetzelfde.


## Catalogus


De technieken zelf dan. *Refactoring* bestaat voor het grootste deel uit een catalogus van diverse refactorings: hoe je een functie extraheert of juist weer *inline* maakt, hoe je een veld van een subclass naar een baseclass verplaats en andersom, hoe je een constructor vervangt door een *factory* method. Van elke techniek legt Fowler in -- ik wil haast zeggen: pijnlijk -- detail bloot hoe je deze toe dient te passen.


De meeste van zijn refactortechnieken zijn geen hogere wiskunde. Sterker nog, het gros ervan kan eenvoudig worden geautomatiseerd -- en dat is precies wat er in de jaren na publicatie is gebeurd. Wie tegenwoordig een method wil abstraheren, hoeft niet meer de moeite te nemen een nieuwe method te declareren, de oorspronkelijke code te kopiëren en plakken, en de compileerfouten op te lossen. Dat zijn taken die je aan je [IDE](https://nl.wikipedia.org/wiki/Integrated_development_environment "'Integrated development environment', Wikipedia") overlaat.


## Miniscuul


De vraag wordt dan: als ik als ontwikkelaar niet meer de stappen voor elke individuele refactortechniek hoef te onthouden, wat is het nut nog van *Refactoring* (het boek dus, niet de techniek *an sich*)? -- Het antwoord zit 'm niet in de inhoud van elke refactorslag, maar in hun reikwijdte. Meer specifiek: hun miniscule reikwijdte.


Want de technieken die Fowler presenteert *zijn* miniscuul -- en dat is precies waarom ze zo waardevol zijn. Veel ontwikkelaars -- ook ik, bijvoorbeeld in [deze blog](/blog/22/08/twee-stijlen-van-refactoren/ "'Twee stijlen van refactoren'") -- nemen veel te grote stappen wanneer ze hun code aanpassen. Ze smijten met variabelen, properties en methods en kijken vervolgens vreemd op wanneer hun code een zooitje is geworden.


Schade en schande heeft me geleerd: code schrijven gaat het best in heel veel heel kleine stapjes.[^2] Sterker nog, het nemen van kleine stappen is onderdeel van de kern van ons vak. Eén van de belangrijkste vaardigheden van elke ontwikkelaar is het vermogen om een groot probleem op te delen in deelproblemen -- en, als het nodig is, die deelproblemen in kleinere deelproblemen.


## Hoe verander ik code?


"Hoe verander ik het ontwerp van deze code?" is zo'n groot probleem. Een deelprobleem is: "Hoe extraheer ik een variabele uit deze logica?" De oplossing van dat deelprobleem is te vinden op bladzijde 119 t/m 122 van de tweede editie. 


Ga na: Fowler besteedt 4 pagina's aan een refactoring die elke ontwikkelaar vrijwel dagelijks uitvoert! We moeten ons niet in de luren laten leggen door de alomtegenwoordigheid van deze codewijziging: ook iets zo simpel als dit bestaat uit discrete stappen. Wanneer we deze één voor één volgen, wijzigen we de code veilig -- en veiligheid is allesbehalve een gegeven in softwareontwikkeling.


Fowlers *Refactoring* is een masterclass in het nemen van kleine stappen om een probleem op te lossen -- en dus een masterclass in softwareontwikkeling. Mijn teleurstelling was volledig ongegrond: het boek is vandaag de dag nog net zo relevant als bij verschijnen -- niet om wat Fowler zegt, maar om wat hij *toont*.


[^1]: Al ontging de kwaliteit van Fowlers werk me niet helemaal: het boek eindigde "slechts" in de eervolle vermeldingen van [de beste boeken over softwareontwikkeling die ik in 2021 las](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/). 


[^2]: Mijn dank gaat ook uit naar [Clare Sudbery](https://www.linkedin.com/in/clare-sudbery-she-her-35939540/), die dit punt herhaaldelijk maakte in [haar praatje over *continuous integration* op GOTO Amsterdam](https://youtu.be/97qyNQz7fxY "'Continuous Integration: That’s Not What They Meant • Clare Sudbery • YOW! 2023', YouTube"), zie [deze blog](/blog/23/09/doe-je-wel-echt-aan-continuous-integration/ "'Doe je wel écht aan continuous integration?'").
