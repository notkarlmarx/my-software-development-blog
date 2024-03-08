---
title: "Een oudergesprek"
author: "Karl van Heijster"
date: 2024-03-08T14:05:06+01:00
draft: true
comments: true
tags: ["software ontwikkelaar (rol)", "werkplezier"]
summary: "Onlangs mocht ik op mijn oude universiteit jonge studenten (en hun ouders) geruststellen: het is goed mogelijk een leuke en degelijk betaalde baan te bemachtigen met een studie filosofie. Na afloop had ik een leuk gesprek met een Steve Jobs-lookalike -- een vader, geen student --, die me vertelde dat ook hij overwoog om te leren programmeren. Hij zei wat iedereen zegt die overweegt te leren programmeren: \"Ik heb het altijd leuk gevonden om dingen uit elkaar te halen om te kijken hoe ze werken.\" -- En ik besefte me opeens: ik heb dat *totaal* niet."
---

Onlangs mocht ik op mijn oude universiteit jonge studenten (en hun ouders) geruststellen: -- je hóeft niet in de goot te eindigen als afgestudeerd filosoof, dat is optioneel. Het is goed mogelijk een leuke en degelijk betaalde baan te bemachtigen met een studie filosofie. (Zie ook [deze](/blog/21/07/mijn-loopbaanwending/ "'Mijn loopbaanwending'") [deze blog] (OVER_FILOSOFIE_EN_SOFTWARE_ONTWIKKELEN).) Na afloop had ik een leuk gesprek met een Steve Jobs-lookalike -- een vader, geen student --, die me vertelde dat ook hij overwoog om te leren programmeren. 


Hij zei wat iedereen zegt die overweegt te leren programmeren: "Ik heb het altijd leuk gevonden om dingen uit elkaar te halen om te kijken hoe ze werken." En: "Ik ben zo iemand die graag met iets loopt prutsen te totdat het werkt."


En ik besefte me opeens: ik heb dat *totaal* niet. -- Ik peins er niet over dingen uit elkaar te halen, want ik als ik het per ongeluk sloop weet ik dat ik een hele middag bezig ben met het weer werkend krijgen. En dat gepruts, dat vind ik eigenlijk maar zonde van mijn tijd.


Betekent dat dat ik een slechte ontwikkelaar ben? Nee, natuurlijk niet. (-- Er zijn heel andere redenen waarom ik een slechte ontwikkelaar ben.) Maar het betekent wel dat de redenen die ik heb om programmeren leuk te vinden, anders zijn dan die van papa Jobs.


## Gevolgen


Wat mij aanspreekt in het ontwikkelen van software is hetzelfde als wat mij aanspreekt in de filosofie: het mogen verhelderen van problemen.[^1] Dit heeft grote gevolgen -- voor de vraag waar ik mijn tijd aan wil besteden in mijn werk en professionele ontwikkeling, bijvoorbeeld. 


