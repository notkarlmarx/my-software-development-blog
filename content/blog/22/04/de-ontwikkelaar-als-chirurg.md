---
title: "De ontwikkelaar als chirurg"
author: "Karl van Heijster"
date: 2022-04-25T07:38:38+02:00
draft: false
comments: true
tags: ["boeken", "clean code", "leermoment", "legacy code", "recensies", "refactoren", "schoonheid", "technische schuld", "testen"]
summary: "*Working Effectively with Legacy Code* van Michael Feathers staat vol met adviezen waar je cleancodershart een slag van overslaat. Vrijelijk raadt Feathers je aan encapsulatie uit het raam te smijten of onhandelbare methods zomaar tot class te promoveren. Zijn inzichten gaan lijnrecht in tegen alle richtlijnen om goede, onderhoudbare code te schrijven. Het boek is zonder twijfel een aanrader voor elke softwareontwikkelaar."
---

[*Working Effectively with Legacy Code*](https://www.pearson.com/us/higher-education/program/Feathers-Working-Effectively-with-Legacy-Code/PGM254740.html) van [Michael Feathers](https://michaelfeathers.silvrback.com/) staat vol met adviezen waar je cleancodershart een slag van overslaat. Vrijelijk raadt Feathers je aan encapsulatie uit het raam te smijten of onhandelbare methods zomaar tot class te promoveren. Zijn inzichten gaan lijnrecht in tegen alle richtlijnen om goede, onderhoudbare code te schrijven.


Het boek is zonder twijfel een aanrader voor elke softwareontwikkelaar.


## Realiteit


Want anders dan de meeste boeken over het ontwerpen, implementeren en ontwikkelen van software, gaat *Working Effectively with Legacy Code* niet uit van ideale condities. Feathers staat met beide benen enkeldiep in de modderige realiteit van *brownfield*-projecten. Hij beseft zich ten volle dat de meeste code waar je als ontwikkelaar mee zal werken, je ook maar in de schoot is geworpen en aan geen enkele kwaliteitsstandaard voldoet. Dat is waar je het mee zult moeten doen - en daar kun je over klagen (en dat werkt vaak heel louterend), maar het is zinvoller om te proberen die situatie ten goede keren.


Hoe je dat voor elkaar krijgt? Door automatische tests te schrijven. Sterker nog, Feathers definieert *legacy code* zelfs als code die niet door automatische tests gedekt wordt. 


Ik hoor je al roepen: maar *legacy code* is vaak notoir moeilijk om te testen! Dat klopt. Zulke code is meestal op zo'n manier opgezet dat het schrijven van tests nagenoeg onmogelijk is gemaakt. - En dat is dus precies waarom je van tijd tot tijd encapsulatie moet breken, of onhandelbare methods zonder vooropgezet ontwerp maar naar hun eigen class moet loodsen.


## Testbaarheid vs. schoonheid


Feathers adviezen dienen een heel specifiek doel: je code testbaar zien te maken. En hij is er heel duidelijk over: dat betekent niet dat je de code mooier maakt. Integendeel, vaak maak je haar zelfs nog een stukje lelijker dan ze al was. Je denkt aanvankelijk misschien nog: lelijker dan dit kan niet - maar nadat je de tests hebt geschreven moet je concluderen: o nee, toch wel.


Dat klinkt alsof je een erge situatie verergert, en dat is in zekere zin ook zo. Maar in zekere zin ook niet, want die lelijke code is nu tenminste wel getest. En dat betekent dat je eraan kan gaan lopen pielen. Je kunt methods extraheren, variabelen introduceren of verwijderen, logica versimpelen. En je kunt vervolgens met één druk op de knop nagaan of je het oorspronkelijke gedrag daarmee veranderd hebt of niet.


Feathers vergelijkt het werk van een met *legacy code* worstelende softwareontwikkelaar met dat van een chirurg. De patiënt is er slecht aan toe - en daarom gaan we 'm open snijden. Natuurlijk, het opensnijden op zichzelf zal z'n situatie niet verbeteren, integendeel. Maar het stelt de chirurg nu wel in staat om bij de oorzaak van het probleem te komen. Pas nadat de situatie is verslechterd, hebben we de mogelijkheden tot onze beschikking om 'm te verbeteren.


## Vuile handen


Dat is een belangrijk en allesbehalve triviaal inzicht. Ik betrap mezelf er regelmatig op wel te willen refactoren, maar daar niet aan te kunnen beginnen door een gebrek aan tests. Als ik vervolgens die tests ga schrijven, merk ik al gauw dat ik een toch al onhandelbare class soms zodanig moet verminken, dat ik ervoor terugdeins om de klus door te zetten. Wat ervoor nodig is om de code goed en wel onder handen te kunnen nemen, schendt zóveel ontwerpprincipes dat ik er mijn naam liever niet mee wil associëren.


Het lezen van Feathers' boek heeft me wat minder terughoudend gemaakt in deze onderneming. Dat is deels omdat het boek vol staat met manieren om code, al dan niet met pijn en moeite, in een testharnas te hijsen. Feathers' tips en trucs zouden standaard in de gereedschapskist van elke goede softwareontwikkelaar moeten zitten. Maar het grootste gedeelte van het vertrouwen komt voort uit het besef dat je je handen - en je code! - vuil, écht vuil moet maken, om 'm op te kunnen schonen.


Men zegt niet voor niks: wie mooi wil zijn, moet pijn lijden - en wie mooie code wil hebben, zal zijn applicatie van tijd tot tijd voor zijn eigen bestwil op de pijnbank moeten leggen. Snijden maar!
