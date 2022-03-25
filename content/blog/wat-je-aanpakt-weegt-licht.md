---
title: "Wat je aanpakt weegt licht"
author: "Karl van Heijster"
date: 2022-03-25T10:28:56+01:00
draft: true
comments: true
tags: ["leermoment", "legacy code", "software ontwikkelen", "verantwoordelijkheid", "zorg"]
summary: "De vloek van een goed functionerend team is dat de organisatie daarvan vindt: die kunnen dit en dat best erbij hebben. De zegening van een goed team is dat de organisatie daarin meestal wel een punt heeft. Dat gezegd hebbende, mijn team was niet blij toen we de opdracht in onze mik geschoven kregen om een bedrijfskritische *legacy* applicatie door te lichten. We hebben ons werk voor die applicatie lange tijd zo ver mogelijk naar achteren geschoven. Maar enkele Sprints terug was het dan toch zo ver. En eerlijk gezegd: het viel alleszins mee."
---

De vloek van een goed functionerend team is dat de organisatie daarvan vindt: die kunnen dit en dat best erbij hebben. De zegening van een goed team is dat de organisatie daarin meestal wel een punt heeft.


Dat gezegd hebbende, mijn team was niet blij toen we de opdracht in onze mik geschoven kregen om een bedrijfskritische *legacy* applicatie door te lichten. Wij concentreerden ons liever op onze eigen applicatie. Deels omdat dat onze taak is, natuurlijk. Maar ook omdat onze eigen applicatie geschreven is door ontwikkelaars die (meestal) wisten waar ze mee bezig waren.


## Andermans code


Maar twee dingen in het leven zijn diepgaand ondoorgrondelijk: het andere geslacht, en andermans code. (En andermans code wil vaak ook zeggen: de code die je jongere ik heeft geschreven. Dat is een teken dat we veranderen naarmate de tijd verstrijkt - en dus in zekere zin niet dezelfde persoon zijn als twee, drie jaar geleden.) 


Al helemaal als die andermans van origine geen ontwikkelaar is. Ik hoef denk ik geen pleidooi te houden voor het feit dat je de zelfstudieprojecten van IT-beheerders niet tot bedrijfskritische applicaties zou moeten verheffen - maar dat was, helaas, nu eenmaal de situatie waar we voor stonden.


We hebben ons werk voor die applicatie lange tijd zo ver mogelijk naar achteren geschoven. Maar enkele Sprints terug was het dan toch zo ver. Vol frisse tegenzin pakten een collega en ik de eerste PBI'tjes op. En eerlijk gezegd: het viel alleszins mee. 


## Onhandig


Natuurlijk, je komt wat onhandige dingen tegen in andermans code. Een veelvuldig aangroepen call naar de database die eerst alle records ophaalt en daar daarna welgeteld één record uit selecteert. - Met enkele duizend records in de database is het geen wonder dat gebruikers mopperden op de performance! 


Sommige zaken waren ronduit raadselachtig. Het ophalen van een `Employee`-object, bijvoorbeeld, dat middels een [`.Select()`-operator](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.select?view=net-6.0) één op één wordt gemapt naar een nieuw `Employee`-object. - Wat er door het hoofd ging van de beheerder die trots die code incheckte? We zullen het nooit weten.


Lastiger dan dit soort laaghangend fruit, was het feit dat de oorspronkelijke ontwikkelaar het niet nodig had gevonden - of waarschijnlijker: er geen rekening mee had gehouden dat het verstandig was - een testomgeving voor zijn applicatie op te zetten. De code zat vol met verwijzingen naar de productiedatabase - en unit tests ontbraken volledig.[^1]


Al met al is het een wonder dat hij zijn applicatie heeft weten te ontwikkelen zonder ernstige schade aan het bedrijf te veroorzaken. Het zou knap zijn, als het niet ook verdrietigmakend was.


## Desinteresse


Het schokkendste aan de code vond ik echter het totale gebrek aan respect waarmee deze gecomponeerd was. De uitlijning was een rommeltje, witregels doken op plekken waar geen weldenkend mens ze zou plaatsen - en ontbraken daar waar je ze zou verwachten. 


Inhoudelijk was de code niet eens een enorme rotzooi. De applicatie is klein en de logica eenvoudig genoeg om als ontwikkelaar snel je weg te vinden. 


Maar de vorm getuigde van een ontmoedigende desinteresse. Dit was een applicatie, geschreven door iemand die verwachtte nooit meer één blik te hoeven werpen op code als deze eenmaal live stond. 


## Het belang van vorm


Je zou kunnen denken: uitlijning, witregels, dat is maar klein bier vergeleken met de nodeloze complexiteit die veel *legacy* applicaties de nek omdraait. En dat is waar. 


Maar de opmaak van de code *wekt de indruk* van nodeloze complexiteit. Het signaleert: dit is code waar de schrijver niet veel om gaf - en zulke code hangt meestal van "slimme" trucs, hacks en schietgebedjes aan elkaar.


Het zou me niets verbazen als deze applicatie al veel eerder door een team professionals onder handen was genomen, als deze alleen maar de indruk had gewekt met zorg in elkaar te zijn gezet. Want eenmaal opgeschoond, hoef je als ontwikkelaar maar twee blikken op de code te werpen, om te zien waar de bug zit. - Dat is het onbedoelde voordeel van een applicatie die is ontwikkeld als zelfstudieproject van een IT-beheerder: zijn code bestaat voor negentig procent uit standaardvoorbeelden. 


## Les


De les is dit: vorm communiceert zorg - of het gebrek eraan. Als de vorm communiceert dat iemand heeft nagedacht over de code, is de stap om mee te denken klein. 


\- Maar de les is ook: vorm zegt niet *alles*. Wat je uitstelt weegt zwaar, wat je aanpakt weegt licht. Of toch in elk geval: lichter dan je vreesde.


[^1]: Waarmee de applicatie zowaar de definitie van *legacy code* belichaamde, zoals uiteengezet in [Michael Feathers](https://michaelfeathers.silvrback.com/) fantastische [*Working Effectively with Legacy Code*](https://www.pearson.com/us/higher-education/program/Feathers-Working-Effectively-with-Legacy-Code/PGM254740.html).
