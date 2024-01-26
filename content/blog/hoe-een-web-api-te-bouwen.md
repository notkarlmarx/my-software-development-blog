---
title: "Hoe een Web API te bouwen"
author: "Karl van Heijster"
date: 2024-01-26T10:48:54+01:00
draft: true
comments: true
tags: ["boeken", "recensies", "testen", "web API's"]
summary: "Onlangs las ik *Building Web APIs with ASP.NET Core* van Valerio De Sanctis -- niet omdat het ontwikkelen van Web API's in ASP.NET Core onontgonnen terrein voor me was, maar omdat het nooit kwaad kan om op zoek te gaan naar gaten in je kennis rondom een techniek die je al tijden gebruikt. Bovendien had ik het boek in een vroege fase gereviewd, en ik was benieuwd wat er uiteindelijk van was geworden."
---

Onlangs las ik [*Building Web APIs with ASP.NET Core*](https://www.manning.com/books/building-web-apis-with-asp-net-core) van [Valerio De Sanctis](https://mvp.microsoft.com/en-US/mvp/profile/f42bd1d8-aa90-e811-813c-3863bb2bca60) -- niet omdat het ontwikkelen van Web API's in ASP.NET Core onontgonnen terrein voor me was, maar omdat het nooit kwaad kan om op zoek te gaan naar gaten in je kennis rondom een techniek die je al tijden gebruikt. (Zie ook [deze blog](/blog/23/07/deze-blog-bevat-tooltips/ "'Deze blog bevat tooltips'"), bijvoorbeeld.) Bovendien had ik het boek in een vroege fase gereviewd[^1], en ik was benieuwd wat er uiteindelijk van was geworden. 


Lang verhaal kort: het is een uitstekende inleiding geworden voor iedereen die Web API's in ASP.NET Core wil leren ontwikkelen. Het boek is een ruim vierhonderd pagina lange technische tutorial, waarin De Sanctis de lezer op een aangenaam rustig tempo bij de hand neemt tijdens de ontwikkeling van een [REST API](https://en.wikipedia.org/wiki/REST "'REST', Wikipedia") in .NET. Het boek is daarom een aanrader voor junior ontwikkelaars.


## Technische


Meer ervaren ontwikkelaars zullen het boek wellicht wat minder enthousiast dichtslaan. De focus van *Building Web APIs* ligt namelijk voornamelijk op het technische: welke (framework-specifieke) code moet ik schrijven om bepaalde functionaliteit voor elkaar te krijgen? 


Dat is een valide invalshoek, maar hij matcht niet helemaal met de opzet van het boek. *Building Web APIs* is namelijk gebouwd rondom één uitgebreide *case study*: het implementeren van een REST API waarmee een gebruiker bordspelletjes kan creëren, lezen, aanpassen en verwijderen. De Sanctis loodst *would be* API-ontwikkelaar door het proces van het aanmaken van een nieuw project in [Visual Studio](https://visualstudio.microsoft.com/) tot aan de uitrol naar productie. Onderweg leert de lezer over belangrijke onderwerpen als logging, caching, autorisatie en (zelfs!) documentatie.


## Bochten afsnijden


Het probleem is alleen dat de code die aan het eind van het boek is geschreven, op belangrijke punten (nog) helemaal niet productierijp is. Om de functionaliteit van ASP.NET Core zo duidelijk mogelijk naar voren te brengen, snijdt De Sanctis regelmatig een bocht af in zijn codevoorbeelden. 


Eén van de meest in het oog lopende *bad practices* die hij bijvoorbeeld etaleert, is het volstoppen van de methods in zijn [Controllers](https://learn.microsoft.com/en-us/aspnet/core/web-api/ "'Create web APIs with ASP.NET Core', Microsoft documentatie") met logica -- tot aan het ophalen van data uit de database aan toe. In een productierijpe applicatie is dat uiteraard een *no go*, een schending van het [Single-Responsiblity Principe](/tags/single-responsibility-principe/ "Blogs met de tag 'single-responsibility principe'") (SRP). Het is namelijk niet de verantwoordelijkheid van een Controller-method om *business rules* te handhaven of om data op te halen. Zo'n method zou een zo dun mogelijke schil moeten zijn rondom classes die die verantwoordelijkheid wél hebben. De enige verantwoordelijkheid die aan de Controller-method toebehoort, is het ontsluiten van die classes aan de gebruikers van de Web API.


## Problematisch


De technische insteek van het boek in het achterhoofd houdend, zijn De Sanctis' codevoorbeelden niet per se problematisch. In die zin is dit dan ook geen punt van kritiek. Maar het is wel iets waar je je -- zeker als junior ontwikkelaar! -- goed bewust van moet zijn. De code in *Building Web APIs with ASP.NET Core* is *niet* bedoeld om één op één in productie te gebruiken, het is bedoeld om je bekend te maken met de techniek.


Wel problematisch is de volledige afwezigheid van enige vorm van geautomatiseerd testen van de Web API in het boek. Want de aanwezigheid van tests is misschien niet voldoende om een stuk code productierijp te maken, hun aanwezigheid is daarvoor wel degelijk noodzakelijk. En de infrastructuur hiervoor bestaat ook gewoon. Met de [`WebApplicationFactory` class](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1 "'WebApplicationFactory<TEntryPoint> Class', Microsoft documentatie") is het mogelijk om een virtuele Web API de lucht in te slingeren om [integratietests](/tags/integratietests/ "Blogs met de tag 'integratietests'") tegen af te vuren.


## Niet optioneel


Nu is het zeker waar dat het testen van een Web API zelfs met deze infrastructuur geen eenvoudige opgave is. Om deze tests voor elkaar te krijgen, zal er ofwel een database moeten worden [gemockt](/tags/mocks/ "Blogs met de tag 'mocks'"), of er zal een testdatabase voor moeten worden opgezet. (Dit is gelukkig dankzij het bestaan van [Testcontainers](https://testcontainers.com/) makkelijker dan ooit.) Het is niet ondenkbaar dat De Sanctis' toch al redelijk ruim uitgevallen boek er dankzij dit onderwerp een stuk dikker op zou zijn geworden.


Maar dat is een consequentie die wat mij betreft meer dan gerechtvaardigd is vanwege het signaal dat ze afgeeft: *testen is niet optioneel*. Wie een stuk code in een professionele context naar productie wil loodsen -- of dat nu een Web API is of iets anders --, *moet* nadenken over geautomatiseerde tests. Sterker nog, als gepassioneerd aanhanger van [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) zou ik willen stellen: zo iemand zal *eerst* na moeten denken over geautomatiseerde tests, voordat deze een GET-, POST-, PUT- of DELETE-endpoint uit begint te coderen.


En hoewel ik blij ben dat ik dankzij De Sanctis nu wat meer weet over de gebruiksvriendelijke features van ASP.NET Core, betreur ik het dat die wereld dankzij *Building Web APIs with ASP.NET Core* niet een stap dichterbij is gekomen.
