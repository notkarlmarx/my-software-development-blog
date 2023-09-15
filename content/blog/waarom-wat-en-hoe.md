---
title: "Waarom, wat en hoe"
author: "Karl van Heijster"
date: 2023-09-15T08:46:15+02:00
draft: true
comments: true
tags: ["code lezen", "intentie van code", "leermoment", "product backlog refinement", "test-driven development"]
summary: "Waarom bestaat deze code? -- wat doet het? -- en hoe doet het dat? Ik maaide het gras van mijn achtertuin, toen me inviel dat het beantwoorden van die vragen niet beperkt blijft tot het *lezen* van code. Elke ontwikkelaar stelt zichzelf precies dezelfde vragen als deze code gaat *schrijven*. En een goede ontwikkelaar beantwoordt ze in de geijkte volgorde."
---

Een tijd geleden schreef ik over de [drie vragen die elk *pull request* (PR) moet beantwoorden](/blog/23/09/drie-vragen-die-elk-pull-request-moet-beantwoorden/). Ze luiden als volgt: (1) Waarom bestaat dit PR überhaupt? (2) Wat doet de code concreet? (3) Hoe doet de code dat?


Ik schreef over die vragen in de context van code reviews. Een codereviewer moet het waarom, het wat en het hoe van de code kennen -- en pas dan kan deze een goed oordeel vormen over de kwaliteit van de code. Een goedkeuring of afwijzing van de codewijziging is afhankelijk van de mate waarin die vragen bevredigend worden beantwoord.


## Code beoordelen


Natuurlijk vormen PR's en code reviews niet de enige momenten waarop we code moeten beoordelen -- dat doen we doorlopend. Wanneer ik een volslagen onbekende codebase voor mijn neus krijg, dan kijk ik eerst de documentatie door om het waarom van de code te achterhalen. Als ik daar eenmaal mee bekend ben, en wat dieper in de code wil duiken, dan ga ik eerst op zoek naar de tests. Zo kom ik erachter wat de code doet, voordat ik me verdiep in de manieren hoe de code dat voor elkaar krijgt.


Eerst het waarom, dan het wat, en pas daarna het hoe.


Ik maaide het gras van mijn achtertuin, toen me inviel dat het beantwoorden van die vragen niet beperkt blijft tot het *lezen* van code. Elke ontwikkelaar stelt zichzelf precies dezelfde vragen als deze code gaat *schrijven*. En een goede ontwikkelaar beantwoordt ze in de geijkte volgorde.


## Waarom


Het achterhalen van het waarom van de te schrijven code, dat is waar [Product Backlog Refinements](/tags/product-backlog-refinement/ "Blogs met de tag 'product backlog refinement'") om draaien in [Scrum](/tags/scrum/ "Blogs met de tag 'scrum'"). Refinements draaien niet primair om de vraag hoe de gewenste functionaliteit de codebase in te fietsen -- ze draaien in eerste instantie om de vraag waarom je überhaupt die functionaliteit zou willen hebben: [het ontdekken van de vraag achter de vraag](/blog/23/04/de-vraag-achter-de-vraag-ontdekken/). (Of, wat net zo vaak voorkomt: het ontdekken van de vraag die je [Product Owner](https://www.scrum.org/resources/what-is-a-product-owner "'What is a Product Owner?' scrum.org") heeft beantwoord met zijn gepresenteerde oplossing.)


Pas als je weet wat je eindgebruikers willen bereiken, kun je verzinnen wat ervoor nodig is om dat voor elkaar te krijgen. 


Het is een misvatting te denken dat softwareontwikkelaars louter en alleen bestaan om "dat wat gebruikers willen" in code om te zetten. Code schrijven is maar een deel van het proces -- en het eenvoudigste deel bovendien (hoewel maar zelden makkelijk!). De echte uitdaging zit 'm in het scherp krijgen van het achterliggende probleem. Daar spelen ontwikkelaars, omdat zij degenen zijn die het op mogen lossen, een belangrijke rol in. Zij hebben vaak een beter idee van wat er softwaretechnisch mogelijk is om een probleem op te lossen dan de eindgebruikers zelf, of hun vertegenwoordigers. Wie ontwikkelaars ziet als codekloppers, benut maar de helft van hun potentie.


## Wat


Als eenmaal duidelijk is waarom er code geschreven zal moeten worden, kan er worden nagedacht over wat die code dan precies moet gaan doen. Nota bene: na het waarom, eerst het wat -- en later pas het hoe.


In de flits van begrip die door mijn hoofd schoot, toen ik het gras aan het maaien was, besefte ik dat dit [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) is. TDD zegt: schrijf eerst een falende test, en vervolgens zo min mogelijk code om de test te doen slagen. Ruim je code op, en begin dan opnieuw: eerst een falende test, daarna zo min mogelijk code om de test te doen slagen.


Oftewel: eerst het wat, dan het hoe; dan weer 't wat, daarna weer 't hoe, enzovoorts.


Een nieuw inzicht is dit niet. TDD wordt al sinds jaar en dag beschreven als met name een ontwerpmiddel, en pas in tweede instantie als testtechniek -- door mezelf, bijvoorbeeld: [hier](/blog/22/09/tests-als-ontwerpmiddel/ "'Tests als ontwerpmiddel'"), [hier](/blog/22/08/test-driven-development-is-een-ontwerpdiscipline/ "'Test-driven development is een ontwerpdiscipline'") en [hier](/blog/22/05/nog-een-reden-om-testgedreven-te-ontwikkelen/ "'Nóg een reden om testgedreven te ontwikkelen'"). 


Maar het herkaderen van dit inzicht in termen van de mogelijkheidsvoorwaarden voor het beoordelen van code, werpt wel een nieuw licht op de zaak. Het toont aan dat het beoordelen van code werkelijk een continu proces is -- iets dat zich voltrekt voor code die zojuist geschreven is, op dit moment geschreven wordt, en zelfs binnenkort geschreven gaat worden.


Wat TDD doet is dat beoordelingsproces expliciet maken -- en inzichtelijk bovendien. Want de tests waarmee je je implementatie opbouwt, geven je bij elke wijziging feedback over wat de code doet, of niet meer doet. En dat maakt het beoordelen van je laatste wijziging een stuk eenvoudiger.


## Hoe


Nog te vaak zie ik mijn collega's beginnen met het hoe. Ze hebben wel enige notie van waarom ze de code schrijven die ze schrijven, en ze hebben ook wel een idee van wat ze willen dat de code doet, maar ze hebben niet de kunde of discipline of interesse om het waarom, wat en hoe in de juiste volgorde te doorlopen. 


Dat is geen kritiek, overigens. Testgedreven kunnen ontwikkelen is een vaardigheid die je maar met moeite verkrijgt. Het vereist geduld en oefening en regelmatige reflectie op wat er werkt en wat niet. De ruimte voor het ontwikkelen van die vaardigheid wordt je niet cadeau gedaan.


Maar als TDD eenmaal in je systeem zit, is het moeilijk terug te gaan naar de oude manier van werken. TDD voorkomt dat je implementatie (het hoe) je interface (het wat) dicteert, het geeft je continue feedback over de staat van je code, het stelt je in staat om in kleine stappen te werken. Er bestaan geen zilveren kogels in de wereld van softwareontwikkeling -- maar één praktijk komt gevaarlijk dicht in de buurt, en dat is TDD.


De conclusie kan dan ook alleen maar zijn: ik zou vaker de achtertuin moeten maaien.
