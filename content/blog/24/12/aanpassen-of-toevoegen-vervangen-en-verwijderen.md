---
title: "Aanpassen of: toevoegen, vervangen en verwijderen"
author: "Karl van Heijster"
date: 2024-12-06T07:58:31+01:00
draft: false
comments: true
tags: ["refactoren"]
summary: "Laatst wilde ik een methodsignatuur op een interface aanpassen. Een naïeve manier om dat aan te pakken, zou zijn: pas de signatuur op de interface aan, kijk naar de compilatiefouten die dat oplevert op de implementerende classes, en werk die weg. -- Maar het probleem van die aanpak is dat dit de codebase voor langere tijd in een gebroken staat houdt."
---

Laatst wilde ik een methodsignatuur op een interface aanpassen. Een naïeve manier om dat aan te pakken, zou zijn: pas de signatuur op de interface aan, kijk naar de compilatiefouten die dat oplevert op de implementerende classes, en werk die weg. 


Het probleem van die aanpak is dat dit de codebase voor langere tijd in een gebroken staat houdt. Zolang er compilatiefouten zijn, is het onmogelijk om de tests te runnen. Pas als alle implementaties zijn rechtgetrokken, is het mogelijk om feedback te krijgen op de wijziging. 


En de kans is groot dat die feedback uiteindelijk zal uitwijzen dat er op meerdere plekken -- in meerdere implementerende classes -- fouten in de code zijn geslopen. Terwijl de tests één voor één gefixt worden, blijft het systeem als geheel in gebroken staat.


Maar het doel van geautomatiseerde tests is juist om jou als ontwikkelaar op het rechte pad te houden tijdens de refactoring. Het brengt een risico met zich mee te refactoren -- en te blijven refactoren -- terwijl een deel van de tests faalt.


## Een minder naïeve manier


Dit is een minder naïeve manier om een methodsignatuur op een interface aan te passen[^1]: voeg een nieuwe method toe met de aangepaste signatuur, en implementeer die method in de implementerende classes -- maar voorlopig met niet meer dan wat dummy-gedrag, zoals het opgooien van een [`NotImplementedException`](https://learn.microsoft.com/en-us/dotnet/api/system.notimplementedexception "'NotImplementedException Class', Microsoft documentatie"). 


Wijzig vervolgens de aanroepende code: laat deze de nieuwe method aanroepen in een [`try catch`-blok](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/exception-handling-statements "'Exception-handling statements - throw, try-catch, try-finally, and try-catch-finally', Microsoft documentatie"), met in de `try` de nieuwe versie en in de `catch` de oude. Vervang vervolgens de dummy-implementatie van elke implementerende class met een correct werkende versie. 


Als alle implementaties zijn vervangen, verwijder dan het `try catch`-blok en de oorspronkelijke method van de interface en van de implementerende classes.


Wanneer er fouten sluipen in een van de nieuwe implementaties, dan zullen alleen de tests van *die* class falen -- alle andere blijven in groene staat. Op die manier blijven je tests gericht feedback geven over de werking van de code: je refactort niet blind.


## Productiviteit


De minder naïeve manier is op het eerste gezicht omslachtiger, maar dat is schijn. Het is eenvoudiger om code aan te passen wanneer de feedbackloops kort zijn. Het is eenvoudiger om je doel te bereiken in veel kleine stapjes, en bij elke stap te checken of je nog op de juiste weg bent. 


Het is juist omslachtig om code aan te passen zonder [vangnet](/blog/22/09/tests-als-vangnet/ "'Tests als vangnet'"). Het is risicovol grote stappen te zetten zonder zeker te weten dat je de juiste kant op loopt.


De productiviteit van een ontwikkelaar wordt niet gedefinieerd door de snelheid waarmee deze code aanpast. Het is verstandiger langzaam maar veilig te werken dan snel en onverantwoord.


[^1]: Zie [deze blog](/blog/23/07/waarom-ik-die-method-dupliceer/ "'Waarom ik die method dupliceer'") voor een variatie op dit thema.
