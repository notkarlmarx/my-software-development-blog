---
title: "Domain Driven Design en Ludwig Wittgenstein"
author: "Karl van Heijster"
date: 2021-08-09T08:13:36+02:00
draft: false
comments: true
tags: ["communicatie", "domain driven design", "filosofie", "microservices", "software architectuur"]
summary: "Vaak gebruiken verschillende delen van de business dezelfde woorden op verschillende manieren, of gebruiken ze verschillende woorden voor hetzelfde concept. Dat is een frustrerende situatie voor een softwareontwikkelaar, maar een feest voor een taalfilosoof."
---

[Eric Evans](https://www.domainlanguage.com/)' [*Domain Driven Design*](https://books.google.nl/books?id=xColAAPGubgC) is zo'n boek dat elke ontwikkelaar gelezen moet hebben. Tenminste, dat zegt men. Ik zou het niet weten, want ik heb het boek nooit gelezen. Gelukkig houdt dat me niet tegen om over Evans' ideeën te praten.


## De taal van software


In het kort komt het idee achter *domain driven design* (DDD) hier op neer: de taal van de software zou de taal van het [domein](https://en.wikipedia.org/wiki/Business_domain) moeten spiegelen. Dat wat in een de toetsconstructie een [*item*](http://www.imsglobal.org/spec/qti/v3p0/guide#h.w7rp6is7v7fd) heet, zou in code niet *vraag* of *opgave* moeten heten.


Om dit voor elkaar te krijgen, stelt Evans voor de taal van het domein vast te leggen in een [*ubiquitous language*](https://martinfowler.com/bliki/UbiquitousLanguage.html). Je kunt dit zien als een domeinspecifiek woordenboek, dat wordt gedeeld tussen de ontwikkelaars en de business, en dat met de tijd mee evolueert.


Dat klinkt als een helder idee, maar de praktijk is, zoals altijd, weerbarstiger. Vaak gebruiken verschillende delen van de business dezelfde woorden op verschillende manieren, of gebruiken ze verschillende woorden voor hetzelfde concept. 


Dat is een frustrerende situatie voor een softwareontwikkelaar, maar een feest voor een [taalfilosoof](https://en.wikipedia.org/wiki/Philosophy_of_language).


## Een oplossing


Er zijn verschillende manieren waarop dit probleem opgelost kan worden. Eén daarvan is dat het ontwikkelteam hard aan de slag gaat om het domein te analyseren en met een voorstel komt voor eenduidige concepten. Het is hun taak, als het ware, de essentie van de gebruikte concepten te vinden en voor eens en altijd vast te leggen in gezaghebbend document.


Klinkt als een goed idee, toch? - Nee, niet doen. In de praktijk werkt deze aanpak eigenlijk nooit.


Ten eerste is het ijdel om te denken dat een ontwikkelteam, los van de business, een domein eenduidig kan doorgronden. De business kan dat zelf niet eens - en zij zijn de experts! Als taalfilosoof meen ik met enig gezag te mogen zeggen: het is moeilijk om dingen goed te definiëren. Of liever gezegd: het is makkelijk om dingen verkeerd te definiëren. Het is onwaarschijnlijk dat het ontwikkelteam zal slagen in deze opzet.


Maar belangrijker nog, zelfs al zou het ontwikkelteam in haar opzet slagen, dan nog zal de werkelijkheid deze onderneming onderuithalen. Het voorstel van het ontwikkelteam zal naar alle waarschijnlijkheid nooit volledig door de business overgenomen worden. 


Er is een grap in de wereld van standaardisering en luidt die als volgt: *Wanneer er twaalf verschillende standaarden bestaan, zal een poging deze standaarden te verenigen resulteren in... een dertiende standaard.*


## Het gevolg


Het gevolg daarvan is dat de spraakverwarring tussen het team en de business alleen maar groter zal worden. Wat begon als een poging om orde te scheppen, zal eindigen in nog grotere chaos.


De eenduidige concepten die het ontwikkelteam heeft verzonnen, zullen nooit helemaal lekker blijken te passen op de *use cases* van (delen van) de business. Om toch waarde te kunnen blijven leveren, zullen de oorspronkelijk eenduidige objecten in de code steeds verder worden aangevuld met nieuwe eigenschappen. Hun samenhang van betekenis gaat met elke aanpassing verder verloren. Dat wat eens een welonderscheiden idee was, zal verworden tot pulp. 


## Een filosofische uitstap


De route van de gezaghebbende, eenduidige definitie valt (met, toegegeven, wat dichterlijke vrijheid) te vergelijken met de route die [Ludwig Wittgenstein](https://plato.stanford.edu/entries/wittgenstein/) bewandelde in zijn [*Tractatus Logico-Philosophicus*](https://books.google.nl/books?id=0gKCAAAAQBAJ) (1921/1922). Daarin probeerde hij het raamwerk te ontwikkelen van hoe taal zich tot de werkelijkheid verhoudt. 


{{<figure src="https://upload.wikimedia.org/wikipedia/commons/a/ab/50._Wittgenstein_in_Swansea_%28taken_by_Ben_Richards%29.jpg" alt="Portret van Ludwig Wittgenstein, 1930" width="300">}}


In het kort: woorden staan voor objecten, en zinnen staan voor de manier waarop objecten zich tot elkaar in feiten verhouden. De primaire eenheid van de werkelijkheid (en van taal) is echter niet het object (woord), maar het feit (zin). Want objecten (woorden) bestaan niet in een vacuüm, maar in samenhang met elkaar.[^1]


Wittgensteins doel toen hij de *Tractatus* begon te schrijven, was om uiteindelijk een volledig eenduidige, logische structuur van de werkelijkheid te kunnen definiëren. Als taal en werkelijkheid met elkaar samen zouden vallen, dan zou duidelijk worden dat alle filosofische problemen voortkomen uit ons eigen onbegrip van hoe taal functioneert. Filosofie zou dan als onzinnig ontmaskerd zijn.


Uiteindelijk kwam Wittgenstein zelf ook tot de conclusie dat die onderneming tot mislukken gedoemd was. Het idee dat er - buiten de taal om! - een raamwerk te ontwikkelen valt van hoe taal zich tot de werkelijkheid verhoudt, is zélf onzinnig. Die wending komt helemaal aan het eind van de *Tractatus*, en interpreten zijn vandaag de dag nog steeds bezig daar chocola van te maken.[^2]


## Een andere route


Evans neemt gelukkig een andere route. (Althans, voor zover ik heb begrepen, want nogmaals: ik heb het boek niet gelezen.) In plaats van de ambiguïteit van domeinconcepten weg te willen definiëren, omarmt hij deze.


Als je merkt dat een deel van de business een bepaald concept structureel op een andere manier gebruikt dan hun collega's, dan zou dat een teken kunnen zijn dat er is sprake van twee onderscheiden domeinen. Dat er sprake is van één woord, betekent niet dat er ook sprake is van één concept. In werkelijkheid zou dat woord twee verschillende concepten kunnen aanduiden.


Let wel, dat betekent niet dat die concepten *totaal verschillend* zijn. Er zal een belangrijke mate van overlap tussen de concepten zitten. Niet voor niets gebruiken de groepen in kwestie hetzelfde woord voor hun onderscheiden concepten. Ze hanteren een soortgelijk maar onderscheiden concept.


## Nog een filosofische uitstap


Om deze situatie te duiden, kunnen we opnieuw te rade gaan bij Wittgenstein. Maar in plaats van zijn vroege filosofie in de *Tractatus*, moeten we ons nu focussen op zijn latere werk, zoals (min of meer) uitgekristalliseerd in het posthuum verschenen [*Philosophical Investigations*](https://books.google.nl/books?id=XN9yyyhYMDoC) (1953).[^3]


In dat boek vraagt Wittgenstein zich opnieuw af wat de betekenis van een woord of zin maakt. Dat is niet het object waar dat woord voor staat of hun samenhang in een feit, zoals hij vroeger dacht. Hij vindt het antwoord op zijn vraag in het *gebruik* van woorden. [De betekenis van een woord *is* hoe dat woord gebruikt wordt](https://plato.stanford.edu/entries/wittgenstein/#MeanUse).


Om dit punt aannemelijk te maken, geeft Wittgenstein een scala aan voorbeelden in de vorm van zogenaamde [*taalspelen*](https://plato.stanford.edu/entries/wittgenstein/#LangGameFamiRese). Dit zijn korte beschrijvingen van hoe een woord of zin wordt gebruikt in een bepaalde context.[^4] 


Hetzelfde woord kan in verschillende taalspelen een andere rol spelen. Het gebruik van het woord verschilt per taalspel, en de betekenis dus ook. Contextuele factoren - de omgeving waarin het woord wordt gebruikt - hebben invloed op de betekenis van het woord.


Ook hier geldt: dat betekent niet dat de betekenissen van die woorden totaal verschillend totaal verschillend zijn van elkaar. Het gebruik over taalspelen heen overlapt op verschillende dimensies. De woorden hebben een [familiegelijkenis](https://plato.stanford.edu/entries/wittgenstein/#LangGameFamiRese) met elkaar.


## Domeinen en taalspelen


Ik hoop dat de parellel duidelijk is. Evans' domeinen kunnen worden opgevat als Wittgensteiniaanse taalspelen. De functie die een woord in het ene domein (taalspel) heeft, is haast per definitie niet dezelfde als die "datzelfde" woord in het andere domein (taalspel) heeft. 


De doorbraak in Evans' idee van *domain driven design* is dat we dit als softwareontwikkelaar moeten accepteren. De verschillende betekenissen die een woord *per domein* kan hebben, moeten terugkomen in de code. De *ubiquitous language* is geen universele taal, maar domeinspecifiek. Concepten dienen te worden gecodeerd in één of meerdere *ubiquitous languages*: één voor elk domein.


Misschien klinkt dat abstract, zeker voor de niet-filosofen onder ons. Hopelijk kan de volgende video van [CodeOpinion](https://www.youtube.com/channel/UC3RKA4vunFAfrfxiJhPEplw) de boel enigszins verduidelijken. (De video gaat over [microservices](https://microservices.io/) en niet over DDD. De twee liggen echter in elkaars verlengde: een goed ontworpen microserviceslandschap kent één microservice per domein.) 


{{<youtube id="2gOOstEI4vU" title="AVOID Entity Services by Focusing on Capabilities)" >}}
<br>


In de video wordt afgeraden om microservices te groeperen per entiteit (*data*). In plaats daarvan wordt voorgesteld om ze te groeperen per vermogen (*capability*).


Dus niet: één `ProductService` die een canoniek `Product` teruggeeft, die vervolgens kan worden gebruikt in verschillende andere services. Maar: een `Catalog`-, `Sales`-, `Purchasing`- en `WareHouseService` die elk een eigen variant van `Product` teruggeven, met alleen de voor hun relevante eigenschappen. Die services hebben elk hun eigen domein. Elk domein kent zijn eigen concept *product*. En de representatie van een *product* ziet er, logischerwijs, dus ook anders uit in elke service.


## De taal van de software *revisited*


Merk op dat de eerste manier van een microservice coderen in lijn is met het vroege gedachtegoed van Wittgensteiniaanse, en de tweede manier in lijn is met zijn latere werk. In Wittgensteiniaanse termen zou de boodschap van de video dus kunnen zijn: groepeer microservices niet per object, maar per taalspel.


En Evans' centrale idee klinkt in Wittgensteiniaanse termen als volgt: *De taal van de software moet de taal van het domein spiegelen. Woorden ontlenen hun betekenis aan hun gebruik. Onze code zou die verschillen in gebruik dus moeten reflecteren.*


[^1]: Wittgenstein ontleende dit punt aan [Gottlob Frege](https://plato.stanford.edu/entries/frege/). Voor een uitstekende boek over de invloeden van op Wittgensteins vroege filosofie, zie [*Representation and Reality in Wittgenstein’s Tractatus*](https://books.google.nl/books?id=vqDoCQAAQBAJ) van José Zalabardo [[recensie](https://deleesclubvanalles.nl/recensie/representation-and-reality-in-wittgensteins-tractatus/)].


[^2]: Zie bijvoorbeeld [*Wittgenstein's Tractatus: An Introduction*](https://books.google.nl/books?id=u83_X1W0t04C) van Alfred Nordmann. Zie ook [*Wittgenstein*](https://books.google.nl/books?id=mDy2UvPJ9xoC) van Anthony Kenny voor een iets toegankelijker en minder opiniërende inleiding in Wittgensteins vroege filosofie.


[^3]: Maar zie ook Wittgensteins [*Blue and Brown Books*](https://en.wikipedia.org/wiki/Blue_and_Brown_Books), samengesteld in de jaren '34-35 en voor het eerst gepubliceerd in 1958. 


[^4]: Het beste boek over dit onderwerp dat ik ooit heb gelezen is [*Wittgenstein on Logic as the Method of Philosophy*](https://books.google.nl/books?id=mUSCDwAAQBAJ) van Oskari Kuusela [[recensie](https://deleesclubvanalles.nl/recensie/wittgenstein-on-logic-as-the-method-of-philosophy/)].
