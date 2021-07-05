---
title: "Low Code: Een Nieuw Paradigma?"
author: "Karl van Heijster"
date: 2021-07-05T04:49:38+02:00
draft: true
comments: true
tags: []
summary: ""
---

Een deel van de teams in het bedrijf waar ik voor werk is overgestapt op dat wat *low code development* wordt genoemd. In plaats van applicaties regel voor regel met de hand te schrijven, klikken ze deze in elkaar met behulp van een tool.


Een deel van mijn collega's staat vijandig (?) tegenover deze ontwikkeling, en dat is niet helemaal onterecht. *Low code* ontwikkeling brengt wat antipatronen met zich mee, zoals *vendor lock* en *the last 10% trap*. En dan heb ik het nog niet eens over het feit dat een deel van het personeel opnieuw opgeleid moet worden om überhaupt op deze manier te kunnen ontwikkelen.


Tegelijkertijd heeft deze manier van softwareontwikkeling wel de potentie om de *time to market* van een product te verkleinen. Immers, een applicatie in elkaar klikken is, op het oog in elk geval, een stuk sneller gedaan dan deze helemaal zelf uit te coderen.


Ik zal het verder niet over de voor- of nadelen van *low code* hebben, want eerlijk gezegd heeft deze techniek zich wat mij betreft nog niet genoeg in de praktijk bewezen om daar met zekerheid iets over te kunnen zeggen. 


Waar ik het over wil hebben, is de manier waarop deze ontwikkelmethode zich verhoudt tot het "ouderwetse" programmeren (*high code*?). Meer specifiek: is *low code* ontwikkeling een nieuw ontwikkelparadigma of niet?


## Wat is een paradigma?


De term "paradigma" komt oorspronkelijk uit de wiskunde en betekent "standaardvoorbeeld" (BRON). De manier waarop ik de term gebruik, is echter ontleend aan de wetenschapsfilosofie, in het bijzonder *The Structure of Scientific Revolutions* van Thomas Kuhn.


Kuhn betoogt in zijn boek dat de wetenschap zich niet lineair ontwikkeld, namelijk als geleidelijke accumulatie van kennis. In plaats daarvan schetst hij een discontinu beeld. Wetenschap ontwikkeld zich gedurende perioden van "normale wetenschap" inderdaad op een lineaire manier. Maar van tijd tot tijd worden er wetenschappelijke theorieën naar voren gebracht die zo ontregelend zijn, dat ze een vakgebied op zo'n ingrijpende manier veranderen dat er niet meer van continuïteit gesproken kan worden.


Het standaardvoorbeeld (*pun intended*) van zo'n wetenschappelijke revolutie, is de Copernicaanse wending. Tot Copernicus werd aangenomen dat de aarde het middelpunt van het heelal was, waar de zon en de rest van de plateneten omheen draaien. De Copernicaanse wending bestaat erin dat hij deze voorstelling op zijn kop zet. Binnen het Copernicaanse model van het zonnestelsel, staat de zon in het middelpunt en draaien de overige planeten, waaronder de aarde, daaromheen.


Deze theorie veranderde de astronomie zo ingrijpend, dat er met recht gesproken mag worden van een periode vóór en na Copernicus.


Een ander voorbeeld van een paradigmawisseling vinden we in de 17e eeuw met de opkomst van de wetenschappelijke methode überhaupt. De tot dan toe heersende methode van wetenschappelijk onderzoek (als je het zo wil noemen), de aristotelische, ging ervan uit dat je de wereld het best kon bestuderen door deze louter te observeren. Wie ingrijpt in de natuur, lokt daarmee immers onnatuurlijk gedrag uit.


Sinds Descartes is dit beeld ingrijpend veranderd. Moderne wetenschappers leggen de natuur juist op de metaforische pijnbank. Ze creëren kunstmatige condities waar ze controle over hebben, om de relevante variabelen te kunnen extraheren. Die kunstmatigheid is juist een essentieel onderdeel van moderne wetenschapsbeoefening. Het is onderdeel geworden van het moderne wetenschapsparadigma.


