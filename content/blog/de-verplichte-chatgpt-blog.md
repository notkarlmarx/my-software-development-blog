---
title: "De verplichte ChatGPT-blog"
author: "Karl van Heijster"
date: 2023-06-23T09:50:15+02:00
draft: true
comments: true
tags: ["bugs", "ChatGPT", "code lezen", "communicatie", "intentie van code", "kunstmatige intelligentie", "leermoment", "luie programmeur", "refactoren", "samenwerking", "software ontwikkelen", "testen"]
summary: "Met hulp van ChatGPT wist ik in een uurtje het functionele equivalent te leveren van code waar ik eerder dagen op heb zitten zwoegen. De tijdwinst is onomstotelijk. En op het vlak van informatieoverdracht is ChatGPT een ons \"echte\" ontwikkelaars mijlenver vooruit."
---

Ik geloof dat ik vrij laat in de [hypecyclus](https://en.wikipedia.org/wiki/Gartner_hype_cycle "'Gartner hype cycle', Wikipedia") zit, maar ook ik ben onlangs gebruik gaan maken van [ChatGPT](https://chat.openai.com/) in mijn werk. De aanleiding was een bug, een [StackOverflowException](https://learn.microsoft.com/en-us/dotnet/api/system.stackoverflowexception?view=net-7.0, "'StackOverflowException Class', Microsoft documentatie") die uit het niets opdook in een class die al ruim een jaar niet was aangeraakt. 


Die code was ervoor verantwoordelijk de binnenkomende data te doorzoeken op elementen die kwetsbaar waren voor [Cross-site scripting](https://en.wikipedia.org/wiki/Cross-site_scripting "'Cross-site scripting', Wikipedia") (XSS), zodat een volgende class die elementen kon opschonen (of [*sanitizen*](https://en.wikipedia.org/wiki/HTML_sanitization "'HTML sanitization', Wikipedia")). Zulke kwetsbaarheid werd in de code vastgelegd middels een [attribuut](https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/reflection-and-attributes/ "'Attributes', Microsoft documentatie") op de relevante [properties](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties "'Properties (C# Programming Guide)', Microsoft documentatie"). De binnenkomende data werd [gescand op properties met zulke attributen middels *Reflection*](https://learn.microsoft.com/en-us/dotnet/standard/attributes/retrieving-information-stored-in-attributes "'Retrieving Information Stored in Attributes', Microsoft documentatie").


 -- Een heleboel [*Reflection*](https://learn.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/reflection "'Reflection in .NET', Microsoft documentatie"), om precies te zijn. Want zo'n attribuut kan verstopt zomaar zitten op een property van een property -- in een lijst van objecten met een bepaalde property. Je begrijpt: dat werkend krijgen had destijds wat voeten in de aarde.


## Complexiteit


Ik deed nu een aanname. Ik nam aan dat de oorzaak van de bug in die code moest zitten. -- En helemaal onterecht was die aanname niet. De kans op fouten is op zijn minst evenredig aan de complexiteit van de code. Hoewel een uitgebreide testsuite me redelijk wat zekerheid gaf over de werking van de code in relatief eenvoudige scenario's, kon ik onvoorziene *edge cases* niet uitsluiten.


Maar ik deinsde er voor terug om uren tijd te gaan steken in het vinden van die *edge cases*. Dat is waar ChatGPT om de hoek kwam kijken. Ik stelde voor dat de chatbot een implementatie van mijn class schreef, in de hoop dat deze de oorzaak van de bug boven water zou krijgen.


Ik bevond me in een gelukkige positie. Ik kon omschrijven elke inputs mijn functie verwachtte, en hoe het resultaat eruit moest zien. Dat zorgde ervoor dat ik die implementatie één op één in mijn class kon plakken, zonder ook maar één aanroep te hoeven veranderen. Bovendien had ik een testsuite die me onmiddellijk op blinde vlekken in ChatGPT's implementatie kon wijzen.


## Iteraties


Uiteindelijk zouden er zes iteraties voor nodig zijn voordat ChatGPT iets had geschreven wat equivalent was aan mijn oorspronkelijke code.


De eerste iteratie was naïef. De code viste de juiste properties eruit op het hoogste niveau, maar kon niet omgaan met geneste classes: attributen op de properties van properties. 


De tweede iteratie omzeilde dat probleem, maar tegen de prijs om op elke bovenliggende property ook een attribuut te moeten plaatsen. Dat was niet acceptabel: als een ontwikkelaar dat over het hoofd zou zien, dan zou de relevante property genegeeerd worden -- met moeizaam te ontrafelen bugs tot gevolg.


Dat probleem werd in de derde iteratie verholpen. Maar de code die ChatGPT ervoor nodig had was in een moeilijk leesbare, declaratieve stijl geschreven. Ik zag kansen om die code wat op te schonen door gebruik te maken van [LINQ](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/ "'Language Integrated Query (LINQ) (C#)', Microsoft documentatie"), en vroeg de chatbot om de code in die stijl te herschrijven voor de vierde iteratie.


En verzamelingen, kon de code omgaan met lijstwaarden die properties hadden die opgeschoond dienden te worden? En lijstwaarden waarbij het attribuut op de properties van de properties verstopt zaten? Nee -- daar waren nog twee iteraties voor nodig.


## Functioneel


Met hulp van ChatGPT wist ik in een uurtje het functionele equivalent te leveren van code waar ik eerder dagen op heb zitten zwoegen. De tijdwinst is onomstotelijk.[^1]


Maar het is niet de code zelf -- dat wil zeggen: de method die ik één op één in mijn eigen codebase kon plakken -- die deze ervaring zo aangenaam maakte. ChatGPT genereerde bij elke codewijziging een voorbeeld van een modelletje en een eenvoudige [consoleapplicatie](https://learn.microsoft.com/en-us/visualstudio/get-started/csharp/tutorial-console?view=vs-2022 "'Tutorial: Create a simple C# console app in Visual Studio (part 1 of 2)', Microsoft documentatie"). De laatste versie zag er als volgt uit:


```cs

public class MyClass
{
    [Sanitize]
    public string Name { get; set; }

    public int Age { get; set; }

    public NestedClass Nested { get; set; }

    public IEnumerable<NestedClass> NestedList { get; set; }
}

public class NestedClass
{
    public string Address { get; set; }

    [Sanitize]
    public string PhoneNumber { get; set; }

    public IEnumerable<OtherClass> OtherList { get; set; }
}

public class OtherClass
{
    [Sanitize]
    public string OtherProperty { get; set; }
}

public static class Program
{
    public static void Main()
    {
        var obj = new MyClass
        {
            Name = "John Doe",
            Age = 30,
            Nested = new NestedClass
            {
                Address = "123 Main St",
                PhoneNumber = "555-1234",
                OtherList = new List<OtherClass>
                {
                    new OtherClass { OtherProperty = "SensitiveData1" },
                    new OtherClass { OtherProperty = "SensitiveData2" }
                }
            },
            NestedList = new List<NestedClass>
            {
                new NestedClass { Address = "456 Elm St", PhoneNumber = "555-5678" },
                new NestedClass { Address = "789 Oak St", PhoneNumber = "555-9012", OtherList = null }
            }
        };

        var sanitizedProperties = ObjectSanitizer.GetSanitizedProperties(obj);

        foreach (var entry in sanitizedProperties)
        {
            Console.WriteLine("Object: " + entry.Key);

            foreach (var prop in entry.Value)
            {
                Console.WriteLine("Sanitized Property: " + prop.Name);
            }
        }
    }
}

```

Dit maakte het voor mij als lezer onmiddellijk duidelijk wat de code -- doet. Ik kon uit de plaatsing van de attributen in het model afleiden welke scenario's er al ondersteund werden en welke niet. En als ik daar over twijfelde, dan zou ik daar eenvoudig achter kunnen komen door de code te runnen in een consoleapplicatie.[^2]


Kort gezegd: ChatGPT verschafte me alle informatie die me in staat stelde om zijn code snel op functionele correctheid te kunnen controleren *zonder dat ik daarvoor naar de implementatie hoefde te kijken*. -- Mensen die mij kennen weten dat mijn paradepaardje nooit ver weg kan zijn na zo'n observatie: ChatGPT ~~bewijst~~ honoreert het punt dat tests een onmisbare vorm van [documentatie](/blog/22/09/tests-als-documentatie/ "'Tests als documentatie'") zijn bij het beoordelen van code. 


Dat de test in dit geval niet de vorm aanneemt van een formele unittest, doet niet af aan het punt. Je hebt als lezer een manier nodig om de werking van de code te kunnen valideren om er iets zinnigs over te kunnen zeggen -- en dat kan ook in een consoleapplicatie, al acht ik dat niet voldoende voor productierijpe code. 


Het is precies de [functionele specificatie](/blog/22/12/tests-zijn-specs/ "'Tests zijn specs'") van de code die veelal ontbreekt bij het beoordelen van code geschreven door programmeurs van vlees en bloed. Op het vlak van informatieoverdracht is ChatGPT een ons "echte" ontwikkelaars mijlenver vooruit.


## Regressie


Toen al mijn unittests slaagden, implementeerde ik ChatGPT's variant op het oorspronkelijk algoritme. En het leek te werken -- heel even. Een nieuwe bug dook op, de [JSON-serialisatie](https://learn.microsoft.com/en-us/dotnet/standard/serialization/system-text-json/how-to?pivots=dotnet-8-0 "'How to serialize and deserialize (marshal and unmarshal) JSON in .NET', Microsoft documentatie") gooide een Exception op bij een [`Option<T>`](https://github.com/louthy/language-ext "'C# Functional Programming Language Extensions', Github") -- dat was nieuw, en er was geen test voor.


Ik was terug bij af -- toen een collega een *pull request* inschoot. Een [*factory method*](https://en.wikipedia.org/wiki/Factory_method_pattern "'Factory method pattern', Wikipedia") had voor een oneindige regressie gezorgd -- totdat de stack overflowde, in elk geval.


Dus ik draaide mijn wijzigingen terug. Bedankt ChatGPT, uw diensten zijn niet meer nodig -- ik nam nog wel de tijd om de chatbot te bedanken.


Opdat onze robotheersers in de toekomst positief over mij zullen oordelen.


[^1]: De vergelijking is niet helemáál eerlijk, want tijdens mijn eerste, handmatige poging de code te schrijven had ik bij voorbaat geen functiesignatuur en tests paraat -- die ontdekken was onderdeel van het proces. Toch blijft het punt overeind: ik twijfel er niet aan dat ik met hulp van ChatGPT sneller tot een soortgelijk resultaat zou zijn gekomen. 

[^2]: Of, wat waarschijnlijker is: ChatGPT vragen welke scenario's er ondersteund worden.
