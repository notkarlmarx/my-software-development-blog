---
title: "Symmetrische en asymmetrische overerving"
author: "Karl van Heijster"
date: 2023-11-25T20:10:52+01:00
draft: true
comments: true
tags: ["classes", "code lezen", "inheritance", "intentie van code", "objectgeoriënteerd programmeren", "schoonheid"]
summary: "Code heeft niet alleen esthetische kwaliteiten. Het communiceert ook een intentie, een bedoeling. Code vertelt een verhaal. Zoals de manier waarop een personage wordt geïntroduceerd in een roman, ons iets vertelt over de rol en het karakter van dat personage, zo vertelt de manier waarop we bepaalde concepten in onze codebase vastleggen hoe we deze moeten \"lezen\". -- Code heeft, net als onze natuurlijke taal, een betekenis."
---

Onlangs schreef ik [over overerving en compositie] (BLOG). Vandaag wil ik het wat uitgebreider over die eerste hebben.


Overerving is een techniek in het objectgeoriënteerd programmeren die ons in staat stelt om code te hergebruiken. We specificeren een baseclass met daarin code die hetzelfde is voor haar erfgenamen, en subclasses met daarin variërende logica.[^1] 


Laten we een voorbeeld nemen uit het domein van de toetsconstructie. Stel, we hebben een toets gemaakt en willen deze uit het systeem exporteren in [QTI-formaat](https://nl.wikipedia.org/wiki/QTI_(bestandstype) "'QTI (bestandstype)', Wikipedia"), verrijkt met wat metadata. QTI is een gestandaardiseerd uitwisselingsformaat dat veel in de onderwijswereld gebruikt wordt. In dit specifieke geval willen we de toets twee keer kunnen exporteren: beide keren als QTI, maar met verschillende soorten metadata voor de verschillende afnameomgevingen die we ondersteunen.


Zulke code zou er als volgt uit kunnen zien:


```cs
public abstract class AssessmentTestPublisher
{
    public PublishedTest Publish(AssessmentTest test)
    {
        var testContent = ConvertTestContent(test);
        var metadata = ConvertMetdata(test);
        return new PublishedTest(testContent, metadata);
    }

    private XDocument ConvertTestContent(AssessmentTest test)
    {
        // Transform AssessmentTest to XML 
    }

    protected abstract XDocument ConvertMetdata(AssessmentTest test);
}

public class AssessmentTestPublisherX : AssessmentTestPublisher
{
    protected override XDocument ConvertMetadata(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard x
    }
}

public class AssessmentTestPublisherY : AssessmentTestPublisher
{
    protected override XDocument ConvertMetadata(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard y
    }
}
```


Wat we hier zien is een baseclass met daarin de logica die voor beide subclasses gelijk is, en een subclass voor elke variatie: overerving volgens het boekje.


## Een alternatief


Maar dat is niet de enige manier waarop je overerving kunt implementeren. In het wild kom ik van tijd tot tijd een constructie tegen als deze:


```cs
public class AssessmentTestPublisherX 
{
    public PublishedTest Publish(AssessmentTest test)
    {
        var testContent = ConvertTestContent(test);
        var metadata = ConvertMetdata(test);
        return new PublishedTest(testContent, metadata);
    }

    private XDocument ConvertTestContent(AssessmentTest test)
    {
        // Transform AssessmentTest to XML 
    }

    protected virtual XDocument ConvertMetdata(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard x
    }
}

public class AssessmentTestPublisherY : AssessmentTestPublisherX
{
    protected override XDocument ConvertMetadata(AssessmentTest test)
    {
        // Transform Metadata to XML 
        // for standard y
    }
}
```


Ook hier wordt gebruik gemaakt van overerving om codeduplicatie te voorkomen. De delen van de code die hergebruikt worden, staan in de baseclass. 


Maar in diezelfde baseclass staat ook het deel van de code dat moet variëren. Om die variatie mogelijk te maken, is de method in kwestie `protected virtual` gemaakt. Dat betekent dat een subclass toegang heeft tot deze method (`protected`) en deze desgewenst kan overschrijven met zijn eigen logica (`virtual`). Dit is wat je in `AssessmentTestPublisherY` ziet gebeuren.


Is de ene manier van overerving beter dan de andere? -- Het antwoord is, dat kan niet missen: *it depends*.


## Esthetisch


Het is interessant om te reflecteren op het effect van deze verschillende manieren om de code vorm te geven. De eerste zal ik "symmetrische overerving" noemen, de tweede "asymmetrisch". 


We kunnen dat effect vanuit verschillende invalshoeken duiden. (Misschien is het zelfs beter om van "de effecten" te spreken.) Als ik mijn eigen reactie op beide codevoorbeelden als uitgangspunt, is één van de meest natuurlijke invalhoeken -- ik gêneer me haast het te zeggen -- de esthetische. 


Het ene voorbeeld vind ik aangenaam om te zien, smaakvol, verfijnd. Het andere maakt me onrustig, brengt me een refactorjeuk die ik maar wat graag weg wil krabben.


(-- Kun je raden welke variant welk effect teweegbrengt? Had je dezelfde reactie, of werd je je pas bewust van het verschil toen je erop gewezen werd?)


Mijn oordeel van de code is met waarde geladen. Het is, esthetisch bezien, niet zo dat beide opties me om het even zijn. Ik vind de eerste *mooier* (-- wat betekent dat in de wereld van code?) dan de tweede. Als ik de vrije keus had, dan zou ik de overervingsrelatie het liefst symmetrisch uitprogrammeren, niet asymmetrisch.


Is dat louter een kwestie van smaak?


## Intentioneel


Misschien, misschien niet. Code heeft niet alleen esthetische kwaliteiten. Het communiceert ook een intentie, een bedoeling. (Zie ook [deze blog] (CODEFLUISTEREN).) 


Code vertelt een verhaal. Zoals de manier waarop een personage wordt geïntroduceerd in een roman, ons iets vertelt over de rol en het karakter van dat personage, zo vertelt de manier waarop we bepaalde concepten in onze codebase vastleggen hoe we deze moeten "lezen". 


Code heeft, net als onze natuurlijke taal, een betekenis.


De symmetrische ("mooie") variant voelt alsof deze in evenwicht is. De code communiceert een verhouding tussen de verschillende soorten metadata: beide opties zijn gelijkwaardig. 


De asymmetrische ("lelijke") legt daarentegen de nadruk op de ene optie, en presenteert de tweede duidelijk *als alternatief*, secundair ten opzichte van de eerste. De lelijke code communiceert naar haar lezer -- je collega, of jijzelf over een paar maanden --: "Deze variant is echt alleen in *dit* geval relevant. Kies in normale gevallen liever de normale versie."


De vraag die we ons moeten stellen is niet: is deze code mooi? Dit gaat niet over mooi of lelijk. De vraag die we ons moeten stellen is: is deze code *waar*? (Zie ook [deze blog](/blog/21/09/waarheid-boven-schoonheid/ "'Waarheid boven schoonheid'")) Zijn scenario *x* en *y* inderdaad gelijkwaardig aan elkaar -- of juist niet? Zo nee, dan is het wellicht beter om de alternatieve, "lelijke" implementatie te verkiezen boven de "mooie".


## Nuance


Code -- alle code, ook wegwerpwegcode -- zit bomvol betekenisnuances als deze. Of we het willen of niet, onze code vertelt ons tussen de regels door iets -- iets waarachtigs of iets (onbedoeld) leugenachtigs. Het is aan ons als ontwikkelaars om ons daar bewust van te zijn en onze schrijfgewoonten erop aan te passen. 


De manier waarop we onze boodschap overbrengen, verdient onze zorg en aandacht. Hoe meer aandacht we tijdens het schrijven van de code besteden aan de manier waarop deze gelezen zal worden, hoe eenvoudiger ons dat lezen af zal gaan. En het is een algemeen bekend feit dat code veel vaker gelezen wordt dan dat het wordt geschreven.


Het is precies om deze reden dat ik (in bijvoorbeeld [mijn vorige blog] (OVERERVING_COMPOSITIE)) zo ageerde tegen de (of: de vermeende) gedachteloosheid waarmee ik soms zie dat er ook code is en wordt geschreven -- ook door mezelf, overigens. Wie op de automatische piloot schrijft, mist een kans -- de kans om te stoppen met schrijven, na te denken over wat je code zegt, en jezelf af te vragen of dat een accurate afspiegeling vormt van je begrip op dat moment.


Wie dat doet, kan alleen maar winnen. Want het antwoord is ofwel "ja" -- en dan kun je vrolijk doorschrijven --, of het is "nee" -- en dan is het niet alleen handig om je code (en daarmee je begrip) te verfijnen, het is noodzaak.


[^1]: Al gaat het in de praktijk vaak ook zo: we merken dat we twee classes hebben met codeduplicatie, en abstraheren die duplicatie naar een derde class waar we de andere van laten erven.
