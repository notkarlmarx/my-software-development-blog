---
title: "Low code: een nieuw paradigma?"
author: "Karl van Heijster"
date: 2021-10-04T08:02:09+02:00
draft: false
comments: true
tags: ["filosofie", "functioneel programmeren", "gestructureerd programmeren", "low code development", "objectgeoriënteerd programmeren", "paradigma's"]
summary: "Een deel van de teams in het bedrijf waar ik voor werk is overgestapt op dat wat *low code development* wordt genoemd. In plaats van applicaties regel voor regel met de hand te schrijven, klikken ze deze in elkaar met behulp van een tool. Hoe verhoudt deze ontwikkelmethode zich tot \"ouderwets\" programmeren? Luidt *low code* een nieuw ontwikkelparadigma in?"
---

Een deel van de teams in het bedrijf waar ik voor werk is overgestapt op dat wat [*low code development*](https://en.wikipedia.org/wiki/Low-code_development_platform) wordt genoemd. In plaats van applicaties regel voor regel met de hand te schrijven, klikken ze deze in elkaar met behulp van een tool.


Een aantal van mijn collega's staat argwanend (om niet te zeggen: vijandig) tegenover deze ontwikkeling, en dat is niet helemaal onterecht. *Low code* ontwikkeling brengt het risico op een stuk of wat antipatronen met zich mee, zoals [*vendor lock-in*](https://en.wikipedia.org/wiki/Vendor_lock-in) en de [*last 10% trap*](https://www.oreilly.com/library/view/evolutionary-architecture-fundamentals/9781492027089/video319438.html). En dan heb ik het nog niet eens over het feit dat een deel van het personeel opnieuw opgeleid moet worden om überhaupt op deze manier te kunnen ontwikkelen.


Tegelijkertijd heeft *low code development* wel de potentie om de [*time to market*](https://en.wikipedia.org/wiki/Time_to_market) van een product te verkleinen. Immers, een applicatie in elkaar klikken is, op het oog in elk geval, een stuk sneller gedaan dan deze helemaal zelf uit te coderen. Geen wonder dat met name de business enthousiast is over deze ontwikkeling.


Ik zal het verder niet over de voor- of nadelen van *low code* hebben, want eerlijk gezegd heeft deze techniek zich wat mij betreft nog niet genoeg in de praktijk bewezen om daar met zekerheid iets over te kunnen zeggen. 


Waar ik het over wil hebben, is de manier waarop deze ontwikkelmethode zich verhoudt tot "ouderwets" (*high code*?) programmeren. Meer specifiek: is *low code development* een nieuw ontwikkelparadigma of niet?


## Wat is een paradigma?


De term "paradigma" komt oorspronkelijk uit de wiskunde en betekent "[standaardvoorbeeld](https://en.wikipedia.org/wiki/Paradigm#Etymology)". De manier waarop ik de term gebruik, is echter ontleend aan de [wetenschapsfilosofie](https://en.wikipedia.org/wiki/Philosophy_of_science), in het bijzonder [*The Structure of Scientific Revolutions*](https://plato.stanford.edu/entries/structure-scientific-theories/) van [Thomas Kuhn](https://plato.stanford.edu/entries/thomas-kuhn/).


Kuhn betoogt in zijn boek dat de wetenschap zich niet lineair ontwikkelt, namelijk als geleidelijke accumulatie van kennis. In plaats daarvan schetst hij een discontinu beeld. Of liever: lange perioden van continuïteit worden volgens Kuhn van tijd tot tijd afgewisseld met een discontinue gebeurtenis die het wetenschappelijk vakgebied op zijn grondvesten doet schudden.


De continue perioden noemt Kuhn "normale wetenschap". Gedurende deze perioden, kent de wetenschap inderdaad een min of meer lineaire ontwikkeling, waarin kennis geleidelijk aan toeneemt. 


De toename van kennis zorgt er echter voor dat de standaardoplossingen niet langer houdbaar blijven. Van tijd tot tijd wordt een vakgebied daarom als het ware opnieuw uitgevonden. De fundamentele aannames van de wetenschap worden herzien en er ontstaat een nieuwe vorm van kennis bedrijven die zich niet met de periode daarvóór laat vergelijken. Kuhn noemt zo'n gebeurtenis een paradigmawisseling. 


De onderstaande afbeelding beschrijft de zogenaamde Kuhniaanse cyclus van wetenschapsbeoefening:


{{<figure src="https://www.legalevolution.org/wp-content/uploads/sites/262/2021/05/P233-KuhnCycle_BasicCyclev2-e1621710116685.png" alt="Afbeelding van de Kuhniaanse ontwikkelcyclus van wetenschap" width="500">}}


De opvattingen van wat goede wetenschap behelst, kan ingrijpend verschillen vóór en na een paradigmawisseling. Om deze reden meent Kuhn dat verschillende paradigma's in zekere zin niet met elkaar te vergelijken zijn: ze zijn [incommensurabel](https://plato.stanford.edu/entries/incommensurability/). Dit is één van de meer controversiële aspecten van zijn werk. 


## Voorbeelden van paradigmawisselingen


Het standaardvoorbeeld (*pun intended*) van zo'n wetenschappelijke revolutie, is de [Copernicaanse wending](https://en.wikipedia.org/wiki/Copernican_Revolution). Tot [Copernicus](https://plato.stanford.edu/entries/copernicus/) werd aangenomen dat de aarde het middelpunt van het heelal was, waar de zon en de rest van de plateneten omheen draaien. De Copernicaanse wending bestaat erin dat deze voorstelling op zijn kop te zetten. Binnen het Copernicaanse model, staat de zon in het middelpunt en draaien de overige planeten, waaronder de aarde, daaromheen.


Deze theorie veranderde de astronomie zo ingrijpend, dat er met recht gesproken mag worden van een periode vóór en na Copernicus.


Een ander voorbeeld van een paradigmawisseling vinden we in de 17e eeuw met de [opkomst van de wetenschappelijke methode](https://en.wikipedia.org/wiki/Scientific_Revolution) überhaupt. De tot dan toe heersende methode van wetenschappelijk onderzoek (als je het zo wil noemen), de [aristotelische](https://plato.stanford.edu/entries/aristotle/), ging ervan uit dat je de wereld het best kon bestuderen door deze louter te observeren. Wie ingrijpt in de natuur, lokt daarmee immers onnatuurlijk gedrag uit.


Sinds de tijd van [Descartes](https://plato.stanford.edu/entries/descartes/) is dit beeld ingrijpend veranderd. Moderne wetenschappers leggen de natuur juist op de metaforische pijnbank. Ze creëren kunstmatige condities waar ze controle over hebben, om de relevante variabelen te kunnen extraheren. Die kunstmatigheid is juist een essentieel onderdeel van moderne wetenschapsbeoefening. Het is onderdeel geworden van het moderne wetenschapsparadigma.


(Merk op dat Kuhns wetenschapsopvatting zelf ook als paradigmawisseling in de wetenschapsfilosofie kan worden gezien. Vóór Kuhn lag de nadruk van dit vakgebied op het vinden van een [aan de logica ontleende rechtvaardiging van het feit dat onze kennis zich vermeerdert](https://plato.stanford.edu/entries/induction-problem/). Kuhn veranderde de lens waarmee filosofen de wetenschap bekeken: van zuiver logisch- theoretisch naar overwegend historisch-praktisch.)


## Paradigma's in de softwareontwikkeling


Ook de softwareontwikkeling kent [zijn eigen paradigma's](https://en.wikipedia.org/wiki/Programming_paradigm). Er zijn verschillende manieren om deze te classificeren, maar ik baseer me met name op deze lezing van Robert "*Uncle Bob*" Martin:


{{<youtube id="ya1xDCCMh7g" title="The Future of Programming Languages at the Confluence of Paradigms" >}}
<br/>


Programmeertalen kunnen worden ondergebracht in een [gestructureerd](https://en.wikipedia.org/wiki/Structured_programming), [objectgeoriënteerd](https://en.wikipedia.org/wiki/Object-oriented_programming) of een [functioneel](https://en.wikipedia.org/wiki/Functional_programming) paradigma. Elk van die programmeerparadigma's beperkt de ontwikkelaar op de een of andere manier in zijn mogelijkheden in het schrijven van code. Gestructureerde code beperkt de ontwikkelaar in het gebruik van [*go to*](https://homepages.cwi.nl/~storm/teaching/reader/Dijkstra68.pdf); objectgeoriënteerde code in het gebruik van [*pointers* naar functies](https://www.ibm.com/docs/en/zos/2.2.0?topic=functions-pointers); functionele code in het gebruik van [*state*](https://en.wikipedia.org/wiki/Side_effect_(computer_science)).


De term "paradigma" is goed gekozen voor het onderscheid dat hier gemaakt wordt. Structurele, objectgeoriënteerde en functionele software hebben elk hun eigen standaardvoorbeelden van hoe ze een veelvoorkomend probleem oplossen of hoe een goed functionerend programma eruitziet. En het is, anders dan Kuhns wetenschappelijke paradigma's, moeilijk om te zeggen dat het ene programmeerparadigma onvoorwaardelijk beter is dan de andere. 


## Low code: een nieuw paradigma?


Luidt *low code* ontwikkeling een nieuw paradigma in de softwareontwikkeling in? Daar valt iets voor te zeggen. De verschillen tussen *low* en *high code* zijn ingrijpend.


In lijn met het bovenstaande, legt *low code development* een ontwikkelaar absoluut bepaalde beperkingen op in het oplossen van problemen. Sterker nog, de beperkingen zijn dusdanig ingrijpend, dat mijn meer argwanender collega's ervoor terugdeinzen het überhaupt nog software ontwikkelen te noemen! 


Maar in zekere zin zijn deze beperkingen maar incidenteel. Hoewel Martins paradigma's allen met beperkingen gepaard gaan, is het de vraag of beperkingen überhaupt een manier van ontwikkelen tot een paradigma verheffen.


Het volgende argument is volgens mij sterker. Je zou kunnen stellen dat programmeren tot dusverre een in wezen talige bezigheid was. *Low code development* is daarentegen visueel van aard. Anders gezeg: "ouderwets" programmeren is wat je een lineaire bezigheid zou kunnen noemen. Klassieke code dient van boven naar beneden gelezen te worden. *Low code* neemt afscheid van die traditie. Programma's in elkaar klikken is iets wezenlijks anders dan ze van boven naar beneden lezen. 


Het zou zomaar kunnen we over tien jaar zeggen dat er een periode vóór en na *low code* is. 


## Continuïteit


Maar aan de andere kant...


Kuhns theorie van wetenschappelijke revoluties, en met name zijn notie van incommensurabiliteit, is omstreden. Er bestaan twijfels over de vraag of de grens tussen twee wetenschappelijke paradigma's wel zo scherp is als dat Kuhn ze presenteert. Wie inzoomt op de overgang, zoals Kuhn, ziet met name conflict tussen verschillende wetenschapsopvattingen. Maar wie verder uitzoomt, ziet ook een belangrijke mate van continuïteit.


Hetzelfde kan gezegd worden van de overgang van *high code* naar *low code*. Het in elkaar klikken van componenten lijkt op het eerste gezicht iets totaal anders dan het schrijven van regels code. Maar vanuit een andere hoek kan deze manier van software ontwikkelen worden gezien als een voortzetting van de lang geleden ingezette opmars van abstracties. (Ik ontleen dit punt aan [Tim Corey](https://www.youtube.com/watch?v=ah1tEvAkojI).)


Immers, *high code* ontwikkelaars schrijven ook niet al hun code zelf. In wezen zijn programmeertalen een abstractielaag over [IL-code](https://en.wikipedia.org/wiki/Intermediate_representation), en IL-code is weer een abstractielaag over [machinecode](https://en.wikipedia.org/wiki/Machine_code). Ook de [standaard-libraries van bijvoorbeeld .NET](https://en.wikipedia.org/wiki/List_of_.NET_libraries_and_frameworks) bieden ontwikkelaars abstracties waar ze mee kunnen werken, zodat ze niet zelf alles hoeven uit te programmeren.


Wat is *low code* anders dan een extreme abstractielaag over wat in wezen niet meer dan "ouderwetse" code is? Het is maar de vraag of *low code development* ontwikkeling een radicaal andere manier van denken vereist ten opzichte van *high code development*.


## Conclusie


Alle theoretische overwegingen ten spijt, zal dit vraagstuk niet beslecht worden in blogs, maar op de werkvloer. Of *low code development* als een nieuw ontwikkelparadigma moet worden gezien, zal afhangen van de mate waarin deze manier van ontwikkelen succesvol blijkt te zijn. Pas als deze praktijk in de breedte opgepakt wordt, de kinderziektes eruit zijn gefilterd en het product volwassen is geworden, kan hier iets zinnigs over gezegd worden.


Dit klinkt misschien als een ontwijkend antwoord, maar dat is schijn. De adoptie van een bepaalde praktijk is een essentieel onderdeel van de status als paradigma. Immers, als helemaal niemand de theorie van Copernicus zou hebben omarmd, zou er ook geen sprake zijn geweest van een Copernicaans pardigma. Dat is nu juist de Kuhniaanse les.
