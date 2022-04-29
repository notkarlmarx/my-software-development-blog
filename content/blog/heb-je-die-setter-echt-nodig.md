---
title: "Heb je die setter echt nodig?"
author: "Karl van Heijster"
date: 2022-04-29T08:58:50+02:00
draft: true
comments: true
tags: ["classes", "clean code", "functioneel programmeren", "immutability", "intentie van code", "objectgeoriënteerd programmeren", "properties"]
summary: "`\"prop\"` + `tab` + `tab` - welke C#-ontwikkelaar maakt niet bijna dagelijks dankbaar gebruik van dat code snippet om zijn ontwikkelsnelheid te verhogen? Standaard properties zijn zo alomtegenwoordig in de wereld van objectgeoriënteerd programmeren in het algemeen - en C# in het bijzonder - dat je er haast niet meer bij stilstaat dat het ook anders kan. Maar dat het ook anders kan, leerde ik dankzij Spencer Schneidenbach, in een uitstekende lezing over *immutability* (onveranderlijkheid)."
---

`"prop"` + `tab` + `tab` - welke C#-ontwikkelaar maakt niet bijna dagelijks dankbaar gebruik van dat [code snippet](https://docs.microsoft.com/en-us/visualstudio/ide/visual-csharp-code-snippets?view=vs-2022) om zijn ontwikkelsnelheid te verhogen? [Standaard properties](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties) zijn zo alomtegenwoordig in de wereld van objectgeoriënteerd programmeren in het algemeen - en [C#](https://docs.microsoft.com/en-us/dotnet/csharp/) in het bijzonder - dat je er haast niet meer bij stilstaat dat het ook anders kan.


