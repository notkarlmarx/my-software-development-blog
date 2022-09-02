---
title: "Collegiale documentatie"
author: "Karl van Heijster"
date: 2022-09-02T07:43:53+02:00
draft: false
comments: true
tags: ["communicatie", "documentatie", "samenwerking", "software ontwikkelen", "testen"]
summary: "Ik ken geen enkele ontwikkelaar die het leuk vindt om documentatie te schrijven - ik ook niet - en dat is omdat goede documentatie schrijven *moeilijk* is. Het is moeilijk, omdat je je vanuit een positie van iemand die snapt hoe iets werkt, je in moet leven in iemand die dat begrip nog niet heeft. Mijn belofte \"even\" documentatie te schrijven werd daarom al gauw \"een uur\" documentatie schrijven. Maar het resultaat is volgens mij wel de moeite waard, dus laten we er even (...een uur?) naar kijken."
---

Ik ken geen enkele ontwikkelaar die het leuk vindt om documentatie te schrijven. - Dat is waarschijnlijk de reden waarom ontwikkelaars zo graag zeggen: goede code documenteert zichzelf. Dat is het ultieme excuus om je alleen maar te hoeven focussen op de onderdelen van je werk die je wél leuk vindt, namelijk: code schrijven.


De crux is natuurlijk dat goede code zichzelf vaak documenteert via de aanwezigheid van unittests - en ik ken maar weinig ontwikkelaars die het leuk vinden om unittests te schrijven. De aan- of afwezigheid van unittests, verraadt of de bovenstaande uitspraak een diepgaande wijsheid is, of inderdaad een excuus.


Hoe dan ook, laatst kwam ik in de ongemakkelijke positie daadwerkelijk documentatie te moeten schrijven. Geen code, geen unittests - nee: een ouderwetse `README.md` met instructies voor mijn collega's.


## PDF's testen


