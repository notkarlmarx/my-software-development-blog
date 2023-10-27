---
title: "De beste boeken over software ontwikkeling die ik in 2023 las"
author: "Karl van Heijster"
date: 2023-10-27T09:27:49+02:00
draft: true
comments: true
tags: ["boeken", "toplijsten"]
summary: "Lezers en softwareontwikkelaars, opgelet! Net als vorig jaar en het jaar daarvoor en het jaar dáárvoor heb ik dit jaar weer enkele fantastische boeken over softwareontwikkeling mogen lezen. Dit waren mijn vijf favorieten -- plus een niet-per-se-aan-software-gerelateerde bonustip."
---

Lezers en softwareontwikkelaars, opgelet! [Net als vorig jaar](/blog/22/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2022-las/) en [het jaar daarvoor](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/) en [het jaar dáárvoor](/blog/21/05/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2020-las/) heb ik dit jaar weer enkele fantastische boeken over softwareontwikkeling mogen lezen. Dit waren mijn vijf favorieten -- plus een niet-per-se-aan-software-gerelateerde bonustip.


## Top 5


### 1. Steven van Deursen & Mark Seemann - [Dependency Injection: Principles, Practices & Patterns](https://www.manning.com/books/dependency-injection-principles-practices-patterns)


Zelden werd een boek zo goed samengevat als in de aanbevelingstekst op de achterflap van deze moderne klassieker:


> Actually three books in one: a really good introduction to DI in .NET, an even better one to DI in general, and an absolutely excellent introduction to OO principles and software design.
>
> -- Mikkel Arentoft, Danske Bank


*Dependency Injection* is het best geschreven boek over softwareontwikkeling dat ik in lange tijd heb gelezen. Met verhelderende analogieën en uitgebreide codevoorbeelden loodsen auteurs Steven van Deursen en Mark Seemann je door alle concepten die je nodig hebt om [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection "'Dependency injection', Wikipedia") (DI) goed en wel in je codebase te introduceren. 


Maar belangrijker nog: het boek daagt je uit om de manier waarop je software structureert te herevalueren, en prikkelt je opnieuw de [SOLID principes](/tags/solid/ "Blogs met de tag 'SOLID'") te doordenken. Sinds het lezen van dit boek, kijk ik niet meer op dezelfde manier naar mijn codebase. Dat maakt dit een absolute aanrader voor elke ontwikkelaar, of je DI nu al gebruikt in je code of niet.


### 2. Karl Wiegers - [Software Development Pearls: Lessons From Fifty Years of Software Experience](https://www.oreilly.com/library/view/software-development-pearls/9780137487806/)


Nee, ik zet dit boek niet op de lijst omdat de auteur zo'n leuke voornaam heeft -- maar jeetje, wat heeft deze auteur een leuke voornaam! *Software Development Pearls* bekijkt het softwareontwikkelproces hoogover, van het verzamelen van requirements tot het ontwerpen van systemen en het managen van projecten en teams. Elk hoofdstuk bevat een les die Wiegers geleerd heeft in de afgelopen vijftig jaar, wat resulteert in een prettig leesbaar boek tjokvol scherpe inzichten. 


Ik schreef [hier](/blog/23/03/aantekeningen-over-requirements-deel-1/ "'Aantekeningen over requirements - deel 1'") en [hier](/blog/23/03/aantekeningen-over-requirements-deel-2/ "'Aantekeningen over requirements - deel 2'") over Wiegers inzichten rondom requirements.


### 3. Sam Newman - [Monolith to Microservices: Evolutionary Patterns to Transform Your Monolith](https://www.oreilly.com/library/view/monolith-to-microservices/9781492047834/)


De belangrijkste les die dit boek me over microservices leerde was: *-- doe het niet!* Of, preciezer: doe het alleen als je er een heel, heel, héél goede reden voor hebt. Want de baten van microservices wegen maar soms op tegen de kosten die ze met zich meebrengen. -- Ik vermoed dat er een hoop organisaties zijn die dat inzicht hadden willen opdoen tegen de kosten van dit boek! 


*Monolith to Microservices* bevat daarnaast een hoop interessante patronen om je code en data veilig te transformeren van de huidige naar een gewenste situatie. De *big bang* is verleden tijd, Newman opteert voor een evolutionaire aanpak. En daar kan ik alleen maar achter staan.


