---
title: "Betere documentatie door PR-templates"
author: "Karl van Heijster"
date: 2022-10-14T07:55:16+02:00
draft: false
comments: true
tags: ["documentatie", "pull requests", "samenwerking", "software ontwikkelen"]
summary: "Elk *pull request* biedt een gelegenheid om documentatie te schrijven. Toen ik dat punt een tijd geleden inbracht tijdens het tweewekelijkse Alignment-overleg van mijn team, viel mij tot mijn verbazing een hoop instemmend geknik ten deel. Hoe plezierig dat ook was, eerlijk gezegd verwachtte ik niet per se dat mijn pleidooi veel navolg zou vinden. Programmeurs en documentatie is en blijft nu eenmaal een moeilijk huwelijk. Maar mijn team verraste me positief."
---

Elk *pull request* (PR) biedt een gelegenheid om documentatie te schrijven. (Ik schreef er onlangs nog over, [hier](/blog/22/10/pull-requests-als-documentatie/).) Toen ik dat punt een tijd geleden inbracht tijdens [het tweewekelijkse Alignment-overleg van mijn team](/blog/21/09/hoe-technische-schuld-te-monitoren-en-prioriteren/), viel mij tot mijn verbazing een hoop instemmend geknik ten deel. 


## PR-templates


Hoe plezierig dat ook was, eerlijk gezegd verwachtte ik niet per se dat mijn pleidooi veel navolg zou vinden. Programmeurs en documentatie is en blijft nu eenmaal een moeilijk huwelijk.


Maar mijn team verraste me positief. Want nog geen dag later schoot een collega een PR in - mét toelichting in de omschrijving en al! - voor het gebruik van [*pull request templates*](https://docs.microsoft.com/en-us/azure/devops/repos/git/pull-request-templates?view=azure-devops). Dat is een eenvoudig markdown-documentje met daarin wat tekst die standaard in de PR-omschrijving terechtkomt.


Het template van mijn collega was even eenvoudig als doeltreffend. Hij vroeg de ontwikkelaar toe te lichten wat zijn wijziging inhield en waarom hij voor deze implementatie had gekozen. Vervolgens definieerde hij een checklist met enkele eisen waarvan we al eerder hadden afgesproken dat elk PR daar eigenlijk aan moest voldoen.


```md
<< Description of the changes in this PR. Make sure to mention the (design) choices you made and why. >>

# Checklist

- [ ] The title of the PR is as follows: `<FEATURE/BUG/REFACTOR> [AzureDevopsId] <Short description formulated as command>`.
- [ ] The description explains *why* this PR was made, what the advantages of this change are.
- [ ] The descriptions explains *what choices* were made *and why* the current implementation was chosen.
- [ ] The relevant work items are linked to the PR.
- [ ] Unit tests validate this change.
- [ ] The code compiles without any errors.
```


## Effect


De wijziging had onmiddellijk effect. Mijn collega's begonnen plotsklaps consequent de wijzigingen in hun PR toe te lichten. De reden is simpel: het template werkt drempelverlagend om documentatie te schrijven.


Meer nog, het maakt 't, psychologisch bezien, *moeilijk* om je PR níet toe te lichten. Niet toelichten houdt immers in dat je ofwel de standaardbeschrijving laat staan, ofwel de hele boel wegdondert. Maar beide opties zijn *not done*, schoolvoorbeelden van oncollegiaal gedrag. 


Nog geen enkele collega is zo boud geweest dat te proberen, maar ik vermoed dat er onmiddellijk commentaar op zou worden gegeven. Voor mij zou het zelfs een reden zijn om het PR ongezien af te keuren. En de munitie ligt bij het template. Het template definieert een standaardpraktijk, het stuurt een boodschap: wij als team committeren ons aan het idee elk PR toe te lichten.


## Event sourced documentatie


Er vallen ten minste twee lessen uit deze episode te trekken.


Ten eerste: wat blijkt, ontwikkelaars hebben niet een hekel aan documentatie schrijven *an sich*. Ze hebben een hekel aan het schrijven van uitgebreide ontwerpdocumenten waarvan ze op voorhand weten dat deze binnen de kortste keren achterhaald is. 


Dat probleem gaat voor goede PR-omschrijvingen niet op. Die documentatie blijft beperkt tot de scope van het PR. Als de code verandert, dan veroudert de documentatie *qua* PR-omschrijving niet. Deze is immers nog steeds op precies dezelfde manier van toepassing op het PR. Waarom de code is veranderd, valt te lezen in een nieuwe PR-omschrijving.


Wie de historie van een stuk code doorloopt, kan middels de omschrijvingen achterhalen wat het oorspronkelijke doel was van de code, en hoe *en waarom* deze in de loop van de tijd is aangepast. Het is een kwestie van omschrijving na omschrijving doorlezen.


Het is een manier van documentatie schrijven die aan [*event sourcing*](https://martinfowler.com/eaaDev/EventSourcing.html) doet denken. In plaats van één gezaghebbende eindstatus te presenteren, definieer je een beginpunt en pas je daar mutaties op toe.


## Beter worden


Ten tweede: deel je verbetervoorstellen altijd met je team. Het openlijk delen van ideeën leidt in het beste geval tot verbeteringen die je zelf niet had kunnen bedenken.


Mijn collega zou nooit op het idee zijn gekomen een template te definiëren zonder mijn pleidooi voor betere PR-documentatie. En die betere PR-documentatie zou er waarschijnlijk nooit zijn gekomen zonder zijn template. Mijn bijdrage lag bij het idee, die van hem bij de technische vertaling daarvan. We vulden elkaar perfect aan.


In een goed functionerend team bouw je voort op elkaars ideeën en help je elkaar om betere softwareontwikkelaars te worden - en betere software te bouwen. 
