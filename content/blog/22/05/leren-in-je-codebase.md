---
title: "Leren in je codebase"
author: "Karl van Heijster"
date: 2022-05-16T07:52:14+02:00
draft: false
comments: true
tags: ["leren", "waarde", "zelfstudie"]
summary: "Laatst had ik een gesprek met een collega van me, over een meningsverschil dat hij had met onze leidinggevende over zijn zelfstudieproject. Hij wilde zijn handen vuil maken - dat is hoe hij het liefst leert -, niet in een klein, losstaand codeproject, maar in een branch van onze productiecodebase. Onze leidinggevende vond dat, tot frustratie van mijn collega, een slecht idee. - Daar was ik het, eerlijk gezegd, wel mee eens."
---

Ik ben van mening dat je met de juiste manier van denken altijd wel iets vindt om van te leren. En dat is goed om je te beseffen, want leergierigheid is één van de belangrijkste eigenschappen die je als ontwikkelaar kunt hebben. 


Er zijn verschillende manieren om te leren. Persoonlijk leer ik graag door boeken te lezen, het liefst over een onderwerp dat ik redelijk eenvoudig in mijn dagelijkse werkzaamheden toe kan passen. Anderen leren het liefst door hun handen vuil te maken in kleine codeprojecten waarin ze nieuwe technieken uitproberen.


Laatst had ik een gesprek met een collega van me, over een meningsverschil dat hij had met onze leidinggevende over zijn zelfstudieproject. Hij wilde zijn handen vuil maken - dat is hoe hij het liefst leert -, niet in een klein, losstaand codeproject, maar in een [branch](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) van onze productiecodebase. Onze leidinggevende vond dat, tot frustratie van mijn collega, een slecht idee.


Daar was ik het, eerlijk gezegd, wel mee eens.


## Toepassing


Niet dat ik niet begrijp waar mijn collega vandaan komt, integendeel. Hij heeft zijn blik gericht op een bepaalde techniek die hij zich eigen wil maken, en ziet in onze productiecode daar een potentieel goede toepassing voor. Waarom zou je één en één niet twee maken? - dat zou je denken, inderdaad.


