---
title: "Eerlijke domeinmodellen"
author: "Karl van Heijster"
date: 2023-01-20T08:14:34+01:00
draft: false
comments: true
tags: ["domain-driven design", "domeinmodel", "eerlijke functies", "functioneel programmeren", "leermoment", "modelleren", "monads", "objectgeoriënteerd programmeren", "options", "properties"]
summary: "Options en Eithers vormen nog maar de eerste aanzetten voor het idee van eerlijke functies. Het zijn constructen die, op het oog althans, redelijk beperkt blijven tot het technische domein. Maar het idee van eerlijke functies past ook uitstekend bij de praktijk van het modelleren van een domein, zoals gebruikelijk in Domain-Driven Design. Dat is een les die ik leerde van Scott Wlaschin op DevTernity."
---

Ik heb eerder op deze blog over [eerlijke functies](/blog/22/07/wat-zijn-eerlijke-functies/) geschreven. Dat was in de context van functies die ook *null* of "geen waarde" terug kunnen geven, zoals databasecalls of het doorzoeken van lijsten.


Het idee achter een eerlijke functie laat zich eenvoudig uitleggen. Een functie is eerlijk als je van de inputs en outputs - de signatuur van de functie - af kunt lezen wat de functie doet. Of: als de signatuur *alles* beschrijft wat de functie doet. Anders gezegd: een eerlijke functie kent geen neveneffecten.


Als de signatuur zegt dat je er een `int` in stopt en een `bool` terugkrijgt, dan doet die functie alléén dat. Hij gaat niet stiekem een globale variabele aanpassen, en hij gooit ook niet stiekem een `Exception` op als de `int` niet aan een bepaalde voorwaarde voldoet.


## Foutafhandeling


Een oplettende lezer zal opmerken dat dat een behoorlijke impact heeft op de manier waarop fouten worden afgehandeld binnen het functionele paradigma. Het concept van `Exceptions` die opgegooid worden en ergens anders in de code worden afgehandeld, kent men in de functionele wereld niet. - En niet geheel onterecht. Die manier van foutafhandeling heeft veel weg van het gebruik van `goto`-statements, en we weten al sinds 1968 dat "[Go To Statement Considered Harmful](https://homepages.cwi.nl/~storm/teaching/reader/Dijkstra68.pdf)".


In functionele talen worden fouten - validatiefouten of exceptionele condities - afgehandeld met (een variant op) een `Either`-*monad*. De *return value* van een functie wordt dan gewikkeld in een *monad* die twee mogelijke uitkomsten kan representeren. Als de functie succesvol verloopt, dan bevat deze de verwachte waarde. Als deze mislukt, dan bevat deze een foutmelding. De signatuur van een functie die potentieel kan mislukken, is glashelder: `Input -> Either<FailState, SuccessState>`. 


