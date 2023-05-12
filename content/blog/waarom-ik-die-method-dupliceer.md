---
title: "Waarom ik die method dupliceer"
author: "Karl van Heijster"
date: 2023-05-12T10:16:50+02:00
draft: true
comments: true
tags: ["boeken", "refactoren", "testen"]
summary: "Een collega keek over mijn schouder mee. Ik was zojuist bezig met een bugfix, dus ik schreef een test, zag 'm falen en navigeerde naar de plek waar ik mijn aanpassing meende te moeten doen. Ik hernoemde de method, plakte er de suffix `_old` achteraan. Daarna dupliceerde ik het geval, en bracht mijn wijziging aan in het duplicaat.Mijn collega vroeg me: \"Wacht, waarom doe je dat?\" Nou..."
---

Een collega keek over mijn schouder mee. Ik was zojuist bezig met een bugfix, dus ik schreef een test, zag 'm falen en navigeerde naar de plek waar ik mijn aanpassing meende te moeten doen.


Wat ik toen deed, riep wat vragen bij hem op. Ik hernoemde de method, plakte er de suffix `_old` achteraan. Daarna dupliceerde ik het geval, en bracht mijn wijziging aan in het duplicaat.


Mijn collega vroeg me: "Wacht, waarom doe je dat?"


Ik zei: "Zodat ik kan zien wat de oorspronkelijke implementatie was. Dan heb ik vergelijkingsmateriaal. Het is een manier om mijn cognitieve druk te verminderen, om minder code tegelijkertijd in mijn hoofd te houden."


"Maar daar heb je toch *version control* voor?"


Daar had 'ie een punt. 


## Gebroken tests


Ik besefte me later dat mijn antwoord eigenlijk maar de helft was van het verhaal. De oude en de nieuwe implementatie in één oogopslag met elkaar kunnen vergelijken is een aardige bijvangst van deze manier van refactoren - maar het is precies dat: bijvangst.


De eigenlijke reden waarom ik die method dupliceer, is om veilig te kunnen refactoren, om bij elke wijziging zo min mogelijk code te kunnen breken. 


Ga maar na wat er gebeurt als je de oorspronkelijke method *inline* vervangt. Als deze op verschillende plekken in de codebase aan wordt geroepen, dan heeft dit met een beetje pech een flink aantal gebroken tests tot gevolg. 


Als de method eenvoudig is, dan hoeft dat geen groot probleem te zijn. Maar de situatie wordt gevaarlijk als de method lang en complex is, met veel mogelijke codepaden. Verschillende tests kunnen dan om verschillende redenen falen. Op dat moment geven de tests geen informatie meer over wat er mis is met de code. Ze vertellen je alleen nog maar dát er iets mis is.


Al die tests terug zien te brengen naar een groene status, kan een behoorlijke inspanning van een ontwikkelaar vragen. Hij zal flink wat context in zijn hoofd moeten houden om die klus te kunnen klaren.


## Ophakken


Maar als je eerst één aanroep vervangt, dan is de context van je wijziging zonneklaar. Je kunt er zeker van zijn dat de code alleen dáár gaat breken. En je hoeft je tijdens je aanpassing dus alleen maar druk te maken over het laten slagen van de tests die bij die ene aanroep horen. En bij de volgende aanroep die je vervangt, hoef je je alleen maar druk te maken over díe tests.


Een goede ontwikkelaar hakt een complex probleem op in kleinere stukken - en dat is precies wat je hier doet. Het oorspronkelijke probleem was: hoe wijzig ik een method die op meerdere plekken wordt gebruikt? Het nieuwe probleem is: hoe wijzig ik een method die op één plek (c.q. twee, drie, vier plekken) wordt gebruikt?


Tijdens dat spel van één voor één aanroepen vervangen kun je zomaar tot nieuwe inzichten over de code komen. Je kan erachter komen dat bepaalde wijzigingen voor maar één aanroep (of één subset aanroepen) relevant zijn. Op dat moment blijkt de oorspronkelijke method eigenlijk twee dingen te doen. - Dat is een inzicht dat je misschien nooit had opgedaan als je de oorspronkelijke method *inline* vervangen had.


Het is op dat moment doodeenvoudig om de oorspronkelijke aanroep te vervangen voor een method die is toegesneden op die specifieke context - want dat is de enige context waar je je op dit moment op hoeft te focussen.


## Flow


*Big bang* wijzigingen in een codebase zijn altijd riskant. Daarom hanteer ik bij het aanpassen van de code eigenlijk altijd deze flow:


1. Hernoem de method die je wil wijzigen, geef 'm een naam die duidelijk maakt dat deze implementatie aan vervanging toe is. Zorg ervoor dat je de tools in je IDE hiervoor gebruikt, zodat alle referenties naar die method meteen geupdate worden.
2. Dupliceer de method en geef de nieuwe versie de juiste naam. 
3. Wijzig de nieuwe implementatie naar eigen inzicht. 
4. Vind één aanroepende method van de oorspronkelijke method, en laat deze naar de nieuwe implementatie wijzen.
5. Trap je tests af. Slagen alle tests, ga dan terug naar stap 4. Faalt er een test, ga dan terug naar stap 3.
6. Doe dit net zo lang totdat de oorspronkelijke method op geen enkele plek meer aangeroepen word.
7. Verwijder de oorspronkelijke method.


Ik meen dat ik deze techniek over heb genomen uit [*Refactoring*](https://martinfowler.com/books/refactoring.html) van [Martin Fowler](https://martinfowler.com/). Maar het zou ook [*Working Effectively with Legacy Code*](https://www.oreilly.com/library/view/working-effectively-with/0131177052/) van [Michael Feathers](https://michaelfeathers.silvrback.com/) kunnen zijn geweest. Hoe het ook zij, beide boeken zijn aanraders. (Zie ook [deze](/blog/21/08/breek-je-test/) en [deze](/blog/22/04/de-ontwikkelaar-als-chirurg/) blog.)


Enfin, beste collega, dat is dus waarom ik die method dupliceer.
