---
title: "Presenteren voor programmeurs"
author: "Karl van Heijster"
date: 2021-07-05T08:38:35+02:00
draft: false
comments: true
tags: ["communicatie", "Developer Meet-up", "presenteren"]
summary: "Ik zal niet beweren dat ik een ster ben in presenteren. Maar vergeleken met mijn collega-ontwikkelaars steek ik klaarblijkelijk niet slecht af. Dat heeft denk ik alles te maken met het feit dat ik mijn publiek meeneem in mijn voorbereiding, en iets van mezelf in zo'n presentatie probeer te leggen. Laatst, bijvoorbeeld, toen ik de intro van de eerste teamoverstijgende *Developer meet-up* aan elkaar mocht praten."
---

Ik zal niet beweren dat ik een ster ben in presenteren. Maar vergeleken met mijn collega-ontwikkelaars steek ik klaarblijkelijk niet slecht af. Dat heeft denk ik alles te maken met het feit dat ik een presentatie, eh, voorbereid.


Nee, dat is te gechargeerd. Ik wil mijn collega's er niet van beschuldigen hun presentaties niet voor te bereiden. Wat ik bedoel is: ik neem mijn publiek mee in mijn voorbereiding, en ik probeer iets van mezelf in zo'n presentatie te leggen.


Het eerste punt is essentieel voor een goede presentatie. Wie zijn presentatie niet afstemt op zijn publiek, loopt het risico om, in aanwezigheid van anderen, voor alleen zichzelf te presenteren. Dit gebeurt bijvoorbeeld wanneer een softwareontwikkelaar een enorm technisch verhaal op gaat hangen tijdens een Sprint Review.


Het tweede punt is datgene wat een presentatie net dat beetje extra kan geven. Dat kan op allerlei manieren - het is niet voor niets iets van jezelf. Omdat ik ten minste de helft van de tijd haast omval van meligheid, probeer ik daar waar het gepast is, een beetje humor in te brengen.


## Developer meet-up


Een voorbeeld. Onlangs organiseerden een paar collega's en ik iets wat we een *Developer meet-up* hebben genoemd: een informele en het liefst interactieve bijeenkomst waarin een aan softwareontwikkeling gerelateerd onderwerp centraal staat. 


Het was aan mij om het intropraatje van die meet-up te doen.


Het publiek bestond uit collega-ontwikkelaars. Het doel was tweeledig. Ten eerste moest ik hen het informeren over de gang van zaken van deze en komende meet-ups. Ten tweede wilde ik een luchtige, liefst gezellige sfeer creëren. 


Mijn presentatie bestond in essentie uit drie delen: (1) een uitleg van het idee achter de meet-ups, (2) een oproep om daar actief aan bij te dragen, en (3) een voorstelrondje van de aanwezigen. 


Het humoristische gedeelte van mijn brein ziet dus (ten minste!) drie gelegenheden voor een grapje.


### Waarom zijn we hier?


De uitleg van het idee achter de meet-up introduceerde ik met een vraag: *Waarom zijn we hier?* Die vraag ondersteunde ik met een afbeelding van een man die naar de sterrenhemel kijkt. 


{{<figure src="https://www.maxpixel.net/static/photo/1x/Night-Sky-Starry-Night-Starry-Sky-Silhouette-1149815.jpg" alt="Afbeelding van een man die naar de sterrenhemel kijkt" width="600">}}


Die keuze verraste mij ook. Ik zette een zo existentieel mogelijk gezicht op en zei: "O... Dat is wel erg diep, ineens." 


Ik vervolgde: "Ik bedoelde het eigenlijk meer zo..." en verving de sterrenhemel door illustratie van een online vergadering. Voor het komisch effect plakte ik die een beetje scheef over de oorspronkelijke afbeelding heen.


Pas daarna vertelde ik over het doel van de bijeenkomst.


Je publiek monitoren tijdens een online vergadering is een uitdaging, dus ik durf niet te stellen dat het publiek krom lag tijdens deze sectie. Maar al heb ik misschien geen lachers op mijn hand gekregen, misschien heb ik wel iemand in een existentiële crisis gestort, en dat is ook wat waard.


### We kunnen dit niet alleen!


De oproep actief bij de dragen aan de meet-ups, introduceerde ik met een uitroep: *We kunnen dit niet alleen!* Het was voor mij een open deur om deze oproep te ondersteunen van een afbeelding van [Uncle Sam](https://nl.wikipedia.org/wiki/Uncle_Sam). 


{{<figure src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Uncle_Sam_%28pointing_finger%29.jpg/800px-Uncle_Sam_%28pointing_finger%29.jpg" alt="Afbeelding van Uncle Sam" width="300">}}


Het bijschrift was een variatie op het beroemde origineel: *WE WANT YOU to deel met ons wat jou enthousiast maakt over softwareontwikkeling*.


De laatste bullet van mijn dia luidde: *Wacht ~~geen~~ een moment (tot deze sessie voorbij is)!* Als iedereen onmiddellijk enthousiast z'n ideeën de ether in zou slingeren, zou het immers maar een chaos worden.


### Voorstelrondje


Voor het voorstelrondje leek het me wel leuk als iedereen iets zou vertellen over wat diegene enthousiast maakt in softwareontwikkelland. Dat maakt het voorstelrondje wat minder stijfjes en heeft een verbroederende werking. Bovendien sloot het goed aan bij het idee achter de meet-up.


Achteraf hoorde ik van een medeorganisator dat dit een riskante move was, die ik absoluut niet bij managers had moeten proberen, wilden we nog aan de eigenlijke sessie toekomen. Waarvan akte.


Omdat ik geen zin had om het voorstelrondje te coördineren, vroeg ik aan de aanwezigen om zelf de volgende persoon aan te wijzen. En omdat het ontwikkelaars betrof, leek het me een goed idee ze dit uit te leggen in een taal die zij begrijpen:


```csharp
var participants = GetParticipants();
var index = 0;

while (participants.Any(p => !p.Introduced))
{
    var participant = participants[index];

    participant.Introduce();
    participant.NameThingThatExcitesMe(
        Subject.SoftwareDevelopment);
    participant.Introduced = true;

    index = participant.ChooseNext(
        participants.Where(p => !p.Introduced));
}
```


Als ik mijn innerlijke [Ivo Niehe](https://www.youtube.com/watch?v=guPLHRacjZs) channel, dan kan ik niet ontkennen dat ik dit een gouden vondst van mezelf vond. (En als ik eerlijk ben, was het schrijven van deze blog voornamelijk een excuus om dit stukje code te laten zien.) De twee doelen van de presentatie én de twee punten uit de intro komen hier bijeen. 


## Unaniem een belachelijk groot succes


Nu zal ik de laatste zijn die zal beweren dat het succes van de Developer meet-up af heeft gehangen van mijn melige presentatiestijl. Maar feit is dat de eerste bijeenkomst positief werd beoordeeld door de aanwezigen. Een bericht op het intranet omschreef de meet-up zelfs als "unaniem een belachelijk groot succes!"


Dat ik dat bericht zelf geschreven heb, doet daar volgens mij maar minimaal aan af. Soms is een succesvolle presentatie geven ook een beetje een kwestie van positieve herinneringen implanteren in het collectieve geheugen.


Wat doe jij om een presentatie tot een succes te maken?
