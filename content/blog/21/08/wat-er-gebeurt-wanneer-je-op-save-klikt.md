---
title: "Wat er gebeurt wanneer je op 'save' klikt"
author: "Karl van Heijster"
date: 2021-08-30T07:59:08+02:00
draft: false
comments: true
tags: ["boeken", "databases", "recensies", "SQL", "zelfstudie"]
summary: "De theorie achter relationele databases en een goede beheersing van SQL is essentieel voor softwareontwikkelaars vandaag de dag. Studenten en professionals die hun kennis willen opfrissen, kunnen voor een toegankelijke inleiding in dit onderwerp terecht bij *Relationele databases en SQL* van Leo Wiegerink, Jeanot Bijpost en Marco de Groot. Dit relatief lijvige boekwerk (520 pagina’s) maakt de lezer in een aangenaam tempo bekend met de basis van de onderwerpen in de titel."
---

Heb je je wel eens afgevraagd wat er gebeurt wanneer je op de *save*-knop drukt, in willekeurig welke [applicatie](https://en.wikipedia.org/wiki/Application_software) (computerprogramma)? Datgene waar je mee bezig was, de gegevens die je hebt ingevoerd, moet in dat geval ergens worden neergezet. En dat niet alleen, die gegevens moeten ook weer makkelijk terug te halen zijn wanneer je verder wil gaan met je werk. Sommige, vaak heel eenvoudige applicatie’s hebben geen data-opslagfunctionaliteit nodig, maar voor de overgrote meerderheid geldt dat niet.


## Tabellen


De meeste applicaties maken voor deze functionaliteit gebruik van zogenaamde [relationele databases](https://en.wikipedia.org/wiki/Relational_database). De term “relationeel” verwijst niet naar het feit dat de opgeslagen gegevens relaties met elkaar kunnen hebben - hoewel dat kan, en in de meeste gevallen zelfs essentieel is. Relationele databases danken hun naam aan de [*relatie*](https://en.wikipedia.org/wiki/Finitary_relation), een wiskundige structuur die veel overeenkomst toont met dat wat we in het dagelijks leven een tabel noemen, een stelsel van rijen en kolommen. Deze opslagsystemen slaan hun gegevens op in één of (meestal) meerdere tabellen.


Om gegevens op te slaan en op te vragen uit een relationele database, wordt gebruik gemaakt van de zogenaamde [Structured Query Language](https://en.wikipedia.org/wiki/SQL) (SQL). Dit is een gestandaardiseerde taal die de gebruiker de mogelijkheid biedt om de gegevens aan een tabel toe te voegen (*create*), lezen (*read*), te wijzigen (*update*) of verwijderen (*delete*). Deze [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)-functionaliteit staat aan de basis van de overgrote meerderheid van de applicaties waar je vandaag de dag mee te maken krijgt.


De theorie achter relationele databases en een goede beheersing van SQL is om deze reden essentieel voor softwareontwikkelaars vandaag de dag. Studenten en professionals die hun kennis willen opfrissen, kunnen voor een toegankelijke inleiding in dit onderwerp terecht bij [*Relationele databases en SQL*](https://www.boomhogeronderwijs.nl/zoeken/100-9593_Relationele-databases-en-SQL-4e-druk) van Leo Wiegerink, Jeanot Bijpost en Marco de Groot. Dit relatief lijvige boekwerk (520 pagina’s) maakt de lezer in een aangenaam tempo bekend met de basis van de onderwerpen in de titel.


## Praktische cursus


Het boek opent met een conceptuele behandeling van wat een relationele database is en hoe de gegevens daarin [genormaliseerd](https://en.wikipedia.org/wiki/Canonical_form#Computing) (niet-redundant) worden opgeslagen. Het grootste gedeelte bestaat echter uit een praktische cursus SQL, waarin de lezer stap voor stap nieuwe technieken leert om de database te bevragen en te wijzigen. Dat begint vrij eenvoudig:


```sql
SELECT Kolom1, Kolom2
FROM Database.Tabel1
WHERE Id = ‘1’
```


Dat ziet er eenvoudig genoeg uit: Kolom1 en Kolom2 worden opgehaald uit Tabel1, voor elke rij waarvoor geldt dat het Id gelijk is aan “1”. Maar wat een naïeve programmeur bijvoorbeeld al gauw over het hoofd zou zien, is dat de bovenstaande query niet van boven naar beneden dient te worden gelezen. Conceptueel bezien is het beter om bij de tweede regel te beginnen: ga uit van Tabel1, neem alle rijen waarvoor het Id gelijk is aan “1”, en geef vervolgens de informatie die in Kolom1 en Kolom2 staat. Het is een subtiel verschil, maar naarmate de queries complexer worden, betaalt deze kennis zich dubbel en dwars terug.


Want queries kunnen al gauw erg complex worden, bijvoorbeeld wanneer er statistische gegevens worden opgevraagd (“hoeveel rijen met conditie *x* heeft deze database?”), of wanneer gegevens uit verschillende tabellen met elkaar gecombineerd moeten worden. De uitleg van de auteurs wordt toegelicht met veel broodnodige voorbeelden. Hoewel de stof naar zijn aard behoorlijk aan de droge kant is, weten de schrijvers de boel te verlevendigen door hun voorbeelden te situeren in aansprekende contexten, zoals een toetjesboek of een ruimtevaartbedrijf.


Daarnaast wordt de lezer uitgedaagd zich actief tot de leerstof te verhouden door middel van opdrachten die de lopende tekst onderbreken en elk hoofdstuk afsluiten. Deze zijn essentieel voor een goede beheersing van SQL. Als softwareontwikkelaar is het belangrijk dat je de taal als het ware “in je vingers” zit, wil je er goed mee kunnen werken. De bijbehorende databases en uitwerkingen van de opdrachten zijn te vinden op de [bijbehorende website](https://www.relationeledatabasesensql.nl/). Deze bevat daarnaast aanvullend materiaal voor docenten en enthousiastelingen over normalisatietheorie.


## Het belang van SQL


De laatste jaren zijn [documentdatabases](https://en.wikipedia.org/wiki/Document-oriented_database), ook wel bekend als [NoSQL-databases](https://en.wikipedia.org/wiki/NoSQL), bezig aan een opmars. Deze systemen laten de gestructureerde opzet van relationele databases los en slaan gegevens op in [XML](https://en.wikipedia.org/wiki/XML)- of [JSON](https://en.wikipedia.org/wiki/JSON)-formaat. Daarnaast hebben zogenaamde [Object-Relational Mappers](https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping) (ORMs) het werk voor ontwikkelaars enorm vereenvoudigd door objectgeoriënteerde code automatisch naar SQL-tabellen te mappen. Is het met deze ontwikkelingen in het achterhoofd nog wel van belang om je SQL eigen te maken?


Het antwoord daarop is een volmondig “ja”. Het gros van de applicaties - waaronder ook veel nieuwe - gebruikt immers nog steeds SQL, al dan niet om historische redenen. En een ORM stelt een ontwikkelaar misschien wel in staat om sneller een applicatie te ontwikkelen, maar is weinig behulpzaam bij het oplossen van SQL-gerelateerde [bugs](https://en.wikipedia.org/wiki/Software_bug). Daarvoor is kennis van de onderliggende techniek noodzakelijk.


Het is met name voor beginnende ontwikkelaars daarom geen overbodige luxe om *Relationele databases en SQL* goed doorgeploegd te hebben. Het boek biedt een gedegen inleiding in de materie. De auteurs schuwen het bovendien niet een kritische houding aan te nemen wanneer de taal minder intuïtief of logisch in elkaar zit dan je zou hopen. Dit is zeker van toegevoegde waarde voor iemand die bezig is de taal te leren. Het herbergt een waardevolle les: in softwareontwikkeling hoef je niet alles als vanzelfsprekend aan te nemen - liever niet, zelfs!


Het laatste, verdiepende deel, kent daarnaast een uitstekende uiteenzettingen over [performanceverbetering](https://en.wikipedia.org/wiki/Software_performance_testing) en, belangrijker nog, hoe complexe queryproblemen stap voor stap kunnen worden opgehakt in eenvoudiger deelproblemen. Die kennis is van toegevoegde waarde voor elke softwareontwikkelaar, of die zich nu intensief bezighoudt met SQL of niet.


*Deze recensie verscheen oorspronkelijk op [De Leesclub van Alles](https://deleesclubvanalles.nl/).*
