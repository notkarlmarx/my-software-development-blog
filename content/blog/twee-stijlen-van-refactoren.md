---
title: "Twee stijlen van refactoren"
author: "Karl van Heijster"
date: 2022-07-22T08:03:51+02:00
draft: true
comments: true
tags: ["incrementele ontwikkeling", "refactoren"]
summary: "Het was een tijd terug 40 graden en dat leek me, om redenen die ik achteraf niet kan bevatten, geen reden om het geairconditioneerde pand van mijn werkgever te bezoeken. In plaats daarvan bleef ik met de gordijnen dicht op mijn snikhete kantoortje zitten en begon aan een grootscheepse refactorslag. Of liever: twee refactorslagen - de ene met een gestaag toenemende hoeveelheid koortsig zweet op mijn voorhoofd, en de ander met een stabiele hoeveelheid normalehittezweet. De ene refactorslag was een ramp, de ander een succes. In beide gevallen moest ik het kantoor nadien goed luchten - dat wel."
---

Het was een tijd terug 40 graden en dat leek me, om redenen die ik achteraf niet kan bevatten, geen reden om het geairconditioneerde pand van mijn werkgever te bezoeken. In plaats daarvan bleef ik met de gordijnen dicht op mijn snikhete kantoortje zitten en begon aan een grootscheepse refactorslag.


Of liever: ik begon aan twee refactorslagen - de ene met een gestaag toenemende hoeveelheid koortsig zweet op mijn voorhoofd, en de ander met een stabiele hoeveelheid normalehittezweet. De ene refactorslag was een ramp, de ander een succes. In beide gevallen moest ik het kantoor nadien goed luchten - dat wel.


## Poging #1


Hoe pak jij 't refactoren van je code normaal gesproken aan? Mijn eerste poging had de volgende structuur: ik keek naar de code, zag wat er mis mee was en had een aardig idee van hoe ik wilde dat het eruit zou komen te zien. En dus begon ik die oplossing te implementeren.


