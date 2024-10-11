---
title: "De filosofische geschiedenis van een ontwerpkeuze"
author: "Karl van Heijster"
date: 2024-10-11T10:38:52+02:00
draft: true
comments: true
tags: ["domain-driven design", "domeinmodel", "filosofie", "properties"]
summary: "Softwareontwikkelaars schrijven niet slechts code, ze scheppen een model van de werkelijkheid. Wat dat betreft staan ze in een lange filosofische traditie. Oftewel: wat kunnen Plato en Wittgenstein ons leren over het modelleren van een (on)geverifieerd e-mailadres?"
---

> "*Philosophy is a battle against the bewitchment of our intelligence by means of language.*" --- Ludwig Wittgenstein, *Philosophical Investigations*


Softwareontwikkelaars schrijven niet slechts code, ze scheppen een model van de werkelijkheid. Wat dat betreft staan ze in een lange filosofische traditie. Oftewel: wat kunnen Plato en Wittgenstein ons leren over het modelleren van een (on)geverifieerd e-mailadres?[^1]


{{< asterisk >}}


## Een zeer, zeer, zeer korte geschiedenis van de filosofie


427 v.Chr.: [Plato](https://plato.stanford.edu/entries/plato/ "'Plato', Stanford Encyclopedia of Philosophy") wordt geboren in Athene, Griekenland. Hij zal beroemd worden om zijn [Ideeënleer](https://en.wikipedia.org/wiki/Theory_of_forms "'Theory of forms', Wikipedia"), die stelt dat de zichtbare werkelijkheid slechts een afspiegeling is van eeuwige, universele Ideeën. Hij sterft in 347 v.Chr..


[Alfred North Whitehead](https://plato.stanford.edu/entries/whitehead/ "'Alfred North Whitehead', Stanford Encyclopedia of Philosophy") zei ooit: "*The safest general characterization of the European philosophical tradition is that it consists in a series of footnotes to Plato.*" Die traditie nemen we nu daarom maar even voor lief.


26 april 1889: [Ludwig Wittgenstein](https://plato.stanford.edu/entries/wittgenstein/ "'Ludwig Wittgenstein', Stanford Encyclopedia of Philosophy") wordt geboren in Wenen, Oostenrijk. In 1922 meent hij alle filosofische problemen op te hebben gelost in zijn [*Tractatus Logico-Philosophicus*](https://en.wikipedia.org/wiki/Tractatus_Logico-Philosophicus "'Tractatus Logico-Philosophicus', Wikipedia"). De werkelijkheid blijkt echter weerbarstiger. Hij sterft op 29 april 1951. In zijn posthuum verschenen [*Philosophical Investigations*](https://en.wikipedia.org/wiki/Philosophical_Investigations "'Philosophical Investigations', Wikipedia") (1953) komt hij iets dichter bij zijn oorspronkelijk gestelde doel. (Het is mijn favoriete boek aller tijden.)


{{< asterisk >}}


## Een geverifieerd e-mailadres (1/2)


2024, het heden. Een ontwikkelaar ontwerpt de inlogfeature voor een website.[^2] De flow: een gebruiker vult zijn gegevens in, krijgt een e-mail toegestuurd, drukt op de daarin aanwezige bevestigingsknop -- en mag de applicatie gebruiken. 


Hij redeneert: ik moet dus een object `EmailAddress` creëren, en dat `EmailAddress` kan bevestigd of geverifieerd zijn, of niet. De vraag: hoe ziet dat object eruit? 


Een voor de hand liggende oplossing is deze:


```cs
public class EmailAddress 
{
    public bool IsVerified { get; set; }
    // Other properties...
}
```


En inderdaad: dat werkt. Maar: 

1. Deze oplossing noodzaakt de ontwikkelaar checks in te bouwen in delen van de code om na te gaan of er sprake is van een geverifieerd e-mailadres. Om na te gaan dat de code werkt zoals bedoeld, zal hij [unittests](/tags/unit-tests/ "Blogs met de tag 'unit tests'") moeten schrijven. 

2. Een functie die een geverifieerd e-mailadres nodig heeft, en daarvoor gebruik maakt van een `EmailAddress` met de property `IsVerified` op `true`, is niet [*eerlijk*](/blog/22/07/wat-zijn-eerlijke-functies/ "'Wat zijn eerlijke functies?'"). De functiesignatuur zegt een `EmailAddress` te verwachten, maar verwacht eigenlijk maar een subset daarvan. 

3. De taal van de code weerspiegelt niet langer de taal van het domein. Domeinexperts maken onderscheid tussen geverifieerde en ongeverifieerde e-mailadressen; in de code zijn deze concepten verpakt in één en dezelfde class.


## Een geverifieerd e-mailadres (2/2)


Dit is een betere oplossing:


```cs
public class EmailAddress 
{ 
    // Properties... 
}

public class VerifiedEmailAddress : EmailAddress 
{ 
    // Properties... 
}
```


Immers:


1. De ontwikkelaar hoeft bij deze oplossing geen checks in te bouwen: de compiler geeft een foutmelding wanneer iemand een `EmailAddress` probeert te gebruiken op een plek waar een `VerifiedEmailAddress` verwacht wordt. Tests zijn daarom niet nodig.

2. De code is eerlijk. Een functie die een geverifieerd e-mailadres verwacht, signaleert die informatie in zijn functiesignatuur.

3. De code weerspiegelt de taal van het domein. Domeinexperts behandelen geverifieerde en ongeverifieerde e-mailadressen anders, en de code ruimt daar dus twee concepten voor in.


{{< asterisk >}}


## De filosofische geschiedenis van een ontwerpkeuze (1/2)


Waarom is de eerste oplossing, de minste oplossing, de meest voor de hand liggende? Mijn stelling is: deze oplossing ligt in de lijn van de Europese filosofische traditie (die kan worden gekarakteriseerd als een reeks voetnoten bij Plato), de traditie die ons denken voor een groot deel heeft gevormd.


Een programmeur in de Platoonse traditie bekijkt de wereld vanuit een [metafysisch](https://plato.stanford.edu/entries/metaphysics/ "'Metaphysics', Stanford Encyclopedia of Philosophy") standpunt, vanuit het standpunt van de eeuwigheid. Hij ziet allerlei dingen en vraagt zich af: wat is er *essentieel* aan die dingen en wat niet?


Bijvoorbeeld: wat is er essentieel aan [Socrates](https://plato.stanford.edu/entries/socrates/ "'Socrates', Stanford Encyclopedia of Philosophy")? Dat hij in Athene geboren is? Dat hij de leraar was van Plato? Dat hij ter dood werd veroordeeld? Nee: we kunnen ons voorstellen dat Socrates ergens anders was geboren, of iemand anders als leerling had, of dat hij een natuurlijke dood stierf -- hij zou nog steeds Socrates zijn. De genoemde eigenschappen van Socrates zijn *accidenteel*.


Kunnen we ons voorstellen dat Socrates een ezel was? Nee: als Socrates een ezel zou zijn, dan zou hij geen Socrates meer zijn. Mens-zijn is een essentiele eigenschap van de filosoof. (Een volgende vraag is: waarin bestaat de essentie van mens-zijn dan? Gelukkig hoeven we ons daar nu niet over te buigen!)


Net zo werkt het bij een e-mailadres. Wat is er essentieel aan een e-mailadres, zeg `socrates@akademeia.gr`? Je zou kunnen zeggen: dat het een lokaal deel bevat (`socrates`), een apenstaartje (`@`) en een domein (`akademeia.gr`). Haal één van deze onderdelen weg, en je houdt geen e-mailadres meer over. Dat is waarom de [*regular expression*](https://en.wikipedia.org/wiki/Regular_expression "'Regular expression', Wikipedia") om te valideren dat je met een e-mailadres te maken hebt, er als volgt uitziet: `^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$`.


Of het e-maildres geverifieerd is of niet, dat is -- vanuit het standpunt van de eeuwigheid bezien -- slechts accidenteel. Het e-mailadres houdt niet op een e-mailadres te zijn als de gebruiker wel of niet op de knop in onze bevestigingsmail drukt. 


## De filosofische geschiedenis van een ontwerpkeuze (2/2)


Maar: is het de taak van de ontwikkelaar om de metafysische kwaliteiten van een e-mailadres in code vast te leggen? Nee: de ontwikkelaar zou zich moeten bekommeren om het probleemdomein.


Wat heeft hem op dit pad gebracht? Wittgensteins zou waarschijnlijk zeggen: de taal zette hem op het verkeerde spoor. De ontwikkelaar hoort de domeinexperts spreken van een "e-mailadres" en een "geverifieerd e-mailadres" en concludeert dat het om één entiteit gaat die al dan niet gekwalificeerd wordt. Het woord "e-mailadres" staat in voor het ding *e-mailadres*, of die nu de eigenschap heeft geverifieerd te zijn of niet.


Dat is een uitdrukking van het idee: *de betekenis van een woord is het ding waar het voor staat*. Het is een centraal idee in de Europese filosofische traditie -- en, volgens Wittgenstein, een misvatting.[^3]


Hij plaatst daar een ander idee tegenover: *betekenis is gebruik*. De vraag die we ons zouden moeten stellen is welke rol de begrippen "e-mailadres" en "geverifieerd e-mailadres" spelen in het [taalspel](https://en.wikipedia.org/wiki/Language_game_(philosophy) "'Language game (philosophy)', Wikipedia") van de domeinexperts.


Wanneer we dat in kaart brengen, zullen we zien dat ze een heel andere functie hebben. Een "geverifieerd e-mailadres" heeft als rol bepaalde functionaliteit te ontsluiten. Het is als het ware de speciale pas waarmee een gebruiker toegang wordt gegeven tot verborgen delen van de applicatie. Een "e-mailadres" is daarentegen slechts datgene wat diegene heeft ingevuld in een aanmeldformulier. 


Je zou het verschil als volgt kunnen karakteriseren. De Platoonse ontwikkelaar ontwerpt een statische taxonomie van objecten in het domein. De Wittgensteiniaan probeert daarentegen recht te doen aan de rol(len) die woorden spelen in het dynamisch verloop van een "levend" businessproces -- dat is immers de plek waar ze thuishoren.


{{< asterisk >}}


Wittgenstein merkt op: de vragen waar we in de filosofie mee worstelen, zijn in de dagelijkse stroom van het leven volslagen onproblematisch. En hij concludeert op basis daarvan dat filosofische vragen schijnvragen zijn. Het zijn vragen die voortkomen uit het feit dat we bepaalde begrippen gebruiken buiten hun oorspronkelijke context, met alle raadselachtige gevolgen van dien. 


Wanneer we de woorden terugbrengen naar hun thuis, verdwijnen de problemen -- ze lossen eenvoudigweg op. Wanneer we de dingen juist zien, is een filosofisch problematisch term volstrekt vanzelfsprekend.


Softwareontwikkelaars schrijven niet slechts code, ze scheppen een model van de werkelijkheid. Wat dat betreft verschillen ze niet van filosofen. En net als filosofen, moeten ze de wereld zien zoals ze is, en niet zoals de taal suggereert dat ze is. Oftewel: ook het ontwerp van code is "*a battle against the bewitchment of our intelligence by means of language.*" 


[^1]: Deze blog schreef ik ter voorbereiding op een *lightning talk* die ik gaf op [Nimma Codes](https://www.nimma.codes/).

[^2]: Ik ontleen dit voorbeeld aan [een praatje](https://www.youtube.com/watch?v=MlPQ0FsPxPY "'Domain Modeling Made Functional – Scott Wlaschin', YouTube") van [Scott Wlaschin](https://scottwlaschin.com/) (ik schreef er al eerder over, [hier](/blog/23/01/eerlijke-domeinmodellen/ "'Eerlijke domeinmodellen'")). Zijn boek [*Domain Modeling Made Functional*](https://pragprog.com/titles/swdddf/domain-modeling-made-functional/) is overigens een aanrader.

[^3]: Kijk daarom uit met versimpelde weergaven van [Domain-Driven Design](/tags/domain-driven-design/ "Blogs met de tag 'domain-driven design'"). Deze stellen soms categorisch: vertaal zelfstandige naamwoorden naar classes en werkwoorden naar methods. Dat is op zijn best een aardige heuristiek, maar brengt het risico met zich mee je op een dwaalspoor te brengen.
