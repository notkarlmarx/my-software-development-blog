---
title: "Bevat Deze Code Een Bug?"
date: 2021-04-24T20:37:36+02:00
draft: true
comments: true
tags: ["clean code", "intentie van code", "leermoment", "refactoren"]
---

Bevat deze code een bug?


{{< gist notkarlmarx 4c7781c440167a12bcd2537875442a89 "ChoiceTypeChecker.cs">}}


Oké, misschien ga ik te snel. Even wat terminologie.


Een [*ChoiceInteraction*](http://www.imsglobal.org/question/qtiv2p2/QTIv2p2-ASI-InformationModelv1p0/imsqtiv2p2_asi_v1p0_InfoModelv1p0.html#Data_ChoiceInteraction) is een meerkeuzevraag. Onze applicatie onderkent twee soorten meerkeuzevragen: *Multiple Choice* (MC) en *Multiple Response* (MR). Bij een MC mag een kandidaat precies één antwoord invullen. Bij een MR mag een kandidaat meer dan één antwoord invullen.


Dus, opnieuw: bevat deze code een bug? Zo ja, wat zou de bug dan zijn?


## De vraag


Laat ik de vraag anders stellen: *Als de MaxChoices van een* ChoiceInteraction *0 is, is het dan een MC of een MR?*


Dit is geen retorische vraag. Dit is precies de vraag die ik mijn collega's onlangs stelde, toen ik in het wild op dit stuk code[^1] stuitte. En tot ze me een antwoord konden geven, maakte ik mezelf gek in een poging er chocola van te maken.


Bestaat er een meerkeuzevraag waarbij de kandidaat maximaal 0 antwoorden mag geven? Wat voor vraag is dat dan? 


Een strikvraag? Is het eigenlijke antwoord dan: alle antwoorden zijn fout? Zou dat dan niet één van de antwoordopties moeten zijn? (Antwoord: [nee](https://www.rcpch.ac.uk/sites/default/files/rcpch/HTWQ/none_of_the_above_or_all_of_the_above.html).) Maar wacht, dat kan het niet zijn, want de kandidaat kan in *ex hypothesi* precies 0 antwoordmogelijkheden aankruisen. Hij of zij zou de vraag dus altijd goed hebben: een waardeloze strikvraag. 


Zou het dan een voorbeeldvraag kunnen zijn, eentje die niet bedoeld is om in te vullen? Maar waarvan is het dan een voorbeeld, van een MC of een MR?


(Ik heb filosofie gestudeerd voordat ik de softwareontwikkeling inrolde, is dat duidelijk?)


## Het antwoord


Het uiteindelijk antwoord bevond zich in minder esoterische sferen. Het was een eenvoudige business-beslissing: *We zien 0 als "onbeperkt", dus dat is een MR.* Klaar, einde discussie.


Dus nee, de bovenstaande code bevat geen bug.


De softwareontwikkelaar neemt dit ter kennisgeving aan en gaat over tot de orde van de dag.


## De oplossing


...of toch niet?


Ik had het bij dat antwoord kunnen laten, natuurlijk. Maar ik ken mezelf: wanneer ik de volgende keer - misschien niet volgende maand, maar volgend jaar zeker wel - opnieuw dit stuk code voor mijn neus zou krijgen, zou ik dezelfde vraag aan mijn collega's stellen. 


En tot ze me een antwoord zouden geven, zou ik mezelf gek maken in een poging er chocola van te maken.


Ik besloot toch even aan de code te rommelen:


{{< gist notkarlmarx 2a87ac6587d13b77f65b01b5c1681f43 "ChoiceTypeChecker.cs">}}


Bevat deze code een bug? *Nee!*


## Lessen


- **Stop niet bij werkende code.** Stop pas wanneer code de intentie weergeeft waarmee je hem geschreven hebt. (Of waarmee een ander hem geschreven heeft, zoals in het voorbeeld.) Wees je bewust van de momenten waarop code vragen bij je oproept. Zijn er manieren waarop je die vragen middels code kunt beantwoorden? Doe dat dan! Hoe minder dingen je je af hoeft te vragen tijdens het lezen van code, hoe sneller je nieuwe features kunt bouwen en waarde kunt leveren voor je eindgebruikers.


[^1]: Goed, niet precies dit stuk code. Ik heb het geheel ietwat aangepast voor het voorbeeld. We zouden nooit het type van een interactie teruggeven als string, we zijn geen barbaren.
