---
title: "Waarom wil Carl niet pairen?"
author: "Karl van Heijster"
date: 2024-08-23T22:19:23+02:00
draft: true
comments: true
tags: ["pair programming", "software ontwikkelaar (rol)", "sprint retrospective", "test-driven development"]
summary: "*Scenario:* Alice en Bob bespreken hun positieve ervaringen met *pair programming* in de Sprint Retrospective. Ze stellen voor het vaker te doen. Carl is defensief. \"Ik vind het niet fijn als een ontwikkelaar op mijn vingers meekijkt hoe ik code typ.\" -- Wat is hier aan de hand?"
---


<span style="text-decoration:underline">Spelers:</span> <span style="font-variant:small-caps;">Alice</span>, <span style="font-variant:small-caps;">Bob</span>, <span style="font-variant:small-caps;">Carl</span>.


<span style="text-decoration:underline">Decor:</span> Flip-over, post-its, stiften, speelkaarten met de fibbonaccireeks erop.


<span style="text-decoration:underline">Scenario:</span> <span style="font-variant:small-caps;">Alice</span> en <span style="font-variant:small-caps;">Bob</span>  bespreken hun positieve ervaringen met [*pair programming*](/tags/pair-programming/ "Blogs met de tag 'pair programming'") in de [Sprint Retrospective](/tags/sprint-retrospective/ "Blogs met de tag 'sprint retrospective'"). Ze stellen voor het vaker te doen. <span style="font-variant:small-caps;">Carl</span> is defensief. "Ik vind het niet fijn als een ontwikkelaar op mijn vingers meekijkt hoe ik code typ." 


-- Leg uit, wat is hier aan de hand?


{{< asterisk >}}


Carl wil iets verbergen. -- Wat? -- Zijn persoonlijke ontwikkelproces. -- Of: het gebrek eraan? 


Hoe ziet het magische moment eruit waarop [requirements](/tags/requirements/ "Blogs met de tag 'requirements'") worden omgezet in functionaliteit? Doorloop je altijd bepaalde stappen? Laat je je leiden door een richtinggevend idee? Of is elke feature uniek? -- je prutst je elke keer richting werkende software.


Dat is een intiem moment, het is iets van jezelf. -- Zo denkt Carl, wellicht.


> <span style="font-variant:small-caps;">Bob</span> 
> <br>
> Wat denk je dat we dan zullen zien?
> <br>
> <br>
> <span style="font-variant:small-caps;">Alice</span> *(sussend)* 
> <br>
> Ik snap dat het ongemakkelijk is.


{{< asterisk >}}


Carl wil niet laten zien dat hij fouten maakt.


Een junior wil niet constant eraan herinnerd worden hoe weinig hij weet. Een senior wil niet laten merken dat hij het ook niet weet. (-- Niet willen *pairen* is ook: sociaal ongemak vermijden.)


Natuurlijk, daarmee berooft hij zich van de ervaring zijn collega te zien worstelen. Elke ontwikkelaar maakt [fouten](/tags/falen/ "Blogs met de tag 'falen'"). (Ik heb mezelf al zo vaak dood gestaard op een falende test die het gevolg was van gekopieerde code.)


> "De beste manier om te groeien als softwareontwikkelaar is door [*Het Bureau*](https://nl.wikipedia.org/wiki/Het_Bureau "'Het Bureau', Wikipedia") te lezen, van [J.J. Voskuil](https://nl.wikipedia.org/wiki/J.J._Voskuil_(schrijver) "'J.J. Voskuil (schrijver)', Wikipedia"). (-- Ik kan me niet herinneren dat er in die roman veel samen werd gewerkt overigens.)" --- <span style="font-variant:small-caps;">Bob</span>


{{< asterisk >}}


-- Of dit: Carl ziet programmeren als een essentieel eenzame bezigheid. Programmeren *hoor* je in je eentje te doen.


