---
title: "De Kwestie Autorisatie"
author: "Karl van Heijster"
date: 2021-07-26T16:15:03+02:00
draft: false
comments: true
tags: ["agile ontwikkeling", "autorisatie", "incrementele ontwikkeling", "iteratieve ontwikkeling", "software architectuur", "software ontwikkelen", "waarde"]
summary: "Onze Product Owner ging anderhalve week ondergronds met onze informatie-analist om een autorisatiematrix uit te tekenen. Toen hij het eindresultaat eindelijk presenteerde aan het team, leidde hij zijn verhaal in met de woorden: \"We gaan jullie meenemen.\" Dat was een slecht teken."
---

# Of: Incrementele Versus Iteratieve Ontwikkeling In De Praktijk


Op een gegeven moment begon onze [autorisatiecode](https://en.wikipedia.org/wiki/Authorization) uit de klauwen te lopen. Het aantal checks op de front end was niet meer op één hand te tellen. 


De ene reeks knoppen moest voor gebruikers met die en die rol worden uitgeschakeld, een andere reeks knoppen voor gebruikers met deze en deze rol worden ingeschakeld, tenzij die en die conditie gold, maar dan weer niet in dit en dit geval. Dat soort dingen.


Aan de back end was de situatie nog nijpender. Omdat het aantal checks - en uitzonderingen daarop - zo talrijk werd, ontstonden er gaten in de beveiliging. De boel onderhouden was zo arbeidsintensief geworden, dat het verleidelijk werd om de [*Authorize*-attributen op onze Controllers](https://docs.microsoft.com/en-us/aspnet/core/security/authorization/simple?view=aspnetcore-5.0) maar helemaal te laten schieten.


## Een verzoek


Dit is geen abnormale situatie in softwareontwikkelland. Het verstrijken van de tijd brengt gewijzigde inzichten met zich mee. Het eenvoudige autorisatiemodel dat we maanden eerder hadden bedacht, bleek maar matig bestand tegen de realiteit.


Om deze situatie het hoofd te kunnen bieden, hadden we als ontwikkelteam een opdracht meegegeven aan onze [Product Owner](https://www.scrum.org/resources/what-is-a-product-owner) (PO): teken een functionele opzet uit voor een autorisatiematrix. 


Dat is geen eenvoudige opdracht, al zou je dat op basis van het eindproduct misschien niet zeggen. Dat is niet meer dan een stel kolommen voor de rollen, en een stel rijen met daarin de handelingen die elke van hen wel of niet uit mag voeren. Zoiets dus:


|                 | Rol A | Rol B | Rol C |
| --------------- | ----- | ----- | ----- |
| **Handeling A** | x     |       | x     |
| **Handeling B** | x     | x     |       |
| **Handeling C** |       |       | x     |


## Een antwoord


Onze PO ging anderhalve week ondergronds met onze informatie-analist. Toen hij het eindresultaat eindelijk kon presenteren aan het team, leidde hij zijn verhaal in met de woorden: "We gaan jullie meenemen."


Dat was een slecht teken.


Wat bleek: onze PO en analist hadden een compleet systeem uitgedacht waarin het mogelijk was om voor elke rol, op elk niveau van de applicatie rechten te definiëren, inclusief een complete overervingsstructuur, die op diverse niveaus weer kon worden overschreven.


Laat ik vooropstellen dat ons team een fantastische PO kent, en een minstens zo fantastische analist. En laat ik benadrukken dat hun samenwerking het team meermaals heeft gezegend met uitstekend uitgewerkte functionele specificaties. De twee werken perfect samen.


Soms iets te perfect.


Na tien minuten riep het team in wanhoop uit: "We ontwikkelen een applicatie om toetsen mee te construeren, geen lanceersysteem van nucleaire raketten!" Eén ontwikkelaar verwoordde het heel kernachtig toen hij zei: "Dit is niks. Of liever: dit is veel te veel."


## Waar het mis ging (1)


Wat was er gebeurd? Er zijn geloof ik twee dingen misgegaan. Deze hangen op een subtiele manier met elkaar samen, maar zijn niet hetzelfde. 


Het eerste punt ligt op het vlak van de communicatie rondom de inhoud van de opdracht.


Het ontwikkelteam had een helder afgebakend idee van wat er uit de functionele analyse zou moeten komen. Namelijk: een autorisatiematrix, zoals hierboven beschreven. Dit had een tabelletje in een Excel of Word kunnen zijn. De moeilijkheid van de opdracht zat hem volgens deze opvatting in het op het juiste niveau definiëren van de rechten voor elke rol. De lijst moet uitgebreid genoeg zijn om alle *use cases* te ondersteunen, maar beperkt genoeg om makkelijk hanteerbaar te blijven.


Onze PO had zijn opdracht echter heel anders opgevat. Hij meende een complete oplossing te moeten hebben uitgedacht over de manier waarop rollen en rechten ingeregeld zouden moeten worden in onze applicatie. Volgens deze opvatting zat de moeiljkheid van de opdracht hem in het specificeren van een flexibel systeem dat alle huidige én toekomstige *use cases* omvat.


Ik vermoed dat het woord "functioneel" de PO en analist op het verkeerde been heeft gezet. Maar het zou ook kunnen dat hun kennis van de te ondersteunen processen hen blokkeerde hun opdracht zo afgebakend op te vatten als het ontwikkelteam dat deed.


Hoe dan ook, het team als geheel heeft onvoldoende gevalideerd of er een gedeeld begrip bestond over de inhoud van de opdracht. 


## Waar het mis ging (2)


Dan het tweede punt.


Een tijd geleden schreef ik over [incrementele en iteratieve ontwikkeling](/blog/21/07/incrementele-versus-iteratieve-ontwikkeling). Deze situatie is volgens mij een uitstekende illustratie van wat er gebeurt wanneer een team niet op één lijn zit wat betreft het te volgen ontwikkelproces.


Laat ik deze beroemde afbeelding van Hans Kniberg opnieuw aanhalen:


{{<figure src="https://blog.crisp.se/wp-content/uploads/2016/01/mvp.png" width="600" alt="Henrik Kniberg: Making sense of MVP (Minimum Viable Product)" >}}


Onze PO en analist hebben een auto ontworpen. Dat is niet erg, ware het niet dat we op dit moment nog onze step aan het ombouwen zijn tot een fiets. Dat is wat het team verwachte: specificaties voor een fiets.


Onze PO en analist hadden, bewust of onbewust (waarschijnlijk onbewust) een incrementele opvatting van ons ontwikkelproces. Het team verwachtte daarentegen, bewust of onbewust (waarschijnlijk onbewust) een iteratieve oplossingsrichting. Ook dit is een communicatieprobleem. 


Maar het is meer dan dat alleen. Het is fundamenteler van aard, en heeft te maken met een visie van hoe softwareontwikkeling eruit dient te zien. Ik deins ervoor terug om het probleem als "filosofisch" te kenschetsen, maar het is aannemelijk dat mijn filosofische achtergrond me wel een handje helpt bij het diagnostiseren van deze situatie.


## De vreugde van incrementeel ontwikkelen


Zoals dat gaat met filosofische problemen, is er geen eenvoudig gelijk in deze kwestie. 


Er zijn goede redenen om een auto te willen ontwerpen, in plaats van een fiets. In [mijn eerdere blog](/blog/21/07/incrementele-versus-iteratieve-ontwikkeling/#voor--en-nadelen) benadrukte ik het feit dat een incrementeel proces een consistent ontworpen oplossing waarborgt. Dat is een argument vanuit de invalshoek van een softwarearchitect.


Voor onze PO speelden en spelen andere overwegingen. Eerst en vooral is een auto, aan het eind van de dag, de meest omvattende oplossing voor het op dit moment relevante businessprobleem.


Maar wat deze episode me vooral deed beseffen, is hoe *leuk* het is om incrementeel te werken. Het geeft een kick op een oplossingsrichting te schetsen die een probleem in zijn totaliteit aanpakt. Een aanvankelijk eenvoudig ontwerp kan met gemak worden aangepast en uitgebreid op elke denkbare *edge case*. 


Meer nog: die aanpassingen en uitbreidingen hebben geen enkele impact op de werking van het systeem - in theorie. Want het systeem werkt alleen nog maar in theorie.


Dat is precies de kwestie. Onze PO en analist hebben gekeken naar het huidige proces, met alle uitzonderingen die erbij komen kijken, *op papier*. Dáár hebben ze een oplossing bij proberen te bedenken. Ze hebben zich mee laten slepen door een visie van wat er uiteindelijk allemaal mogelijk zou moeten zijn - in een ideale wereld, bovendien, waarin tijd en geld geen rol spelen. 


En die visie leek haalbaar, want op papier is hij snel en eenvoudig te verwezenlijken. Maar in de praktijk is een auto duur en complex. 


## *Agile* ontwikkelen


Door het hanteren van een theoretische lens, is een belangrijke vraag over het hoofd gezien: moet je het complete proces inclusief alle uitzonderingen wel *willen* ondersteunen? Of, bescheidener: moet je dat complete proces *nu* willen ondersteunen?


Daarom is het *op korte termijn* een beter idee om nu een fiets te ontwikkelen. Een fiets is verre van een ideale oplossing van het probleem, maar het is tenminste wel een oplossing die snel en goedkoop kan worden opgeleverd.


Dit is de kerngedachte achter *agile* ontwikkeling. Het is beter nu waarde te leveren, hoe imperfect ook, dan veel tijd en geld te steken in een idee dat misschien op langere termijn meer oplevert. "Misschien" is het sleutelwoord hier. In softwareontwikkelland zijn er geen garanties dat een oplossing op het moment van implementatie even goed werkt als op het moment van ontwerp.


## Een weg vooruit


Het team heeft onze PO terug naar de tekentafel gestuurd, ditmaal met de opdracht een autorisatiematrix uit te tekenen voor het proces *zonder* alle mogelijke uitzonderingen. We gaven hem mee: "Stel dat we hiermee 80% van de gebruikers ondersteunen, dan hebben we al 80% winst gemaakt. Met een eenvoudige oplossing bovendien."


Toch vind ik dat onze taak als softwareontwikkelaar er hiermee nog niet op zit. Het is moeilijk om een proces te analyseren, al helemaal als je zo diep in de materie zit als onze PO en analist. Het kan geen kwaad om daar een helpende hand bij te bieden. Soms heeft iemand een derde persoon nodig die zegt: "Dit gaan we niet doen." En diegene kan maar beter een softwareontwikkelaar zijn, want die heeft er zicht op hoe complex het kan zijn om de oplossing te implementeren.


In wezen komt het er hier op neer: de ontwikkelaar moet de PO zo ver krijgen zijn ogen van het uiteindelijke increment af te wenden, en te richten op de eerstvolgende iteratie.


Soms zit de moeilijkheid van software ontwikkelen niet in de complexiteit van de oplossing. Vaak zit de moeilijkheid in de poging de oplossing zo simpel mogelijk te houden. 
