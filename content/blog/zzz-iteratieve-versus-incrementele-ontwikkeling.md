---
title: "Iteratieve Versus Incrementele Ontwikkeling"
author: "Karl van Heijster"
date: 2021-06-21T12:15:20+02:00
draft: true
comments: true
tags: []
summary: ""
---

Als ik geen zin heb om over software ontwikkeling te lezen [tijdens mijn ontbijt](/blog/21/05/lees-elke-dag-een-kwartier-over-je-vak), zet ik een filmpje op YouTube op. Laatst keek ik deze van software architect [George Fairbanks](https://www.georgefairbanks.com/) over het minimaliseren van [technische schuld](https://en.wikipedia.org/wiki/Technical_debt):

{{<youtube id="REd5AUlcAh8" title="How to Minimize Your Technical Debt" >}}
<br/>
Ik at die ochtend afbakbroodjes met jam, als ik het me goed herinner. Het was dus in meerdere opzichten een prima ochtend.


## Twee ontwikkelprocessen


Fairbanks haalt in zijn video een bekend onderscheid aan tussen incrementele en iteratieve ontwikkeling aan. 


Bij incrementele ontwikkeling bouw je één bepaalde oplossing gedurende een lange periode steeds iets verder uit. Die ene oplossing is bedoeld om een bepaald probleem in zijn totaliteit op te lossen. Merk op dat je voor deze oplossingsrichting een redelijk compleet beeld moet hebben van het probleem, voordat je begint te bouwen.


Iteratieve ontwikkeling kent die beperking niet. Bij iteratieve ontwikkeling bouw je elke keer een zo simpel mogelijke oplossing voor een probleem *zoals je deze op dat moment begrijpt*. Dat presenteer je aan je opdrachtgever, degene met het probleem. Accepteert deze de oplossing, dan ben je klaar. 


Maar waarschijnlijk is je oplossing te simpel, en blijven bepaalde niet-triviale aspecten van het probleem in stand. Je volgende increment is een zo simpel mogelijke oplossing voor het oorspronkelijke probleem, plus de meest prangende van die niet-opgeloste aspecten.


Dat zijn redelijk wat woorden om het verschil uit te leggen, maar deze illustratie van [Henrik Kniberg](https://www.crisp.se/konsulter/henrik-kniberg) is er meer dan duizend waard:


{{<figure src="https://blog.crisp.se/wp-content/uploads/2016/01/mvp.png" width="600" alt="Henrik Kniberg: Making sense of MVP (Minimum Viable Product)" >}}


Niet voor niets hangt deze op ons kantoor (en die van een boel andere bedrijven, stel ik me zo voor).


## Incrementieve ontwikkeling?


Knibergs illustratie is bepaald niet ambigu in zijn boodschap: incrementele ontwikkeling valt te verkiezen boven iteratieve. Toch is iteratieve ontwikkeling niet per se de norm. Ook niet bij ons op kantoor, alle wanddecoratie ten spijt. 


Fairbanks merkt in zijn video op - en dit is ook mijn ervaring - dat software ontwikkeling in de praktijk een combinatie van beide is. Dat betekent echter niet dat daarmee automatisch het beste van beide werelden gecombineerd wordt.


Het voordeel van iteratieve ontwikkeling is dat het ontwerp van de oplossing consistent is. Dit is ook logisch: het ontwerp is immers grotendeels op voorhand uitgedacht. Concreet betekent dit bijvoorbeeld dat bepaalde stukken code in eerste instantie zijn opgezet met later hergebruik in het achterhoofd.


Je ziet het ook terugkomen in de illustratie van Kniberg. Het wiel dat in de eerste iteratie is ontwikkeld, blijft gehandhaafd gedurende de volgende drie.


Het voordeel van incrementele ontwikkeling is dat je snel in kunt spelen op nieuwe problemen die opkomen tijdens de ontwikkeling. Maar het gevolg hiervan is dat het ontwerp van increment tot increment volledig om kan worden gegooid. 


Ook dit komt terug in de illustratie. Het wiel dat in het eerste increment is ontwikkeld, kan misschien nog worden hergebruikt in het tweede, maar verdwijnt volledig uit beeld in de daaropvolgende.


Wie iteratieve en incrementele ontwikkeling probeert te combineren, wil nogal eens eindigen met een auto met skateboardwieltjes. Of een skateboard met autobanden eronder, daar wil ik vanaf zijn.


## ...


Incrementele en iteratieve ontwikkeling staan op gespannen voet met elkaar. Het vergt inspanning om beide met elkaar te *kunnen* verenigen. 


Maar het kan, betoogt Fairbanks. De truc is te weten wanneer je iteratief bezig moet zijn, en wanneer incrementeel. Of anders gezegd: wanneer je bezig moet zijn met het ontwerp van je applicatie, en wanneer je nieuwe features moet toevoegen om een probleem op te lossen. 


Je kunt beide doen, alleen niet tegelijkertijd.


Laat ik Knibergs illustratie nog één keer als voorbeeld gebruiken. Om het wiel uit de eerste twee incrementen (aangenomen dat het ruwweg hetzelfde wiel is) te kunnen hergebruiken in increment drie, moet er eerst een tijd wat inspanning worden gestoken in het ontwerp. Het wiel moet van de step worden gedemonteerd en aangepast, wil het in de derde increment kunnen fungeren. 


Sterker nog, grote delen - waarschijnlijk het overgrote deel - van dat wiel zullen moeten worden weggegooid. Het nieuwe wiel zal grotendeels van de grond af aan worden opgebouwd. Het oorspronkelijke wiel heeft *geen plek* in het derde increment. Althans, niet letterlijk.


Dat lijkt inefficiënt, en in zekere zin het dat ook. Idealiter zou je het wiel nooit hebben hoeven vervangen, omdat je op voorhand al wist hoe het er uiteindelijk uit zou moeten komen te zien. Maar iedereen die ooit als softwareontwikkelaar heeft gewerkt, weet dat de werkelijkheid zich verre houdt van het ideaal. Deze inefficiëntie is het gevolg van het roeien met de riemen die je hebt.


Vraag jezelf eens af: is het inefficiënt om een stuk van de applicatie vrijwel van de grond af aan opnieuw op te bouwen met je nieuwe inzichten? Is het efficiënter om een stuk code te hergebruiken dat eigenlijk niet goed past?


Het wiel uit de eerste twee incrementen heeft geen letterlijke plek in de derde increment, maar is daar nog wel in aanwezig *als [spoor](https://en.wikipedia.org/wiki/Trace_(deconstruction))*.[^1] Het wiel was een stapsteen naar een betere implementatie. Het diende een dubbel doel: waarde leveren gedurende de eerste twee iteraties, en bron van gestold inzicht zijn gedurende derde.


...


Er is een te grote focus op het hergebruiken van code die je in eerdere incrementen hebt geschreven. Dit zorgt ervoor dat je applicatie zich op een manier ontwikkelt die vreemde architecturen met zich meebrengt. 


[^1]: Maak ik filosofisch onverantwoord misbruik van de term van [Jacques Derrida](https://en.wikipedia.org/wiki/Jacques_Derrida)? Ongetwijfeld, maar postmoderne Franse filosofie is ook nooit mijn sterkste punt geweest.
