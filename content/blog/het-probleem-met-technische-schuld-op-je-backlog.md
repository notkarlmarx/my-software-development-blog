---
title: "Het probleem met technische schuld op je backlog"
author: "Karl van Heijster"
date: 2022-05-18T15:15:26+02:00
draft: true
comments: true
tags: ["boy scout rule", "clean code", "leermoment", "product backlog items", "professionaliteit", "refactoren", "scrum", "software ontwikkelen", "speelruimte", "technische schuld", "testen", "verandering", "waarde"]
summary: "Zo gaat mijn team om met het monitoren van technische schuld: we prikken elke Sprint een moment waarop we er met elkaar over praten, en als we het belangrijk genoeg vinden om er wat aan te doen, dan voeren we een Product Backlog Item op om die schuld weg te werken. Die aanpak werkt goed - goed genoeg, in elk geval. De technische schuld van onze huidige applicatie blijft grotendeels binnen de perken. En bovendien - dat is nog veel belangrijker - is iedereen in het team op de hoogte van het feit dat sommige plekken verbetering behoeven, en welke plekken dat zijn. Maar toch zit iets me niet helemaal lekker in die aanpak."
---

Een tijd geleden beschreef ik [hoe mijn team omgaat met het monitoren van technische schuld](/blog/21/09/hoe-technische-schuld-te-monitoren-en-prioriteren/). Lang verhaal kort: we prikken elke Sprint een moment waarop we er met elkaar over praten, en als we het belangrijk genoeg vinden om er wat aan te doen, dan voeren we een [Product Backlog Item](/tags/product-backlog-items/) (PBI) op om die schuld weg te werken.


Dat is beter dan het alternatief: niet erover praten, geen PBI's opvoeren en nadat je applicatie de onvermijdelijke status van een *big ball of mud* heeft bereikt, voorstellen helemaal opnieuw te beginnen. - Dat is de strategie die het team hanteerde ten tijde van het ontwikkelen van de *legacy*-applicatie die we nu uit proberen te faseren.


Die aanpak werkt goed - goed genoeg, in elk geval. De technische schuld van onze huidige applicatie blijft grotendeels binnen de perken. En bovendien - dat is nog veel belangrijker - is iedereen in het team op de hoogte van het feit dat sommige plekken verbetering behoeven, en welke plekken dat zijn.


## Beweging


Maar toch zit iets me niet helemaal lekker aan die aanpak. En dat is het volgende: als je technische schuld op de Backlog plaatst, dan is er geen garantie dat deze binnen afzienbare tijd weggewerkt gaat worden. Het zou zomaar kunnen dat die PBI's steeds maar weer naar beneden worden geschoven. Bijvoorbeeld omdat de business en de Product Owner (PO) van mening zijn dat nieuwe features nu meer prioriteit hebben, of omdat ontwikkelaars zich liever storten op kansen om nieuwe *shiny* technieken uit te proberen in plaats hun rommel op te ruimen.


Het bespreken van een probleem en het schrijven van een PBI lossen dat probleem nog niet op - maar ze geven wel het gevoel dat er wat in beweging is gezet. Maar daadwerkelijk bewegen, dat kan nog wel eens een brug te ver zijn. - Ten nadele van de applicatie als geheel.


## ObjectMothers en TestBuilders


Een concreet voorbeeld. Een tijd geleden stelde ik tijdens zo'n [Alignment-sessie](/blog/21/09/hoe-technische-schuld-te-monitoren-en-prioriteren/) voor de objectcreatie in onze testclasses te stroomlijnen door gebruik te maken van het [ObjectMother-patroon](https://martinfowler.com/bliki/ObjectMother.html) voor simpele objecten, en [TestBuilders](http://natpryce.com/articles/000714.html) voor complexere objecten. (Zie ook [deze blog](/blog/21/09/droger-tests-met-factory-methods/).) Onze unit- en integratietests liepen over van de codeduplicatie als het ging om het instantiëren van nieuwe objecten, dus iedereen was het daar volmondig mee eens.


En daarom gebeurde er de maanden daarop precies niks op dat gebied. Het opruimen van de unit- en integratietests was [wel belangrijk, maar nooit urgent](https://leansixsigmagroep.nl/lean-agile-en-six-sigma/eisenhower-matrix/).


## Actie


Wat te doen? Het probleem was bekend bij iedereen in het team, en toch voelde niemand zich geroepen om in actie te komen. - Ikzelf niet uitgezonderd. 


Sterker nog, het bestaan van het technische schuld-PBI op onze Backlog hield me actief tegen om zomaar aan deze onderneming te beginnen. Het opruimen van de tests was een bezigheid die onder *dat* PBI viel, en niet onder de PBI's die ik maand na maand oppakte. Het kwam eenvoudigweg niet in me op om refactorslagen - laat slaan refactorslagen van *tests* (*\*vies gezicht trekken doet\**) - mee te nemen bij het bouwen van nieuwe features. 


Als we grootscheeps meenden te moeten refactoren, dan moesten we dat apart op de Backlog zetten, zodat onze PO dat kon prioriteren - of nalaten. Dat was mijn impliciete mening.


## Speelruimte


Die instelling veranderde toen ik in [*The Art of Agile Development*](https://www.oreilly.com/library/view/the-art-of/9780596527679/) de notie van [speelruimte](/blog/22/05/tevreden-ontwikkelaars-en-stakeholders-dankzij-speelruimte/) ontdekte. 


Plots viel het kwartje: refactoren is niet iets wat je op speciaal daarvoor bestemde momenten doet. Het is iets wat je doorlopend in je werk oppakt. En daarvoor is het nodig dat je er tijd voor inplant. Niet door een PBI op de Sprint te slepen, maar door er standaard ruimte voor te reserveren in de Sprint - de speelruimte.


## *Boy Scout Rule*


De grap is natuurlijk dat ik dit op een bepaald niveau altijd wel geweten heb. De [*Boy Scout Rule*](https://wiki.c2.com/?BoyScoutRule) - laat de boel schoner achter dan je 'm aantrof - is elke goede ontwikkelaar bekend. Maar ik had deze regel ongemerkt altijd opgevat als: pas hier en daar een variabelenaam aan, maar maak het vooral niet te gek. Ruim wat papiertjes en lege blikjes op hier en daar, je hoeft het bos niet schoon te vegen.


Maar ook relatief fikse refactorslagen vallen onder de *Boy Scout Rule*. Want waarom zou je in hemelsnaam niet een paar honderd regels code aan de ene kant introduceren, als dit je code aan de andere kant enorm vereenvoudigt? Dat kleine - of iets grotere - beetje *effort* dat je er in steekt, verdien je ruimschoots terug.


## Een stapje, twee stapjes


Bovendien: je hoeft niet je complete applicatie te herstructureren. Begin maar gewoon met de code waar je in bezig bent. Als de unit- en integratietests die je code raakt, gebruik maken van een ObjectMother, dan is dat al winst. De speelruimte doet de rest: een volgende keer, als je andere tests raakt, dan neem je die mee. 


\- En zo is het. Elke dag een stapje beter, en op sommige dagen twee stapjes - of de PO dat nu geprioriteerd heeft of niet. Dat maakt het verschil tussen een goede programmeur en een goede softwareontwikkelaar.
