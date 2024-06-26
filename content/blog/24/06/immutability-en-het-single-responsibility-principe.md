---
title: "Immutability en het Single-Responsibility Principe"
author: "Karl van Heijster"
date: 2024-06-14T08:29:05+02:00
draft: false
comments: true
tags: ["clean code", "code reviews", "eenvoud", "functioneel programmeren", "immutability", "single-responsibility principe"]
summary: "Het correct -- en dus volledig -- instantiëren van een object is één verantwoordelijkheid. Het geïnstantieerde object gebruiken is een andere. Wie beide met elkaar vermengt, schrijft onnodig complexe code. Dat is waarom we er naar moeten streven onze objecten nooit aan te willen passen."
---

[Simon Painter](https://www.thecodepainter.co.uk/functionalcsharp.html) noemt in het eerste hoofdstuk van [*Functional Programming with C#*](https://www.oreilly.com/library/view/functional-programming-with/9781492097068/ "Simon Painter, 'Functional Programming with C#', O'Reilly") zeven kenmerken van functionele code. De eerste daarvan is [*immutability*](/tags/immutability/ "Blogs met de tag 'immutability'") (onveranderlijkheid).


Functionele code is *immutable* code. Het is code waarin objecten één keer worden geïnstantieerd en daarna niet meer worden aangepast. Het resultaat van een functie -- en alles in de wereld van [functioneel programmeren](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'") is uiteindelijk een functie -- is een gloednieuw object, nooit een geupdatete versie van een al bestaande. 


Het voordeel hiervan is dat dit het onderhoud van je code versimpelt. Je hoeft je er als programmeur nooit druk over te maken of de waarden van het object waar je mee werkt, misschien buiten de huidige context zijn aangepast. Dat zorgt ervoor dat je als ontwikkelaar meer aannames mag doen over de werking van je code, en voorkomt een complete klasse moeilijk te diagnosticeren bugs. (Ik schreef [hier](/blog/22/05/heb-je-die-setter-echt-nodig/ "'Heb je die setter echt nodig?'") eerder over de voordelen van *immutability*.)


## Records


Een goed voorbeeld hiervan in [C#](https://learn.microsoft.com/en-us/dotnet/csharp/ "'C# language documentation', Microsoft documentatie") zijn [records](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record "'Records (C# reference)', Microsoft documentatie"). Records zijn net als classes, maar dan met enkele bijzondere eigenschappen. Records worden bijvoorbeeld op waarde(n) met elkaar vergeleken, en niet op referentie. En als je `.ToString()` aanroept op een record, dan krijg je *by default* die waarden te zien, en niet de naam van de class. 


Maar de belangrijkste eigenschap van records -- überhaupt, maar zeker in de context van deze blog --, is hun *immutability*. Neem de volgende code.


```cs
public record Example(string Name, int Number);

var example = new Example("example", 1);

// This won't compile:
example.Name = "updated";
```


De waarden voor `Name` en `Number` kunnen alleen worden geset bij het aanmaken van een nieuw record. Het is niet meer mogelijk om die waarden aan te passen. Wie desondanks objecten aan wil passen, zal er een kopie van moeten maken met geupdatete waarden:


```cs
var updated = example with 
{
    Name = "updated"
};
```


## Classes


Records belichamen het idee van *immutability* ten volle. Maar het is niet zo dat *immutability* in C# alleen met hulp van records te implementeren is. Sterker nog, de bovenstaande code genereert onder water een ouderwetse class met de properties `Name` en `Number`, zij het met private setters zodat ze alleen kunnen worden geset tijdens instantiatie. 


Classes kunnen dus net zo goed *immutable* worden gemaakt.[^1] We kunnen dat eenvoudig eigenhandig afdwingen door de `set` van onze properties te vervangen door een `private set` (kan alleen binnen de context van deze class worden geset, meestal in de constructor) of een `init` (kan alleen worden geset tijdens initialisatie). 


En zelfs als dat geen optie is, kunnen we onze code behandelen alsof deze *immutable* is. We zouden er een goede gewoonte van kunnen maken nooit een property aan te passen van een bestaand object.


Het aanpassen van een object zou ons de kriebels moeten geven.


## Code review


En onlangs overkwam mij ook precies dat. Ik deed een [code review](/tags/code-reviews/ "Blogs met de tag 'code reviews'") en stuitte op een call naar een eenvoudige mapping-functie, waarin het ene object naar het andere werd getransformeerd. Maar zodra die conversie erop zat, was mijn collega nog niet klaar met het resultaat. Wat hij na die call deed, was vrolijk het resultaat verder aanpassen op basis van twee andere objecten.


Het was voor mijn gevoel niet het gebrek aan *immutability* die mij voor deze code deed terugdeinzen, eerlijk gezegd. Het was dat knagende gevoel (zie ook [deze blog](/blog/23/12/codefluisteren/ "'Codefluisteren'")) dat je krijgt wanneer een verantwoordelijkheid niet duidelijk is gedefinieerd. Want wie had hier nu precies de taak om de juiste waarden in dat nieuwe object te fietsen, die mapping-functie of de aanroepende code? Wat het antwoord ook was, het kon niet zijn: allebei een beetje.


Dus ik stelde voor om die twee andere objecten eveneens als parameter mee te geven aan de mapping-functie, en deze de verantwoordelijkheid te geven het nieuwe object te instantiëren. Mijn idee was: met de complexiteit die bij die operatie komt kijken, wil ik me niet bezighouden in de aanroepende code. Ik wil een eenvoudige call doen en daarna direct met het resultaat aan de slag kunnen.[^2] 


## Verantwoordelijkheid


Het was wat mij betreft een toepassing van het [Single-Responsiblity Principe](/tags/single-responsibility-principe/ "Blogs met de tag 'single-responsibility principe'") (SRP). De mapping-functie had de verantwoordelijkheid het nieuwe object *in zijn volledigheid* te instantiëren op basis van *alle* benodigde informatie. De aanroepende code had de verantwoordelijkheid met het resultaat te werken.


Dat wijst op een interessant verband tussen het *immutability* en het SRP. Het correct -- en dus volledig -- instantiëren van een object is één verantwoordelijkheid. Het geïnstantieerde object gebruiken is een andere. Wie beide met elkaar vermengt, schrijft onnodig complexe code. Dat is waarom we er naar moeten streven onze objecten nooit aan te willen passen.


Mijn ontwerpintuïtie zegt niet: *mutabillity* is slecht -- punt. Het is eerder: mijn ontwerpintuïtie drijft me richting *immutability* omdat dit eenvoudiger en beter onderhoudbare code oplevert.


[^1]: Al merkt Painter op dat classes in C# nooit volledig *immutable* zijn. Er valt, dankzij [reflection](/tags/reflection/ "Blogs met de tag 'reflection'"), altijd wel om deze beperking heen te hacken. Maar Painter oordeelt pragmatisch: we kunnen in onze code altijd doen alsof.

[^2]: "*Pushing complexity down*" is het achterliggende idee. Ik heb de kreet ooit voorbij horen komen in een podcast, ik meen dat het er een van [*Software Engineering Radio*](https://se-radio.net/) was, maar ik kan de bron niet meer terugvinden.