---
title: "De leercurve van Angulartests beklimmen - Deel 4"
author: "Karl van Heijster"
date: 2022-01-21T10:58:32+01:00
draft: true
comments: true
tags: ["angular", "clean code", "dry", "leermoment", "mocks", "ontwerppatronen", "software ontwikkelen", "testen", "unit tests", "web development"]
summary: "Wat is de kern van ons onderhoudprobleem probleem? Codeduplicatie - of liever: de duplicatie van informatie. Het opzetten van een bepaalde service en haar afhankelijkheden gebeurt voor elke (reeks) test(en) handmatig in de `beforeEach`-methode. Als dezelfde afhankelijkheid in twee verschillende reeks testen voorkomt, moet de ontwikkelaar deze twee keer uitschrijven. Maar is dat nu echt nodig?"
---

# Droger Angulartests met factory classes


In [het vorige deel] (LINK) in deze reeks toonde ik de noodzaak van mocks aan om onze tests onderhoudbaar te houden. Het had tests tot gevolg die er ongeveer zo uitzien:


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "example.service.spec.ts">}}


## Het probleem


Maar er kleven nadelen aan deze opzet. Want wat als de afhankelijkheden van een service veranderen? Of erger nog, wat als het gedrag van een afhankelijkheid verandert? 


In dat geval moet je als ontwikkelaar alle logica nalopen waarin die services en mocks figureren. En met het aantal services en afhankelijkheden dat onze applicatie inmiddels kent, zou dat onbegonnen werk zijn. Een bekend probleem roert zich opnieuw: de ontwikkelaar is meer bezig zijn tests te onderhouden dan waarde toe te voegen!


Wat is de kern van dit probleem? Codeduplicatie - of liever: de duplicatie van informatie. Het opzetten van een bepaalde service en haar afhankelijkheden gebeurt voor elke (reeks) test(en) handmatig in de `beforeEach`-methode. Als dezelfde afhankelijkheid in twee verschillende reeks testen voorkomt, moet de ontwikkelaar deze twee keer uitschrijven.


## De oplossing


Maar is dat nu echt nodig? Natuurlijk niet! In een [eerdere blog](/blog/21/09/droger-tests-met-factory-methods/) heb ik precies om deze reden gepleit voor het gebruik van factory methods.


In die blog beperkte ik me tot dezelfde afhankelijkheid in één testclass, maar het principe schaalt. We kunnen - moeten, zou ik willen zeggen! - de factory methods verhuizen naar een aparte class en deze in diverse tests gebruiken. Dat ziet er zo uit:


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "service.factories.ts">}}


(De mocks heb ik gedupliceerd, omdat het zou kunnen dat services verschillend gedrag kunnen verlangen om te functioneren. In principe geldt hier echter ook: bij wijziging van het gedrag van de mocks moet je op meerdere plekken dingen aanpassen. Je kunt als ontwikkelaar zelf kiezen hoe ver je hierin wil gaan.)


De intialisatielogica van de test ziet er nu een stuk schoner uit:


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "welcome.service.with-factory.spec.ts">}}


## Variatie


Zijn we nu dan eindelijk bij het einde van het verhaal? Bijna, maar nog niet helemaal. Want afhankelijkheden zijn niet zomaar afhankelijkheden: afhankelijkheden hebben impact.


Eén van onze geïnjecteerde services is bijvoorbeeld verantwoordelijk voor de [permissies](/blog/21/08/check-op-permissies-niet-op-rollen/) van een gebruiker. Afhankelijk van de permissies die in die afhankelijkheid zijn gedefinieerd, kan het gedrag in de testclass in kwestie verschillen.


Hoe ga je daar mee om in de context van factory classes? Allereerst bied je een mogelijkheid om datgene wat varieert te injecteren in de factory:


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "service-permissions.factory.ts">}}


De variatie kun je vervolgens in je testcases introduceren door Jasmines `describe`s in `describe`s te plaatsen. 


In de buitenste `describe` schrijf je de logica die over alle tests gelijk blijft. In dit geval is dat alleen het initialiseren van de `Service`. In de `beforeEach` van elke binnenste `describe` breng je de variatie aan, in dit geval de verschillende permissies[^1]:


{{< gist dotkarl 3086ecdaffd9bac3151a25173e2c093f "service-permissions.spec.ts">}}


## Conclusie


*Et voilà*: dankzij geparameteriseerde factory classes zijn onze tests onderhoudbaar én flexibel. Is de leercurve van Angulartests daarmee met de grond gelijk gemaakt? Nog lang niet, maar ietsje minder stijl is 'ie - wat mij betreft, althans - wel.


En zo heeft een eenvoudige .NET-ontwikkelaar het met pijn en moeite voor elkaar gebokst zijn programmeervaardigheden een heel klein beetje uit te breiden.


## Meer in deze reeks


1. [Van *end to end* naar unit tests] (LINK)

2. [Van integratie- naar unit tests] (LINK) 

3. [Zijn deze tests onderhoudbaar?] (LINK)

4. **Droger Angulartests met factory classes**


[^1]: Ik ontleen deze oplossing aan [dit antwoord](https://github.com/jasmine/jasmine/issues/1274#issuecomment-461678314) van [Cody Herzog](https://github.com/codyherzog) op een vraag op GitHub.
