---
title: "Een kleine stap voor de code..."
author: "Karl van Heijster"
date: 2024-12-13T10:43:26+01:00
draft: true
comments: true
tags: ["continuous integration", "end to end tests", "falen", "leermoment", "software ontwikkelen", "web API's"]
summary: "Het idee dat je software het best kunt ontwikkelen in heel veel heel kleine stapjes hoorde ik voor het eerst in een praatje van Clare Sudbery. Sindsdien is die notie alleen maar dieper mijn brein in gehamerd door Mark Seemanns zeer leesbare *Code That Fits in Your Head*. -- Dus toen een collega van me laatst vastliep op het omschrijven van wat authenticatielogica, sprong ik graag bij. Ik wist immers wat de juiste weg voorwaarts was: heel veel heel kleine stapjes."
---

Het idee dat je software het best kunt ontwikkelen in heel veel heel kleine stapjes hoorde ik voor het eerst in [dit praatje](https://youtu.be/97qyNQz7fxY "'Continuous Integration: That’s Not What They Meant • Clare Sudbery • YOW! 2023', YouTube") van [Clare Sudbery](https://www.linkedin.com/in/clare-sudbery-she-her-35939540/) -- of liever: daar registreerde ik het idee voor het eerst bewust. Sindsdien is die notie alleen maar dieper mijn brein in gehamerd door [Mark Seemanns](https://blog.ploeh.dk/) zeer leesbare [*Code That Fits in Your Head*](https://www.oreilly.com/library/view/code-that-fits/9780137464302/ "'Code That Fits in Your Head: Heuristics for Software Engineering', Mark Seemann, O'Reilly Media").


Dus toen een collega van me laatst vastliep op het omschrijven van wat authenticatielogica, sprong ik graag bij. Ik wist immers wat de juiste weg voorwaarts was: heel veel heel kleine stapjes.


We begonnen inderdaad voorspoedig. De [middleware](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-8.0 "'ASP.NET Core Middleware', Microsoft documentatie") die de [autorisatie](https://en.wikipedia.org/wiki/Authorization "'Authorization', Wikipedia") van onze [Web API](https://en.wikipedia.org/wiki/Web_API "'Web API', Wikipedia") bleek ook verantwoordelijk voor de [authenticatie](https://en.wikipedia.org/wiki/Authentication "'Authentication', Wikipedia"). Dus we maakten een nieuw stukje middleware aan, splitsten de code op, maakten een [*pull request*](/tags/pull-requests/ "Blogs met de tag 'pull requests'") (PR) aan -- en door.


## Administrators en "gewone" gebruikers


De volgende stap was het scheiden van de logica die op rechten van administrators en "gewone" gebruikers checkte. Het was inefficiënt om dit op één en dezelfde plek af te handelen, want het controleren op administratorrechten was maar op een klein aantal endpoints van toepassing. Hier kwam de eerste horde op de weg: deze verantwoordelijkheden bleken niet alleen in de middleware met elkaar verweven te zijn, maar ook in de aangeroepen service.


Nu wilden we onze services sowieso uitfaseren ten faveure van een [*vertical slice architecture*](https://www.jimmybogard.com/vertical-slice-architecture/ "'Vertical Slice Architecture', Jimmy Bogard") (zie ook [deze blog](/blog/24/05/technieken-vs-trucjes/ "'Technieken vs trucjes'")), dus we besloten de oude code niet aan te passen. In plaats daarvan creëerden we twee nieuwe [queries](https://en.wikipedia.org/wiki/Command%E2%80%93query_separation "'Command–query separation', Wikipedia"): één voor de administratorrechten en één voor de "gewone" rechten -- uiteraard: in kleine stapjes. Met [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) ontwikkelden we de ene -- commit! --, daarna de ander -- idem!


We maakten een filter aan op de endpoints van de administrator -- commit! -- en zorgden dat de oorspronkelijke middleware voor die endpoints werd omzeild -- commit!


## De laatste stap


Het enige wat nu nog restte, was de rechten-check van de oorspronkelijke middleware te vervangen door de nieuwe. Opnieuw: kleine stapjes. We vervingen de twee regels die de oorspronkelijke service aanriep door twee regels die gebruik maakte van onze query.


-- En toen ging alles helemaal naar de mallemoer.


In één klap faalden er ruim tachtig tests op tig verschillende endpoints. Geen probleem, dachten we, want onze [*end to end* (E2E)-tests](/tags/end-to-end-tests/ "Blogs met de tag 'end to end tests'") waren wel vaker een beetje flaky. Dus we runden de tests opnieuw -- en opnieuw -- en opnieuw (en dat duurde een hele tijd, want E2E-tests zijn van nature langzaam), maar het gros van die falende tests wilde maar niet weggaan.


Het was inmiddels het eind van de dag en we -- met "we" bedoel ik: "ik" -- werden een beetje kribbig van het gedoe. Maar toen we in de tests doken, bleek al gauw waar het probleem zat: de falende tests gingen uit van het gedrag dat we zojuist hadden gewijzigd. Ze rekenden erop dat een administrator bepaalde dingen deed, waar deze nu geen rechten meer toe had.


Maar het fixen van die tests was geen triviale onderneming. De vooronderstellingen die in de tests waren geslopen, varieerden van overduidelijk tot geniepig subtiel. Bovendien: een kleine stap kun je het onmogelijk noemen, in één keer bijna tachtig tests rechttrekken. 


## Code versus gedrag


Waar was het misgegaan? We hadden toch de hele tijd alleen maar kleine stappen genomen? Hoe kon het dan dat we nu met zo'n grote puinhoop opgescheept zaten?


Pas toen ik die avond terug thuis kwam, viel het kwartje bij me. We hadden kleine stappen genomen vanuit *code*perspectief. Elke wijziging betrof nooit meer dan een handvol regels code. 


Maar die laatste stap, het aanpassen van die middleware, dat was vanuit dat codeperspectief misschien een kleine stap, maar vanuit het *gedrags*perspectief was het een gigantische wijziging. Die twee regels pasten het gedrag aan op *alle* endpoints -- althans, alle endpoints die *niet* voor administrators bedoeld waren.


Het was, om [Neil Armstrong](https://en.wikipedia.org/wiki/Neil_Armstrong "'Neil Armstrong', Wikipedia") te parafraseren, *een kleine stap voor de code, maar een gigantische sprong voor het gedrag van het systeem.*


## Opdracht


Ik had onze opdracht verkeerd begrepen. En de oplossing diende zich onmiddellijk aan: we moesten de endpoints één voor één gebruik laten maken van de nieuwe query. We zouden op elk endpoint een filter kunnen zetten, precies zoals we ook voor de administrator hadden gedaan, de tests van dat endpoint kunnen runnen, en eventueel fixen wat er dan omviel. 


Zo zouden we stap voor stap de nieuwe functionaliteit uitbreiden, net zo lang totdat alle endpoints gebruik maakten van de nieuwe middleware. Op dat moment zou de oorspronkelijke middleware kunnen worden opgeruimd, de applicatie kunnen worden geconfigureerd om voor alle (niet-administrator)endpoints gebruik te maken van de nieuwe logica, en konden alle filters worden verwijderd.


Pas niet aan; [voeg toe, vervang en verwijder](/blog/24/12/aanpassen-of-toevoegen-vervangen-en-verwijderen/ "'Aanpassen of: toevoegen, vervangen en verwijderen'"). Dát is werken in kleine stappen.