(Hoe is het voor Carl om een [GitHub Copilot](https://github.com/features/copilot) te gebruiken? Voelt dat als samenwerken of als een *tool*? Wat zegt dat over zijn kijk op [AI](https://en.wikipedia.org/wiki/Artificial_intelligence "'Artificial intelligence', Wikipedia") -- en wat over de onze?)


{{< asterisk >}}


Programmeren, coderen is als schrijven (opnieuw die [boekmetafoor](KARL_OVERDENKT_EEN_METAFOOR)!) -- dat doe je ook alleen. 


Tenzij je een komedie schrijft, dan werkt het samenspel.


> <span style="font-variant:small-caps;">Bob</span> 
> <br>
> Oftewel: coderen is geen komedie. (De broncode is geen blijspel.)


{{< asterisk >}}


Het is waar dat *pair programming* iets verandert in de manier waarop je code schrijft. Sommige delen blijven hetzelfde (het typen), andere veranderen (nadenken -- hardop nadenken, je gedachtegang communiceren en expliciteren).


{{< asterisk >}}


Sinds ik regelmatig pair, zie ik programmeren niet meer als een eenzame bezigheid. Er zijn nog wel momenten waarop je alleen schrijft, maar ze maken niet de essentie van het werk uit.


{{< asterisk >}}


Nadenken, het probleem begrijpen, is een groter deel van het werk. Het risico bestaat dat dat deel in zuivere eenzaamheid weggedrukt raakt.


De meesten van ons hebben een ander nodig om te kunnen nadenken -- goed te kunnen nadenken. 



{{< asterisk >}}


Carl wil niet laten zien dat hij fouten maakt. De uitweg is: fouten te omarmen. Je pair inlichten: "Ik ga dit eerst lelijk doen." -- en het dan lelijk doen.


*Red* -- *green*: dat is nog niet het moment waarop je je druk maakt over de integriteit van de code. Dat komt straks, in de *refactor*. (Zie ook [deze blog](/blog/22/03/agile-en-test-driven-development/ "'Agile en Test-Driven Development'").) Het is een gewoonte die je je al TDD'end eigen hebt gemaakt: scheid het aanpassen van het gedrag (*green*) van het aanpassen van de structuur (*refactor*).


{{< asterisk >}}


Ik heb nooit (echt?) gepaird zonder [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD), het is een fijne manier om de ontwikkelwerkzaamheden te structureren. Als ik hardop na moet (!) denken, dan heb ik een raamwerk nodig, een verhaal dat mijn gedachten op het juiste spoor houdt.


Woorden alleen zijn niet genoeg, klanken vervliegen maar.


TDD structureert het (samenwerkings)proces. TDD geeft het paar een duidelijk pad: (1) verhelder het probleem met testcases, (2) schrijf een falende test; (3) laat de test slagen, (4) refactor de code -- (5) terug naar (1).


{{< asterisk >}}


De eerste implementatie *moet* de verkeerde implementatie zijn. Anders was ofwel 't probleem triviaal, ofwel hebben we aan 't eind niets geleerd.


Fouten maken betekent ook: leren – voor degene die bereid is van fouten te leren.


> <span style="font-variant:small-caps;">Alice</span> & <span style="font-variant:small-caps;">Bob</span> *(in koor)* 
> <br>
> Hoe leer je sneller van fouten: alleen of samen?


{{< asterisk >}}


Vergeet nooit dat ontwikkelaars ook mensen zijn. 

> <span style="font-variant:small-caps;">Carl</span> 
> <br>
> [ChatGPT](https://openai.com/chatgpt/) is geen ontwikkelaar.


{{< asterisk >}}


## Epiloog


Pair programmen is ook: het probleem van samenwerking (Voskuil), de kruising van verschillende gezichtspunten ([Arendt](https://plato.stanford.edu/entries/arendt/ "'Hannah Arendt', Stanford Encyclopedia of Philosophy")) -- het moment waarop je ermee geconfronteerd wordt dat jouw blik op de zaken maar *een* perspectief vertegenwoordigt. 


Dat soort reflectie is niet voor iedereen weggelegd -- [Socrates](https://plato.stanford.edu/entries/socrates/ "'Socrates', Stanford Encyclopedia of Philosophy") werd het fataal.


> <span style="font-variant:small-caps;">Bob</span> 
> <br>
> Stel je voor: pair programmen met Socrates.
>
>
> Zo’n zweterige ouwe vent. In een toga. Griekse dingen te zeggen. "Ja Socrates!" knikken. Wat voor code levert dat aan ‘t eind van de dag op?
> <br>
> <br>
> <span style="font-variant:small-caps;">Carl</span>
> <br>
> [De Idee van Goede Code.](DE_ALLEGORIE_VAN_DE_GROT)
> <br>
> <br>
> <span style="font-variant:small-caps;">Alice</span>
> <br>
Maar toch: ik garandeer je dat je aan ‘t eind van zo’n sessie met Socrates wijzer bent geworden – al was het maar omdat je weet dat je minder weet dan je dacht. 


<br>


<span class="center">*(Opeens kickt het besef in: dat de [vroege dialogen](https://plato.stanford.edu/entries/plato-ethics-shorter/ "'Plato’s Shorter Ethical Works', Stanford Encyclopedia of Philosophy") van [Plato](https://plato.stanford.edu/entries/plato/ "'Plato', Stanford Encyclopedia of Philosophy") in een* [aporie](https://en.wikipedia.org/wiki/Aporia "'Aporia', Wikipedia") *eindigen is een literaire verbeelding van het [Idee](https://en.wikipedia.org/wiki/Theory_of_forms "'Theory of Forms', Wikipedia") dat [ik weet dat ik niets weet](https://en.wikipedia.org/wiki/I_know_that_I_know_nothing "'I know that I know nothing', Wikipedia"). Einde.)*</span>
