---
title: "Incidentanalyse zonder schuldigen"
author: "Karl van Heijster"
date: 2022-05-13T08:31:51+02:00
draft: false
comments: true
tags: ["boeken", "incidentanalyse", "leercultuur", "procesverbetering", "productieverstoring", "verantwoordelijkheid"]
summary: "Wat doet jouw team na een productieverstoring? En wat doet jouw team als een eindgebruiker een bug meldt? - Wat bij een grote bug? Wat bij een kleine? Neem je het ter kennisgeving aan, en ga je op dezelfde weg door? Ga je met vingers wijzen en mensen uitfoeteren voor hun nalatigheid? Of kijk je naar manieren waarop je de productieverstoring of bug in de toekomst kunt voorkomen? En waar kijk je dan naar - naar het individu, of het systeem?"
---

Het is een *best practice* om na elke productieverstoring met het team bij elkaar te komen en te bekijken hoe deze heeft kunnen gebeuren. Die praktijk wordt ook wel een *post mortem* genoemd. Maar dat klinkt wat macaber, daarom verkiest [James Shore](https://www.jamesshore.com/) in [*The Art of Agile Development*](https://www.oreilly.com/library/view/the-art-of/9780596527679/) de term *incidentanalyse*.


## *Better practice*


Het is een *better practice* om dit te doen bij elke bug die op de productieomgeving terecht komt, niet alleen de bugs die je eindgebruikers het werk onmogelijk hebben gemaakt. (En een bug wil hier zoveel zeggen als: alles wat naar de productieomgeving is gegaan en achteraf toch nog *rework* behoefde.) Zelfs een typfout verdient het om besproken te worden door het team. Hoe kan het dat een eindgebruiker de applicatie kon configureren in het *Enghlish* in plaats van het *English*?


Klinkt overdreven? Misschien. Maar Shore maakt een goed punt: dezelfde factoren die ervoor zorgen dat een typfout overleeft tot aan de eindgebruiker, zorgt ervoor dat een catastrofale bug het overleeft. In beide gevallen geldt: het systeem dat wij als ontwikkelaars hebben opgezet om te voorkomen dat fouten eindgebruikers bereiken, heeft gefaald.


## Systeem


Het sleutelwoord in die zin is: *systeem*. Een goede incidentanalyse neemt het perspectief van het systeem in. De handelingen van individuen maken onderdeel uit van dat systeem, zeker, maar het is de verantwoordelijkheid van het systeem om ervoor te zorgen dat een foutieve handeling tijdig wordt opgemerkt en gecorrigeerd.


Een goede incidentanalyse ziet er dan ook niet zo uit: "Jan checkte code met een bug in, en daardoor crashte de applicatie. Jan moet de volgende keer dus beter zijn best doen om code te schrijven die geen bugs bevat." Die analyse legt de schuld eenzijdig bij Jan. Maar Jan is maar een actor in het systeem. En zijn foutieve code is misschien wel de oorzaak van de bug, maar dat is iets anders dan te zeggen dat Jan - en Jan alleen - verantwoordelijk is voor die foutieve code.


Een betere incidentanalyse zou zijn: "Jan checkte code met een bug in, en daardoor crashte de applicatie. De bug werd niet opgemerkt tijdens de codereview. Er waren geen unit tests voor het stuk code waarin Jan de wijziging deed die deze bug konden afvangen. De tester heeft niet het pad getest waarin de bug optrad. Hetzelfde geldt voor de acceptant van de *story*." - Ben je, na dit alles gelezen te hebben, nog steeds van mening dat de schuld van de bug eenzijdig bij Jan ligt?


## Zwakke plekken


Het doel van een incidentanalyse is: erachter komen waar de zwakke plekken in jullie systeem van software ontwikkelen ligt. Fouten zullen altijd gemaakt worden, dat is het punt niet. Maar dat betekent niet dat fouten noodzakelijkerwijs hun weg naar de productieomgeving moeten kunnen vinden. Een goed systeem merkt zo'n fout in een eerder stadium op, en sluit de boel kort.


En een goed systeem merkt een fout *zo vroeg mogelijk* op. Je kunt een systeem verbeteren door de acceptant van een *story* beter te instrueren in zijn of haar manier van testen, of door als tester meer tijd uit te trekken om een nieuwe feature goed door te testen, of als codereviewer wat grondiger de implicaties van elke regel code te doordenken. Maar nog beter zou zijn als je unit tests schrijft voor elke nieuwe regel code - liever nog: dat je die code schrijft middels [Test-Driven Development](/tags/test-driven-development/). Hoe eerder je systeem in staat is een fout op te merken, hoe beter het systeem functioneert om de fout te voorkomen.


## Geen schuldigen


Incidentanalyses zijn niet bedoeld om schuldigen aan te wijzen.[^1] *Er zijn geen schuldigen bij incidenten* - vanuit een systeemperspectief valt er niemand aan te wijzen die de verantwoordelijkheid draagt voor een bug. Er valt alleen maar vast te stellen dat het systeem als geheel niet gewerkt heeft, en er valt vast te stellen welke gaten in het systeem gedicht worden om een soortgelijk incident in de toekomst te voorkomen. - Dat is waar de winst te behalen valt.


Dus vraag jezelf eens af: wat doet jouw team na een productieverstoring? En wat doet jouw team als een eindgebruiker een bug meldt? - Wat bij een grote bug? Wat bij een kleine? Neem je het ter kennisgeving aan, en ga je op dezelfde weg door? Ga je met vingers wijzen en mensen uitfoeteren voor hun nalatigheid? Of kijk je naar manieren waarop je de productieverstoring of bug in de toekomst kunt voorkomen? En waar kijk je dan naar - naar het individu, of het systeem? 


[^1]: Bij Google spreekt men van *blameless post mortems*. Ik kwam de term voor het eerst tegen in de bundel [*Building Secure & Reliable Systems*](https://www.oreilly.com/library/view/building-secure-and/9781492083115/).