### 4. Ola Ellnestam & Daniel Brolund - [The Mikado Method](https://manning.com/books/the-mikado-method)


Hoe pak je een non-triviale refactorslag aan? Door gewoon maar te beginnen, maak je van je code een zooitje. Maar wie eerst een zorgvuldige analyse maakt, loopt het risico te verdrinken in mogelijke oplossingen. 


Ellnestam en Brolund stellen een pragmatische aanpak voor: begin met de meest voor de hand liggende verbetering, kijk wat je breekt -- maak een aantekening en draai je wijziging terug. Je hebt nu iets geleerd: wat je zal moeten aanpassen voordat je de meest voor de hand liggende verbetering door kunt voeren. Dus: pas dat aan, kijk wat je breekt -- maak een aantekening en draai je wijziging terug. Doe dat net zo lang totdat je wijziging niets meer breekt, en werk dan stap voor stap terug naar de initiële verbetering.


Dat is in een notendop wat de auteurs de Mikado-methode noemen. Het is een eenvoudige, empirische aanpak om code veilig te kunnen refactoren. De kerninzichten waarop de methode is gestoeld, zijn even wijs als vanzelfsprekend: je vergaart het meeste inzicht in code door ermee aan de slag te gaan, en wijzigingen zijn het best door te voeren in zo klein mogelijke stapjes.


### 5. Neal Ford - [Functional Thinking: Paradigm Over Syntax](https://www.oreilly.com/library/view/functional-thinking/9781449365509/)


Mijn *aha!-erlebnis* met betrekking tot functioneel programmeren (FP) had ik vorig jaar al, toen ik Enrico Buonanno's [Functional Programming in C#](https://www.manning.com/books/functional-programming-in-c-sharp-second-edition) las, maar deze handzame inleiding in het functionele paradigma vormt daar een prima aanvulling op. 


Ford heeft een interessant perspectief op de materie: met FP besteden ontwikkelaars *low level concerns* uit aan de ontwikkelaars van functionele talen. Het wordt niet meer de taak van een ontwikkelaar om te specificeren *hoe* een systeem iets moet doen, maar zoveel mogelijk *wat* deze moet doen. Dat maakt ons leven eenvoudiger -- om voor de hand liggende redenen. Maar komt ook de kwaliteit (waaronder performance) van de code ten goede, want de kans dat de ontwerpers van een taal die *low level concerns* beter zullen implementeren dan jij is -- wees eerlijk -- aanzienlijk.


## Bonustip!


### Daniel C. Dennett - [Darwin's Dangerous Idea: Evolution and the Meanings of Life](https://www.penguin.co.uk/books/15596/darwins-dangerous-idea-by-daniel-cdennett/9780140167344)


Dit is geen boek over softwareontwikkeling, maar het is -- en dat had ik op voorhand niet verwacht -- wel een boek over *design*. Dat maakte Daniel Dennetts filosofische ontleding van de evolutietheorie een fascinerende leeservaring voor mij als filosoof-annex-softwareontwikkelaar. Die fascinatie legde ik in mijn zomervakantie vast in twee blogs -- [hier](/blog/23/09/coderen-met-luchthaken-en-hijskranen/ "'Coderen met luchthaken en hijskranen'") en [hier](/blog/23/10/evolutionair-programmeren/ "'Evolutionair programmeren'") --, en dat zegt wat, want tijdens mijn vakantie wil ik helemaal niet over mijn werk nadenken.


Evolutie is sowieso een terugkerend thema in deze toplijst. *Monolith to Microservices* is het meest voor de hand liggende voorbeeld -- evolutie zit nota bene in de ondertitel van het boek. Maar ook *The Mikado Method* beziet code als een evoluerende entiteit, en hetzelfde kan gezegd worden van de voorbeelden in *Dependency Injection*.


Het afgelopen jaar is me meer dan ooit duidelijk geworden dat softwaresystemen niet statisch zijn. Goede software kent geen bouwfase en geen onderhoudsfase: beide lopen naadloos in elkaar over. Goede software past zich continu aan aan zijn omgeving. Daar zijn kleine, gecontroleerde veranderingen in gedrag (en onderliggend: code) voor nodig, die gevalideerd moeten worden door het systeem "in het wild" los te laten.


Als softwaresystemen (noodgedwongen) evolutionerende entiteiten zijn, dan kunnen wij als ontwikkelaars veel over ons vak leren door ons te verdiepen in de evolutietheorie.
