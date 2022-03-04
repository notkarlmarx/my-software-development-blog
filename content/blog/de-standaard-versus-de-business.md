---
title: "De standaard versus de business"
author: "Karl van Heijster"
date: 2022-03-04T08:23:19+01:00
draft: true
comments: true
tags: ["datamigratie", "domeinmodel", "informatieanalyse", "leermoment", "modelleren", "productieverstoring", "refactoren", "software ontwikkelen", "waarde", "YAGNI"]
summary: "Onze business volgt de QTI-standaard, maar ze gebruiken niet alles. Zo bestaat er - op dit moment - nog geen behoefte om Items te construeren die uit meerdere rijen bestaat. Bij het modelleren van ons domein, werden we voor een keus gesteld: volgen we de QTI-standaard bij het uitschrijven van ons model? Of leggen we alleen vast wat de business nodig heeft, en laten we ons eigen model daarmee afwijken van de standaard? Concreet: ondersteunen we meerdere rijen of niet? "
---

Mijn team ontwikkelt een applicatie in het domein van de toetsconstructie. Sterker nog, we ontwikkelen een nieuwe applicatie, die onze inmiddels veertien jaar oude legacy-applicatie dient te vervangen. Dat gaf ons de unieke mogelijkheid om *from scratch* na te denken over ons domeinmodel. Een kans, zonder meer, maar ook een grote uitdaging.