Ik verplaatste code naar logischer plekken, veranderde de [signaturen](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods#method-signatures) van diverse [methods en functies](https://www.tutorialspoint.com/difference-between-method-and-function-in-chash), definieerde [interfaces](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface). Ik brak een heleboel tests - eerst omdat ze niet meer wilden compileren, en daarna omdat mijn code niet meer hetzelfde gedrag vertoonde. Ik zei tegen mezelf: dat trek ik recht als de oplossing er staat. (En ik overtuigde mezelf ervan dat dat mijn eigen keuze was, en niet het gevolg van mijn aanpak.)


Op een gegeven moment slaagden de meeste van mijn tests en was ik erg tevreden met mezelf. De middag vorderde, de temperatuur steeg maar hoger en hoger, en ik zonk dieper en dieper weg in het moeras van mijn refactorslag. Aan het eind van de dag was ik de wanhoop nabij en zei tegen mezelf: morgenvroeg is het hier beter uit te houden - ik maak het morgen wel af.


De volgende ochtend stuitte ik op een circulaire referentie in mijn code, waardoor het project niet meer wilde starten, en gooide ik al mijn werk weg.


## Poging #2


Voor mijn tweede refactorslag richtte ik me op een ander stuk code. Een eenvoudiger stuk, misschien - en dat zou een onderdeel van het succes kunnen zijn, dat accepteer ik. Maar een groter deel van het succes zit 'm, denk ik, in een vernieuwde aanpak. 


Ook deze keer keek ik naar de code, zag wat er mis mee was en had een aardig idee van hoe ik wilde dat het eruit zou komen te zien. Maar in plaats van direct voor het goud te willen gaan, stelde ik me een bescheidener doel.


De code in kwestie combineerde het ophalen van data met het manipuleren ervan. (Zie ook [deze blog] (LINK).) De code die de data ophaalde, de databasecall, bevond zich in een [`for each`-loop](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/statements/iteration-statements#the-foreach-statement). Dat vond ik een slecht idee. Dus ik trok die code daar uit. 


\- Let wel: ik verplaatste de code niet naar waar ik die databasecall uiteindelijk wilde hebben. Nee, ik plaatste 'm vóór aanvang van die loop, in dezelfde method nog. Daar haalde ik in één keer de data op. Ik paste de code in de loop aan zodat deze alleen nog maar de data manipuleerde - meer niet. Daarna trapte ik de tests af - en ze slaagden.


## Kopie


Toen wilde ik de databasecall uit die method halen. Ik verhuisde deze naar de aanroepende method, en veranderde de parameters van de aangeroepen method. Deze hoefde immers niet meer de informatie te hebben waarmee de databasecall gedaan kon worden, maar alleen het resultaat van die call te slikken. 


Mijn tests faalden. De method werd op verschillende plekken aangeroepen en mijn wijziging had de code gebroken. Een dag eerder zou ik alle aanroepende methods hebben aangepast om de code werkend te krijgen. Maar daar had ik vandaag geen zin in. Dus ik herstelde de oorspronkelijke method (en checkte of mijn tests weer slaagden). 


Toen trok ik een kopie daarvan, en paste de parameters van die kopie aan om het resultaat van de databasecall te accepteren. Daarna richtte ik me één aanroepende method aan om mijn nieuwe stukje code te gebruiken. Ik verhuisde de databasecall naar die method en liet 'm naar de aangepaste code wijzen. Ik trapte de tests af - en ze slaagden. Ik voerde dezelfde wijziging door voor de rest van de calls - en mijn tests bleven slagen. Ten slotte verwijderde ik de oorspronkelijke method.


## Van method naar class


Dit proces herhaalde zich nog twee keer. Elke keer, stapje voor stapje, trok ik de databasecall een niveau hoger. En elke keer zorgde ik ervoor dat mijn tests bleven slagen.


Uiteindelijk kwam ik op een punt waarop het omhoog trekken van de databasecall ervoor zou zorgen, dat 'ie uit de class verdween. Daar waar oorspronkelijk de [Repository](https://martinfowler.com/eaaCatalog/repository.html) in de [constructor](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/constructors) [geïnjecteerd](https://docs.microsoft.com/en-us/dotnet/core/extensions/dependency-injection) werd, zou ik zo dadelijk kunnen volstaan met het injecteren van de data zelf.


Dus dat was precies wat ik deed. Ook hier trok ik weer een kopie van de constructor, en gaf deze de juiste parameters mee. Daarna keek ik naar de plekken waar de oorspronkelijke constructor aangroepen werd, en verhuisde de databasecall daar naartoe. Eenmaal verhuisd, maakte ik gebruik van de nieuwe constructor. Dat deed ik voor elke aanroep. 


En elke keer trapte ik de tests af, uiteraard, en zorgde ervoor dat ze slaagden - als ze dat niet onmiddellijk al deden.


## Onverwacht


Mijn refactorslag had een interessante consequentie. Het stelde me namelijk in staat om de gefactorde class [`static`](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/static) te maken - de code was plotsklaps veranderd in een verzameling [pure functies](https://docs.microsoft.com/en-us/dotnet/standard/linq/refactor-pure-functions). 


Het gevolg daarvan was op zijn beurt weer dat ik deze class nergens anders meer in de constructor hoefde te injecteren. Het spreekt voor zich dat ik dit ook stapsgewijs aanpakte: een kopie class verving aanroep voor aanroep de oorspronkelijke class. 


Mijn refactorslag had dus niet alleen de oorspronkelijke class vereenvoudigd, het vergemakkelijkte ook de instantiatie van diverse andere classes. Een onverwacht - maar zeer welkom - resultaat!


## *Big bang* versus incrementeel


Het mag duidelijk zijn waar het verschil tussen de eerste en de tweede stijlen van refactoring 'm in zitten. 


De eerste gaat uit van een *big bang*-manier van dingen wijzigen. Alle wijzigingen moeten er in één keer staan om de boel goed en wel te laten werken. Tot je bij het eindresultaat bent aangekomen, is de code stuk - *kaputt*.


De tweede gaat uit van een incrementele manier van code wijzigen. In kleine tussenstapjes werk je toe naar het gewenste resultaat. Gedurende elk stapje blijft de code werken zoals bedoeld. 


Dat de incrementel aanpak mijn voorkeur heeft, hoeft niemand te verbazen. 


## Debuggen


Door in kleine stapjes te werken en steeds opnieuw je tests af te trappen, krijg je direct feedback over de werking van je code. Doordat je maar één wijziging per keer in je hoofd hoeft te houden, is het doodsimpel te achterhalen waar de bron van een bug zit. Je hebt er zelfs geen [debugger](https://en.wikipedia.org/wiki/Debugger) bij nodig.


Wie op een *big bang* hanteert, heeft die context niet. Die moet, nadat de nieuwe implementatie voltooid is, met de debugger in de hand actief op zoek naar de oorzaak van het probleem. Dat is geen enorme opgave als je maar één falende test hebt, maar als het er tientallen of zelfs honderden zijn, dan is die taak eenvoudigweg overweldigend.


In de taal van [Felienne Hermans](https://www.felienne.com/)' [*The Programmer's Brain*](https://www.manning.com/books/the-programmers-brain): de incrementele aanpak is een stuk vriendelijker voor met name je kortetermijn- en werkgeheugen.


## Betere code


Maar het interessantste van incrementele aanpak, is dat deze je in staat stelt om tijdens het refactoren van koers te wisselen. Door in kleine stapjes te werken, en na elke stap te reflecteren op de volgende, doe je inzichten in je code op die je op voorhand nooit had gedaan. 


Ik had op voorhand niet voorzien dat ik een verzameling pure functies zou creëren, dat was een gelukkig toeval. Maar ik ben blij dat het gebeurd is, want het heeft uiteindelijk wel betere code opgeleverd.


Ik heb mijn lesje dus wel geleerd. Voortaan als ik ga refactoren, dan pak ik dat incrementeel aan. Wat jij?
