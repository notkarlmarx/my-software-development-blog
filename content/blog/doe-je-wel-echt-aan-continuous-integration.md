---
title: "Doe je wel écht aan continuous integration?"
author: "Karl van Heijster"
date: 2023-07-14T10:21:21+02:00
draft: true
comments: true
tags: ["conferenties", "continuous integration", "procesverbetering", "teamcultuur", "trunk-based development"]
summary: "Clare Sudbery stelde een goede vraag op GOTO Amsterdam: doe je écht aan *continuous integration* (CI), of denk je dat alleen maar? Dat roept de vraag op: wat is \"echte\" CI?"
---

[Clare Sudbery](https://www.linkedin.com/in/clare-sudbery-she-her-35939540/) stelde een goede vraag op [GOTO Amsterdam](https://gotoams.nl/2023): doe je écht aan [*continuous integration*](https://en.wikipedia.org/wiki/Continuous_integration "'Continuous integration', Wikipedia") (CI), of denk je dat alleen maar?


Dat roept de vraag op: wat is "echte" CI -- of liever: wat is CI zoals het oorspronkelijk bedacht is? Volgens Sudbery voldoet volbloed CI aan drie voorwaarden:


1. Elke ontwikkelaar commit dagelijks naar een gedeelde *main* branch.
2. Elke commit trapt de build en de tests af.
3. Wanneer een commit de build breekt, dan is de build binnen tien minuten teruggebracht naar een correcte staat.


Wat bleek: de zaal *dacht* vooral aan CI te doen. Sudbery vroeg iedereen die aan CI deed z'n hand op te steken. Als je niet aan een voorwaarde voldeed, moest je 'm laten zakken. Na de eerste voorwaarde viel de helft van de handen weg. Na de derde was er nog maar één over. 


Hij kreeg een welgemeend applaus van het publiek.


## Mijn team


En inderdaad, ook in mijn team doen we -- klaarblijkelijk -- niet écht aan CI. Hoewel we heus wel ons best doen om onze code zo snel mogelijk te integreren in de *main* branch, werken we vaak enkele dagen aan nieuwe functionaliteit op een een featurebranch. En als een commit de build breekt, dan wil het wel eens elf of twaalf minuten duren voordat we de oorzaak van de fout hebben gevonden -- soms langer. 


Iets langer. Heel soms.


De enige voorwaarde waar we echt aan voldoen, is #2. Dat is misschien ook wel de eenvoudigste. Wie zijn [*build pipeline*](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/what-is-azure-pipelines "'What is Azure Pipelines?', Microsoft documentatie") één keer goed inricht, heeft daar gedurende de hele levensduur van het project plezier van. (Al wil ik niet de indruk wekken dat het inrichten van een *pipeline* een eenmalige actie is. Mijn team voegt regelmatig nieuwe stappen toe, of splitst bepaalde stappen op, of verwijdert stappen die door nieuwe ontwikkelingen overbodig zijn geworden. Net als code is een *pipeline* een levend ding.)


## Waarom CI?


Er ligt nog een vraag achter Sudbery's vraag, natuurlijk: waarom zou je überhaupt CI willen doen? Uit de [*State of DevOps Reports*](https://dora.dev/) die de laatste jaren verschenen, blijkt keer op keer dat snelheid een constante is in de best functionerende softwareteams ter wereld. Hoe eerder een team nieuwe functionaliteit naar de productieomgeving weet te brengen, des te sneller kunnen ze feedback vergaren, en des te sneller kunnen ze hun product verbeteren.


Test-Driven Development (TDD) is één van de manieren waarop je de ontwikkelsnelheid van een team kunt verhogen -- zonder te beknibbelen op kwaliteit. CI is een andere manier. Hoe sneller je nieuwe features in de bestaande code integreert, des te minder tijd ben je kwijt aan het oplossen van mergeconflicten, en des te meer kun je je focussen op de code.


[*Accelerate*](https://www.oreilly.com/library/view/accelerate/9781457191435/) van [Nicole Forsgren](https://nicolefv.com/), [Jez Humble](https://www.linkedin.com/in/jez-humble/) en [Gene Kim](https://www.linkedin.com/in/realgenekim/) schijnt een *must read* te zijn op dit gebied. Maar de eerlijkheid gebiedt me te zeggen dat het boek al tijden op mijn leeslijstje staat, maar dat ik er zelf nog altijd niet aan toegekomen ben.


## Trunk-Based Development


Terug naar Sudbery. Hoe zorg je ervoor dat je als team echt continu met elkaar integreert? Eenvoudig: door maar één branch te hebben. En elke ontwikkelaar pusht zijn of haar wijzigingen continu -- het zit 'm al in de naam -- naar die branch. Er is een naam voor die stijl van ontwikkelen: [*Trunk-Based Development*](https://trunkbaseddevelopment.com/) (TBD).


Voor kleine teams betekent dat een definitief afscheid van feature branches. Alle wijzigingen worden rechtstreeks naar *main* gepusht. Voor grotere teams worden feature branches getolereerd, maar die mogen niet langer dan een dag bestaan -- of, in het uiterste geval, enkele dagen. 


Het doel is: mergeconflicten voorkomen door ze onmogelijk of zo klein mogelijk te maken. Wie continu *main* binnenhaalt en continu wijzigingen weer terugstuurt, elimineert zoveel mogelijk frictie die rondom die wijzigingen ontstaat.


Des te sneller vinden je wijzigingen hun weg naar *main*, en des te sneller staan ze op de productieomgeving. 


## Zilveren kogel?


Betekent dat dat TBD een zilveren kogel is die een team in staat stelt snel en hoogwaardig nieuwe features uit te rollen? Nee en ja.


Nee, want TBD op zichzelf garandeert niet dat het proces van software ontwikkelen op het juiste niveau is om continu te kunnen integreren in *main*. Sudbery was er heel duidelijk over: TBD veronderstelt een bepaalde teamcultuur. Je kunt geen TBD doen zonder *pair programming* en zonder goede geautomatiseerde testsuite -- het liefst ontwikkeld middels Test-Driven Development (TDD). Want de wijzigingen zullen in [veel meer, veel kleinere stapjes](https://www.geepawhill.org/2021/09/29/many-more-much-smaller-steps-first-sketch/ "'Many More Much Smaller Steps – First Sketch', GeePaw Hill") naar *main* moeten worden gebracht, wil TBD kunnen werken.


Betekent dat dat je past kunt TBD toe kunt passen nadat je teamcultuur een bepaalde vorm heeft? Niet per se -- TBD zou immers ook de impuls kunnen geven meer te *pairen*, meer tests te schrijven, kleinere stapjes te nemen. Uiteraard veronderstelt dat op zijn beurt weer een teamcultuur waarin mensen open staan om te proberen dingen op een andere manier aan te pakken dan voorheen -- en waarin de ruimte wordt geboden om dat soort experimenten te ondernemen.


## Aantekening


Zie ik mogelijkheden om TBD te introduceren op mijn werk? Ik twijfel. Op de tweede conferentiedag pende ik de volgende aantekening neer:


> **Wat vind ik van *Trunk-Based Development* (TBD)?**
>
> 1. Geen PR's meer. Dat is (gedeeltelijk?) goed nieuws, je kunt dit met *pairen* ondervangen.[^1] Maar dat moet wel in de cultuur van je team passen.[^2]
>
> 2. TDD is noodzakelijk om dit te kunnen laten werken. Mijn team is daar nu nog niet -- de codebase zou snel degenereren.[^3] -- Misschien is het goed hen dit juist te laten ervaren? -- Maar zouden ze daar de juiste les uit trekken? 
>
> 3. Features die onaf zijn zullen in de *main* branch terechtkomen. -- Hoe zou je dit als positief kunnen zien? De ultieme test voor code is hoe deze functioneert in PROD. 
>
> 4. Stimuleert het code te schrijven die functioneert voor zover het functioneert, i.e. geen bestaande code om zeep helpt? 
>
> 5. Het stimuleert misschien wel om kleine stapjes te nemen. Als je elke 10 minuten commit, dan moet je er wel voor zorgen dat het elke 10 minuten werkt, je code. Dat voor elkaar krijgen is een grote uitdaging. Het vraagt een heel andere manier van coderen -- van jezelf, van het hele team. -- Het kan wel, die kleine stapjes, dat heb ik eigenhandig ervaren.[^4] 
>
> 6. Dit introduceren in het team is een langdurig proces. Het maakt pairen ook essentieel, want maar weinig [nieuwe] programmeurs zullen zo [i.e. in kleine stapjes] werken.


## Moeten?


Maar een net zo terecht vraag is: *moet* je TBD introduceren op je werk? -- Nee, erger nog: moet je TBD introduceren op je werk *alleen maar omdat je je dit op een conferentie hebt laten vertellen*? Die vraag stelde [Joris Kuipers](https://www.linkedin.com/in/jkuipers/) zich dezelfde dag nog tijdens zijn keynote. En zijn antwoord was duidelijk: -- nee!


Want conferenties zijn er om je te inspireren om nieuwe dingen te proberen -- niet om je ertoe te bewegen nieuwe technieken en praktijken te introduceren "omdat dat zo moet." 


Er is niet één manier om software te ontwikkelen. Het proces van software ontwikkelen dat je hanteert, moet passen bij je team en organisatie. 


Het gaat er dus niet om of je "echt" CI doet of niet. Het gaat erom dat je zo efficiënt mogelijk waarde levert met je code. De echte vraag is dus: zie je -- in jouw specifieke context -- kansen om meer waarde te leveren door CI en TBD te omarmen?


[^1]: [Dave Farley](https://www.davefarley.net/) is dezelfde mening toegedaan, ik schreef er [hier](/blog/23/01/wel-code-reviews-geen-pull-requests/) over. Een collega van Sudbery verwoordde de kritiek op PR's overigens heel beeldend: PR's gebruiken in een vast team dat op dezelfde locatie werkt, is als je familie vragen door de luchthavenbeveiliging te gaan, elke keer als ze je huis binnen komen. Het is op zijn best onnodig en toont op zijn slechtst een gebrek aan vertrouwen. 

[^2]: Het schrikbeeld dat ik in [deze blog](/blog/23/07/de-tester-als-code-reviewer/) zat op het moment van schrijven nog vers in mijn geheugen.

[^3]: Zie met name [deze blog](blog/23/04/tijdreis/).

[^4]: De beste manier om jezelf tot kleine stappen te dwingen, is door te TDD'en. Ik schreef er [hier](/blog/22/04/een-test-per-keer/) en [hier](/blog/22/06/mijn-eerste-testgedreven-stapjes/) over.
