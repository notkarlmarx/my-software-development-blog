---
title: "Eenvoudige SQL Versus Performante SQL"
author: "Karl van Heijster"
date: 2021-07-23T10:13:16+02:00
draft: false
comments: true
tags: ["clean code", "intentie van code", "leermoment", "performance", "SQL"]
summary: "Als ik zeg dat je al mijn kennis van SQL op de achterkant van een bierviltje kunt schrijven, dan overdrijf ik schromelijk. Maar twee bierviltjes, dat zou best kunnen. Toen ik onlangs de taak had een prachtig performante SQL-query uit te breiden, had dat nogal wat voeten in de aarde."
---

Als ik zeg dat je al mijn kennis van [SQL](https://en.wikipedia.org/wiki/SQL) op de achterkant van een bierviltje kunt schrijven, dan overdrijf ik schromelijk.


Maar twee bierviltjes, dat zou best kunnen.


Dat komt deels doordat ik [van huis uit een filosoof](/blog/21/07/mijn-loopbaanwending) ben. Dan heb je natuurlijk weinig met [databases](https://en.wikipedia.org/wiki/Database) te maken, [relationeel](https://en.wikipedia.org/wiki/Relational_database) of [anderszins](https://en.wikipedia.org/wiki/NoSQL). Trouwens, de meeste applicaties waar je als ontwikkelaar mee te maken krijgt gebruiken een [*Object-Relational Mapper*](https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping) (ORM) zoals [Entity Framework](https://docs.microsoft.com/en-us/ef/). Dus ook op de werkvloer zul je maar zelden direct in aanraking komen met ruwe SQL.


Ik moest de volgende query[^1] dan ook even (twee keer) twee keer nalopen:


```sql
INSERT INTO GroupedObject (GroupId, ObjectId)
    SELECT NewValues.*
    FROM (
        SELECT @groupid AS Id,
        value FROM STRING_SPLIT(@objectids, ',')
    ) AS NewValues
    LEFT OUTER JOIN GroupedObject O
        ON O.GroupId = NewValues.Id
        AND O.ObjectId = NewValues.value
    WHERE O.GroupId IS NULL
```


## De query


Deze query voegt (*insert*) een reeks nieuwe records in een koppeltabel in. Hij kent twee parameters. De eerste is een GroupId. Dit is de identifier van een groep waar objecten toe behoren. De tweede is een ObjectId. De naam daarvan spreekt hopelijk voor zichzelf. 


In het kader van performance is ervoor gekozen geen aparte insert te doen voor elk ObjectId, maar om in één keer meerdere ObjectIds toe te voegen voor elke GroupId. Om dit voor elkaar te krijgen, worden deze als een door komma's gescheiden lijst in string-vorm meegegeven. 


De *left outer join* is ervoor bedoeld om dubbele inserts te voorkomen.


## De requirement


Helemaal prima, zou je denken. Maar wat was nu het geval: er moest een extra waarde aan deze query worden toegevoegd. Voor elk ObjectId moest ook het type object worden meegegeven.


Hoe vlieg je dat nu aan? Mijn twee bierviltjes aan SQL-kennis lieten me hier behoorlijk in de steek. Maar uiteindelijk zou het, stelde ik me voor, zoiets moeten worden:


```sql
INSERT INTO GroupedObject (GroupId, ObjectId, ObjectType)
    SELECT NewValues.*
    FROM (
        SELECT @groupid AS Id,
        value AS ObjectId FROM STRING_SPLIT(@objectids, ','),
        value AS ObjectType FROM STRING_SPLIT(@objecttypes, ',')
    ) AS NewValues
    LEFT OUTER JOIN GroupedObject O
        ON O.GroupId = NewValues.Id
        AND O.ObjectId = NewValues.ObjectId
    WHERE O.GroupId IS NULL
``` 


Het leek me voor de hand liggend om de ObjectTypes op dezelfde manier toe te voegen als de ObjectIds. *If it ain't broke, don't fix it*.


Alleen: dat is geen valide SQL-query. 


## Een oplossing


Dit is dat wel:


```sql
INSERT INTO GroupedObject (GroupId, ObjectId, ObjectType)
    SELECT NewValues.*
    FROM (
        SELECT
            @groupid AS Id,
            ObjectIds.VALUE As ObjectId,
            ObjectTypes.VALUE As ObjectType
        FROM (
            SELECT VALUE, ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS RW
            FROM STRING_SPLIT(@objectids, ',')
        ) ObjectIds
        INNER JOIN (
            SELECT VALUE, ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS RW
            FROM STRING_SPLIT(@objecttypes, ',')
        ) ObjectTypes
        ON ObjectIds.RW = objecttypes.RW
    ) As NewValues
    LEFT OUTER JOIN GroupedObject O
        ON O.GroupId = NewValues.Id
        AND O.ObjectId = NewValues.ObjectId
    WHERE O.GroupId IS NULL
``` 


Ik zal de details achterwege laten van hoe ik uiteindelijk op deze query uit ben gekomen. Laten we het erop houden dat het nogal wat voeten in de aarde had.


Feit is dat dit een niet bijzonder leesbare query is. Filosofen die moeite hebben met de eerste query, zullen bij deze met de handen in het haar zitten. En niet alleen filosofen. Zelfs mijn meer SQL-*savvy* collega's moesten de query (ten minste) twee keer nalopen om 'm goed en wel te kunnen volgen.


Maar belangrijker is dat de query, alle voeten in aarde ten spijt, nog steeds niet helemaal is wat het moet zijn. `STRING_SPLIT` kent namelijk niet [de garantie de volgorde van de lijst te bewaren](https://www.sqlservercentral.com/articles/an-overview-of-string_split). Dit brengt het risico met zich mee dat bepaalde ObjectIds gepaard worden met een onjuist ObjectType. 


De query is moeilijk te lezen, nog moeilijker uit te breiden, en boven alles nog een bron voor nauwelijks reproduceerbare bugs.


## Een oplossing voor de oplossing


Wat te doen? Een technisch georiënteerde ontwikkelaar zou de oplossing misschien in SQL gezocht hebben. Deze ontwikkelaar zou zichzelf net zo lang in die taal verdiept hebben, totdat hij op een passende oplossing voor het probleem was gestuit. 


Ik heb die optie overwogen, al was het maar om mijn exemplaar van het [*SQL Cookbook*](https://www.oreilly.com/library/view/sql-cookbook-2nd/9781492077435/) uit de kast te kunnen halen. 


Ik heb die optie, niet lang na het uit de kast halen van dat boek, meteen weer verworpen.


## Een stapje terug


Een teamgenoot stelde me een heel voor de hand liggende vraag: is dit wel de moeite waard? Weegt de performancewinst van deze query (aangenomen dat die er is!) op tegen de complexiteit ervan?


Een blik op onze code verschafte die vraag al gauw van een antwoord. De query werd namelijk alleen aangeroepen binnen de context van een [foreach-loop](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/statements/iteration-statements#the-foreach-statement). De code in die loop roept een methode aan in onze [repository](https://docs.microsoft.com/en-us/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application#the-repository-and-unit-of-work-patterns) om één object te inserten in de koppeltabel. Die methode wrapt dat ene object in een lijst, en roept de methode aan die de bovenstaande query op de database afvuurt.


Met andere woorden: de omliggende code zorgt ervoor dat er nooit meer dan één record tegelijk wordt toegevoegd aan die koppeltabel. De performancewinst van deze query is niet alleen onbewezen, hij is louter theoretisch.[^2]


Het is een schoolvoorbeeld van code die door een te goede programmeur is geschreven.


## De les


Het is verleidelijk voor een softwareontwikkelaar om te denken dat de waarde van zijn werk afhangt van zijn technische kwaliteiten. Eerlijk is eerlijk, voor een deel is dat ook zo. Een ontwikkelaar die geen C# beheerst, zal nooit een goede applicatie in die taal kunnen schrijven.


Maar wie denkt dat technische expertise de doorslaggevende factor is in softwareontwikkeling, komt van een koude kermis thuis. Het gaat in software ontwikkeling niet altijd (misschien wel: meestal niet?) om de beheersing van een bepaalde techniek. 


Je hoeft geen geweldig ingewikkelde SQL te kunnen schrijven om een bepaald probleem op te lossen. Wie oog houdt voor de omliggende context, vindt misschien wel een veel eenvoudiger oplossing.


Sterker nog, een te grote focus op technische expertise kan een valkuil zijn. Als ik een expert was geweest in SQL, had ik misschien een pracht van een query geschreven, zonder ooit op te merken dat alle performancewinst die ik ermee meende te behalen, niet-bestaand was. 


Ik zou mijn collega's in het beste geval hebben opgezadeld met een query waar de filosofen geen kaas van lusten. En het slechtst geval zou mijn query zo ingewikkeld en moeilijk uitbreidbaar zijn geweest, dat het team van mij afhankelijk zou zijn geworden voor elke gang naar de database.


## De oplossing


In plaats daarvan heb ik de method die meerdere objecten tegelijkertijd in de database insert, verwijderd, en de eerste method de volgende query af laten vuren:


```sql
INSERT INTO GroupedObject
        (GroupId
        ,ObjectId
        ,ObjectType)
    VALUES
        (@groupid
        ,@objectid
        ,@objecttype)
```


Daar kan zelfs een filosoof als ik mee uit de voeten.


[^1]: Althans, een structureel identieke variant. Mijn team noemt zijn variabelen beter dan dit.


[^2]: Je kunt er je vraagtekens bij zetten of de omringende code wel op een juiste manier is opgezet. De lezer zal van me aan moeten nemen dat er in dit geval goede redenen bestaan om de objecten één voor één toe te voegen aan de koppeltabel.