Gelukkig hoefden we niet in het luchtledige te werken. We hadden het model van onze legacy-applicatie, natuurlijk, maar dat model was in veertien jaar tijd behoorlijk ondoorgrondelijk geworden. Daarom baseerden we ons bij het modelleren op een ander model, namelijk de [QTI-standaard](https://en.wikipedia.org/wiki/QTI), de internationale standaard om toetsen uit te kunnen wisselen.


## QTI


Wat nu volgt, is een minicursus QTI. Maar schrik niet: de les van deze blog reikt verder dan de domeinspecifieke overwegingen die haar aanleiding vormden.


QTI definieert hoe een [toets](http://www.imsglobal.org/spec/qti/v3p0/guide#h.wdhut6r9sqwp) eruit moet zien om uitgewisseld te kunnen worden. Toetsen bestaan uit toetsvragen, die in het veld Items worden genoemd. Het spreekt voor zich dat QTI ook definieert hoe een [Item](http://www.imsglobal.org/spec/qti/v3p0/guide#h.w7rp6is7v7fd) eruit hoort te zien. Een Item bestaat ruwweg uit drie delen: (1) de inhoud, dat wil zeggen: de vraag en eventuele tekst en media daaromheen; (2) het juiste antwoord, en (3) een regel die specificeert hoe het Item gescoord dient te worden.  


De inhoud van een Item heeft in QTI een tabelachtige structuur. Ze bestaat uit rijen, die op hun beurt kolommen hebben. In theorie is het mogelijk om een Item te construeren dat bestaat uit drie rijen, waarbij de eerste rij één kolom heeft, de tweede rij twee kolommen en de derde rij drie kolommen.


## Rijen en kolommen


Tot zover de standaard. Onze business volgt de QTI-standaard, maar ze gebruiken niet alles. Zo bestaat er - op dit moment - nog geen behoefte om Items te construeren die uit meerdere rijen bestaat. Onze businessregels geven aan: een Item heeft ofwel één, ofwel twee kolommen. En daar volgt uit dat een Item altijd maar één rij heeft.


Bij het modelleren van ons domein, werden we voor een keus gesteld: volgen we de QTI-standaard bij het uitschrijven van ons model? Of leggen we alleen vast wat de business nodig heeft, en laten we ons eigen model daarmee afwijken van de standaard? Concreet: ondersteunen we meerdere rijen of niet? 


\- Wat zou jij hebben gedaan, denk je?


## Voors, tegens


Beide standpunten hadden hun voors en tegens, natuurlijk. 


Voor: Als we de QTI-standaard zouden volgen, dan zouden we daar een stukje flexibiliteit mee inbouwen. Stel dat de business in de toekomst zou beslissen tóch Items met meerdere rijen te ondersteunen, dan zouden we daar geen codewijzigingen voor hoeven doen.


Bovendien zou dat onze applicatie breder inzetbaar maken dan voor onze business-stakeholders alleen. Als er een moment zou komen waarop we onze applicatie aan andere gebruikers zouden willen aanbieden - bijvoorbeeld door de boel te opensourcen -, dan zou het volgen van de QTI-standaard ons een maximaal bereik bezorgen.


En trouwens, we zouden huidige businesscase kunnen ondersteunen mét rijen in ons model. Het zou er in de praktijk alleen op neerkomen dat de Items in onze database allemaal uit één rij bestonden. Dat kan toch zeker geen kwaad?


Tegen: [YAGNI](https://martinfowler.com/bliki/Yagni.html).


\- Wat weegt zwaarder, vind je? Wat mijn team betreft, wij vonden argumenten vóór destijds overtuigend genoeg om te beslissen meerdere rijen te ondersteunen in het model. Baat het niet, redeneerden we, dan schaadt het niet.


## Corruptie


*Flash forward* naar twee jaar later. Onze applicatie draait inmiddels met een langzaam uitdijende gebruikersgroep op productie. De business heeft nog geen indicatie gegeven meerdere rijen te ondersteunen, dus dat is jammer. Maar aan de andere kant: ze zitten ook niet in de weg. Inderdaad, baat het niet, dan schaadt het niet.


Maar dan: [refactorslagen](/blog/22/03/de-noodzaak-van-refactoren/) noodzaken ons datamigraties mogelijk te maken middels [Migrations.Json.Net](https://github.com/Weingartner/Migrations.Json.Net). (Ik schreef er eerder al over, [hier](/blog/21/09/stapje-voor-stapje-data-migreren/).) 


De implementatie lijkt op het eerste gezicht vlekkeloos te gaan, maar na verloop van tijd begint ons vreemd gedrag op te vallen in sommige Items. Wat blijkt: een bugje in de implementatie, zorgt ervoor dat de Items meeerdere rijen hebben gekregen! Soms twee, soms drie of vier of meer, maar allemaal hebben ze identieke kopieën van die eerste, oorspronkelijke en enige belangrijke rij in het Item.


Oftewel: onze data is gecorrumpeerd geraakt.


Geen zorgen: de aanleiding van het probleem bleek ook meteen haar oplossing te zijn. Dankzij Migrations.Json.Net bleek het heel eenvoudig om Items met meerdere rijen bij conversie om te zetten naar Items met één rij.[^1] Het probleem kon dus zonder vervelende neveneffecten worden opgelost - maar er gingen wel wat spannende momenten aan vooraf.


## Dus: YAGNI


Achteraf kun je zeggen: dat ene argument tegen woog zwaarder - of liever: had zwaarder moeten weten - dan de drie argumenten vóór. We hadden ons moeten realiseren dat *You Ain't Gonna Need It* niet voor niets zijn eigen afkorting heeft gekregen.


Alle code die je schrijft als softwareontwikkelaar, is code die je moet onderhouden. En de onderhoudslast van code weegt altijd zwaarder dan je op voorhand durft te denken. Niet voor niets worden de meeste kosten van het bouwen van software gemaakt in de onderhoudsfase. Dit is het moment waarop de keuzes die in de ontwikkelfase zijn genomen, hun duurzaamheid - of gebrek daaraan - bewijzen.


Ik stel een vuistregel voor: als we het als softwareontwikkelaars de moeite waard vonden een lekker bekkende afkorting te verzinnen voor een bepaalde praktijk, dan moet je wel verdomd goede redenen aandragen waarom je van die praktijk af wil wijken.


"Maar in de toekomst misschien..." is geen goede reden om YAGNI te schenden. YAGNI is nu precies bedacht omdat dit soort redeneringen vrijwel nooit opgaan. "Het kan geen kwaad" is zowaar een nog slechtere reden. Want het kan geen kwaad, totdat het kwaad blijkt te kunnen - en dan zit je met de gebakken peren. 


Dus: volg je de standaard of de business? Door schade en schande wijs geworden, neig ik naar de laatste. - Wat jij?


[^1]: In de fase waarin we het model van onze applicatie uitwerkten, hadden we nog geen Migrations.Json.Net - helaas, haar bestaan had er zomaar voor kunnen zorgen dat we hadden besloten voorlopig nog geen rijen te ondersteunen. Deze techniek stelt ons immers net zo goed in staat rijen *toe te voegen* als ze te verwijderen. Zo kunnen we Items-zonder-rijen *backwards compatible* maken met een geupdate model waarin rijen wél worden ondersteund. 