Dat het ook anders kan, leerde ik dankzij [Spencer Schneidenbach](https://schneids.net/), in een uitstekende lezing over [*immutability*](https://en.wikipedia.org/wiki/Immutable_object) (onveranderlijkheid) tijdens de [NDC Conferentie](https://ndcconferences.com/) in Oslo, eind vorig jaar. (Uiteraard - en helaas - vanaf mijn comfortabele sofa, thuis. Het [YouTube-kanaal van NDC](https://www.youtube.com/c/NDCConferences/playlists) is overigens een dankbare bron van kennis.)


{{<youtube id="Hpz6h3izPgY" title="Using Immutable Data Structures - Spencer Schneidenbach - NDC Oslo 2021" >}}
<br>


## ~~Twiet~~ Tweet


Schneidenbach begint zijn lezing met een aansprekend voorbeeld. Zou het niet fijn zijn als [Twitter](https://twitter.com/) de mogelijkheid zou aanbieden om je tweet te kunnen bewerken? Alle ongeduldige, dikduimige autocorrectslachtoffers knikken hard ja, natuurlijk! - Maar wacht! zegt Schneidenbach, want heb je de implicaties van dat feature request wel overzien?


Wat doe je als een tweet al geretweet is, of geciteerd of geliket? Blijft die informatie dan bewaard of niet? - In de eerste instantie zou je misschien willen zeggen: ja, natuurlijk! En dat is niet gek, want waarschijnlijk denk je aan scenario's waarin mensen hun spelfouten corrigeren, en dat de inhoud van de tweet dus gelijk blijft. 


Maar wat doe je als iemand zijn tweet aanpast van "Ik hou van poezen" - dertigduizend likes, tweehonderdduizend retweets - naar "Ik hou van poezen verdrinken"? Accepteer je dat dertigduizend mensen het leuk vinden dat poezen worden verdronken, en tweehonderdduizend mensen dat actief uitdragen? En zo ja, denk je dat dat je in dank af zou worden genomen door de ongetwijfeld miljoenen Twitteraars die meer moeite hebben met verdronken poezen?


Oké, is het dan misschien mogelijk om het beste van twee werelden te verenigen? Bijvoorbeeld dat je je tweet maar tot bepaalde hoogte aan mag passen, of maar gedurende een korte tijd? Maar wat betekent "tot een bepaalde hoogte aanpassen" dan precies? Valt het toevoegen van één woord, zoals hierboven, niet onder die definitie? En wat doe je met Twitteraars die miljoenen volgers hebben, wiens tweets binnen enkele seconden opblazen tot enorme proporties?


## Eenvoud


Je ziet: zo wordt een niet onredelijk klinkende feature - wat zeg ik, misschien zelfs wel een heel erg voor de hand liggende feature - al gauw een mijnenveld voor PR-medewerkers en een onderhoudsnachtmerrie voor ontwikkelaars.


De oplossing voor dat probleem is simpel: begin er niet aan. Dat is ook precies wat Twitter gedaan heeft. Ze ondersteunen simpelweg niet de mogelijkheid om tweets te bewerken - en voorkomen er meer problemen mee dan ze veroorzaken.


Dat is wat je koopt voor een beperktere set aan features: de luxe om niet over bepaalde problemen na te hoeven denken. Twitter verliest met de onveranderlijkheid van haar tweets een gewilde feature, maar koopt daar eenvoud voor terug. Het stelt het bedrijf in staat om zich op één ding te concentreren, en dat goed te doen, en zich geen zorgen te hoeven maken om de complexiteit die een uitgebreidere featureset met zich mee zou brengen.


## Onveranderlijke code


Nu is Twitter een dienst voor jan en alleman - maar het principe is net zo goed van toepassing op dat waar wij ontwikkelaars ons mee bezig houden: code. Want C# is een taal die *out of the box* veranderlijkheid ondersteunt: het gemiddelde C#-object staat bol van velden die je middels setters naar hartelust kunt aanpassen. Met alle complexiteit van dien.


Maar die veranderlijkheid is geen natuurgegeven dat we nu eenmaal moeten accepteren. Functionele programmeertalen zoals [F#](https://docs.microsoft.com/en-us/dotnet/fsharp/what-is-fsharp) ondersteunen juist onveranderlijkheid *out of the box*. Wie een object aanmaakt in die taal, heeft daarna niet meer de mogelijkheid om deze aan te passen. Wie dat wil, zal een kopie moeten maken van dat object, en op dat nieuwe object de gewenste aanpassingen moeten doen.


Dat klinkt alsof het zonde van het geheugengebruik is, en misschien is dat ook zo. Maar wat je ervoor terugkrijgt als ontwikkelaar is niet te verwaarlozen: de zekerheid dat het object waar je mee werkt niet onder je neus ineens ongemerkt van eigenschappen verandert. 


Denk eens aan hoeveel bugs je in de loop van je carrière je hebt lopen fixen, omdat een method een object veranderde zonder daar transparant over te zijn! Wie zijn datastructuren *immutable* maakt, zal ongetwijfeld nog genoeg gelegenheid vinden om op zijn code te schelden, maar in elk geval niet meer vanwege dát soort bugs!


## Records


Ook het team achter C# heeft de voordelen van onveranderlijkheid ingezien, blijkens de introductie van het [Records](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record) in [C# 9.0](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-9). 


Records zijn onder water gewone classes, maar ze hebben de bijzondere eigenschap dat de properties die je erop definieert niet meer aan kunt passen, en dat de vergelijking tussen twee Records op basis van haar waarden geschiet, en niet op basis van de referentie. Ik zal niet te diep ingaan op alle features die Records, wie zich daarvoor interesseert kan prima terecht bij de [documentatie](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record) of [deze video](https://www.youtube.com/watch?v=9Byvwa9yF-I) van [Tim Corey](https://www.iamtimcorey.com/).


## Les


Nu betekenen Records heus niet het eind van normale classes in C#. C# is immers geen functionele taal, en veranderlijkheid zal daarom altijd een onderdeel van code in die taal zijn en blijven. En dat is ook helemaal niet erg. Er zijn genoeg situaties denkbaar waarin het juist wél van toegevoegde waarde is om objecten na hun instantiatie aan te kunnen passen, met alle complexiteit van dien. 


Complexiteit op zichzelf is immers geen zonde. *Nodeloze* complexiteit daarentegen, dat is een heel ander verhaal. De les van Schneidenbach is dan ook niet: gebruik nooit meer veranderlijke objecten. De les is deze: *wees je bewust* van de complexiteit die je daarmee introduceert. Heb je die setter echt nodig?
