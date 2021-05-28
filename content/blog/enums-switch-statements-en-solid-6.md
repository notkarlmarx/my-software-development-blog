---
title: "Enums Switch Statemens en Solid Deel 6"
author: "Karl van Heijster"
date: 2021-05-24T12:20:26+02:00
draft: true
comments: true
tags: []
summary: ""
---

# Conclusie

De afgelopen weken heb ik een stuk code gerefactord om meer in lijn te zijn met SOLID-principes. Door gebruik te maken van *Single-Responsiblity*, *Dependency inversion* en het *Open-closed* principe, hebben we de code makkelijker onderhoudbaar gemaakt, zonder de performance van die code te hoeven offeren. De conclusie lijkt duidelijk dus: laat alles vallen wat je doet, en verwerk de SOLID-principes in je code!


- Is het de moeite waard om deze code te refactoren?
- Verandert de code vaak? Zo ja, doen!
- Is de code goed geunittest? Zo nee, laten!
- Heb je op dit moment andere prioriteiten? Zo ja, laten!
- Is de impact van de refactorslag groot? Zo ja, wees dan voorzichtig! Stel dat je op een heleboel plekken hetzelfde switch-statement hebt staan, dan kan de refactorslag zich lonen. Maar hoe groter het aantal switch statements, hoe risicovoller je refactorslag. Zorg dat je weet wat je doet, voordat je gaat refactoren. Het enige dat nog erger is dan een brakke implementatie met veel switch statements, is een halfbakken oplossing: je houdt de switch statements en voegt daar een tweede oplossing aan toe. Dat legt een extra cognitieve last op degene die je code moet onderhouden.