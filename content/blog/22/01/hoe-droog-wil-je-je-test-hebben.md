---
title: "Hoe droog wil je je test hebben?"
author: "Karl van Heijster"
date: 2022-01-31T08:07:12+01:00
draft: false
comments: true
tags: ["clean code", "DRY", "intentie van code", "leermoment", "testen", "unit tests"]
summary: "Ik heb in het verleden over droger tests geschreven, want ik ben een softwareontwikkelaar en wij herhalen onszelf niet graag. En precies daarom ga ik het nóg een keer over droger tests hebben - of liever: minder droge tests. Want, anders dan je als naïeve ontwikkelaar zou verwachten, gelden er voor productiecode en testcode andere regels wat betreft de mate waarin herhaling tolerabel of zelfs wenselijk is. "
---

Ik heb in het verleden over [droger tests](/blog/21/09/droger-tests-met-factory-methods/) geschreven, want ik ben een softwareontwikkelaar en [wij herhalen onszelf niet graag](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). En precies daarom ga ik het nóg een keer over droger tests hebben - of liever: minder droge tests.


Want, anders dan je als naïeve ontwikkelaar zou verwachten, gelden er voor productiecode en testcode[^1] andere regels wat betreft de mate waarin herhaling tolerabel of zelfs wenselijk is. 


## Droge productiecode


