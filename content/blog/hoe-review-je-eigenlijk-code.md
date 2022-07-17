---
title: "Hoe review je eigenlijk code?"
author: "Karl van Heijster"
date: 2022-07-15T22:47:34+02:00
draft: true
comments: true
tags: ["boeken", "code lezen", "code reviews"]
summary: "Hoe lees je eigenlijk code? Waar begin je? En in welke volgorde loop je code door? - En zit er verschil tussen het lezen van code tijdens je programmeerwerk en tijdens een code review? Ik stelde mezelf onlangs die vragen, na in Felienne Hermans' *The Programmer's Brain* te hebben gelezen dat gevorderde programmeurs op een andere manier code lezen dan nieuwelingen. "
---

Hoe lees je eigenlijk code? Waar begin je? En in welke volgorde loop je code door? - En zit er verschil tussen het lezen van code tijdens je programmeerwerk en tijdens een [code review](https://en.wikipedia.org/wiki/Code_review)?


## Nieuw versus gevorderd


Ik stelde mezelf onlangs die vragen, na in [Felienne Hermans](https://www.felienne.com/)' [*The Programmer's Brain*](https://www.manning.com/books/the-programmers-brain) te hebben gelezen dat gevorderde programmeurs op een andere manier code lezen dan nieuwelingen. 


Beginners lezen code zoals ze een tekst lezen: van boven naar beneden. Gevorderde programmeurs daarentegen volgen vaker de stack: als zij code tegenkomen die een bepaalde method aanroept, dan bekijken ze eerst die. En als die method op zijn beurt een method aanroept, dan inspecteren ze die. Daarna keren ze terug naar de aanroepende method.


Blijkbaar, concludeert Hermans, is code lezen een vaardigheid die je ontwikkelt naarmate je langer programmeert. 


## Achterdocht


En dat is waar - onder andere in de volgende zin. Een beginnende ontwikkelaar die een method genaamd `GetFoos` leest, concludeert dat die method een verzameling objecten ophaalt van het type `Foo`. Een gevorderde programmeur weet door schade en schande dat code vaak niet zo simpel in elkaar zit, en wil toch even controleren of dat écht is wat er gebeurt. Het zal immers niet de eerste keer zijn dat code bepaalde neveneffecten heeft - het *setten* van een bepaalde variabele, bijvoorbeeld - die niet in de naamgeving terugkomt. (Zie ook [deze blog](/blog/22/07/wat-zijn-eerlijke-functies/).)


Die achterdocht is een waardevolle eigenschap. Dat hebben de makers van [Integrated Development Environments](https://en.wikipedia.org/wiki/Integrated_development_environment) (IDE's) als [Visual Studio](https://visualstudio.microsoft.com/) ook goed begrepen. Niet voor niets is het mogelijk om met één druk op de knop [naar de definitie van een method of variabele te springen](https://docs.microsoft.com/en-us/visualstudio/ide/go-to-and-peek-definition). Gemakkelijk kunnen inspringen op je gerechtvaardigde gevoel van achterdocht is essentieel voor een programmeur om veilig en vloeiend te kunnen prorgrammeren.


Maar ook tijdens code reviews loont het zich om de stack te volgen. Wanneer je de nieuw ingecheckte code van je collega's naloopt, is het altijd een goed idee om te kijken of ze de belofte van hun gekozen namen ook waarmaken. - Sterker nog, dat is precies één van de redenen waarom we überhaupt aan code reviews doen!


## Tooling


Helaas helpt de tooling daar niet altijd even goed bij mee. code reviews - of ze nu in [GitHub](https://github.com/) plaatsvinden of in [Azure DevOps](https://azure.microsoft.com/nl-nl/services/devops/) of een ander codeplatform -, bestaan in de regel uit [*diffs* van platte tekstbestanden](https://nl.wikipedia.org/wiki/Bestanden_vergelijken): aan de linkerkant de oude code, en aan de rechterkant de aangepaste variant. 


Het gevolg daarvan is dat je, anders dan in je IDE, handmatig naar andere classes moet navigeren, wanneer de code een bepaalde verantwoordelijkheid daar naartoe delegeert. Dat is een onhandig klusje wanneer de aangeroepen code in de *diff* is inbegrepen. Maar als er een method in een ongewijzigde class wordt aangeroepen, houdt dat in dat je je achterdocht ergens anders moet bevredigen - in je eigen IDE, waar je de broncode open hebt staan, bijvoorbeeld.


Het zou me niet verbazen als veel gevorderde programmeurs, uit tijdgebrek of gemakzucht, hun gevorderde leesgewoonten daarom wat vaker laten schieten En het zou me ook niet verbazen als dit één van de redenen is waarom code reviews zo'n matig middel zijn om vroegtijdig bugs te achterhalen.[^1]


## Waar te beginnen?


De conclusie lijkt dus eenvoudig: volg ook bij het doorlopen van code tijdens je code reviews de stack, niet de tekst. Zo ontdek je des te eerder wanneer code niet precies doet wat de naamgeving belooft. Het kost wat meer handwerk, maar het levert wel een grondiger begrip van de code op. 


Maar die conclusie laat een gerelateerde vraag buiten beschouwing. Het is duidelijk hoe je het best code kunt lezen, als je eenmaal in een method zit, maar het is nog helemaal niet duidelijk bij welke method je überhaupt moet beginnen tijdens je code review.


Een gewetensvraag: wie werkt zo'n *review* van boven naar beneden door? - Nou, ik dus. 


## Van boven naar beneden


Stel dat mijn collega's me vragen een *pull request* te bekijken dat zowel de front- als de back-end raakt (en dat gebeurt regelmatig, want [we proberen onze PBI's zoveel mogelijk vertical te schrijven](/blog/21/10/horizontale-of-verticale-pbis/)). Ik, naïeve ontwikkelaar, zou dan vrolijk beginnen bij de voorkant en eindigen bij de tests. 


Waarom? Omdat Azure DevOps - door een alfabetisch toeval - de code van de front-end bovenaan zet, dan die van de back-end toont, en als laatst de gewijzigde tests laat zien.


Het hoeft niemand te verbazen dat ik er niet van overtuigd ben dat dit per se de beste manier is om code reviews te doorlopen. Dat vind ik niet eens omdat ik in dit scenario de code van boven naar beneden lees, zoals een beginnend programmeur. Erger vind ik dat ik een toevalligheid mijn werkwijze laat bepalen, in plaats van een bewust besluit te nemen.


## Hoe lees je code?


De vraag is dus: als ik een bewust besluit zou moeten nemen over hoe ik mijn code reviews aanvlieg, hoe zou dat er dan uit moeten zien? Waar zou ik beginnen? En waarom? - Wat denk jij dat een goede aanpak zou kunnen zijn?


[^1]: Dat code reviews zo matig presteren op dit gebied is overigens geen toeval: het doel van zulke *reviews* is namelijk helemaal niet om bugs te achterhalen! Het is hoogstens mooi meegenomen. Mensen zijn notoir slecht in het herkennen van bugs in de code. Voor die klus zijn geautomatiseerde tests veel beter geschikt.