(Merk op dat Kuhns wetenschapsopvatting zelf ook als paradigmawisseling in de wetenschapsfilosofie kan worden gezien. Vóór Kuhn lag de nadruk van dit vakgebied op het vinden van een aan de logica ontleende rechtvaardiging van het feit dat onze kennis zich vermeerdert. Kuhn veranderde de lens waarmee filosofen de wetenschap bekeken: van zuiver logisch- theoretisch naar overwegend historisch-praktisch.)


## Incomensurabiliteit


...


## Paradigma's in de softwareontwikkeling


Ook de softwareontwikkeling kent zijn eigen paradigma's. Programmeertalen kunnen bijvoorbeeld worden ondergebracht in een structureel, objectgeoriënteerd of een functioneel paradigma. Elk van die programmeerparadigma's beperkt de ontwikkelaar op de een of andere manier in zijn mogelijkheden in het schrijven van code (BRON: ROBERT MARTIN). En elk paradigma heeft zijn eigen standaardvoorbeelden van hoe een goed functionerend programma eruitziet.


Luidt *low code* ontwikkeling een nieuw paradigma in de softwareontwikkeling in? 


Die case valt te maken. *Low code* ontwikkeling legt een ontwikkelaar absoluut bepaalde beperkingen op, en past in die zin in het bovengenoemde rijtje.


Maar de verschillen tussen de voorgaande paradigma's en *low code* ontwikkeling zijn veel ingrijpender dan dat. Klassiek programmeren is in zekere zin een lineaire bezigheid: code dient van boven naar beneden gelezen te worden. *Low code* neemt afscheid van die traditie. Programma's in elkaar klikken is iets wezenlijks anders dan ze van boven naar beneden lezen. 


(UITWERKEN)


## Continuïteit


Kuhns theorie van wetenschappelijke revoluties, en met name zijn notie van incommensurabiliteit, is omstreden. Er bestaan twijfels over de vraag of de grens tussen twee wetenschappelijke paradigma's wel zo scherp is als dat Kuhn ze presenteert. Wie inzoomt op de overgang, zoals Kuhn, ziet met name conflict tussen verschillende wetenschapsopvattingen. Maar wie verder uitzoomt, ziet ook een belangrijke mate van continuïteit.


Hetzelfde kan gezegd worden van de overgang van *high code* naar *low code*. Het in elkaar klikken van componenten lijkt op het eerste gezicht iets totaal anders dan het schrijven van regels code. Maar vanuit een andere hoek kan deze manier van software ontwikkelen worden gezien als een voortzetting van de lang geleden ingezette opmars van abstracties. (Ik ontleen dit punt van Tim Corey (BRON).)


Immers, *high code* ontwikkelaars schrijven ook niet al hun code zelf. In wezen zijn programmeertalen een abstractielaag over IL-code, en IL-code is weer een abstractielaag over machinecode. Ook de standaard-libraries van bijvoorbeeld .NET bieden ontwikkelaars abstracties waar ze mee kunnen werken, zodat ze niet zelf alles hoeven uit te programmeren.


Wat is *low code* anders dan een extreme abstractielaag over wat in wezen niet meer dan ouderwetse code is?


Het is daarom maar de vraag of *low code* ontwikkeling daadwerkelijk andere vaardigheden vna je vraagt dan als *high code* ontwikkelaar.


## Conclusie


Of *low code* development als een nieuw ontwikkelparadigma moet worden gezien, zal afhangen van de mate waarin deze manier van ontwikkelen succesvol blijkt te zijn. Pas als deze praktijk in de breedte opgepakt wordt, de kinderziektes eruit zijn gefilterd en het product volwassen is geworden, kan hier iets over gezegd worden.


Dit klinkt misschien als een ontwijkend antwoord, maar dat is schijn. De adoptie van een bepaalde praktijk is een essentieel onderdeel van de status als paradigma. Immers, als helemaal niemand de theorie van Copernicus zou hebben omarmd, zou er ook geen sprake zijn geweest van een Copernicaans pardigma.