Zoals elke goede ontwikkelaar weet, geldt voor productiecode het aloude adagium [*Don't Repeat Yourself*](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) (DRY). Dit principe stelt, in de formulering van [David Thomas](https://pragdave.me/) en [Andrew Hunt](https://toolshed.com/) in [*The Pragmatig Programmer*](https://pragprog.com/titles/tpp20/the-pragmatic-programmer-20th-anniversary-edition/), dat "elk stukje kennis één enkele, ondubbelzinnige, gezaghebbende representatie" moet hebben binnen een systeem.


De reden daarvoor mag als vanzelfsprekend worden beschouwd. Als de kennis op één plek geconcentreerd is, dan hoeft deze ook maar op één plek te worden aangepast wanneer er een bug wordt vastgesteld of wanneer de specificaties wijzigen. Wanneer dat niet zo is, moet je als ontwikkelaar je complete applicatie doorlopen om (ogenschijnlijk) simpele zaken aan te passen, zoals als de kleur van je layout.


## Droge testcode?


Voor tests ligt de boel wat genuanceerder. Bekijk bijvoorbeeld eens de volgende testcase (die ik overneem uit hoofdstuk 12, *Unit Testing*, van het [fantastische](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/) [*Software Engineering at Google*](https://www.oreilly.com/library/view/software-engineering-at/9781492082781/)):


```java
@Test
public void shouldNavigateToAlbumsPage() {
    String baseUrl = "http://photos.google.com/";
    Navigator nav = new Navigator(baseUrl);
    nav.goToAlbumPage();
    assertThat(nav.getCurrentUrl())
        .isEqualTo(baseUrl + "/albums");
}
```


De schrijver van deze test heeft zich prima aan het DRY-principe gehouden: de waarde van de `baseUrl` komt precies één keer voor in deze test.


Maar de test bevat ook een bug. (Zie je 'm al?) En die bug is een direct gevolg van de toepassing van DRY. (En nu?) 


## Tests en logica


In de laatste regel wordt gekeken of de huidige URL gelijk is aan deze waarde: `http://photos.google.com//albums`. Ik kan je nu al vertellen: dat gaat 'ie niet zijn. Met een beetje geluk ziet 'ie er namelijk als volgt uit: `http://photos.google.com/albums`.


De les die [Erik Kuefler](https://www.linkedin.com/in/erikkuefler/), de schrijver van het hoofdstuk, uit dit voorbeeld trekt is: stop geen logica in je test. Logica wil in dit geval niet meer zeggen dan: [string concatenatie](https://en.wikipedia.org/wiki/Concatenation).


Dat zorgt er namelijk voor dat je tests minder leesbaar worden. In plaats van in één oogopslag te kunnen zien wat een test doet, zal een ontwikkelaar de logica in zijn achterhoofd moeten houden om de test te kunnen doorgronden. Merk op dat zelfs een relatief laagdrempelig beroep op de coginitieve vermogens van de lezer - het onthouden de waarde van de `baseUrl` - al gauw bugs de testcode in smokkelt.


## DAMP


Het lijkt, in het licht van DRY, misschien een goed idee lijkt om testcode vol te proppen met slimme trucjes. Maar het is verstandiger om enige mate van codeduplicatie te tolereren als dat testcode descriptiever en betekenisvoller maakt. De onderstaande testcase bevat géén bug:


```java
@Test
public void shouldNavigateToAlbumsPage() {
    Navigator nav = new Navigator("http://photos.google.com/");
    nav.goToAlbumPage();
    assertThat(nav.getCurrentUrl())
        .isEqualTo("http://photos.google.com/albums");
}
```


Ontwikkelaars zouden geen ontwikkelaars zijn als deze les niet gepaard zou gaan met een grappig gevonden afkorting. Je testcode kan beter DAMP zijn dan DRY, dat wil zeggen: bestaan uit *Descriptive And Meaningful Phrases*.


Zeg mij nu na: "Als je testcode logica bevat, denk dan: DAMP!" 


## En droger tests dan?


Maar ook: "Als je voor het testbegrip relevante informatie wegabstraheert: DAMP!" 


Ho ho! denk je nu misschien. Hoe verhoudt dit zich tot de [droger tests](/blog/21/09/droger-tests-met-factory-methods/) waar ik eerder over schreef? In die blog pleitte ik er *juist* voor om informatie uit de test te abstraheren in een poging ze beter lees- en onderhoudbaar te maken. Ik had het in het bijzonder over de instantiatie van objecten met bepaalde afhankelijkheden. Moet ik op mijn eerder advies terugkomen?


Nee. De crux zit hem in de frase "*voor het testbegrip relevante* informatie". Alle informatie die niet onmiddellijk bijdraagt aan het begip van de test, kan zonder problemen weg worden geabstraheerd. Vaak (maar niet altijd!) valt de instantiatie van objecten daar onder. 


Als je het gedrag van een bepaalde class test, dan zullen de [geïnjecteerde afhankelijkheden](https://en.wikipedia.org/wiki/Dependency_injection) van die class op dat moment niet relevant zijn. Je test in dat geval het gedrag, aangenomen dat de class op de juiste manier geïnstantieerd is. Die informatie mag daarom voor de lezer verborgen blijven.


Het is natuurlijk een ander verhaal wanneer je test hoe een class reageert als je bepaalde afhankelijkheden *niet* injecteert, of kijkt naar het gedrag bij verschillende soorten afhankelijkheden. In dat geval is het belangrijk om die informatie naar de lezer van de test te communiceren.


## Aanvulling


DAMP is geen vervanging voor DRY; het is een aanvulling erop. Helper methods in het algemeen, en factory methods in het bijzonder, hebben nog steeds hun plek in de infrastructuur van je tests. Ze verhelderen tests door niet-relevante informatie te verbergen.


Maar DRY is niet zaligmakend. Een te rigide toepassing van dit principe zorgt ervoor dat je tests *minder* lees- en onderhoudbaar worden. Herhaling op zichzelf is niet slecht, zolang het je tests betekenisvoller en descriptiever maakt. Aan een beetje vocht gaat niemand dood.


[^1]: Het onderscheid tussen die twee is problematisch, natuurlijk. Productiecode is pas productierijp als er een goede testcoverage tegenover staat, en in die zin is testcode een belangrijk onderdeel van productiecode. Dit onderscheid heeft volgens mij zelfs ten onrechte het idee gepromoot bij veel ontwikkelaars dat testcode niet aan dezelfde standaard hoeft te voldoen als productiecode, met alle negatieve gevolgen van dien. Zie ook de uitstekende lezing [*Testing as an equal 1st class citizen (to coding)*](https://www.youtube.com/watch?v=1u6DdiFFH6Q) van [Jon Jagger](http://jonjagger.blogspot.com/).
