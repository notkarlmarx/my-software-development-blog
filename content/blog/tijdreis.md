---
title: "Tijdreis"
author: "Karl van Heijster"
date: 2023-03-10T07:43:42+01:00
draft: true
comments: true
tags: ["documentatie", "druk", "leermoment", "procesverbetering", "professionaliteit", "requirements", "samenwerking", "shift left", "software ontwikkelen", "technische schuld", "test-driven development", "testen"]
summary: "Ik vroeg mijn collega's: \"Wat doet dit ding precies?\" - waarop ze prompt de code tevoorschijn haalden en me stap voor stap door het importproces loodsten. Het was alsof ik terug werd geslingerd naar het begin van mijn ontwikkelcarrière, toen we met z'n allen een twaalf jaar oude *legacy* applicatie onderhielden die alleen te doorgronden was door nauwgezet de code te doorlopen. Wat blijkt: tijdreizen bestaat - je hoeft alleen maar bij een ander team te buurten."
---

Het was een frustrerende Sprint - voor mij net zozeer als voor mijn collega's, stel ik me zo voor.


## Enthousiasteling


Mensen die mij een beetje kennen, weten dat [ik houd van tests](/tags/testen/). Geautomatiseerde tests zijn wat mij betreft zowaar belangrijker dan de geteste code. Immers, als ik een goede testsuite heb - [leesbare tests](/blog/23/02/waarom-dry-waarom-damp/) [met de juiste scope](/blog/22/11/test-het-systeem-niet-de-class/) -, dan kan ik die geteste code vrijelijk refactoren, aanpassen en uitbreiden. Wat ik ook doe, zolang ik de vinkjes groen houd, weet ik dat ik op de juiste weg zit. 


Ik mag mezelf graag een *testenthousiasteling* noemen.


Mijn collega's hebben daar andere woorden voor. Zij noemen me dingen als *testmaniak*. Of *testnazi*.


Of *testikel*.


Maar dat was maar één keer.


## Import


Wat ik bedoel te zeggen is: als ik in een team terechtkom dat minder waarde hecht aan testen dan ik, dan geeft dat schuring. En dat is precies wat er onlangs gebeurde, toen ik mijn werk in het ene featureteam inruilde om een stel collega's te ondersteunen bij de bouw van een importfunctionaliteit.


Ik heb de afgelopen jaren hard mijn best gedaan om tests en [Test-Driven Development](/blog/22/03/agile-en-test-driven-development/) (TDD) te promoten in mijn omgeving, dus mijn mond viel open van verbazing toen ik de importcode bekeek. Of liever: toen ik het [testproject doorzocht op documentatie](/blog/22/09/tests-als-documentatie/) van die importcode - en nul op mijn rekest kreeg. 


Ik vroeg mijn collega's: "Wat doet dit ding precies?" - waarop ze prompt de code tevoorschijn haalden en me stap voor stap door het importproces loodsten.


Het was alsof ik terug werd geslingerd naar het begin van mijn ontwikkelcarrière, toen we met z'n allen een twaalf jaar oude *legacy* applicatie onderhielden die alleen te doorgronden was door nauwgezet de code te doorlopen. Wat blijkt: tijdreizen bestaat - je hoeft alleen maar bij een ander team te buurten.


Hoewel de importer nog geen maand oud was, zat 'ie al vol met technische schuld. Er waren interfaces met methods die niet gebruikt werden. Verantwoordelijkheden waren maar vaag gedefinieerd. (Vraag: "Wat doet de `MediaImportHandler`?" Antwoord: "De media-import afhandelen.") Op het moment dat ik aanhaakte, was de centrale architect achter de importer bezig een cyclische afhankelijk uit de code te refactoren. Zonder [tests als vangnet](/blog/22/09/tests-als-vangnet/).


...*uiteraard*, zou ik er haast aan toe willen voegen. Maar dan neemt mijn cynisme de overhand, dus dat doe ik niet.


## Ergernis


Ik zal de eerste zijn die toegeeft dat ik er misschien niet helemaal adequaat op reageerde. Want mijn reactie was: *W-w-wablief? Maar h-h... godverdegodverdegodverde... - HOE DAN?!*


Daarna declameerde ik plechtig dat ik elke wijziging aan de code zou blokkeren die niet werd gedekt door tests. Normaal gesproken zou ik dat met een brede glimlach doen. Deze keer ging het met een ondertoon van nauwelijks bedwongen ergernis.


Hoewel, het was eigenlijk verbazing - verbazing verpakt in frustratie. Na een jaar lang te hebben ge-TDD't, kon ik me het gewoon niet meer voorstellen dat er ook ontwikkelaars op de wereld zijn die (nog?) niet de zegeningen van tests eigenhandig hebben ervaren. Achteraf bezien had ik wat minder mogen vloeken en wat meer empathie mogen tonen naar mijn teamgenoten - daar ben ik me nu bewust van.


Want begrijp me niet verkeerd, het is niet zo dat mijn collega's tests totaal onbelangrijk vinden. Als ik hen er naar vraag, dan geven ze allemaal aan dat tests een belangrijk onderdeel zijn van softwareontwikkeling. 


## Handelen


