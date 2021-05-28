---
title: "Objectgeoriënteerd Denken"
author: "Karl van Heijster"
date: 2021-05-28T12:37:05+02:00
draft: true
comments: true
tags: []
summary: ""
---

Waarom lees ik een inleiding in objectgeoriënteerd programmeren?


Het viel me op dat onze code base, ondanks dat deze in C# is geschreven, op bepaalde plekken behoorlijk gestructureerde code bevat. Het betreft met name helper-classes.
Dit jeukt bij mij. Dat zal voor een deel een stijldingetje zijn, maar een deel van me meent ook dat die code beter zou moeten kunnen.


Met dit boek hoopte ik wat handvaten te vinden om die code te kunnen refactoren. Het was met name de titel die me die kant op stuurde. Ik wilde het objectgeoriënteerde gedachteproces meer internaliseren in de hoop daarmee een uitweg te zien uit die structurele onderdelen.


Het boek zelf legt met name de nadruk op dingen als inheritance en composition. De voorbeelden zijn ontleend aan dagelijkse objecten: stel dat je een hond of een auto zou moeten modelleren, hoe zou dat er dan uitzien?


Je merkt dat het boek is geschreven voor programmeurs die zich het vak eigen hebben gemaakt in een gestructureerd paradigma, dat komt goed uit.


Klassieke objectgeoriënteerde concepten zoals inheritance en polymorfisme zijn eigenlijk niet de sleutel om die gestructureerde code weg te refactoren. Het is met name een gedachtegang die gedurende het hele boek op de achtergrond aanwezig is: het gaat om objecten. 


De crux zit hem in het feit dat een “helper” geen object is. Althans, geen vastomlijnd object. En dat zorgt ervoor dat je het design van die class (voor zover je daarvan kan spreken, want dit soort classes ontstaan eerder dan dat ze ontworpen worden) geen best practices honoreert.


Concreet voorbeeld: het zoeken naar een bepaalde item was ingebouwd in onze ItemService. De benodigde informatie werd aan elke method middels een parameter doorgegeven. Dit is een schoolvoorbeeld van gestructureerde code. Ik kon al deze methods in één klap naar een aparte (static) class verplaatsen en de boel bleef werken. Het voordeel daarvan was dat ik wat encapsulation had bereikt - maar één method hoefde daadwerkelijk zichtbaar te zijn voor de ItemService -, maar de boel bleef wel behoorlijk procedureel. Door deze methods als een object te gaan beschouwen - geen ItemHelper maar een ItemSearcher -, kon ik de boel ombouwen om meer objectgeoriënteerde concepten toe te passen. Middels composition - het strategy pattern: SearchStrategies - kon ik de boel ook flexibel uitbreiden.
