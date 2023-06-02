---
title: "Objectgeoriënteerd programmeren draait niet om objecten"
author: "Karl van Heijster"
date: 2023-06-02T07:57:24+02:00
draft: false
comments: true
tags: ["actor-model", "mentaal model", "objectgeoriënteerd programmeren", "paradigma's"]
summary: "Van Anjana Vakil leerde ik een interessante les: objectgeoriënteerd programmeren draait niet om objecten, het draait om het uitwisselen van informatie."
---

Van [Anjana Vakil](https://anjana.dev/) leerde ik een interessante les: [objectgeoriënteerd programmeren](https://en.wikipedia.org/wiki/Object-oriented_programming) (OOP) draait niet om objecten, het draait om het uitwisselen van informatie. Maar luister vooral naar haar zelf:


{{<youtube id="TbP2B1ijWr8" title="Object Oriented Programming is not what I thought -- Talk by Anjana Vakil" >}}
<br/>


(In [deze video](https://www.youtube.com/watch?v=Pg3UeB-5FdA) brengt Vakil hetzelfde punt naar voren in een wat bredere context van programmeerparadigma's. Hetzelfde punt wordt naar voren gebracht door [Dave Thomas](https://pragdave.me/) in [deze video](https://www.youtube.com/watch?v=kLnPXMoh0H8).)


## Objecten


Vakil brengt in haar praatje naar voren dat er bij OOP in de eerste instantie vaak wordt gedacht aan classes, de samenkomst van data en gedrag, overerving en compositie. Anders gezegd: er wordt gedacht aan objecten en de verschillende manieren waarop deze met elkaar samenhangen.


Helemaal onterecht is dat natuurlijk niet, want het woord "object" zit in de naam nota bene. En daar zit ook precies het probleem, *dixit* [Alan Kay](https://nl.wikipedia.org/wiki/Alan_Kay), de naamgever van het paradigma. Want de naam suggereert dat object-zijn hét definiërende kenmerk is van OOP. 


Het suggereert dat je classes een voorwerp in de wereld representeren dat bepaalde eigenschappen heeft -- vastgelegd in *private fields* -- en dat een zeker gedrag kan vertonen -- vastgelegd in *methods*. Ik heb [elders op deze blog](/blog/23/01/eerlijke-domeinmodellen/) eens een parallel getrokken met de substantieleer van [René Descartes](https://plato.stanford.edu/entries/descartes/) -- dat is waar objecten mij als filosoof aan doen denken. 


## Cellen


Maar Kay haalde zijn inspiratie ergens anders vandaan. Als biologiestudent vergeleek hij objecten met cellen. Cellen hebben een kern en een membraan waarmee ze met de buitenwereld communiceren. Het membraan bepaalt welke informatie de celkern bereikt en welke niet.[^1]


De data van een object -- haar *private fields* -- zijn vergelijkbaar met de celkern. En de communicatie met de buitenwereld, het membraan, dat is waar de *methods* voor bedoeld zijn. De voor het object interessante data die in de buitenwereld bestaat, wordt via deze publieke ingang op de private data van het object overgebracht.


Een object beschrijft niet een ding in de wereld met bepaalde eigenschappen. Het is een houder van informatie die op een bepaalde manier met de buitenwereld communiceert.


## Auto's


De *methods* op een object geven niet aan: "Dit is wat ik als object allemaal kan." Ze geven aan: "Als je de informatie in mijn kern wil wijzigen, dan moet je dat via deze weg doen." 


`car.Drive()` zegt niet: "Deze auto gaat nu rijden." Het zegt: "Ik, de aanroepende code, instrueer deze auto nu te gaan rijden." Om te kunnen rijden moet de auto wat aan zijn interne toestand veranderen. Wat daar precies bij komt kijken, dat is voor andere objecten niet interessant. -- En dat is waarom deze informatie in tot de kern van de auto behoort en niet tot die van een ander object.


Is dat verschil subtiel? Misschien. Heeft het verstrekkend gevolgen? Geen idee. -- Daar hoop ik in de toekomst op terug te kunnen komen.


## *Actors*


Eén concreet gevolg heeft dit nieuwe [mentale model](/blog/22/08/wat-is-jouw-mentale-model/) wel al gehad. 


Een tijd terug op [Future Tech](https://futuretech.nl/) hoorde van het [*actor*-model](https://en.wikipedia.org/wiki/Actor_model). Dit model is geïntroduceerd om om te kunnen gaan met *mutable state* in de wereld van gedistribueerde en parallelle processen. Er bestaan verschillende frameworks die het *actor*-model implementeren, zoals [Akka.NET](https://getakka.net/) en [Microsoft Orleans](https://learn.microsoft.com/en-us/dotnet/orleans/overview). Het idee is dat bepaalde objecten -- Actors in Akka.NET, Grains in Orleans -- verantwoordelijk zijn voor *mutable state*, en dat andere *actors* deze alleen kunnen veranderen door een bericht naar die objecten te sturen.


Gedurende de conferentie kon ik de gedachte niet onderdrukken dat het achterliggende idee precies hetzelfde was als bij classes -- alleen de toepassing ervan was op een andere schaal. Immers, ook een *actor* is, net als een class, een houder van informatie die via berichten communiceert met andere *actors* c.q. classes.


## Observeren


Dat gezegd hebbend, ik heb nog nooit *hands on* met het *actor*-model gewerkt, dus in hoeverre die overeenkomsten in de praktijk standhouden, durf ik niet te zeggen. De bedoeling van deze blog is ook niet te zeggen dat classes en *actors* één en hetzelfde zijn. De bedoeling is veeleer: observeren welke aspecten deze "nieuwe" manier van OOP bezien naar voren brengt. 


Stel jezelf eens de vraag: hoe zag jij OOP? En hoe zie je het nu?  


[^1]: Ik geef toe: ik heb geen idee of cellen daadwerkelijk zo werken -- biologiestudenten, *don't @ me* --, maar daar gaat het me nu ook niet om. Het gaat me om het mentale model via welke we objecten in OOP moeten bezien.
