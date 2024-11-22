---
title: "Teveel tegelijk"
author: "Karl van Heijster"
date: 2024-11-22T09:47:26+01:00
draft: true
comments: true
tags: ["aannames", "continuous integration", "pair programming", "samenwerking", "software ontwikkelaar (rol)", "sprint retrospective", "teamcultuur", "verandering"]
summary: "\"We zijn met teveel dingen tegelijk bezig,\" constateert een ontwikkelaar tijdens de Retrospective. Die is met dit bezig, die met dat; hij met zus en zij met zo. Er is geen eenheid, iedereen werkt op zijn eigen eiland. -- Het is een terugkerend thema. Waar ligt dat aan?"
---

"We zijn met teveel dingen tegelijk bezig," constateert een ontwikkelaar tijdens de [Retrospective](/tags/sprint-retrospective/). Die is met dit bezig, die met dat; hij met zus en zij met zo. Er is geen eenheid, iedereen werkt op zijn eigen eiland.


Het is een terugkerend thema. -- Waar ligt dat aan?


{{< asterisk >}}


Het is verleidelijk om te zeggen: "De business maakt geen keuzes. Ze vinden: dit moet eerst, maar dit ook en dat ook -- en het moet allemaal nu." En het is waar: keuzes maken is niet altijd de sterkste kant van onze stakeholders.


Maar betekent dat dat wij als ontwikkelaars daarin mee moeten gaan? Zijn we verplicht om te proberen alle deadlines tegelijkertijd te halen?


We zouden ook kunnen vragen: wat is het aller-, aller-, allerbelangrijkst? -- Dan gaan we daar eerst mee aan de slag. En als dat klaar (of: klaar genoeg) is, dan pakken we het aller-, allerbelangrijkste punt op.


Als team heb je een keuze: vijf dingen half doen, of drie dingen goed.


{{< asterisk >}}


Natuurlijk is het niet altijd de business die ons ertoe verleidt onze focus op te splitsen. Vaak genoeg constateren we: het heeft geen zin om daar met z'n tweeën aan te werken, dan lopen we elkaar alleen maar in de weg.


Wat we dan bedoelen is: het heeft geen zin om daar met z'n tweeën *individueel* aan te werken.


Veel ontwikkelaars zien programmeren als een in essentie eenzame bezigheid, iets wat ze doen in volledige afzondering van de rest van het team. Maar programmeren *hoeft* er niet zo uit te zien.


We zouden kunnen [*pairen*](https://www.karlvanheijster.com/tags/pair-programming/ "Blogs met de tag 'pair programming'"). Je kunt *wel degelijk* met z'n tweeën aan een feature te werken -- het zou zelfs met een heel team kunnen, als je wil. 


De problematische veronderstelling is dat het werk individueel moet worden opgepakt. 


{{< asterisk >}}


-- Meer nog: we bedoelen, het heeft geen zin om daar met z'n tweeën *individueel* aan te werken *zonder onderlinge afstemming of tussentijdse samenvoeging van ons werk*.


Maar zelfs zonder *pair programming* zou je met z'n tweeën aan een feature kunnen werken -- als je maar regelmatig elkaars wijzigingen integreert. Dat is het idee achter [*continuous integration*](/tags/continuous-integration/ "Blogs met de tag 'continuous integration'") (CI). 


De problematische veronderstelling hier rust 'm in het feit dat we elkaars wijzigingen zo lang mogelijk van elkaar gescheiden houden op aparte *feature branches* die pas samenkomen aan het eind van de rit -- met een pijnlijke (want grote) *merge* tot gevolg.


Er zijn twee manieren om pijnlijke *merges* te voorkomen. De ene is: de werkverdeling zodanig te in te richten, zodat er überhaupt geen *merge* plaats hoeft te vinden. De andere is: het werk zodanig opzetten dat er aan de lopende band *merges* plaatsvinden.


{{< asterisk >}}


In databasemetaforen zou je kunnen zeggen: wat wij deden was *pessimistic [locking](https://en.wikipedia.org/wiki/Lock_(computer_science) "'Lock (computer science)', Wikipedia")*, en CI is *optimistic locking*. (Ik ontleen de metafoor aan [Mark Seemanns](https://blog.ploeh.dk/) uitstekende [*Code That Fits in Your Head*](https://www.oreilly.com/library/view/code-that-fits/9780137464302/ "'Code That Fits in Your Head: Heuristics for Software Engineering', Mark Seemann, O'Reilly Media").)


{{< asterisk >}}


CI is een tegenintuïtief idee. Als je continu rekening dient te houden met de wijzigingen van je collega's, hoe kun je dan ooit de rust vinden om jouw feature goed en wel te ontwikkelen?


De crux zit 'm in de grootte van die wijzigingen. Want zolang de wijzigingen klein zijn, is het niet moeilijk om eventuele conflicten te verwerken. Dat wordt het pas als je aan het eind een heel grote wijziging moet zien te integreren.


Maar CI is niet makkelijk. Het veronderstelt dat elke wijziging die je deelt met je collega's het systeem als geheel niet breekt. CI is dus alleen mogelijk met een uitputtende testsuite, ontwikkeld met [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD).


{{< asterisk >}}


Een Sprint Retrospective gaat over wat *jij* kunt veranderen, over het minimale wat je *nu* kunt doen om een situatie te verbeteren.


De terugkerende observatie dat we met teveel dingen tegelijk bezig zijn, heeft er niet toe geleid dat we individueel werken of *feature branches* bij het grofvuil hebben gezet. 


Waarom niet? -- Omdat dat *moeilijk* is. Het vraagt van een team ingesleten patronen te herzien en te veranderen. De veranderde werkwijze zal op korte termijn geen voordeel opleveren, omdat het zich daar aanvankelijk nog niet comfortabel bij zal voelen. Het team zal fouten maken -- beginnersfouten -- en, als het tegenzit, uit frustratie teruggaan naar de oude manier van werken.


Maar het is het enige wat het team *kan* doen -- het enige wat *volledig* binnen zijn eigen invloedsfeer ligt.


De schuld bij de besluiteloosheid van de business leggen is daarentegen *makkelijk*. Maar: die besluiteloosheid ligt (gedeeltelijk of misschien zelfs volledig) buiten de invloedsfeer van het team. En dus kan een team dat zich daar op besluit te focussen, aan het eind van de dag weinig anders doen dan de situatie te accepteren.