Ik vind de nieuwste technieken niet per se interessant -- niet op zichzelf, althans. Nieuwe technieken interesseren me voor zover ze me in staat stellen een probleem (op een elegantere manier) op te lossen. Ik zal in Refinements niet snel voorstellen om de boel om te bouwen naar [microservices](https://microservices.io/) gemanaged in [Kubernetes](https://kubernetes.io/) -- niet zomaar. Ik zou eerder de vraag stellen: waarom zou je dat willen?


Ook het schrijven van code vind ik geen doel op zich. (Integendeel, zou ik eerder willen zeggen; zie [deze blog](/blog/21/08/moet-je-dit-willen-testen/ "'Moet je dit willen testen?'").) Code is maar een middel, een implementatiedetail, een manier om een probleem op te lossen. Het is, als je het mij vraagt, beter een probleem te doorgronden en tot de conclusie te komen dat daar geen code voor nodig is, dan om een halfbegrepen oplossing te bakken die van razendinteressante [ontwerppatronen](/tags/ontwerppatronen/ "Blogs met de tag 'ontwerppatronen'") aan elkaar hangt.


Begrijp me niet verkeerd, natuurlijk geeft het me een kick als ik een stuk code werkend krijg. Zo is je tests van rood naar groen zien gaan één van de dingen die [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") zo verslavend maakt. Maar dat vind ik niet het leukst aan programmeren. Het leukst aan programmeren is de stap die daarna komt: de refactorslag waarin de intentie van de code geëxpliciteerd wordt. Wat me fascineert aan code is de mogelijkheid om ideeën erin uit te drukken. 


Werkende code is de ondergrens -- ons ideaal als professional zou hoger moeten liggen dan dat. En niet alleen omdat dáár de (wat mij betreft) interessantste dingen gebeuren.


## Ander daglicht


Na mijn gesprek zag ik plots sommige keuzes van mijn collega-ontwikkelaars[^2] in een heel ander daglicht. Waarom checken ze hun codewijziging *nu* in? Waarom nemen ze niet de tijd er nog een stuk of drie, vier keer op te itereren, totdat ze uitdrukt wat ze in mijn beleving zou moeten uitdrukken? Waarom nemen ze genoegen met deze technische schuld? -- Een deel van het antwoord ligt 'm in het feit dat die collega *nu* klaarblijkelijk op het punt is gekomen waar 'ie energie van krijgt: er is geprutst, en nu werkt het.


(Natuurlijk -- dat begrijp ik heel goed -- is dat niet het hele verhaal. Er spelen ook andere zaken mee, zoals werkdruk en/of deadlines en/of teamcultuur en/of het feit dat sommige ontwikkelaars überhaupt nog nooit diepgaand hebben overwogen dat code ook *mooi* -- eenvoudig, helder, expressief -- kan zijn; laat staan dat het dat *moet* zijn.)


Dit is geen excuus om genoegen te nemen met "slechts" werkende code. Maar het verklaart wel waarom een team vol mensen die ervan houden dingen uit elkaar te halen en weer in elkaar te prutsen, de code oplevert die ze soms oplevert. Het is niet zo dat ze niet capabel zijn hun creatie onder controle te houden -- daar zijn ze slim genoeg voor. Maar hun interesses drijven hen tot het ontwerpen -- of liever: niet-ontwerpen -- van een systeem dat vol toffe technieken zit maar niet onderhoudbaar is.


Veel programmeurs worden er blij van aan nieuwe, spannende dingen te mogen beginnen. Te weinig programmeurs worden er blij van oude, bekende dingen te onderhouden en verfijnen.


## Conclusie


Het is te kort door de bocht om te concluderen: dat is waarom er meer filosofen de softwareontwikkeling in zouden moeten rollen. Immers, niet elke filosoof is hetzelfde. Maar het is terecht om te concluderen dat een team softwareontwikkelaars moet worden samengesteld uit individuen met verschillende persoonlijkheden, interesses en aandachtsgebieden.


Want begrijp me niet verkeerd: er is *niets* mis mee een softwareontwikkelaar te zijn die graag dingen uit elkaar haalt en ze weer in elkaar prutst. Dit soort ontwikkelaars kunnen juist een drijvende kracht vormen in de vernieuwing van een codebase. Ik ben de papa Jobs in mijn team heel dankbaar voor wat zij toevoegen. Maar hun liefde voor het werkend krijgen van nieuwe dingen moet gebalanceerd worden met de wens dat op een verantwoordelijke manier te doen, de wens om over een halfjaar nog steeds te kunnen begrijpen wat en waarom de code doet wat deze doet.


En dan blijken al die ochtenden en middagen en avonden die heb zitten zwoegen op het doorgronden van ondoordringbaar filosofisch proza ineens hun vruchten af te werpen. Dus misschien is de conclusie tóch dat meer filosofen de softwareontwikkeling in moeten rollen. 


Al zijn hun vaders natuurlijk ook van harte welkom.


[^1]: Eerder, in [deze blog](/blog/23/05/waar-doe-je-het-voor/ "'Waar doe je het voor?'"), gaf ik overigens nog een heel ander antwoord op dezelfde vraag. Nu zal ik niet ontkennen in veel van mijn werk door luiheid gedreven te worden, maar het is dunkt me te lollig om dit als centrale drijfveer te kenschetsen.  


[^2]: Nota bene, ik heb, als ik dit zeg, geen specifieke collega op het oog. Ik doel op collega's in het algemeen: mensen die in hetzelfde werkveld actief zijn als ik.
