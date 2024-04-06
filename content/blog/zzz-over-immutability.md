---
title: "Over immutability"
author: "Karl van Heijster"
date: 2024-04-06T21:21:48+02:00
draft: true
comments: true
tags: []
summary: ""
---

[Simon Painter](https://www.thecodepainter.co.uk/functionalcsharp.html) noemt in het eerste hoofdstuk van [*Functional Programming with C#](https://www.oreilly.com/library/view/functional-programming-with/9781492097068/ "Simon Painter, 'Functional Programming with C#', O'Reilly") zeven kenmerken van functionele code. De eerste daarvan is [*immutability*](/tags/immutability/ "Blogs met de tag 'immutability'") (onveranderlijkheid).


Functionele code is *immutable* code. Het is code waarin objecten één keer worden geïnstantieerd en daarna niet meer worden aangepast. Het resultaat van een functie -- en alles in de wereld van [functioneel programmeren](/tags/functioneel-programmeren/ "Blogs met de tag 'functioneel programmeren'") is uiteindelijk een functie -- is een gloednieuw object, nooit een geupdatete versie van een al bestaande. 


Het voordeel hiervan is dat dit het onderhoud van je code versimpelt. Je hoeft je als programmeur er nooit druk over te maken of de waarden van het object waar je mee werkt, misschien buiten de huidige context is aangepast. Dat zorgt ervoor dat je als ontwikkelaar meer aannames mag doen over de werking van je code, en voorkomt een complete klasse moeilijk te diagnosticeren bugs. (Ik schreef [hier](/blog/22/05/heb-je-die-setter-echt-nodig/ "'Heb je die setter echt nodig?'") eerder over de voordelen van *immutability*.)


## Records


Een goed voorbeeld hiervan in [C#](https://learn.microsoft.com/en-us/dotnet/csharp/ "'C# language documentation', Microsoft documentatie") zijn [records](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record "'Records (C# reference)', Microsoft documentatie"). Records zijn net als classes, maar dan met enkele bijzondere eigenschappen. De belangrijkste daarvan -- überhaupt, maar zeker in de context van deze blog --, is haar *immutability*. 


Neem de volgende code.


```cs
public record Example(string Name, int Number);

var example = new Example("example", 1);

// This won't compile:
example.Name = "updated";

// ...
```


De declaratie van het type is voor records enorm efficiënt: meestal één regel code. De waarden voor `Name` en `Number` kunnen alleen worden geset bij het aanmaken van een nieuw record. Het is niet meer mogelijk om die waarden aan te passen. Wie desondanks objecten aan wil passen, zal er een kopie van moeten maken met geupdatete waarden:


```cs
// ...

var updated = example with 
{
    Name = "updated"
};
```


## Classes


Records belichamen het idee van *immutability* ten volle. Maar het is niet zo dat *immutability* in C# alleen met hulp van records te implementeren is. Sterker nog, de bovenstaande code genereert onder water een ouderwetse class met de properties `Name` en `Number`, zij het met private setters zodat ze alleen kunnen worden geset tijdens instantiatie. Classes kunnen dus net zo goed *immutable* worden gemaakt.[^1] 


We kunnen *immutability* in onze classes afdwingen door de `set` van onze properties te vervangen door een `private set` (kan alleen binnen de context van deze class worden geset) of een `init` (kan alleen worden geset tijdens initialisatie). En zelfs als dat geen optie is, kunnen we onze code behandelen alsof deze *immutable* is. We zouden er een goede gewoonte van kunnen maken nooit een property aan te passen van een bestaand object.


Het aanpassen van een object zou ons de kriebels moeten geven.


## Code review


En onlangs overkwam mij ook precies dat. Ik deed een [code review](/tags/code-reviews/ "Blogs met de tag 'code reviews'") en stuitte op een call naar een eenvoudige mapping-functie, waarin het ene object naar het andere werd getransformeerd. Maar zodra die conversie erop zat, was mijn collega nog niet klaar met het resultaat. Wat hij na die call deed, was vrolijk het object verder aanpassen op basis van twee of drie andere objecten.


Het was niet het gebrek aan *immutability* die mij voor deze code deed terugdeinzen, eerlijk gezegd. Het was dat knagende gevoel (zie ook [deze blog](/blog/23/12/codefluisteren/ "'Codefluisteren'")) dat je krijgt wanneer een verantwoordelijkheid niet duidelijk is gedefinieerd. Want wie had hier nu precies de taak om de juiste waarden in dat andere object te fietsen, die mapping-functie of de aanroepende code? Wat het antwoord ook was, het kon niet zijn: allebei een beetje.


Dus ik stelde voor om de twee andere objecten eveneens als parameter mee te geven aan de mapping-functie, en deze de verantwoordelijkheid te geven het nieuwe object te instantiëren. Mijn idee was: met de complexiteit die bij die operatie komt kijken, wil ik me niet bezighouden in de aanroepende code. Ik wil een eenvoudige call doen en daarna direct met het resultaat aan de slag kunnen.[^2] Het was wat mij betreft een toepassing van het [Single-Responsiblity Principe](/tags/single-responsibility-principe/ "Blogs met de tag 'single-responsibility principe'") (SRP).


Dat wijst op een interessant verband tussen het *immutability* en het SRP. Het correct -- en dus volledig -- instantiëren van een object is één verantwoordelijkheid. Het geïnstantieerde object gebruiken is een andere. Wie beide met elkaar vermengt, schrijft onnodig complexe code. We zouden er dus naar moeten streven onze objecten nooit aan te willen passen.


## Ontologie


Toch voelt het voor de meesten van ons vreemd, een totaal nieuw object te instantiëren wanneer één property wijzigt. Volgens mij ligt de oorzaak daarvan -- *excusez-moi*, nu neemt de filosoof in mij het woord -- in [de ontologie die we in ons dagelijks leven hanteren](https://seop.illc.uva.nl/entries/natural-language-ontology/ "'Natural Language Ontology', Stanford Encyclopedia of Philosophy") en die we onbewust meenemen in het [mentale model](/tags/mentaal-model/ "Blogs met de tag 'mentaal model'") waarmee we onze code lezen.


In het dagelijks taalgebruik zeggen we dingen als: "Het ding verandert van kleur." Daarmee impliceren we: er is iets wat onveranderlijk blijft -- de vorm van het object, bijvoorbeeld -- en iets wat verandert.[^3] En dat introduceert op de achtergrond tijd als relevante variabele. Iets wat verandert, verandert in de tijd; en dat wat hetzelfde blijft, blijft hetzelfde in die tijd.


Het ding -- één en hetzelfde ding -- was blauw op tijdstip *t<sub>0</sub>* maar rood op tijdstip *t<sub>1</sub>*. Daarom willen we code schrijven als:


```cs
var thing = new Thing { Color = "red"};
thing.Color = "blue";
```


En dat is waarom er van [objectgeoriënteerde code](/tags/objectgeoriënteerd-programmeren/ "Blogs met de tag 'objectgeoriënteerd programmeren'") zo vaak wordt gezegd dat het ons in staat stelt om onze manier van denken te spiegelen in onze code. We kunnen onze mentale modellen uitprogrammeren, want we denken vaak in termen van objecten die bestaan in de tijd.


##


...


Maar -- vervolgt de, *excusez-moi*, filosoof -- deze dingenontologie is slechts één manier om de werkelijkheid in te delen. We hoeven de wereld niet per se in te delen in dingen die blijven voortbestaan in de tijd. We kunnen de wereld ook zien als een reeks objecten die bestaan uit vier dimensies, in plaats van de huidige drie: breedte, hoogte, diepte én tijd. Een object *x* met de coördinaten 1-1-1-0 verschilt van 


We zien de wereld als vier-dimensionaal. Als we zouden moeten beschrijven waar een object zich bevindt in coördinaten van een raster, dan zouden we zeggen dat het zich op *die* breedte, *die* hoogte en *die* diepte bevindt *op dit moment*.



[^1]: Al merkt Painter op dat classes in C# nooit volledig *immutable* zijn. Er valt, dankzij [reflection](/tags/reflection/ "Blogs met de tag 'reflection'"), altijd wel om deze beperking heen te hacken. Maar Painter oordeelt pragmatisch: we kunnen in onze code altijd doen alsof.

[^2]: "*Pushing complexity down*" is het achterliggende idee. Ik heb de kreet ooit voorbij horen komen in een podcast, ik meen dat het er een van [*Software Engineering Radio*](https://se-radio.net/) was, maar ik kan de bron niet meer terugvinden.

[^3]: Op basis van het onveranderlijke deel beschouwen we het object als nog altijd hetzelfde object. Het veranderlijke wordt daarmee gedegradeerd naar "maar" een toevallige eigenschap van dat object. Zie ook [deze blog](/blog/23/01/eerlijke-domeinmodellen/ "'Eerlijke domeinmodellen'").
