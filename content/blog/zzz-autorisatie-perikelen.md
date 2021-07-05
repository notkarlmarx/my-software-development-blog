---
title: "Autorisatie Perikelen"
author: "Karl van Heijster"
date: 2021-07-04T10:23:40+02:00
draft: true
comments: true
tags: []
summary: ""
---

Onze autorisatiecode begint uit de klauwen te lopen. Het aantal checks op de front end is inmiddels niet meer op één hand te tellen. 


Deze reeks knoppen moet voor gebruikers met deze rol worden uitgeschakeld, een andere reeks knoppen voor gebruikers met die rol worden ingeschakeld, tenzij deze en deze conditie geldt, maar dan weer niet in dit en dit geval. Dat soort dingen.


Dit is geen abnormale situatie in softwareontwikkelland. Het verstrijken van de tijd brengt gewijzigde inzichten met zich mee. Het eenvoudige autorisatiemodel dat we maanden geleden hebben bedacht, blijkt niet altijd even bestand gebleken tegen de realiteit.


Om deze situatie het hoofd te kunnen bieden, hadden we als ontwikkelteam een opdracht meegegeven aan onze Product Owner (PO): teken een autorisatiematrix voor ons uit. Dat is geen eenvoudige opdracht, maar het eindproduct is dat wel: een stel kolommen voor de rollen, en een stel rijen met daarin de handelingen die elke van hen wel of niet uit mag voeren.


Onze PO ging anderhalve week ondergronds met onze informatie-analist. Toen hij het eindresultaat eindelijk kon presenteren aan het team, leidde hij zijn verhaal in met de woorden: "We gaan jullie meenemen."


Dit is doorgaans een slecht teken.


Onze PO en analist hadden een compleet systeem uitgedacht waarin het mogelijk was om voor elke rol, op elk niveau van de applicatie rechten te definiëren, inclusief een complete overervingsstructuur, die op diverse niveaus weer kon worden overschreven.


Na tien minuten zag het team zich genoodzaakt in te grijpen. De kritiek was niet mals. "Dit is niks," zei één ontwikkelaar - of liever: dit is veel te veel. "We ontwikkelen een toetsconstructiesysteem, geen lanceersysteem van nucleaire raketten."


Wat was er gebeurd?


Laat ik deze beroemde illustratie van Hans Kniberg opnieuw aanhalen:


{{<figure src="https://blog.crisp.se/wp-content/uploads/2016/01/mvp.png" width="600" alt="Henrik Kniberg: Making sense of MVP (Minimum Viable Product)" >}}


Onze PO en analist hebben een auto ontworpen. Daar is niets mis mee, want een auto is aan het eind van de dag de beste oplossing voor het op dit moment relevante probleem. Maar een auto is ook duur en complex. 


Daarom is het op korte termijn een beter idee om een skateboard te ontwikkelen. Een skateboard is verre van een ideale oplossing van het probleem, maar het is tenminste wel een oplossing die snel en goedkoop kan worden ingezet.


Onze PO en analist hebben zich mee laten slepen door een visie van wat er uiteindelijk allemaal mogelijk zou moeten zijn - in een ideale wereld, bovendien, waarin tijd en geld geen rol spelen. 


Ze hebben gekeken naar het huidige proces, met alle uitzonderingen die erbij komen kijken, en een oplossing proberen te bedenken die dat complete plaatje ondersteund.


Maar een belangrijke vraag is daarbij over het hoofd gezien: moet je het complete proces inclusief alle uitzonderingen wel *willen* ondersteunen? Of, bescheidener: moet je dat complete proces *nu* willen ondersteunen?


Het team heeft onze PO terug naar de tekentafel gestuurd, ditmaal met de opdracht een autorisatiematrix uit te tekenen voor het proces *zonder* alle mogelijke uitzonderingen. We gaven hem mee: "Stel dat we hiermee 80% van de gebruikers ondersteunen, dan hebben we al 80% winst gemaakt. Met een eenvoudige oplossing bovendien."


Toch vind ik dat onze taak als softwareontwikkelaar er hiermee nog niet op zit. Het is moeilijk om een proces te analiseren - al helemaal als je zo diep in de materie zit als onze PO -, en het kan geen kwaad om daar een helpende hand bij te bieden. Soms heeft iemand een derde persoon nodig die zegt: "Dit gaan we niet doen." En diegene kan maar beter een softwareontwikkelaar zijn, want die heeft er zicht op hoe complex het kan zijn om de oplossing te implementeren.


Soms zit de moeilijkheid van software ontwikkelen niet in de complexiteit van de oplossing. Vaak zit de moeilijkheid in de poging de oplossing zo simpel mogelijk te houden.