Omdat dit concept vaak gebruikt wordt voor validatiefouten en exceptionele condities, bevatten veel talen ook gespecialiseerde *monads* voor deze *use cases*. [*LanguageExt*](https://github.com/louthy/language-ext), de grootste *library* met functionele uitbreidingen voor [C#](https://learn.microsoft.com/en-us/dotnet/csharp/), kent hier bijvoorbeeld een [`Validation`](https://louthy.github.io/language-ext/LanguageExt.Core/Monads/Alternative%20Value%20Monads/Validation/index.html)- en een [`Try`](https://louthy.github.io/language-ext/LanguageExt.Core/Monads/Alternative%20Value%20Monads/Try/Try/index.html)-object voor.


## Domeinen


[Options](/blog/22/08/spelen-met-options/) en Eithers vormen echter nog maar de eerste aanzetten voor het idee van eerlijke functies. Het zijn constructen die, op het oog althans, redelijk beperkt blijven tot het technische domein.


Maar het idee van eerlijke functies past ook uitstekend bij de praktijk van het modelleren van een domein, zoals gebruikelijk in [Domain-Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design) (DDD). Dat is een les die ik leerde van [Scott Wlaschin](https://scottwlaschin.com/) op [DevTernity](https://devternity.com/).


Wlaschins voorbeeld was even eenvoudig als aansprekend. Stel je een willekeurige applicatie voor waarvoor je je als gebruiker moet inschrijven. - Dit proces heb je vaak zat doorlopen: je geeft je gegevens op en je e-mailadres, je drukt op een grote, mooie knop en je krijgt een bevestingsmail in je inbox. In die mail druk je opnieuw op een grote, mooie knop - "*Inschrijven bevestigen*" of iets dergelijks -, en vanaf dat moment kun je de applicatie gebruiken.


Als je naar het domeinmodel van zo'n applicatie kijkt, dan moet daar een object `EmailAddress` bestaan. Meer nog, dat `EmailAddress` moet op de een of andere manier kunnen communiceren dat het bevestigd is of niet. Immers, een gebruiker die wel op de eerste grote, mooie knop heeft gedrukt, maar nog niet op de tweede, kan nog niet in de applicatie aan de slag.


## `EmailAddress`, objectgeoriënteerd


Hoe zou een typische objectgeoriënteerde ontwikkelaar dat object uitschrijven? Ik zal je vertellen wat ik zou doen: ik zou een *property* op dat object toevoegen, waarschijnlijk een `bool`, om aan te geven of het adres bevestigd is of niet:


```cs
public class EmailAddress 
{
    public bool Verified { get; set; }
    // Other properties...
}
```


Functies die het `EmailAddress` nodig hebben, zouden moeten controleren of deze geverifieerd is, voordat ze ermee aan de slag gaan:


```cs
public void DoSomething(EmailAddress email)
{
    if (!email.Verified)
    {
        return;
    }

    // Do something...
}
```


Laat ik vooropstellen dat dit in principe geen verkeerde oplossing is - de applicatie doet immers wat ervan verwacht wordt. Deze opzet is echter wel foutgevoelig. Het is eenvoudig om tijdens het programmeren de bovenstaande check te vergeten in te bouwen - zeker als deze op verschillende plekken voorkomt. Er zullen tests nodig zijn om te controleren dat dit soort validaties niet omvallen na refactorslagen.   


Een tweede nadeel is dat de `Verified`-property door iedereen in de code vrijelijk aan te passen is. Zelfs al worden alle checks zorgvuldig ingebouwd en getest, dan nog kunnen er bugs in de applicatie sluipen wanneer een ontwikkelaar op een verkeerde plek in de code `Verified` op `true` zet.


Dan: is de signatuur van deze method eerlijk? Nee! Want de signatuur zegt een `EmailAddress` te verwachten, maar wie de inhoud van de method bekijkt, ziet al snel dat dat `EmailAddress` aan bepaalde voorwaarden dient te voldoen. 


\- Maar natuurlijk, het objectgeoriënteerde paradigma kent niet zoiets als eerlijke functies, dus die vraag is (*no pun intended*) niet helemaal eerlijk. Laat ik daarom de volgende vraag stellen: hoe zouden we dit stukje van het domein kunnen modelleren op zo'n manier dat deze wél eerlijk zou zijn?


Ga je gang, neem even de tijd om erover na te denken.


## `EmailAddress`, functioneel


Klaar? Dit is wat Wlaschin erover zei.


\- Merk op dat een e-mailadres en een bevestigd e-mailadres *vanuit het perspectief van het domein* niet dezelfde dingen zijn. Sommige delen van de applicatie werken uitsluitend met het onbevestigde e-mailadres - de inschrijfmodule, bijvoorbeeld -, terwijl andere delen uitsluitend met de bevestigde variant werken. Het domeinmodel zou dat moeten reflecteren. Het zou een `EmailAddress` en een `VerifiedEmailAddress` moeten kennen:


```cs
public class EmailAddress { /* Properties... */ }
public class VerifiedEmailAddress : EmailAddress { /* Properties... */ }
```


Functies die een bevestigd e-mailadres nodig hebben, kunnen dat vanaf nu eenvoudig via hun signatuur communiceren:


```cs
public void DoSomething(VerifiedEmailAddress email)
{
    // Do something...
}

```


Dankzij deze oplossing is het niet meer nodig om in de method body te controleren of het object zich wel in de juiste staat bevindt - dat handelt de compiler vanaf nu voor je af. Het is dus ook niet meer nodig om tests te schrijven die verifiëren dat deze checks zijn omgevallen. Het is voor ontwikkelaars eenvoudigweg onmogelijk geworden om hier nog fouten in te maken.


Het tweede nadeel, de property die vrijelijk aan te passen was, kan worden ondervangen door een service te definiëren die controleert of een e-mailadres geverifieerd is. Zo ja, dan geeft deze het juiste object terug. Zo nee, dan niet. Die service zou een functie kennen met de volgende signatuur: `EmailAddress -> Option<VerifiedEmailAddress>`.[^1] Als dit de enige plek in de code is waar je een `VerifiedEmailAddress` kunt verkrijgen, dan sluit dat de weg voor de bovengenoemde verzameling bugs.


## Substantieleer


Ik zal je eerlijk zeggen: Wlaschins inzichten bliezen me van mijn stoel. Het idee dat je dit verschil kunt vastleggen in twee verschillende typen was voor mij tegelijkertijd totaal vanzelfsprekend én compleet onverwacht.


Een tijd lang heb ik lopen malen waar deze ogenschijnlijke paradox vandaan komt. En omdat ik een filosoof ben, kom ik dan al gauw in metafysische sferen terecht. Meer specifiek: in de substantieleer, die stelt dat elk object bestaat uit een substantieel en accidenteel deel. Het substantiële deel is dat wat een object écht is, dat wat je niet kunt veranderen zonder het object teniet te doen - haar essentie, zo je wil. Het accidentele deel is het tegenovergestelde daarvan. Bij een verandering van accidenten blijft het object in stand.


Een klassiek voorbeeld is: de mens, voorgesteld als rationeel dier.[^2] De ratio behoort tot het substantiële deel van de mens. Zouden we iemand van zijn of haar ratio strippen, dan zou diegene ophouden een mens te zijn. Haarkleur of kleding of de specifieke taal die iemand spreekt, behoort daarentegen tot het accidentele deel. Iemand kan zijn haar verven, een ander kledingstuk aantrekken of een nieuwe taal leren, en dat heeft geen enkele invloed op zijn of haar mens-zijn.


Nu, is bevestigd-zijn een substantiële of een accidentele eigenschap van een e-mailadres? Mijn eerste ingeving zou zijn: accidenteel - vandaar dat ik geneigd zou zijn om het als een property te modelleren, en niet als apart type. - Maar het eigenlijke antwoord is: *de vraag is verkeerd*. De vraag veronderstelt dat er een metafysisch punt - buiten tijd, buiten ruimte - van waar we naar de dingen kunnen kijken en hen kunnen classificeren. Dat is een standpunt dat we vaak - onbewust - in proberen te nemen wanneer we een domein modelleren.[^3] 


Dit is mijn conclusie: mijn filosofische vooronderstellingen - en ook: mijn onwetendheid over de praktijk van eerlijke functies - hebben mijn capaciteit om een domein correct te modelleren beïnvloed. Of iets substantieel of accidenteel is, is niet de juiste vraag. - Wat de plek en functie van een object is *in een domein* - en niet in de werkelijkheid, wat dat ook moge betekenen -, dat is wat je je als softwareontwikkelaar af dient te vragen.


Of dat onze taak makkelijker of moeilijker maakt, dat durf ik nog niet te stellen.


[^1]: Of, wat natuurlijk ook zou kunnen: `EmailAddress -> Validation<VerifiedEmailAddress>`, als je een foutmelding mee terug wil geven.

[^2]: Deze definitie, [ontleend aan Aristoteles](https://plato.stanford.edu/entries/aristotle/#EssHom), is controversieel, natuurlijk. Een voor de hand liggend kritiekpunt is bijvoorbeeld dat mensen met een zware geestelijke beperking *ex hypothesi* geen mens zouden zijn.

[^3]: Of wanneer we filosoferen. Maar beide hebben opvallend veel met elkaar gemeen, kan ik als ervaringsdeskundige inmiddels concluderen.