Helaas handelen ze daar niet altijd naar - niet onder bepaalde omstandigheden. 


Bijvoorbeeld als de druk wordt opgevoerd vanuit de business. De importer had een deadline - een strakke deadline, zelfs. Het hele geval moest binnen anderhalve maand af zijn. Er moest dus code worden geschreven - en snel! Wie onvoldoende doordrongen is van de waarde van tests, is dan snel geneigd om deze te laten vallen. Immers, tests voegen geen nieuwe functionaliteit toe - en dat is een luxe die we ons niet kunnen veroorloven als er nog zoveel op de planning staat!


Maar het idee dat tests je afremmen in het ontwikkelen van het systeem, is gebaseerd op een misvatting. Natuurlijk, zolang je tests schrijft, voeg je geen nieuwe functionaliteit toe. Maar dat doe je ook niet als de tester een bug in je code vindt, en je die moet gaan fixen. En hoe minder tests je hebt, des te groter de kans dat de tester bugs zal vinden. Uiteindelijk zul je dus langer bezig zijn met een feature zonder tests dan met tests.


Een gevoel van opgejaagdheid is denk ik één van de grootste redenen waarom ontwikkelaars het testen laten schieten. Maar ze houden zichzelf daarmee voor de gek. Wie zegt: "Ik heb een deadline, ik heb geen tijd voor tests!" zegt eigenlijk: "Deze functionaliteit is zó belangrijk dat het niet uitmaakt of de code klopt of niet." 


Maar als het niet uitmaakt of je code klopt of niet, hoe kan die functionaliteit dan ooit belangrijk zijn?


## Ontwerpmiddel


Aan het eind van de Sprint vroeg ik twee ontwikkelaars gewoonweg waarom ze verzuimd hadden tests te schrijven. Grappig genoeg noemden ze tijdsdruk allebei niet als argument.


De eerste zei: "Ik had toen ik begon met het opzetten van de importer nog geen idee hoe ik het precies aan wilde pakken, dus ik kon er nog geen test voor schrijven." Een ironisch antwoord, omdat TDD je nu juist *helpt* bij het uitdenken van hoe je je code wil aanpakken. 


[Tests zijn een ontwerpmiddel.](/blog/22/09/tests-als-ontwerpmiddel/) Het eerste wat je doet bij het schrijven van een test is definiëren welke output je verwacht bij een bepaalde input. Het is een manier om vast te leggen: dit is wat ik wil dat de code doet. Hoe je code het uiteindelijk voor elkaar krijgt om de in- en outputs aan elkaar te koppelen, dat is van later zorg. 


Het had hem kunnen helpen om verantwoordelijkheden te definiëren en complexe methods te kunnen versimpelen. Bijzonder verwarrend vond ik bijvooreeld een centrale method die een `Result`-object teruggaf waar de aanroependende kant niet in geïnteresseerd was. Waar het die om ging, was om een input-parameter die ergens op driekwart van de method in bepaalde condities aangepast werd. 


Als mijn collega eerst de test had geschreven, had hij die method ongetwijfeld anders gedefinieerd. Hij had het `Result`-object gelaten voor wat het was, en in plaats daarvan de method de relevante informatie laten retourneren.


## Vastleggen


De tweede ontwikkelaar zei: "De requirements waren zo vaag dat het geen zin had om daar tests voor te schrijven." Hij bedoelde: we hadden wel tests *kunnen* schrijven, maar die hadden we toch weer om moeten gooien, dus dat zou verspilde moeite zijn geweest.


Geen tests schrijven is natuurlijk geen oplossing voor vage requirements. De requirements scherper in kaart brengen is een oplossing voor vage requirements.


En ook hier kunnen tests juist helpen. In principe zou je na elke test - [op het juiste niveau gedefinieerd](/blog/22/12/tests-zijn-specs/) - aan een stakeholder of businessanalist kunnen vragen: is dit wat je bedoelt? De concrete aard van tests helpt mensen om hun gedachten op een rijtje te krijgen. Het dwingt hen om te zeggen: in dit *specifieke* geval moet *dat* gebeuren.


Maar zelfs als stakeholders of analisten niet beschikbaar zijn om de tests te bediscussiëren, dan nog loont het zich ze te schrijven. Want hoe vaag de requirements ook zijn, *het systeem is dat niet*. Code verdraagt geen vaagheid, code doet wat het doet. Je kunt daarom maar beter vastleggen wat de code *nu* doet. Dat zorgt er in elk geval voor helderheid over de huidige werking van het systeem. Het geeft in elk geval inzicht wanneer je wijziging zorgt voor een afwijking daarvan - en dat is al winst ten opzichte van een situatie waarin je dat niet weet.


## Excuses


De komende Retrospective ga ik het team mijn excuses aanbieden voor de manier waarop ik op het belang van tests gehamerd heb. Mijn verbazing-plus-frustratie-is-ergernis heeft een constructieve houding in de weg gezeten.


Maar achter de inhoud van mijn vele pleidooien sta ik nog steeds. De gevallen waarin het écht een beter idee is om geen tests te schrijven, zijn op één hand te tellen. 


De hand van een vuurwerkslachtoffer, welteverstaan.
