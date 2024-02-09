---
title: "Meer over refactoren"
author: "Karl van Heijster"
date: 2024-02-09T07:58:51+01:00
draft: false
comments: true
tags: ["intentie van code", "refactoren", "schoonheid"]
summary: "Waarom wil je refactoren? -- dat is de eigenlijke vraag, natuurlijk. Je wil refactoren omdat de code iets moet kunnen wat het nu nog niet kan, en omdat de structuur van de code moet worden voorbereid op dat wat straks moet kunnen. Je wil refactoren omdat je *met* je code wil werken, of *in* -- maar in elk geval niet *tegen*. "
---

Waarom wil je [refactoren](/blog/24/02/een-herwaardering-van-fowlers-refactoring/ "'Een herwaardering van Fowlers Refactoring'")? -- dat is de eigenlijke vraag, natuurlijk. Je wil refactoren omdat de code iets moet kunnen wat het nu nog niet kan, en omdat de structuur van de code moet worden voorbereid op dat wat straks moet kunnen. Je wil refactoren omdat je *met* je code wil werken, of *in* -- maar in elk geval niet *tegen*. 


Refactoren is het *soft* houden van de software. Of je nu een nieuw systeem ontwikkelt of een *legacy*-applicatie onderhoudt, de code *zal* wijzigen. Als je dat nu en in de toekomst wil blijven doen, dan moet de code veranderen naar gelang de situatie wijzigt.


Waarom is het makkelijker om met de code te werken na een goede refactoring? -- Omdat het een idee beter uitdrukt dan voorheen. Het idee is: *het proces verloopt zus en zo*. Maar de werkelijkheid is *het proces verloopt zus<sub>1</sub> of zus<sub>2</sub> en zo*. Code die zus<sub>1</sub> en zus<sub>2</sub> als twee entiteiten onderscheidt, drukt de werkelijkheid accurater uit.[^1]


## Mooi 


Gerefactorde code is vaak mooier en meer waar dan ongerefactorde code -- of het is geen gerefactorde code. Een refactorslag die mislukt, omdat halverwege de complexiteit van de wijziging explodeerde, wordt weggegooid. Een refactorslag die slaagt, is mooier omdat de code meer aandacht heeft mogen genieten. Merk op: er is aandacht gegaan naar de code *an sich*, in plaats van naar de code als middel om functionaliteit te realiseren (dat is de bril waardoor we naar code kijken als we het gedrag wijzigen).


Het is meer waar, dan en slechts dan als de gerefactorde code het gevolg is van een nieuw inzicht -- en niet van een loos moment waarop je besloot de code eens om te gooien. Elke refactorslag is mooier, maar sommige zijn niet meer dan dat. Goede refactorslagen zorgen ervoor dat de code de waarheid meer benadert, natuurgetrouw en zo elegant mogelijk gegeven de omstandigheden. (Zie ook [deze blog](/blog/21/09/waarheid-boven-schoonheid/ "'Waarheid boven schoonheid'").)


## Overerving


Wat ik bedoel zette ik eerder uiteen in [deze blog](/blog/24/01/symmetrische-en-asymmetrische-overerving/ "'Symmetrische en asymmetrische overerving'"). Er zijn (ten minste) twee manieren om overerving te implementeren. In het ene scenario bevat baseclass *α* een default implementatie die op gezette plekken te overschrijven is door subclass *β*. In het andere scenario erven zowel *α* als *β* over van baseclass *ω*. *ω* bevat abstracte overrides die de subclasses moeten implementeren.


Ik concludeerde dat ik de tweede manier mooier vond dan de eerste. Maar de tweede was niet per se minder waar.


## Variant


Als *α* en *β* "gelijkwaardige" opties zijn, dan is de tweede manier meer waar. Maar als *α* voorrang heeft op *β*, dan geldt dat voor de eerste. (-- Filosofische terzijde: het beeld van taal -- en code is ook taal -- als afbeelding van de werkelijkheid (cf. [Wittgenstein](https://plato.stanford.edu/entries/wittgenstein/ "'Ludwig Wittgenstein', Stanford Encyclopedia of Philosophy"), [*Tractatus Logico-Philosophicus*](https://en.wikipedia.org/wiki/Tractatus_Logico-Philosophicus "'Tractatus Logico-Philosophicus', Wikipedia")), dringt zicht hier op. De latere Wittgenstein zou zich, als hij programmeur was geworden, ongetwijfeld afvragen: "Maar is dat de enige manier waarop de taal van code functioneert?" Zie ook [deze blog](/blog/21/08/domain-driven-design-en-ludwig-wittgenstein/ "'Domain-Driven Design en Ludwig Wittgenstein'").)


Stel, onze code veronderstelt dat *α* voorrang heeft op *β*, maar dan ontstaat de vraag naar een variant *γ* die zich op een andere manier tot *α* en *β* verhoudt als die twee tot elkaar.[^2] Dit is een uitstekend moment om onze oorspronkelijke ontwerpkeuze te herzien. Als blijkt dat de veronderstellingen waarop deze gebaseerd is, niet meer gelden, dan is het de arbeidethische plicht van een ontwikkelaar de structuur van de code te veranderen naar nieuwe inzichten. (Zie ook [deze](/blog/23/08/overpeinzingen-over-vakmanschap/ "'Overpeinzingen (over vakmanschap)'") en [deze blog](/blog/23/12/drie-kernwaarden/ "'Drie kernwaarden'").)


## Pragmatisme


De ontwikkelaar moet de code refactoren om een nieuwe functionaliteit mogelijk te maken. Na de refactorslag weerspiegelt de code de feitelijke situatie beter, meer natuurgetrouw, meer waar dan het origineel. 


Het [pragmatisme](https://plato.stanford.edu/entries/pragmatism/ "'Pragmatism', Stanford Encyclopedia op Philosophy") definieert de waarheid als *dat wat werkt*. Het valt te bezien of die definitie recht doet aan ons pretheoretische waarheidsbegrip. (Het is de vraag of dat de kern van waarheid is of alleen maar een aangenaam bijproduct.) Maar één ding is wel waar (*no pun intended*!): wie de waarheid omarmt, kan beter uit de voeten in de werkelijkheid. 


Daarom wil je regelmatig refactoren.


[^1]: Of het proces al die variaties zou moeten incorporeren, is een heel andere vraag.


[^2]: Excuses, ik heb veel te veel lol met de variabelen!
