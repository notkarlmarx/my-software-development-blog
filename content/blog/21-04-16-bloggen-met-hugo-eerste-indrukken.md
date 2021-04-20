---
title: "Bloggen Met Hugo: Eerste Indrukken"
date: 2021-04-16T10:44:36+02:00
draft: false
comments: true
tags: ["bloggen", "dotkarl", "gatsby", "hugo", "leermoment", "static site generator"]
---

Soms is het goed om je af te vragen hoe je hier gekomen bent.


## Waarom ik blog


Het korte antwoord: omdat [Scott Hanselman](https://www.hanselman.com/) me ervan overtuigde dat het een goed idee zou zijn. 


En het lange antwoord? Ik zou zijn woorden kunnen parafraseren, maar hij bracht het zelf beter dan ik zou kunnen doen in zijn toespraak aan een nieuwe lichting [Microsoft Learn Student Ambassadors](https://studentambassadors.microsoft.com/):
{{< youtube 8HE5LJwAv1k >}}


(De video duurt een ruime drie kwartier, dus kan met recht een lang antwoord genoemd worden. Maar het is de tijd meer dan waard, geloof me.)


## Static Site Generators


Het was ook dankzij zijn video dat ik op het idee kwam om te bloggen middels een [Static Site Generator](https://jamstack.org/glossary/ssg/) (SSG). 


Het idee van zo'n Generator klonk interessant, en niet alleen omdat het me een kans bood een nieuwe techniek uit te proberen. 


Het starten van een blog moet laagdrempelig zijn. Je begint er niet aan als je eerst een hele tijd bezig bent om een drielagenmodel aan de back-end op te zetten, inclusief database. En dan heb ik het nog niet over de Angular- of React- of Vue-applicatie aan de front-end. Trouwens, ik was er ook vrij zeker van dat ik al die overhead niet nodig zou hebben. 


## Vallen en opstaan


De vraag die zich dan opwerpt, is: welke SSG? Wie zoekt naar een overzicht van de verschillende alternatieven, komt erachter dat er [nogal wat Generators](https://jamstack.org/generators/) zijn. Waarom ik koos voor [Hugo](https://gohugo.io/)? Het korte antwoord: omdat ik er niet uit kwam met [Gatsby](https://www.gatsbyjs.com/).


Gatsby was mijn eerste keuze, omdat dat framework me in staat stelde om met HTML en JavaScript te werken. Het leek me verstandig om de leercurve van zo'n nieuwe techniek te verzachten met wat bekende elementen. 


Maar de proxy van mijn laptop kreeg ruzie met de Node Package Manager (NPM), en na een uur Googlen op NPM-issues besloot ik dat het de moeite niet waard was.


Destijds ervoer ik dat als een nederlaag. Maar daar ben ik van teruggekomen. Zoals ik al zei: het opzetten van een blog moet laagdrempelig zijn. En in plaats van een blog te beginnen en Gatsby onder de knie te krijgen, was ik een hoop tijd kwijt aan worstelen met NPM. 


Bovendien, het doel dat ik mezelf gesteld had, was niet: werken met Gatsby. Het doel was een blog beginnen met een SSG, en de problemen waar ik tegenaan liep, verhinderden me dat doel te bereiken.


## Waarom Hugo?


Soms gaat het zo in het leven: je moet genoegen nemen met je tweede keuze. Hugo, dus. 


Ik had gehoord dat Hugo de eenvoudigste SSG was. Je kunt je voorstellen dat dat me na mijn eerste poging goed in de oren klonk. En volgens zijn [website](https://gohugo.io/) is Hugo ook de snelste. 


Maar Hugo werkt met [Go](https://golang.org/), en dat is de reden waarom hij niet mijn eerste keus was. Op voorhand vreesde ik dat ik Go als programmeertaal zou moeten beheersen om met Hugo te kunnen werken. 


Wat deed me deze vrees overwinnen? Misschien dat het feit dat mijn beheersing van JavaScript me geen steek verder had gebracht bij het opzetten van een Gatsby-project. Redelijk is dit natuurlijk niet. Voor hetzelfde geld zou ik bij Hugo tegen soortgelijke problemen aanlopen en deze *daarnaast* moeten overwinnen in een taal die ik niet ken. 


Och, wie niet waagt, wie niet wint.


## *Getting started*


Voor het maken van deze blog heb ik Hugo's eigen [*quick start*](https://gohugo.io/getting-started/quick-start/) als uitgangspunt genomen. Verder heb ik me voornamelijk op deze [uitstekende *how to* van Aaron Katz](https://www.freecodecamp.org/news/how-to-build-a-blog-using-a-static-site-generator-and-a-cdn/) gebaseerd. Dat stelde me in staat om het gros van deze website in een middagje in elkaar te zetten. 


Een criticaster zou op kunnen merken dat ik me daarbij van mijn makkelijkste kant heb betoond. Ik heb bijvoorbeeld niet de moeite genomen om een ander thema te gebruiken dan Katz in zijn blog voorstelde. Dat zou je luiheid kunnen noemen - en dat is het deels misschien ook wel. 


Maar het is voor een groot deel ook zelfbescherming. Als ontwikkelaar is het verleidelijk om jezelf meteen te verliezen in alle kleine details van een nieuwe techniek. In een persoonlijk projectje is dat nog niet zo erg, maar het is belangrijk om het doel van je project - persoonlijk of professioneel - voor ogen te houden. Dat doel was in dit geval: een blog opzetten met een SSG. Een meer eigen look en feel, dat komt straks wel.


Trouwens, ik vind het [*tale*-thema](https://github.com/EmielH/tale-hugo) op zijn minimalistische manier best mooi. En het had *out of the box* support voor het toevoegen van een pagina met tags, dus mijn luiheid betaalde zich onmiddellijk terug.


Ook het toevoegen van comments was dankzij deze [blog van Peter Baumgartner](https://portfolio.peter-baumgartner.net/2017/09/10/how-to-install-disqus-on-hugo/) een eitje. 


Het is belangrijk om te beseffen dat ik voor vrijwel alle acties om de website draaiende te krijgen, nauwelijks iets met Go heb hoeven doen. Mijn vrees was dus ongegrond. Natuurlijk is dat op dit moment nog het gevolg van de eenvoud van mijn blog. Of Go een bottleneck zal blijken te zijn bij het verder ontwikkelen van de website, zal in de toekomst moeten blijken.


## Lessen


Mijn eerste ervaringen met Hugo zijn positief. *[Hier een grap over onze minister van volksgezondheid en/of coronatests - red.]* Maar belangrijker dan werken met Hugo in het bijzonder of Static Site Generators in het algemeen, vind ik deze lessen:


- **Wees niet bang om technieken uit te proberen waar je geen ervaring mee hebt.** Misschien valt het allemaal wel mee! Zoals gezegd is werken met Hugo betrekkelijk eenvoudig. Daar waar ik Go nodig had, volstond een eenvoudige Google-search om het antwoord te vinden.


- **Begin eenvoudig.** Schuif de meer geavanceerde features vooruit. (En "geavanceerd" betekent niet: ingewikkeld. Het aanpassen van tekstkleur is geavanceerd ten opzichte van het überhaupt hebben van tekst.) Het is belangrijker een werkende app te hebben dan een app die helemaal naar je wens is. Als je op iets stuit wat je later anders of beter wil doen, zet dit dan op je backlog. Deze feature kun je later oppakken en aftikken.


- **Hou je doel voor ogen.** Is het doel: werken met deze techniek? Nee? Probeer dan een andere techniek. Wees niet bang om te schrappen - en hoe eerder, hoe liever. Want hoe minder tijd je hebt besteed aan een oplossing voor een probleem, hoe meer je aan die oplossing gehecht raakt. Je had in dat uur waarin je NPM-issues Googlede ook een werkende Hugo-blog de lucht in kunnen slingeren - waarvan akte.
