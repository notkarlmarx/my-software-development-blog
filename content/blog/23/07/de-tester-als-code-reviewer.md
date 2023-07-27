---
title: "De tester als code reviewer"
author: "Karl van Heijster"
date: 2023-07-14T07:54:13+02:00
draft: false
comments: true
tags: ["code reviews", "pair programming", "procesverbetering", "pull requests", "samenwerking", "shift left", "software ontwikkelen", "testen", "tester (rol)", "verantwoordelijkheid"]
summary: "Mijn team heeft onze tester onlangs tot verplichte reviewer gemaakt voor elk *pull request* (PR). Hij heeft een heel specifieke opdracht -- drie, eigenlijk: 1. Ga na of het PR unit- of integratietests bevat. Zo nee, keur het PR dan af. 2. Ga na of je de unit- en/of integratietests kunt begrijpen. Zo nee, keur het PR dan af. 3. Ga op basis van de unit- en/of integratietests na of de code werkt zoals bedoeld. Zo nee, keur het PR dan af. Pas als aan alle drie voorwaarden is voldaan, is het PR klaar om naar de main branch te mergen."
---

Het is dinsdag. Je sleept een taak op de Sprint Backlog van *to do* naar *doing* en duikt in de code. Eén, twee, drie uur later start je de applicatie op, je klikt wat rond en concludeert: het werkt. Dus je maakt een *pull request* (PR) aan. Die staat de hele middag te wachten.


Het is woensdag. Je trekt je collega aan z'n jas, of 'ie even naar dat PR van gister wil kijken. Dat wil 'ie heus wel, maar hij is ook druk met zijn eigen werk. Dus je collega bekijkt de boel diagonaal -- een formaliteit, want hij wil graag geloven dat je heus wel weet waar je mee bezig bent. Hij keurt het PR goed. De boel wordt naar Test uitgerold -- dat duurt een goede twintig minuten. De tester kan er naar kijken.


Maar ook de tester is druk -- met al het testwerk dat je collega's hem hebben bezorgd. Dus de code blijft staan. Het is donderdag als 'ie er eindelijk aan toe komt. Hij start de applicatie op, klikt wat rond, en -- er gebeurt iets, iets wat 'ie niet verwacht. De waarden op het scherm kloppen niet, of er verschijnt een foutmelding -- of erger nog, de applicatie crasht. Dus hij maakt een bug aan en zet 'm op de Backlog.


Het is maandag eer je eraan toekomt die op te pakken.


Dat moet, zou je denken, efficiënter kunnen.


## Pair programming


En dat kan het ook. Eén van de dingen die je kunt doen, is ophouden met PR's en overstappen op pair programming (zie [deze blog](/blog/23/01/wel-code-reviews-geen-pull-requests/ "'Wel code reviews, geen pull requests'")). Sterker nog, op basis van [wat ik hoor](/blog/23/05/waarom-zou-je-naar-tech-podcasts-luisteren/ "'Waarom zou je naar tech podcasts luisteren?'") van verschillende experts in het vak, lijkt dit de beste oplossing te zijn voor dit probleem. 


Twee weten meer dan één, en daarom is code die je samen met een collega schrijft over het algemeen van hogere kwaliteit van code die je in je eentje schreef. -- En zelfs al is de kwaliteit hetzelfde, dan nog is er door te pairen winst geboekt op het vlak van kennisdeling.


Maar ik zeg er meteen bij: deze manier van werken kan om een behoorlijke cultuuromslag vragen. Veel ontwikkelaars -- ook ik -- zijn introvert en gehecht aan het ritueel zich in stilte (of [juist niet](/tags/muziek/ "Blogs met de tag 'muziek'")) vast te bijten in een netelig probleem. [Mijn goede voornemen meer te pairen](/blog/23/01/wel-code-reviews-geen-pull-requests/ "'Wel code reviews, geen pull requests'") is ergens in januari al ergens gestrand, ben ik bang.


