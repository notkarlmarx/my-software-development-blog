---
title: "Moet je dit willen testen?"
author: "Karl van Heijster"
date: 2021-08-27T08:09:58+02:00
draft: false
comments: true
tags: ["boeken", "integratietests", "leermoment", "testen", "unit tests", "waarde"]
summary: "\"*Code is a liability, not an asset.*\" Van alle zinnen in Vladimir Khorikovs *Unit Testing: Principles, Practices, and Patterns* is deze me het meest bijgebleven. Ironisch, want op het eerste gezicht is het geen zin die iets te doen heeft met unit testing. Maar ook testcode kan een een blok aan het been zijn. Bijvoorbeeld wanneer je de code eigenlijk niet zou moeten willen unittesten."
---

"*Code is a liability, not an asset.*" Van alle zinnen in [Vladimir Khorikovs](https://enterprisecraftsmanship.com/) [*Unit Testing: Principles, Practices, and Patterns*](https://www.manning.com/books/unit-testing) is deze me het meest bijgebleven. Ironisch, want op het eerste gezicht is het geen zin die iets te doen heeft met unit testing. 


Dat klopt echter maar gedeeltelijk. Een groot deel van Khorikovs boek gaat ook expliciet *niet* over unit tests zelf, maar de manier waarop je je productiecode zo kunt opzetten dat deze goed testbaar is. De indringendste boodschap die Khorikov voor de lezer in petto heeft, is dan ook: codeer het niet, dan hoef je het ook niet te testen.


## Testcode als *liability*


Maar de zin heeft niet alleen betrekking op productiecode. Ook testcode kan een *liability* zijn, een blok aan het been. Bijvoorbeeld wanneer deze slecht leesbaar is door een overdaad aan afhankelijkheden, of wanneer deze vol codeduplicatie zit.


Of wanneer je de code eigenlijk niet zou moeten unittesten.


Dat klinkt misschien als een tegenintuïtieve reden. Het is min of meer een dogma in de programmeerwereld dat de testcoverage van je code zo hoog mogelijk moet zijn. (Ik zeg "*min of meer* een dogma", omdat een hoge testcoverage in veel projecten - helaas! - nog een te lage prioriteit heeft voor het ontwikkelteam.) 


Maar Khorikov wijst erop: hoewel een lage testcoverage een indicatie is van slechte code, hoeft een hoge testcoverage niet te betekenen dat de code van hoge kwaliteit is. Sommige code is zo triviaal, dat het schrijven van een unit test eigenlijk de moeite niet loont. Andere code is zo complex, dat unit tests niet het juiste middel zijn om hun werking te testen. 


## Twee assen


Khorikov geeft dit idee handen en voeten door code te plotten op twee assen. 


De verticale as geeft de algoritmische complexiteit en domeinsignificantie aan. De redenen voor het kiezen van deze metrieken liggen voor de hand. Hoe complexer een algoritme, des te groter de kans op bugs, en hoe significanter de code is voor het domein, des te belangrijker dat deze ook werkt zoals bedoeld. Code zal hoger geplot worden op deze as naarmate een algoritme complexer wordt of meer waarde levert in termen van het domein. 


De horizontale as de complexiteit van de code, gemeten in het aantal classes waarmee de code interacteert (*collaborators*). Deze metriek is relevant voor unit tests, omdat deze classes, al dan niet via mocks, geïnstantieerd zullen moeten worden om de test te kunnen draaien. Hoe meer classes de code nodig heeft om een bepaalde taak ten uitvoer te brengen, des te hoger (rechtser) zal deze as geplot worden.


(Merk op dat dit het perspectief op de code verandert. Het is voor een softwareontwikkelaar gebruikelijk om naar de tests te kijken vanuit hun waarde voor de productiecode. Khorikov kijkt naar de productiecode vanuit hun waarde voor de tests.)


## Vier kwadranten


Alle code valt in één van vier kwadranten:

|                                |                             |                             |
|:------------------------------:|-----------------------------|-----------------------------|
|                                | Domeinmodel, algoritmen (4) | Overgecompliceerde code (3) |
| **Domeinsignficantie&#8593;**  | Triviale code (1)           | Controllers (2)             |
|                                | **Complexiteit&#8594;**     |                             |
<br>

Code die weinig complex is en weinig domeinsignificantie heeft, en met weinig andere classes interacteert, is triviaal (1). Denk aan getters en setters op een bepaald object. Deze code is de moeite van het testen niet waard.


Weinig complexe code die met veel classes interacteert, noemt Khorikov *controllers* (2). Dit zijn classes wiens doel het is om de samenwerking van bepaalde objecten (met hoge complexiteit of domeinsignificantie) te orchestreren. Denk aan code die bepaalde *unmanaged dependencies* aanroept, zoals een message bus. Deze code dient te worden geïntegratietest.


Complexe, domeinsignificante code die met veel classes interacteert, is te complex (3) om goed en wel te kunnen testen. Unit tests voor deze code zullen door de vele afhankelijkheden moeilijk onderhoudbaar zijn. Deze code moet worden uitgesplitst naar eenvoudige domeinsignificante code enerzijds en controllers anderszijds.


Wat overblijft, is complexe en/of domeinsignificante code die met weinig classes interacteert (4). Dit soort code is de uitgelezen kandidaat om te unit testen. De algoritmische complexiteit en/of domeinsignificantie maken het bestaan van deze tests essentieel, en hun lage complexiteit zorgen ervoor dat deze eenvoudig geschreven kunnen worden.


## Testen, testen, testen, of...?


Vóór het lezen van Khorikovs boek, had ik een eenvoudige filosofie als het op unit tests aankomt: schrijf er zoveel mogelijk. Ik testte zoveel mogelijk code met zoveel mogelijk paden. Natuurlijk, ik probeerde de de boel een beetje onderhoudbaar te houden door het gebruik van helper methods, maar toch, aan het eind van de dag was het een filosofie van *testen testen testen*.


Met dit model in het achterhoofd, is duidelijk waar mijn vorige testfilosofie faalde. Ten eerste testte ik triviale code. Hoewel deze tests makkelijk zijn om te schrijven, leverden ze maar weinig waarde. Ten tweede testte ik overgecompliceerde code. Deze leverden misschien wel waarde, maar waren zo moeilijk onderhoudbaar, dat ze hun investering niet waard waren.


De op één na indringendste boodschap in *Unit Testing: Principles, Practices, and Patterns* luidt dan ook: test niets wat je niet zou moeten willen testen.
