---
title: "Tevreden ontwikkelaars én stakeholders dankzij speelruimte"
author: "Karl van Heijster"
date: 2022-04-01T09:50:02+02:00
draft: true
comments: true
tags: ["agile ontwikkeling", "boeken", "leermoment", "procesverbetering", "productiviteit", "professionaliteit", "scrum", "sprint planning", "stakeholders", "verantwoordelijkheid", "werkbalans"]
summary: "Dit is denk ik voor veel teams een herkenbare situatie: de ene Sprint verbranden jullie achttien *effort points*, de volgende twintig, de keer daarop vijftien. Wat is dan de capaciteit van het team? Hoe kun je voorspellen wat jullie de volgende Sprint gaan opleveren, als de capaciteit fluctueert van keer tot keer? Het antwoord is: dat kun je niet. Maar in *The Art of Agile Development* van James Shore vond ik hier een oplossing voor."
---

Dit is denk ik voor veel teams een herkenbare situatie: de ene Sprint verbranden jullie achttien [*story points*](https://www.scrum.org/resources/blog/why-do-we-use-story-points-estimating), de volgende twintig, de keer daarop vijftien.[^1] Wat is dan de [capaciteit](https://www.agile-academy.com/en/agile-dictionary/capacity/)[^2] van het team? Hoe kun je voorspellen wat jullie de volgende [Sprint](https://www.scrum.org/resources/what-is-a-sprint-in-scrum) gaan opleveren, als de capaciteit fluctueert van keer tot keer?


Het antwoord is: dat kun je niet. Soms zal de inschatting van het team meevallen, de andere keer valt het tegen. Wat betekent het dan als je zegt: "Volgende Sprint verwachten we feature *x* op te leveren?" Iets, ja, maar niet veel. Aan het eind van de dag zijn je stakeholders aan het lot overgeleverd.


## Voorbij


Mijn team bevindt zich zo ongeveer in die situatie - of liever: we zijn er al voorbij. Er was een tijd dat we een inschatting van onze capaciteit maakten op basis van de vorige paar Sprints, maar die getallen fluctueerden zo hevig dat we stilzwijgend hebben besloten dat maar te laten  voor wat het was. Wat we nu doen is op gevoel een inschatting maken tijdens de Sprint Planning - en hopen dat het mee zal vallen de komende twee weken.


Dat kan methodischer, natuurlijk. Sterker nog, het móet methodischer, want onze Product Owner (PO) moet de stakeholders een indicatie kunnen geven van wat we wanneer op denken te leveren.


In [*The Art of Agile Development*](https://www.oreilly.com/library/view/the-art-of/9780596527679/) van [James Shore](https://www.jamesshore.com/) vond ik een manier die ons misschien kan helpen. Een centraal begrip in zijn adviezen is dat van *speelruimte* ("[*slack*](https://www.solutionsiq.com/resource/blog-post/the-importance-of-slack-in-achieving-speed-and-quality/)"). 


## *Done done*


Maar vóórdat ik daar kom, moet ik eerst iets zeggen over het inschatten van de verwachte capaciteit. Gelukkig kan ik daar kort over zijn: dat is wat je de vorige Sprint af hebt gemaakt. 


En met afgemaakt bedoel ik *afgemaakt*: [*done done*](https://www.scrum.org/forum/scrum-forum/5930/done-vs-done-done) volgens jullie [*Definition of Done*](https://www.scrum.org/resources/blog/done-understanding-definition-done) (DoD). Dingen die half af zijn, tellen niet mee voor de capaciteit. - Nee, ook niet voor de helft van de punten. Dingen die driekwart af zijn of voor negentig procent af zijn ook niet. - En dus ook niet voor driekwart of negentig procent van de punten. 


Shore is hier streng in. Ook [Product Backlog Items](https://www.scrum.org/resources/what-is-a-product-backlog) (PBI's) die alle fasen van de ontwikkeling hebben doorstaan, maar nog niet zijn uitgerold naar de Productie-omgeving, tellen niet mee: voor niks nada nul-komma-noppes - aangenomen dat "uitrollen naar Productie" op je DoD staat, natuurlijk.[^3]


## Wat niet te doen


Stel nu dat je de ene Sprint PBI's ter waarde van twintig punten naar *done done* hebt geloodst, en de volgende Sprint vijftien, dan - heel simpel - wordt de capaciteit vijftien. 


Nu kan het heel goed zijn dat je de komende Sprint alle vijftien punten hebt verbrandt vóór het eind van de Sprint. Wat doe je dan? 


Ik zal je zeggen wat wij als team deden: we sleepten doodleuk de volgende PBI's de Sprint op en we keken wel hoe ver we daar mee kwamen. Als we ze af kregen, dan konden we de stakeholders een verrassinkje bieden, en als dat niet lukte, dan hadden we alvast een beginnetje gemaakt met de volgende Sprint. Slim toch?


## Verbeteren


Nou, zo moet het dus niet! Maar waarom niet? Is het niet zonde om de capaciteit die je over hebt niet te besteden aan het bouwen van de volgende feature?


Nee. De capaciteit die je over hebt gebruik je om je applicatie op te schonen. Verbeter het design daar waar nodig is. Splits die onhandig grote [class](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/classes) die je met de vorige feature hebt gecreëerd in tweeën, voeg wat [tests](/tags/testen/) toe daar waar ze ontbreken. Richt je nog niet op het volgende project, de volgende feature. Richt je op het verbeteren van wat er nu al is.


Niet alle stakeholders - zelfs niet alle PO's - zullen je die houding in eerste instantie in dank afnemen. In hun beleving is een applicatie een verzamelbak van features, en elk moment dat de inhoud van die bak niet wordt uitgebreid, is verloren tijd.


Maar jij als ontwikkelaar weet beter - toch? Daarom gebruik je de speelruimte die je hebt gecreëerd met je (toegegeven, misschien wel enigszins conservatieve) inschatting om te werken aan de dingen die belangrijk zijn om de applicatie onderhoudbaar te houden. Des te makkelijker maak je het jezelf om de volgende Sprint weer nieuwe functionaliteit te implementeren.


En die rigide stakeholder van je? Die heeft niets te klagen, want je levert precies op wat je tijdens de Sprint Planning zei te doen. Het mooie is: hij of zij hoeft geeneens te weten dat jij de afgelopen Sprint hebt besteedt aan iets wat in zijn ogen onbelangrijk is. (Mocht je stakeholder wel oog hebben voor de productkwaliteit van je applicatie, dan mag je het natuurlijk altijd delen.)


## De volgende Sprint


Dus: je plant de hoeveelheid werk in waarvan je zeker weet dat je het af kan krijgen - en je gebruikt de speelruimte die daarbij ontstaat om de onderhoudbaarheid van je applicatie te verbeteren. En nu?


De volgende Sprint plan je weer op een capaciteit van vijftien. Misschien ben je weer ruim op tijd klaar, maar misschien ook niet. Zo niet, mooi: dan was vijftien een getrouwe inschatting. Zo ja, mooi: dan heb je opnieuw wat extra speelruimte om je applicatie nog wat verder op te schonen.


Als je dit lang genoeg doet, dan is je applicatie zo goed onderhouden, dat het team eraan kan gaan denken wat meer hooi op zijn vork te nemen, de volgende Sprint. Je zet de capaciteit op, zeg, achttien. Haal je dat? Prima! Volgende keer gewoon op die koers van achttien doorgaan dus! En haal je dat niet? Geen probleem: verlaag dan opnieuw de capaciteit naar het aantal punten dat je helemaal af hebt weten te maken.


## Inzicht


Het inzicht in deze manier van werken, is dat software ontwikkelen er niet over gaat om zo snel mogelijk zoveel mogelijk features op te leveren. Het gaat erom op een *duurzame en betrouwbare* manier features op te leveren.


Als je team elke Sprint vijftien punten verbrandt, dan weten stakeholders precies wat ze aan je hebben. Als je de ene keer vijftien punten verbrandt, dan twintig en dan achttien, dan moeten ze er maar op hopen dat hun feature de volgende Sprint overleeft.


Speelruimte geeft je twee dingen. Het eerste is betrouwbaarheid naar de mensen buiten je team toe. En als gevolg daarvan zul je ook vertrouwen ontvangen. Het tweede is de mogelijkheid te verbeteren en te experimenteren. Wie zichzelf speelruimte gunt, zet zichzelf op een pad te groeien, in plaats van op te branden.


[^1]: Sommige teams verbranden tien punten per Sprint, andere teams zestig. Anders dan sommige managers wel eens willen geloven, zegt dat niets over hoe hard die teams werken. Het zegt alleen iets over de manier waarop de teams hun PBI's inschatten. De getallen zijn relatief - en wat de teams als referentie nemen voor één punt is willekeurig.


[^2]: Scrum spreek van "*velocity*", maar die metafoor is misleidend. De snelheid van een voertuig kun je eenvoudig opschroeven door meer gas te geven. Maar het is niet zo dat een team harder kan gaan door "gewoon" harder z'n best te doen.


[^3]: Sommige teams zijn afhankelijk van derden om uit te kunnen rollen naar Productie. Voor hen geldt het eenvoudige advies: neem dat niet op in je DoD. In de DoD moeten alleen zaken staan waar het team verantwoordelijkheid voor kan nemen.