## Code review


Maar ook als het team er (nog) niet klaar is voor is om over te stappen op pair programming, valt er hier genoeg te winnen. En die winst zit 'm in de fase van de code review.


Ik doel dan geeneens op de drukke ontwikkelaar die maar met een schuin oog naar het PR kijk -- hoewel daar natuurlijk ook winst te behalen valt, zie [deze](/blog/22/08/hoe-review-je-eigenlijk-code/ "'Hoe review je eigenlijk code?'") en vooral ook [deze blog](/blog/22/09/test-driven-code-reviews/ "'Test-Driven Code Reviews'").


Ik doel op het werk van de tester. PR's moeten niet langer een feestje (hoewel, feestje...) zijn van de ontwikkelaars. 


De tester moet code gaan reviewen.


## Opdracht


Mijn team heeft onze tester onlangs tot verplichte reviewer gemaakt voor elk PR. Hij heeft een heel specifieke opdracht -- drie, eigenlijk: 


1. Ga na of het PR unit- of integratietests bevat. Zo nee, keur het PR dan af.
2. Ga na of je de unit- en/of integratietests kunt begrijpen. Zo nee, keur het PR dan af.
3. Ga op basis van de unit- en/of integratietests na of de code werkt zoals bedoeld. Zo nee, keur het PR dan af.


Pas als aan alle drie voorwaarden is voldaan, is het PR klaar om naar de main branch te mergen.


Het is een zuiver voorbeeld van de [*shift left*](/tags/shift-left/ "Blogs met de tag 'shift left'")-gedachte. Waarom zou je wachten met het betrekken van de tester totdat je code op de testomgeving staat? Als deze in een eerder stadium al kan bijdragen aan het opkrikken van de kwaliteit van de code -- door bugs te spotten of (wat waarschijnlijker is) de aanwezigheid van tests überhaupt af te dwingen --, dan scheelt dat tijd, geld en moeite.


## Voorwaarden


