---
title: "Test-driven development is een ontwerpdiscipline"
author: "Karl van Heijster"
date: 2022-07-29T07:35:45+02:00
draft: true
comments: true
tags: ["boeken", "clean code", "samenwerking", "single-responsibility principe", "software ontwikkelen", "test-driven development", "testen"]
summary: "Een collega benaderde me laatst met een vraag over een stuk code. Hij was bezig met het implementeren van een feature om een toets met afbeeldingen om te zetten naar een PDF-representatie ervan. Zijn vraag was: hoe kom ik aan die afbeelding? Of liever: waar kom ik aan die afbeelding? Zijn eerste ingeving was om via dependency injection de relevante repository mee te geven aan de `ImagePdfGenerator`. - Het is een klassiek geval van het verknopen van het ophalen van data en het manipuleren ervan. Ik bleef wel met een knagend gevoel achter: hoe makkelijk blijkt het om dankzij een DI-container de verantwoordelijkheden van classes te verwateren - en wat moeten we daarmee?"
---

Ik ga het nog één keer hebben over het scheiden van code die data ophaalt van code die data manipuleert ~~en dan hou ik ermee op~~.


## Van code naar PDF


Een collega benaderde me laatst met een vraag over een stuk code. Hij was bezig met het implementeren van een feature om een toets om te zetten naar een PDF-representatie ervan. 


Ons datamodel schrijft voor: een [toets](http://www.imsproject.org/spec/qti/v3p0/impl#h.j41e5xe4h9bo) is een object dat - onder andere - een lijst met verwijzingen naar toetsvragen bevat. In het veld noemen we zulke vragen "[items](http://www.imsproject.org/spec/qti/v3p0/impl#h.77l136x98r3)". De items bevatten tekst - een inleiding, de feitelijke vraag - en interacties - meerkeuzemogelijkheden, een antwoordveld enzovoort. 


Onze codebase bevat diverse `PdfGenerators` voor de verschillende onderdelen van een item. We hebben classes die verantwoordelijk zijn voor het omzetten van de inleiding, de vraag, de interacties, enzovoort enzoverder.


## Afbeeldingen


Een item kan ook media bevatten, zoals een afbeelding.[^1] Het object in onze code dat een item vertegenwoordigt, bevat in dat geval een verwijzing naar een media-object dat in de [Azure BlobStorage](https://docs.microsoft.com/nl-nl/azure/storage/blobs/storage-blobs-introduction) leeft.


Welnu, de vraag van mijn collega was: hoe kom ik aan dat media-object? Of liever: waar kom ik aan dat media-object? Zijn eerste ingeving was om via [dependency injection](https://en.wikipedia.org/wiki/Dependency_injection) de [repository](https://martinfowler.com/eaaCatalog/repository.html) die de Blobstorage aanspreekt, mee te geven aan de `ImagePdfGenerator`.


Het is een klassiek geval van het verknopen van het ophalen van data en het manipuleren ervan.


## Verantwoordelijkheden


Ga maar na: het is verantwoordelijkheid van de `ImagePdfGenerator` om data te manipuleren. De class is ervoor verantwoordelijk om de afbeelding waar in het `Item` naar wordt gerefereerd, een plekje te geven in de PDF. 


De `ImagePdfGenerator` is er *niet* voor verantwoordelijk om die afbeelding op te halen. [Het ophalen van data dient te worden gescheiden van het manipuleren ervan.] (LINK)


De truc is dan ook niet om een repository als afhankelijkheid de class in te injecteren. De truc is om de juiste afbeelding als afhankelijkheid te injecteren. Het ophalen van die afbeelding dient al veel eerder te zijn gebeurd.


## *Clean Craftmanship*


Nu had ik toevallig een [blog] (LINK) geschreven over het scheiden van code die data ophaalt van code die data manipuleert, dus ik draaide er mijn hand niet voor dit inzicht op om mijn collega over te brengen. Maar ik bleef wel met een knagend gevoel achter: hoe makkelijk blijkt het om dankzij een [DI-container](https://docs.microsoft.com/en-us/dotnet/core/extensions/dependency-injection) de verantwoordelijkheden van classes te verwateren - en wat moeten we daarmee?


Een paar dagen later las ik in *Clean Craftmanship* van Robert C. Martin de volgende zin: 


> It is that cycle [of red -> green -> refactor] that helps us to prevent harm to behavior and harm to structure. It is that cycle that allows us to prioritize structure over behavior. And that's why we consider TDD to be a *design* technique as opposed to a testing technique.


En dankzij de vraag van mijn collega klikte die zin op een heel nieuwe manier met me.


## Wat als...


Want stel nu dat mijn collega zijn `ImagePdfGenerator` via [Test-Driven Development](/tags/test-driven-development/) (TDD) zou hebben ontwikkeld. Zou hij dan ook bij me te rade gegaan met de vraag of hij een repository in die class zou moeten injecteren?


Ik denk het niet, eerlijk gezegd. Want als je eerst een test schrijft voor die class, dan peins je er niet over om een repository te injecteren om de boel draaiende te krijgen. 


Ten eerste kun je al niet *the real deal* injecteren, want dat zou inhouden dat je unittest een afhankelijkheid heeft naar de Blobstorage - en daarmee het rijk van de unittests ver achter zich laat. 


En ten tweede denk je wel twee keer na voordat je een [mock](https://en.wikipedia.org/wiki/Mock_object) van die repository gaat injecteren. Denk je eens in hoeveel regels code je zou moeten schrijven, voordat je je test draaiend hebt!


Nee, ik denk dat als mijn collega zijn feature bijeen had ge-TDD'd, dat 'ie dan haast gedachteloos een afbeelding (of een lijst met afbeeldingen, of een [`Dictionary`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=net-6.0) met afbeeldingen en hun id's - afhankelijk van de requirements) zou hebben meegegeven als afhankelijkheid.


## Eerst de interface


Het is zoals [James Shore](https://www.jamesshore.com/) zei in [*The Art of Agile Development*](https://www.oreilly.com/library/view/the-art-of/9780596527679/): [TDD dwingt je om éérst na te denken over de interface van je code, en daarna pas over haar implementatie](/blog/22/05/nog-een-reden-om-testgedreven-te-ontwikkelen/). Precies dáárom is TDD een ontwerpdiscipline, geen testdiscipline.


\- Dat middels TDD ontworpen code een haast perfecte testcoverage heeft, is *bijvangst*. Bedenk eens wat voor een bizarre constatering dat is!


[^1]: Een item kan ook audio of video bevatten, maar dat is voor de PDF-representatie minder relevant. Tot mijn grote spijt is ons papier nog altijd niet in staat om video en audio af te spelen.