Dat zat zo: we gebruiken sinds kort een library genaamd [*QuestPDF*](https://www.questpdf.com/) om PDF-representaties te kunnen genereren van toetsen. (Zie ook [deze blog](/blog/22/08/test-driven-development-is-een-ontwerpdiscipline/).) Omdat ik nu eenmaal ik ben, heb ik me er hard voor gemaakt die functionaliteit grondig te testen.


De vraag is natuurlijk: hoe test je code die een toets als input verwacht, en een PDF als output uitspuugt? Dat is gelukkig een probleem dat mijn team en ik niet zelf hoeven op te lossen. Er bestaat een open source library genaamd [*Verify.QuestPDF*](https://github.com/VerifyTests/Verify.QuestPDF) - wat op zijn beurt een extensie is op een open source library genaamd [*Verify*](https://github.com/VerifyTests/Verify) - die in deze behoefte voorziet.


Ik heb me dus een halve Sprint beziggehouden met het schrijven van tientallen unittests die elk hoekje en gaatje van onze `AssessmentTestPdfGenerator` test en was heel tevreden met mezelf.


## "Wat doe ik verkeerd?"


Toen kreeg ik de vraag van mijn collega: "Hé, ik heb een unittest geschreven voor een nieuw stukje code, maar ik krijg 'm maar niet groen. Wat doe ik verkeerd?" 


Het antwoord was: helemaal niets, je moet alleen even weten hoe *Verify* de uitkomst van haar tests, eh, verifieerd. Ik loodste mijn collega door het proces - en beloofde: ik zal hier even wat documentatie voor schrijven, want jij gaat ~~hopelijk~~ ongetwijfeld niet de laatste zijn die hier tegenaan loopt.


Ik ken geen enkele ontwikkelaar die het leuk vindt om documentatie te schrijven - ik ook niet - en dat is omdat goede documentatie schrijven *moeilijk* is. Het is moeilijk, omdat je je vanuit een positie van iemand die snapt hoe iets werkt, je in moet leven in iemand die dat begrip nog niet heeft. Dat "even" documentatie schrijven werd daarom al gauw "een uur" documentatie schrijven. 


## README.md


Maar het resultaat is volgens mij wel de moeite waard, dus laten we er even (...een uur?) naar kijken.


> ### Instructions on how to use Verify to test PDF generation
> 
> 
> #### TL;DR
> 
> 
> Make sure this folder contains a file named `{testClass}.{testName}.received.png` and a file named `{testClass}.{testName}.received.txt` in order to make your tests pass. These files specify what correct PDF should look like for each test.
> 
> 
> #### On Verify
> 
> 
> The unit tests in this folder use [Verify](https://github.com/VerifyTests/Verify) to assert the correct generation of PDF AssessmentTests. It also uses some code, based on [Verify.QuestPDF](https://github.com/VerifyTests/Verify.QuestPDF)[^1], to verify the contents of your newly generated PDFs. The code for this functionality can be found in the subfolder named *VerifyQuestPDF*[^2].
> 
> 
> Verify is a library that requires you to specify what the correct result looks like in a very specific way. It assumes the existence of some files, and will compare the output of each unit test to those files.
> 
> 
> #### Test outputs
> 
> 
> Each Verify test produces (at least) two files in the same folder as the test:
> 
> 
> 1. An image named `{testClass}.{testName}.received.png`
> 
> 2. A text file named `{testClass}.{testName}.received.txt`
> 
> 
> These files represent the output of the test. The first file shows a representation of the PDF in an image format, the second file specifies the metadata of the generated PDF.
> 
> 
> The files will be compared to two files named `{testClass}.{testName}.verified.png` and `{testClass}.{testName}.verified.txt` respectively, which are assumed to live in the same folder.
> 
> 
> #### Why your test fails
>
>  
> If you write a new test, it will fail for two reasons. 
> 
> 
> 1. Verify will try to compare the image output of your test with a file named `{testClass}.{testName}.verified.png`. However, such a file does not yet exist. Since the test does not have anything to compare `{testClass}.{testName}.received.png` with, it will fail. 
> 
> 2. Verify will compare the textual output of your test with a file named `{testClass}.{testName}.verified.txt`. By default, Verify will generate an empty document with this name. This will by definition not match the outcome of the test, since in your test you've generated a PDF, thus resulting in a failing test.
>  
> 
> #### How to make your test(s) pass
> 
> 
> In order to make your test pass, you will have to specify what a succesful outcome should look like for both files.
> 
> 
> 1. First, inspect `{testClass}.{testName}.received.png`. If it matches your expectation, rename the file to `{testClass}.{testName}.verified.png`. (A new file named `{testClass}.{testName}.received.png` will be generated on each subsequent test run, so you don't have to worry about losing any information.)
> 
> 2. Then, copy the contents of `{testClass}.{testName}.received.txt` to `{testClass}.{testName}.verified.txt`.
> 
> 
> Now, Verify has an idea of what a successful test looks like. On each test run, it will compare these files with the output of the test, i.e. two newly generated files named `*.received.*`. If they match the verified results, the tests will pass.
> 
> 
> Happy testing!


## Commentaar


Ik zou graag de aandacht willen vestigen op de volgende punten:


- Deze tekst bevindt zich in een bestand dat `README.md` heet, en zich bevindt in dezelfde map als de *Verify*-tests. Ik heb overwogen de tekst toe te voegen bij de rest van de algemene documentatie van onze applicatie (ja, onze applicatie heeft algemene - en rap verouderende - documentatie!), maar daar heb ik uiteindelijk vanaf gezien. Ik acht de kans een stuk groter dat een ontwikkelaar de documentatie daadwerkelijk leest, als deze binnen handbereik is.

- De titel van de tekst beschrijft zo in één zin zo helder mogelijk wat volgt. Wat volgt zijn: instructies over hoe je *Verify* gebruikt om het genereren van PDF's te testen - niet meer, niet minder.

- Na de titel volgt een [*TL;DR*](https://nl.wikipedia.org/wiki/TL;DR) met een zo kort mogelijke samenvatting van wat volgt. Deze heb ik als laatst toegevoegd, toen de rest van de tekst al geschreven was. Ontwikkelaars zijn over het algemeen niet de meest geduldige mensen, dus als je hen op weg kan helpen met minder tekst, dan zullen ze je dankbaar zijn.

- De eigenlijke inleiding van de tekst bevat links naar de documentatie van *Verify* en *Verify.QuestPDF*. Hierdoor hebben ontwikkelaars die geïnteresseerd zijn in de materie of die vast komen te zitten in complexe *edge cases*, een handvat om zelf op onderzoek uit te gaan. De daarop volgende sectie geeft een algemeen beeld van wat ervoor nodig is om een test te laten slagen.

- Dan zoomt de tekst in op een concreet scenario: waarom je *huidige* test faalt, en wat je moet doen om ervoor te zorgen dat deze slaagt. Deze opzet komt uiteraard voort uit het feit dat ik vlak voor het schrijven een gesprek met mijn collega had met dit als centrale vraag. Maar het loont zich volgens mij om dit op deze manier in de documentatie te zetten, omdat ontwikkelaars (en niet alleen ontwikkelaars, overigens) over het algemeen pas naar documentatie gaan kijken nádat ze zelf zonder succes aan hebben lopen prutsen.

- *Verify.QuestPDF* levert twee bestanden op waartegen gevalideerd wordt: een .png-bestand met een afbeelding en een .txt-bestand met metadata. Ik heb deze volgorde bewust consequent aangehouden in de tekst, zodat een vluchtige lezer altijd weet waar hij aan toe is. Ik heb het .png-bestand altijd op de eerste plek gezet, omdat dit het belangrijkste deel van de test vormt.

- Tot slot: een blije afsluiter omdat ik nu eenmaal een blij persoon ben.


## Documentatie en code


Lang verhaal kort: er komen best wel wat overwegingen kijken bij het schrijven - en herschrijven! - van documentatie. Documentatie schrijven is net als code schrijven: een iteratief proces, waarbij je je bij elke stap af dient te vragen of je de boel wat schoner, wat helderder, wat toegankelijker hebt achtergelaten dan je het aantrof.


Nee, zo leuk als coderen zal het nooit worden. Maar elke keer als een ontwikkelaar de tijd neemt voor documentatie, plukt het team daar de vruchten van plukken. Dat "even" documenteren betaalt zich dubbel en dwars terug.


[^1]: Ik heb de code van *Verify.QuestPDF* onze codebase ingetrokken en licht aangepast, omdat deze me op bepaalde plekken beperkte in wat ik wilde. Het totale aantal regels code is beperkt en de werking mijn eigen wijzigingen heb ik via unittests gedocumenteerd (!). Daardoor is dit extra kleine beetje onderhoudslast dat ik op de schouders van mijn team leg, volgens mij gerechtvaardigd. 

[^2]: Het oorspronkelijke document linkt hier direct naar de folder in kwestie. 