Maar wil deze opzet slagen, dan moet er natuurlijk wel aan enkele voorwaarden worden voldaan. Ten eerste moet de tester code kunnen lezen. -- En dat is geen gegeven in de testwereld. Ik [sprak](/public-speaking/) onlangs (met veel plezier overigens!) op het [Voorjaarsevent](https://www.testnet.org/evenement/entry/6495/?evenement=voorjaarsevenement) van [TestNet](https://www.testnet.org/)[^1] en één van de dingen die me daar opviel, was hoe groot het aantal handmatige testers anno 2023 nog altijd is. 


Daar moet verandering in komen. Als we de kwaliteit van een systeem duurzaam willen waarborgen, dan zullen testers minimaal code moeten leren lezen. (En het liefst ook schrijven: waarom zou je tijd besteden aan het documenteren van een testplan als je die tijd ook in geautomatiseerde tests kunt steken?).


Maar niet alleen de testers zullen moeten veranderen. Ook ontwikkelaars zullen aan de slag moeten. Om de lasten niet eenzijdig bij de tester neer te leggen, zullen ze betere tests moeten schrijven. Ze zullen bijvoorbeeld meer aandacht moeten besteden aan de scope van hun tests. Deze moeten geschreven worden op een abstractieniveau dat geen kennis van de interne werking van het systeem vereist. Ik schreef er [hier](/blog/22/06/testen-via-de-voordeur/ "'Testen via de voordeur'"), [hier](/blog/22/12/tests-zijn-specs/ "'Tests zijn specs'") en [hier](/blog/22/11/test-het-systeem-niet-de-class/ "'Test het systeem, niet de class'") over. 


Ook de leesbaarheid zullen ze flink omhoog moeten klikken. Tests moeten *vertellen* wat het systeem doet; de lezer zou dat niet op basis van de tests moeten hoeven beredeneren. [Dit praatje](https://www.youtube.com/watch?v=D7LKslgwxmQ "Test Driven Development in JavaScript – writing tests that don’t suck! - David Whitney") van [David Whitney](https://davidwhitney.co.uk/) is een absolute aanrader op dat vlak. Zelf schreef ik er [hier](/blog/22/09/tests-als-documentatie/ "'Tests als documentatie'"), [hier](/blog/23/02/waarom-dry-waarom-damp/ "'Waarom DRY? Waarom DAMP?'"), [hier](/blog/22/12/over-de-volgorde-van-je-unit-tests/ "'Over de volgorde van je unit tests'") en [hier](/blog/23/03/testen-met-productiedata/ "'Testen met productiedata'") over.


## Nadeel?


Een kritische (en ongeduldige) ontwikkelaar zou tegen kunnen werpen dat de verplichte goedkeuring onze tester tot een *single point of failure* gemaakt heeft. Als hij druk is, of ziek, dan stapelen de PR's zich op zonder mogelijkheid om ze naar de main branch te kunnen mergen. 


Maar dat argument gaat volgens mij niet op. In geval van ziekte kan de verplichte goedkeuring omzeild worden, en bij drukte kan een ontwikkelaar met testaffiniteit de taak op zich nemen. In wezen is het niet belangrijk dat *de tester* de bovenstaande drie vragen afvinkt. Het is belangrijk dat dit überhaupt gebeurt. Ik benadruk de rol van testers slechts vanwege hun testaffiniteit, en de potentie die dat meebrengt om in een team het kwaliteitsgeweten te spelen. 


Daarnaast, in de meeste ontwikkelteams vormt de tester sowieso een *stage gate* die bepaalt of functionaliteit aan bepaalde kwaliteitseisen voldoet. Deze strategie haalt het moment waarop die bepaling plaatsvindt alleen naar voren. Het verandert de functie van de tester niet.


Bovendien zie ik het verplichte karakter van de goedkeuring ook niet als wezenlijk onderdeel van deze strategie. Het is een -- hopelijk tijdelijk -- middel dat de ontwikkelaars ertoe brengt het schrijven van geautomatiseerde tests als integraal onderdeel van hun werkwijze te gaan zien. In het ideale geval maakt het team zich deze werkwijze zodanig eigen, dat er geen tester én geen verplichting meer nodig is de aanwezigheid van leesbare tests af te dwingen -- dat is het uiteindelijke doel.


## Resultaat


Tot die tijd speelt de tester een belangrijke rol in het dichterbij brengen van dat streven. Ik ben overtuigd van de waarde die testers toe kunnen voegen aan een code review -- want ik heb het uit de eerste hand mogen ervaren. Deze strategie betaalde zich eigenlijk onmiddellijk al terug -- in die zin dat er vanaf dat moment ([wél](/blog/23/04/tijdreis/ "'Tijdreis'")) *standaard* tests werden toegevoegd aan elk PR.


(Het is een interessante observatie: ontwikkelaars -- in elk geval de ontwikkelaars in míjn team -- hadden de verplichte goedkeuring van een niet-ontwikkelaar nodig om het schrijven van tests in hun werkwijze op te nemen. Wat maakt dat wij ontwikkelaars niet in staat zijn ons zelf aan die standaard te houden?)


Er heeft in zekere zin een [paradigmawisseling](/blog/21/10/low-code-een-nieuw-paradigma/ "'Low code: een nieuw paradigma?'") plaatsgevonden. Een PR zonder tests is van regel naar uitzondering veranderd. De afwezigheid van tests moet tegenwoordig beargumenteerd worden, in plaats van dat de aanwezigheid ervan geprezen wordt. En dat komt de kwaliteit van het systeem ten goede.


[^1]: De slides van die presentatie zijn [hier](/talks/altijd-up-to-date-documentatie-met-maximaal-descriptieve-tests/ "'Altijd up to date documentatie met maximaal descriptieve tests'") te vinden.
