---
title: "De leercurve van Angulartests beklimmen - Deel 3"
author: "Karl van Heijster"
date: 2022-01-13T15:43:01+01:00
draft: true
comments: true
tags: ["angular", "clean code", "leermoment", "mocks", "software ontwikkelen", "technische schuld", "testen", "unit tests", "web development"]
summary: "Hoe onderhoudbaar was onze testopzet? Onze services verwachtte niet één afhankelijkheid, maar wel vijf of zes of zeven - en soms zelfs meer. En die afhankelijkheden verwachtten op hun beurt ook weer vijf, zes, zeven afhankelijkheden. Het is niet ondenkbaar dat zo'n ontwikkelaar langer bezig zal zijn met het opzetten van al die afhankelijkheden, dan het daadwerkelijk verifiëren van het gedrag van het stukje code waar hij in is geïnteresseerd."
---

# Zijn deze tests onderhoudbaar?


In de vorige twee blogs in deze reeks zette ik uiteen (1) waarom oorspronkelijke plan van mijn team om de front end via *end to end*-tests te testen, [tot mislukken gedoemd was] (LINK) en (2) hoe we de leercurve van het testen in Angular probeerden te verkleinen door [services te testen in plaats van componenten] (LINK). Hoewel die laatste poging redelijk succesvol was, gaf ik aan dat dat nog niet het eind van het verhaal was.


Onze tests zagen er ongeveer zo uit:


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "welcome.service.spec.ts">}}


Voor services die maar één afhankelijkheid verwachten - in het bovenstaande de `UserService` - is dit een prima oplossing. 


## Drempel


Helaas hadden wij die luxe niet. Onze services verwachtte niet één afhankelijkheid, maar wel vijf of zes of zeven - en soms zelfs meer. En die afhankelijkheden verwachtten op hun beurt ook weer vijf, zes, zeven afhankelijkheden.


Dit werpt een behoorlijke drempel voor het schrijven van unit tests voor onze services. Een ontwikkelaar zal voor elke service een aanzienlijke tijd bezig zijn met het opzetten van een complexe afhankelijkheidsboom. 


Bovendien zal hij op deze manier bij elke nieuwe reeks testen de boom van de grond af aan op moeten bouwen - en met de hand elke keer opnieuw het benodigde gedrag moeten implementeren die als precondities gelden om de service in kwestie te kunnen testen.


Het is niet ondenkbaar dat zo'n ontwikkelaar langer bezig zal zijn met het opzetten van al die afhankelijkheden, dan het daadwerkelijk verifiëren van het gedrag van het stukje code waar hij in is geïnteresseerd.[^1]


## Kip-ei


Wat nu? De bovenstaande bevinding is een signaal dat onze services te zeer met elkaar verweven zijn - dat klopt. Wat we eigenlijk zouden moeten doen is dit: die services kritisch tegen het licht houden en opsplitsen waar nodig. Idealiter zou een service niet meer dan een handvol afhankelijkheden moeten kennen.


Maar het probleem daarvan is dat het ontzettend risicovol is om de services te refactoren, vóórdat er een goede testcoverage is. Het is gevaarlijk om zulke wijzigingen door te voeren zonder een geautomatiseerde manier hebben om te verifiëren dat die wijzigingen niet meer schade toebrengen dan wat anders. De hoeveelheid code die met goedbedoelde refactorslagen om zeep is geholpen, is gigantisch. 


Het is een klassiek kip-ei-probleem. Om te kunnen refactoren hebben we tests nodig. Maar om goede tests te kunnen schrijven, zouden we eerst moeten refactoren.


## Mocks, mocks, mocks


Een tweede optie is uitgebreid vertrouwen op mocks om de gaten in de implementatie in te vullen. [Mockobjecten](https://en.wikipedia.org/wiki/Mock_object) zijn objecten die speciaal gemaakt zijn om de eigenschappen en gedragingen te simuleren van afhankelijkheden ongeschikt zijn om in tests zelf te gebruiken.


Onze tests zouden er in dat geval zo uit kunnen komen te zien:


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "example.service.spec.ts">}}


In het voorbeeld zie je twee soorten afhankelijkheden: mocks en services. De mocks reserveer ik voor *third party*-code, de services bestaan louter en alleen uit code die het team zelf in beheer heeft.[^1]


Het gebruik van mocks versimpelt het opzetten van de afhankelijkheden voor een ontwikkelaar aanzienlijk. Sterker nog, deze opzetten *zonder* mocks is eigenlijk onbegonnen werk. De afhankelijkheidsboom kan ontzettend diep worden, en als ontwikkelaar heb je lang niet altijd directe toegang tot alle classes die je daarvoor nodig hebt.


## Nadelen


Maar er kleven ook nadelen aan het gebruik van mocks.[^2] Ten eerste zijn ze onderhoudsintensief. Het verwachte gedrag moet door een ontwikkelaar handmatig uitgeschreven worden. En omdat verschillende tests in principe verschillend gedrag van dezelfde afhankelijkheid zou kunnen verwachten, kun je uitkomen dat je voor elke test aparte mocks moet uitschrijven. 


\- En dan heb ik het nog niet eens over de situatie waarin het gedrag van een afhankelijkheid verandert! In zo'n situatie moeten alle mocks aangepast worden. Het maakt tests, met andere woorden, broos voor verandering.


Bovendien is deze werkwijze foutgevoelig. Een ontwikkelaar die het verwachte gedrag van een afhankelijkheid verkeerd inschat, schrijft een niet-waarheidsgetrouwe mock. De tests die van die mock afhankelijk zijn, zijn in feite waardeloos. Ze geven de illusie van werkende code, zonder dat ze bugs in de productie-omgeving voorkomen.


## *To be concluded*


Wat betekent dat nu voor onze situatie? We kunnen niet refactoren, want we hebben onvoldoende tests. En het is moeilijk om snel tests te voegen, vanwege de hoeveelheid afhankelijkheden. Mocken zal noodzakelijk zijn, maar het is op zichzelf geen eenvoudige oplossing voor ons probleem.


Hoe nu verder? Dat leg ik in de laatste blog in deze reeks uit. Hint: het heeft [hier](/blog/21/09/droger-tests-met-factory-methods/) iets mee van doen.


## Meer in deze reeks

1. **Van *end to end* naar unit tests**

2. Van integratie- naar unit tests [volgt binnenkort]

3. Zijn deze tests onderhoudbaar? [volgt binnenkort]


[^1]: Er bestaat in de testwereld enige controverse over de vraag of je zulke code ook zou moeten mocken in unit tests. Vladimir Khorikov heeft in [*Unit Testing*](https://www.manning.com/books/unit-testing) mijns inziens de discussie beslecht in het voordeel van de bovenstaande implementatie.


[^2]: Zie opnieuw Khorikovs [*Unit Testing*](https://www.manning.com/books/unit-testing), en hoofdstuk 13 in [*Software Engineering at Google*](https://www.oreilly.com/library/view/software-engineering-at/9781492082781/).
