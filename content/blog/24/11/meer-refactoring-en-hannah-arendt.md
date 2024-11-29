---
title: "Meer refactoring en Hannah Arendt"
author: "Karl van Heijster"
date: 2024-11-29T08:06:50+01:00
draft: false
comments: true
tags: ["filosofie", "refactoren", "technische schuld"]
summary: "Wanneer ontwikkelaars refactortaken apart inplannen of refactoren nalaten omdat ze er geen toestemming voor hebben, dan is dat een teken dat ze de activiteit van het refactoren fundamenteel verkeerd begrijpen. Helaas is dat misbegrip stevig verankerd in de wereld van de softwareontwikkeling dankzij de metafoor van technische schuld."
---

Wat is de aard van [refactoring](/tags/refactoren/ "Blogs met de tag 'refactoren'")? In [een eerdere blog](/blog/24/09/refactoring-en-hannah-arendt/ "'Refactoring en Hannah Arendt'") stelde ik dat refactoren, in de terminologie van [Hannah Arendt](https://plato.stanford.edu/entries/arendt/ "'Hannah Arendt', Stanford Encyclopedia of Philosophy") een vorm van arbeid is. Dat wil zeggen: het is een activiteit in dezelfde categorie als stofzuigen, afwassen of tanden poetsen. Het is een activiteit die steeds opnieuw terugkeert en die geassocieerd is met de last van het bestaan. We kunnen refactoren (stofzuigen, afwassen, tanden poetsen) wel efficiënter maken, maar het is niet de soort activiteit waarvan we ooit kunnen stellen: *nu* is het klaar.


Dit heeft implicaties voor de manier waarop we met refactortaken om moeten gaan. Het betekent bijvoorbeeld dat je als ontwikkelaar niet hoeft te wachten op toestemming om te refactoren. Refactoren voordat je een nieuwe feature toevoegt, is als wat rommel uit de weg ruimen voordat je een nieuwe bank in je woonkamer installeert. Het opruimen is niet een aparte taak, het is eerder een deeltaak van het installeren van de nieuwe bank. Je hoeft dus ook niet apart goedkeuring te krijgen om aan die taak te mogen beginnen. 


Het betekent ook dat refactoring *in de regel* niet apart hoeft te worden ingepland op de backlog.[^1] Immers: refactoren is een doorlopende activiteit zonder duidelijk begin- of eindpunt, en kan daarom niet ingepland worden. We plannen stofzuigen, afwassen en tanden poetsen ook niet (expliciet) als aparte activiteiten in in onze dag; dit zijn dingen die in de stroom van het leven nu eenmaal moeten gebeuren.


## Over technische schuld


Wanneer ontwikkelaars refactortaken apart inplannen of refactoren nalaten omdat ze er geen toestemming voor hebben, dan is dat een teken dat ze de activiteit van het refactoren fundamenteel verkeerd begrijpen. Helaas is dat misbegrip stevig verankerd in de wereld van de softwareontwikkeling dankzij de metafoor van [technische schuld](/tags/technische-schuld/ "Blogs met de tag 'technische schuld'").


Om de praktijk van refactoring te rechtvaardigen, zeggen we dingen als: we hebben gedurende de vorige implementatie een schuld opgebouwd, en die lossen we af door te refactoren. Deze metafoor is succesvol gebleken -- helaas niet in de zin dat er op massale schaal gerefactord wordt, maar in de zin dat het in ons vakgebied normaal is om te spreken van technische schuld in onze code.


De metafoor is echter problematisch.[^2] Het aflossen van een schuld is een fundamenteel andere activiteit dan stofzuigen of afwassen of tanden poetsen. (Stel je voor dat iemand zegt: "Ik ga zo dadelijk een hygiënische schuld aflossen" -- zo iemand zouden we een apart tiep vinden!) Het aflossen van een schuld is, opnieuw in de terminologie van Arendt, een vorm van werk. Dat wil zeggen: het is een activiteit in dezelfde categorie als het vervaardigen van een speer of een auto of een blog, een doelgerichte activiteit met een duidelijk begin- en eindpunt.


De vraag of we nu tijd moeten steken in het aflossen van onze schuld, of dat we verder moeten "investeren" (i.e. meer schulden maken) in nieuwe features, is een vraag waar ontwikkelaars slechts over kunnen adviseren; de uiteindelijke beslissing ligt bij de business in de vorm van de Product Owner (PO). Dat is waarom ontwikkelaars om toestemming vragen om te mogen refactoren. 


En omdat de verantwoordelijkheid voor de keuze om te refactoren binnen deze context bij de PO ligt, specificeren ze die taken apart zodat deze daar rekening mee kan houden in de planning. Het gevolg laat zich natuurlijk raden: er is nooit genoeg tijd om te refactoren. De schuld stapelt zich op totdat het toevoegen van nieuwe features zoveel tijd kost dat refactoren een noodzakelijkheid is geworden -- en veel moeilijker.


## Populariteit


Wat verklaart de populariteit van het idee van technische schuld, als dit zo'n slecht passende metafoor is om refactoring mee te rechtvaardigen? In mijn eerdere blog haalde ik een [tweet](https://mastodon.social/@yvonnezlam/112475015951527765) aan van [Yvonne Lam](https://x.com/yvonnezlam "@yvonnezlam, X"). Daarin zoekt ze de oorzaak in het feit dat de meeste mensen in de softwareontwikkeling meer kaas hebben gegeten van schulden maken dan van huishouding.[^3]


Daar zit een kern van waarheid in -- en, vermoed ik, een diepere dan Lam zich zelf realiseert. Arendt stelt in [*The Human Condition*](https://en.wikipedia.org/wiki/The_Human_Condition "'The Human Condition', Wikipedia") dat de categorie van arbeid überhaupt over het hoofd is gezien door vrijwel alle grote denkers in de Westerse filosofiegeschiedenis. En de weinige denkers die het thema wel aanstipten, hadden ze de neiging het fenomeen te willen reduceren tot werk.


Waar komt die neiging vandaan? Ik denk (lees: speculeer) dat het tekenend is voor de wens om problemen op te willen lossen -- of liever: *definitief* op te willen lossen. En daar waar een definitieve oplossing is, is er sprake van een einddoel. En een einddoel is een aansprekend vooruitzicht -- in elk geval voor filosofen en softwareontwikkelaars. Omgekeerd geldt ook: de afwezigheid van een definitief einddoel is *niet* aansprekend, en dat is waarom arbeid als categorie van menselijke activiteit zo vaak over het hoofd is gezien.


Wanneer er sprake is van een einddoel, bevinden we ons in de sfeer van werk. "Oplossingen" in de sfeer van arbeid zijn daarentegen altijd voorlopig: hoe goed ik ook mijn tanden poets, ze zullen altijd weer smerig worden. 


De metafoor van technische schuld verkoopt ons een einddoel: schuldvrije code. Maar dat vergezicht is illusoir. Code is nooit definitief af, en de noodzaak om te refactoren zal daarom altijd blijven bestaan. Refactoring is, alle praat over technische schuld ten spijt, een vorm van arbeid en niet van werk. 


[^1]: Regels laten uitzonderingen toe. Grote herstructureringen van systemen kunnen en moeten wel degelijk apart ingepland worden. Dit is het onderwerp van [Maude Lemaires](https://maudethecodetoad.com/) uitstekende [*Refactoring at Scale*](https://www.oreilly.com/library/view/refactoring-at-scale/9781492075523/) (een van [de beste boeken over softwareontwikkeling die ik in 2021 las](/blog/21/12/de-beste-boeken-over-software-ontwikkeling-die-ik-in-2021-las/)).

[^2]: Waarmee ik niet wil impliceren: totaal ontoepasbaar. [Dit praatje](https://www.youtube.com/watch?v=u6s8S63OOIE "'The Technical Debt Trap • Doc Norton • YOW! 2017' @ YouTube") van [Doc Norton](https://docondev.com/) overdenkt de voor- en nadelen en het toepassingsgebied van de metafoor. 

[^3]: En trouwens: "technische schuld" klinkt ook een stuk toffer dan "softwarehuishouding", zie de comments op [mijn vorige blog](/blog/24/09/refactoring-en-hannah-arendt/ "'Refactoring en Hannah Arendt'") over dit onderwerp. 