En hij is niet de enige. Een andere collega heeft, eveneens tegen de wil van onze leidinggevende in, [Azure Cognitive Search](https://azure.microsoft.com/nl-nl/services/search/) onze productiecode in geschreven. Hij zag de techniek en hij zag de usecase - of liever: hij zag een dataset die hij zó kon benutten - en hij is gewoon aan de slag gegaan. En naderhand oogstte hij lof van precies die leidinggevende die hem die onderneming had afgeraden - het kan vreemd lopen!


En toch: is dat de beste manier om je een nieuwe techniek eigen te maken? Er zijn genoeg redenen te bedenken om terughoudend te zijn met deze praktijk.


## Complexiteit


Ten eerste kent je productiecode allerhande complexiteit die niets met je zelfstudieproject te maken heeft. Deels is dat de aantrekkingskracht, natuurlijk. De bestaande code kan de input vormen voor je nieuwe techniek (zoals in het geval van Azure Cognitive Search). Of het is juist de uitdaging de nieuwe techniek te integreren in een complexe omgeving.


Maar het is goed om in je achterhoofd te houden dat je op dat moment met twee dingen tegelijkertijd bezig bent: de nieuwe techniek te leren kennen én deze te integreren in een complexe omgeving. En die twee kunnen elkaar bijten. Het kan zijn dat je de techniek nog niet goed genoeg snapt om hem goed en wel te kunnen integreren. En het kan ook zijn dat de complexiteit van de omgeving je in de weg zit de nieuwe techniek te begrijpen. Het gevolg is in beide gevallen hetzelfde: een gebrekkig begrip én brakke code - het slechtste van beide werelden.


Je productiecode kent nog een andere vorm van complexiteit: hij verandert voortdurend. De omgeving waarin je je de nieuwe techniek eigen maakt, is niet stabiel. Erger nog, je hebt geen controle over de stabiliteit van de omgeving. Je collega's checken nieuwe code in en refactoren de bestaande code wanneer nodig. Je zult dus een deel van je tijd bezig zijn met het oplossen van [*merge conflicts*](https://css-tricks.com/merge-conflicts-what-they-are-and-how-to-deal-with-them/), in plaats van nieuwe dingen te leren. Ook dat in die zin ben je met meerdere dingen tegelijkertijd bezig.


## Afhankelijkheid


Een tweede problematisch punt, is dat je je zelfstudieproject afhankelijk maakt van datgene waar je team feitelijk mee bezig is. Dat gebeurt op twee manieren.


Ten eerste maak je je interesse in de techniek afhankelijk van de usecase die je ziet (of meent te zien) in de huidige applicatie. Maar wat als er tussen het moment waarop je het zelfstudieproject aanvangt en afrondt, de applicatie dusdanig is veranderd dat de usecase niet meer zo interessant is? Of erger nog: wat als deze zelfs niet meer van toepassing is? Ben je dan gemotiveerd genoeg om het project door te zetten? Of bleek het willen toevoegen van waarde belangrijker te zijn dan het willen opdoen van kennis?


Ten tweede maak je je kennis van de nieuwe techniek afhankelijk van de usecase die voor je ligt. In plaats van een techniek in de breedte te onderzoeken, spits je je kennis ervan al in een vroeg stadium toe op één welbepaald scenario. Is dat werkelijk de beste manier om nieuwe kennis op te doen? Wat als er een nieuwe usecase oppopt? Heb je de techniek dan breed genoeg onderzocht om hem ook daar toe te kunnen passen, of moet je eigenlijk opnieuw beginnen?


De afhankelijkheid wordt pas echt problematisch als de nieuwe techniek in een te vroeg stadium wordt opgenomen in de daadwerkelijke productiecode, als je studie-*branch* te vroeg wordt samengevoegd met *develop*. In dat geval heb je het team verantwoordelijk gemaakt voor nieuwe techniek, terwijl eigenlijk niemand voldoende verstand van heeft om deze in zo'n situatie goed en wel te kunnen onderhouden. Dat is vragen om problemen!


## Een betere opzet


De kern van het probleem is kort gezegd dit: er is een verschil tussen kennis opdoen en kennis toepassen. Wie zijn zelfstudieproject direct de productiecode infietst, doet beide tegelijkertijd - en doet daarmee beide tekort. Je moet leren lopen, vóórdat je kunt rennen.


Dit zou denk ik een betere opzet zijn. Eerst doe je nieuwe kennis op in een eenvoudige, gecontroleerde en geïsoleerde omgeving. Hier heb je de ruimte om te experimenteren - en te falen. De eenvoudige, gecontroleerde context waarin je onvermijdelijke misstap plaatsvond, maakt het makkelijk om je stappen te herleiden en opnieuw te beginnen. Het feit dat je zelfstudieproject losstaat van alle andere code, maakt het mogelijk om verschillende kanten op te experimenteren - ook in richtingen waar je op dit moment nog niet onmiddellijk de toegevoegde waarde van ziet.


Dit is de fase waarin je kennis opdoet. Hoe lang die fase duurt, bepaal je zelf. Je kunt je context eenvoudig houden of juist meer en meer complexiteit toevoegen om na te gaan of de oplossing standhoudt in een echte productieomgeving - het is maar net hoe ver je daarin wil gaan.


Als die fase voorbij is, ga je naar de toepassingsfase. Dit is het moment waarop je de nieuwe techniek in de bestaande applicatie integreert. Omdat je voldoende grip hebt op de techniek zelf, kun je je nu louter en alleen focussen op de integratie ervan. Je hebt voldoende kennis van de mogelijkheden van de techniek om daar gedegen keuzes in te maken.


## Speeltuin


Je productiecode is geen speeltuin. Die codebase is een plek waar je nieuwe kennis toepast, niet een plek waar je die opdoet.


Let wel: ik zeg niet dat er niets te leren valt van je bestaande codebase. Integendeel, de codebase waar ik nu al jaren elke dag in werk, heeft geregeld iets nieuws voor me in petto. Dat gebeurt bijvoorbeeld wanneer mijn collega's een vertrouwd stuk code gerefactord hebben. Of juist wanneer ik een hoekje opzoek dat al langere tijd niet is aangepast en daardoor ongemerkt van de rest van de code is gaan verschillen.


Maar dat is een ander soort leren. Het is een verdieping van je bestaande kennis, geen uitbreiding erop. Leren in je bestaande codebase mag geen risico vormen voor de eindgebruiker - het moet de risico's voor de eindgebruiker juist verkleinen.


## *Separation of concerns*


Leren is net als software ontwikkelen: het loont zich dingen te scheiden, [één ding tegelijkertijd](/blog/22/04/een-test-per-keer/) te doen. Dat gaat de meeste mensen niet vanzelf af - dat is geen kritiek, dat is mensen eigen. We willen met zevenmijlslaarzen acht dingen tegelijkertijd doen. Maar daarmee schenden we één van de belangrijkste principes in de softwareontwikkeling: dat van een *separation of concerns*. 


Wie dat idee serieus neemt - niet alleen in zijn code, maar ook in zijn leerproces -, heeft daar zijn hele carrière plezier van.
