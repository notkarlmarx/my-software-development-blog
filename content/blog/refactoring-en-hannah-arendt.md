---
title: "Refactoring en Hannah Arendt"
author: "Karl van Heijster"
date: 2024-07-20T13:25:20+02:00
draft: true
comments: true
tags: ["clean code", "filosofie", "refactoren", "software ontwikkelaar (rol)", "technische schuld", "zorg"]
summary: "Yvonne Lam stelt dat er een betere metafoor voorhanden is voor dat wat we gewoonlijk \"technische schuld\" noemen: huishouding (*housework*). Het deed me aan Hannah Arendt denken. -- Beroepsdeformatie, denk ik!"
---

Uit een [praatje](https://www.youtube.com/watch?v=Q91d59tW75s "'Kevlin Henney - Refactoring Is Not Just Clickbait - Joy of Coding 2024', YouTube") van [Kevlin Henney](http://kevlin.tel/)[^1] leen ik de volgende tweet -- die dan weer van [Yvonne Lam](https://x.com/yvonnezlam "@yvonnezlam, X") is:


{{< twitter user="yvonnezlam" id="1376628481878990852" >}}


Lam stelt dat er een betere metafoor voorhanden is voor dat wat we gewoonlijk "[technische schuld](/tags/technische-schuld/ "Blogs met de tag 'technische schuld'")" noemen: huishouding (*housework*).[^2] 


(Haar tweet heeft een scherp randje, ze stelt dat we met de mindere metafoor opgescheept zitten omdat de sector vol zit met mensen die zich niet bekommeren om het huishouden (mannen?). Het is een grappige illustratie van hoe onze (gegenderde) ervaringen ons wereldbeeld bepalen.[^3])


Het deed me aan [Hannah Arendt](https://plato.stanford.edu/entries/arendt/ "'Hannah Arendt', Stanford Encyclopedia of Philosophy") denken. ([Beroepsdeformatie](/tags/beroepsdeformatie/ "Blogs met de tag 'beroepsdeformatie'"), denk ik!)


## De menselijke conditie


In [*The Human Condition*](https://en.wikipedia.org/wiki/The_Human_Condition "'The Human Condition', Wikipedia") onderscheidt de filosofe [fenomenologisch](https://plato.stanford.edu/entries/phenomenology/ "'Phenomenology', Stanford Encyclopedia of Philosophy") drie fundamentele activiteiten van het menselijk zijn[^4] -- arbeid (*labor*), werk (*work*) en actie (*action*). 


Arbeid is geassocieerd met het *animal laborans*, werk met *homo faber*, actie met *homo sapiens*; arbeid is circulair, werk is lineair, actie: initiatie. Arbeid keert steeds opnieuw terug, werk doen we richting een doel, actie is het in gang zetten van iets nieuws. (-- Maar natuurlijk doet deze schets geen recht aan de diepgang van haar analyse. In het vervolg van deze blog zal ik me op de eerste twee activiteiten richten.)


Wat heeft dit met Lams tweet te maken? De metafoor die we gebruiken wanneer we technische schuld "afbetalen" is een fundamenteel andere metafoor dan die van doen van je huishouden -- koken, wassen, schoonmaken (uitgaan, de financiën op orde houden); [zorgen](/tags/zorg/ "Blogs met de tag 'zorg'"). 


Het afbetalen van een schuld is een doelgerichte activiteit met een begin- en eindpunt, een onderneming van *homo faber*. Huishouden is een steeds terugkerende activiteit, vandaar de circulariteit; de last van *animal laborans*. De eerste is werk, de tweede arbeid.[^5]


## (Verheldering)


(Mijn vrouw vraagt: maar als ik de vloer dweil, dan werk ik toch ook richting een doel, namelijk een schone vloer? En ze heeft een punt. Als we de taak op zichzelf en inhoudelijk bekijken, is dweilen een vorm van werk. Maar bezien vanuit de stroom van het leven -- de zoveelste keer dat we (moeten!) dweilen -- is het arbeid. 


Je zou kunnen zeggen dat het arbeid of werk is naargelang de houding die we aannemen tot de activiteit. -- Maar dat klinkt te intellectualistisch, alsof we de keuze maken het zus of zo te zien. Misschien is het beter om zo te stellen: arbeid of werk, dat is onze *ver*houding tot deze of gene activiteit.)


## Afbetalen...


En het verklaart ook iets -- misschien. Misschien verklaart het waarom zoveel softwareteams technische schuld op laten bouwen -- tot het boven hun hoofd groeit en ze hun managers bekennen: "We kunnen pas verder wanneer we de code fiks onder handen hebben genomen." -- "Hoe lang gaat dat duren?" -- "Drie maanden tot een halfjaar."


Zulke teams zien technische schuld als iets dat zich opbouwt in de loop der tijd. Wanneer er een bepaalde grens is bereikt, wordt de schuld problematisch en dient deze vermindert te worden (maar precies groot genoeg om hakkelend verder te kunnen!). Er wordt een doel gesteld: binnen zus en zoveel tijd willen we de code in deze of gene doeltoestand brengen. En vanaf dat moment is het een kwestie van het bereiken van dat doel -- binnen drie tot zes maanden.


## ...of huishouden?


Zou iets dergelijks ook een team kunnen overkomen dat "het wegwerken van technische schuld" als een huishoudelijke activiteit ziet -- als stofzuigen, de afwas uitruimen, de wasmachien inruimen? Laat ik het zo zeggen: een huishoud(st)er die de stofzuiger pas tevoorschijn haalt wanneer de stofnesten zich opstapelen, is geen ster in het huishouden.


De wijsheid van arbeid is: doe het nu, dan hoef je het morgen niet te doen. Want of je het nu vandaag of morgen doet, de afwas moet worden gedaan -- en die duplicate code geabstraheerd naar een eigen class --, en morgen is het alleen maar vervelender. In een circulaire tijdsopvatting is het *nu* doorslaggevend. (Werk wijst daarentegen richting de toekomst.)


## (Over *Clean Code*)


([Robert Martins]((https://en.wikipedia.org/wiki/Robert_C._Martin)) [*clean code*](/tags/clean-code/ "Blogs met de tag 'clean code'")-metafoor is wellicht daarom zo treffend. [Zijn boek](https://www.pearson.com/us/higher-education/program/Martin-Clean-Code-A-Handbook-of-Agile-Software-Craftsmanship/PGM63937.html) ([mijn favoriete boek over softwareontwikkeling in 2020](/blog/21/05/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2020-las/ "'De beste boeken over software ontwikkeling die ik in 2020 las'")) is een handwerk in het schoonmaken en schoon houden van code.


[David Whitney](https://davidwhitney.co.uk/) bekritiseert *Clean Code* (in [dit praatje](https://www.youtube.com/watch?v=vw2XffPmlYo "'Intentional Code - Minimalism in a World of Dogmatic Design - David Whitney - NDC London 2023', YouTube")) omdat het vraagstukken over het ontwerp van code heeft gereduceerd tot de vraag welke namen we variabelen we moeten geven. Misschien is dit inderdaad hoe Martins werk is ontvangen -- maar het zou kunnen dat de fout dan bij die ontvangst ligt. 


Is *Clean Code* een boek over het ontwerpen van software, of het onderhouden ervan? In geval van het laatste, is het alsof Whitney afgeeft op een boek over schoonmaken omdat het je niet leert je huis in te richten.)


## Refactoren


Goede ontwikkelteams houden hun code continu op orde. Als ze nieuw gedrag toevoegen, dan passen ze de structuur van de code aan zodat dat gedrag er goed in past; ze construeren geen bouwwerken op een wanordelijk fundament. [Refactoren](/tags/refactoren/ "Blogs met de tag 'refactoren'") -- zorgdragen voor de structuur van de code, zonder het gedrag te wijzigen; code schoon houden, "opruimen" -- is arbeid. Het is, net als schoonmaken, een steeds terugkerende activiteit, zonder definitief einddoel. 


Worstelende ontwikkelteams laten hun code verslonzen. Ze bouwen nieuw gedrag bovenop bestaand gedrag, en de naden van hun werk zijn zichtbaar. (Zie ook [deze blog](REFACTORING_ALS_COMMUNICATIEMIDDEL).) Refactoren doen ze nauwelijks -- alleen wanneer hun stakeholders hen toestemming geven de enorme rommel op te ruimen die de ontwikkelaars zelf gecreëerd hebben. 


## Fenomenologie


Maar neem het ze eens kwalijk: het ligt niet in de lijn van de ervaring continu zorg te dragen voor het afbetalen van je schuld (tenzij je schulden je boven het hoofd zijn gegroeid, natuurlijk). Mijn hypotheek wordt elke maand automatisch van mijn rekening afgeschreven; ik ben niet de helft van die dertig dagen kwijt aan het zorgvuldig vullen van een spaarpot, om 'm aan het eind in één klap te zien verdampen. 


Inderdaad laat de metafoor van technische schuld zich moeilijk rijmen met deze fenomenologie van code onderhouden. Het aanzien van arbeid voor werk heeft de relaties van veel teams tot hun eigen codebase verstoord.[^6] Hadden ze maar Hannah Arendt gelezen, dan was het wellicht nooit zo ver gekomen!


[^1]: Ik zat op de eerste rij! En ook [dit praatje](https://www.youtube.com/watch?v=GJsu9LIzfc0 "'Yulia Startsev - To loosen up, to put together -Joy of Coding 2024', YouTube") van [Yulia Startsev](https://www.yuliastartsev.com/) maakte ik van dichtbij mee -- eveneens een aanrader!

[^2]: Het oorspronkelijk woord is moeilijk met tevredenheid te vertalen. "Huiswerk" doet teveel aan school denken; "huishoudelijke klusjes" legt te zeer nadruk op de concrete taken waarin het concept zich manifesteert in de werkelijkheid. (Ik zou van beroep een waardeloze vertaler zijn.) 

[^3]: Cf. "de grenzen van mijn taal zijn de grenzen van mijn wereld", [Wittgensteins](https://plato.stanford.edu/entries/wittgenstein/ "'Ludwig Wittgenstein', Stanford Encyclopedia of Philosophy") [*Tractatus*](https://en.wikipedia.org/wiki/Tractatus_Logico-Philosophicus "'Tractatus Logico-Philosophicus', Wikipedia"); misschien ook: "*form of life*", uit zijn [*Philosophical Investigations*](https://en.wikipedia.org/wiki/Philosophical_Investigations "'Philosophical Investigations', Wikipedia"). (Zie ook [deze](/blog/21/08/domain-driven-design-en-ludwig-wittgenstein/ "'Domain-Driven Design en Ludwig Wittgenstein'"), [deze](/blog/23/09/pseudofilosofische-onderzoekingen-i-en-ii/ "'Pseudofilosofische onderzoekingen (I & II)'") [deze blog](/blog/23/12/logisch-filosofische-verhandeling/ "'Logisch-filosofische verhandeling'"))

[^4]: "*Being-in-the-world*" wordt het in [haar lemma](https://plato.stanford.edu/entries/arendt/#HumaCond "'4.2 The Vita Activa: Labor, Work and Action' in 'Hannah Arendt', Stanford Encyclopedia of Philosophy") van de [*Stanford Encyclopedia of Philosophy*](https://plato.stanford.edu/index.html) genoemd. Het is verleidelijk het als "[erzijn](https://en.wikipedia.org/wiki/Dasein "'Dasein', Wikipedia")" (*Dasein*) te vertalen, maar daarmee presenteren we Arendt ongewild als leerlinge van [Heidegger](https://plato.stanford.edu/entries/heidegger/ "'Martin Heidegger', Stanford Encyclopedia of Philosophy") -- wat niet onwaar is, maar haar denken geen recht doet. In het eerste hoofdstuk van het boek noemt ze het "*ways of life*" (of "*bioi*"; het Grieks ontleent ze aan [Aristoteles](https://plato.stanford.edu/entries/aristotle/ "'Aristotle', Stanford Encyclopedia of Philosophy")) -- en dat doet dan weer aan Wittgenstein denken.[^3] 

[^5]: De term "*housework*" komt niet voor in *The Human Condition*. Maar Arendt bespreekt op verschillende momenten wel het huishouden (*household*), met name in contrast met het openbare leven in de Griekse *polis*. 

[^6]: Een echo uit [Kent Becks](https://www.kentbeck.com/) [*Tidy First?*](https://www.oreilly.com/library/view/tidy-first/9781098151232/ "Kent Beck, 'Tidy First?: A Personal Exercise in Empirical Software Design', O'Reilly Media, 2023"); zie ook [deze blog](/blog/24/07/grote-refactorslagen-ondermijnen-vertrouwen/ "'Grote refactorslagen ondermijnen vertrouwen'").
