---
title: "Overwegingen bij het uitzoeken van een thema"
author: "Karl van Heijster"
date: 2021-06-07T07:43:05+02:00
draft: false
comments: true
tags: ["dotkarl", "hugo", "leermoment", "thema's", "web development"]
summary: "Ik ben aan het overwegen het thema van mijn blog te veranderen. Begrijp me niet verkeerd, het huidige thema is prachtig minimalistisch en ik ben er gek op. Maar het is zo... het eerste wat ik tegenkwam. Nu hoeft het eerste wat je tegenkomt niet per se iets slechts te zijn, maar ja, het is wel het eerste wat je tegenkwam. Snap je?


De afgelopen week ben ik dus op zoek gegaan naar een waardige vervanger."
---

Ik ben aan het overwegen het thema van mijn blog te veranderen. Begrijp me niet verkeerd, [*tale*](https://themes.gohugo.io/tale-hugo/) is een prachtig minimalistisch thema en ik ben er gek op. Maar het is zo... [het eerste wat ik tegenkwam](/blog/21/04/bloggen-met-hugo-eerste-indrukken). Nu hoeft het eerste wat je tegenkomt niet per se iets slechts te zijn, maar ja, het is wel het eerste wat je tegenkwam. Snap je?


De afgelopen week ben ik dus op zoek gegaan naar een waardige vervanger.


## Requirements


Deze situatie bracht me in de ongemakkelijke positie van een klassieke stakeholder: eentje die niet precies weet wat hij wil, maar bij elk voorstel iets scherper heeft wat 'ie sowieso *niet* wil. Het is een ervaring die ik elke ontwikkelaar aan kan raden.


Het enige wat ik zeker wist, was dat het thema minimalistisch zou moeten zijn. Die requirement volgt rechtstreeks uit de filosofie achter *dotkarl*: het is een blog. Niet minder, maar ook zeker niet meer. Een minimalistische uitstraling spiegelt die minimalistische opzet.


Mijn hoop is dat de minimalistische presentatie uitnodigt om te focussen op de inhoud van de blog, want dat is waar het me om draait. *Less is more*, zeggen ze. In dit geval: *less* vorm en *more* inhoud.


En ook: *less* onderhoud. Dat is de luie programmeur in me.


## De zoektocht

Aan [thema's](https://themes.gohugo.io/) heeft Hugo geen gebrek. Tijdens het zoeken kwamen de volgende requirements vanzelf bovendrijven. 


Zo kwam ik erachter dat ik niet graag zie dat bezoekers van deze blog eerst door moeten klikken voordat ze bij het leesvoer aankomen. Thema's met een homepagina met daarop alleen een foto en een korte biografie, vielen dus af.


Ook thema's die op de homepagina alleen de datum en titel van de blogs tonen, moesten eraan geloven. Dat korte voorproefje van de blog die komen gaat, is nu juist één van de dingen die me zo bevallen aan *tale* - iets wat ik op voorhand overigens helemaal niet wist.


Wat ik ook niet wist, is hoe kieskeurig ik kan zijn, en hoe pietluttig de dingen zijn op basis waarvan ik een thema naar de prullenbak verwijs. 


Hoe dan ook, twee thema's hebben de eerste schifting overleefd. In deze blog zal ik mijn ervaringen met de eerste beschrijven; mijn ervaringen met de tweede reserveer ik voor een [andere keer](/blog/21/06/meer-overwegingen-bij-het-uitzoeken-van-een-thema/). Gedurende de tweede schifting trok ik de thema's naar binnen en bekeek hoe goed ze standhielden zodra ze mijn eigen woorden moesten presenteren.


## *hello-friend*


Ik zal eerlijk zijn: het was met name dat knipperende cursortje in [*hello-friend*s](https://themes.gohugo.io/hugo-theme-hello-friend/) titel dat mijn hart sneller deed kloppen. Het is een detail dat het onderwerp van deze blog onmiddellijk en zonder woorden naar de gebruiker communiceert. Het monochromatische kleurenpalet en het strakke, schreefloze font versterken dat gevoel: *hier wordt over code geschreven!* 


Het thema heet niet voor niets *hello-friend*, natuurlijk.


Nog een positief punt: ik zie dat [*internationalization*](https://en.wikipedia.org/wiki/Internationalization_and_localization) (i18n) wordt ondersteund. Dat is goed nieuws, want de taal van deze blog moet consistent zijn. 


Maar belangrijker nog, er is een dark mode! Dit is typisch zo'n feature waarvan je niet weet dat je hem wil hebben, totdat hij binnen handbereik is. 


## bye-bye-friend


Maar hoe mooi een thema er ook uitziet op een [demo-pagina](https://themes.gohugo.io/theme/hugo-theme-hello-friend/), je ervaart pas echt wat hij waard is als je je eigen woorden erin weergegeven ziet. Die reactie is direct, fysiek haast. Ten goede, maar ook ten slechte. 


De nul, bijvoorbeeld, die heeft zo'n streepje erdoorheen. Dat bevalt me niet, niet in de lopende tekst in elk geval. En zonder die mooie, paginabrede afbeelding uit de demo, gaapt er een onprettig groot gat tussen de navigatiebalk en de blogs. En de tags hebben een hashtag, daar ben ik allergisch voor.


En dan heb ik het alleen nog maar over esthetiek. *hello-friend*s i18n is minimaal. De meeste woorden blijk ik handmatig te moeten vertalen in de `config.toml`. Dat is opvallend. Waarschijnlijk is i18n pas later als feature toegevoegd, en daarom niet consistent in het thema toegepast.


Ik besluit dat voorlopig te laten rusten en concentreer me op de tags. Die hashtags moeten weg, natuurlijk. En de tags zelf wil ik naar beneden verhuizen. Ik ben nog geen kwartier bezig en ik wil nu al dit thema customizen.


Als ik in de code duik, bekruipt me een ongemakkelijk gevoel. De HTML bezaaid met inline if-statements. Hier en daar breekt de boel op vreemde manieren af, midden in een span, bijvoorbeeld. De HTML is veelal ook niet uitgesplitst in *partial* bestanden, waardoor de code relatief moeilijk te hanteren is.


Ik ben gestuit op een requirement waar ik van tevoren totaal niet bij stil had gestaan. Ik heb een thema nodig dat zodanig is geschreven dat ik ermee *wil* werken. Het tweaken van de layout moet leuk zijn: een eenvoudige wijziging moet onmiddellijk het resultaat opleveren dat ik verwacht. 


Maar prettig om te tweaken is *hello-friend* niet. Dat is de doorslaggevende reden om het thema af te wijzen. 


(Let wel, ik schrijf deze blog *niet* om *hello-friend* af te branden. Het is een mooi thema. Het heeft niet voor niets de eerste schifting overleefd. Maar het past niet bij me, deels uit esthetische en deels uit codekwalitatieve overwegingen. Dat is mijn punt.)


## Lessen


Ondanks dat *hello-friend* mijn huidige thema niet heeft kunnen vervangen, heb ik toch het een en ander van deze ervaring geleerd.


- **Je waardeert pas wat je hebt als je het kwijt bent.** *tale* is op meerdere manieren een fantastisch thema. Wat ik bijvoorbeeld nooit echt heb gewaardeerd, totdat ik probeerde over te stappen naar *hello-friend* is dat de lijst met blogs geen *Lees meer*-knop heeft. De datum, de titel, het voorproefje: het maakt niet uit waar je klikt, je komt bij de blog in kwestie terecht. Dat is een subtiel maar sterk staaltje gebruikersgemak.

  Maar vooral: het thema is met zorg uitgecodeerd. Het thema bevat zelfs lege HTML-bestanden met alleen een stukje commentaar: *Dit is een placeholder. Creëer een bestand genaamd folder/filename.html in je eigen project om deze te overschrijven*. Ook dat is een stukje gebruikersgemak, niet voor de lezer van de blog, maar de schrijver ervan. En dat verdient een compliment.

- **Wees niet te streng voor stakeholders die niet weten wat ze willen.** Het is ook moeilijk om dat op voorhand te weten. Erger je niet, stel jezelf constructief op. Vind manieren om zo snel mogelijk de impliciete wensen en behoeften naar boven te halen.

- **Er gaapt een gat tussen een goede demo en een goede applicatie.** Het is één ding om een thema te zien functioneren met iemand anders' tekst, en iets heel anders met die van jezelf. Deze les is belangrijk om te onthouden wanneer eindgebruikers erover klagen dat de gewenste functionaliteit in de praktijk toch niet zo prettig werkt als bedacht. 

- **Bestudeer de broncode vóórdat je de beslissing maakt een *third party* component te gebruiken.** Aangenomen dat die broncode beschikbaar is, natuurlijk. Maar voor de thema's van Hugo geldt dat in elk geval wel, en die broncode bevat een schat aan informatie. Kies code die goed is opgezet en prettig leesbaar is. Een inspectie van vijf of tien minuten kan je een boel frustratie achteraf besparen.
