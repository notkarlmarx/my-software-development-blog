---
title: "Laatste Overwegingen Bij Het Uitzoeken Van Een Thema"
author: "Karl van Heijster"
date: 2021-08-17T08:11:16+02:00
draft: true
comments: true
tags: ["dotkarl", "hugo", "leermoment", "open source", "thema's", "web development"]
summary: "Mijn eerste pull requests zijn goedgekeurd! Een historische gebeurtenis! Van volslagen insignificant niveau, weliswaar, maar toch. Dit lijkt me een mooie gelegenheid om mijn overwegingen bij het uitzoeken van een thema af te ronden. Of toch in elk geval: voorlopig af te ronden."
---

[Mijn allereerste pull request is goedgekeurd!](https://github.com/nodejh/hugo-theme-mini/pull/95) Een historische gebeurtenis! Van volslagen insignificant niveau, weliswaar, maar toch.


Sterker nog, [mijn allertweedste pull request is ook goedgekeurd!](https://github.com/nodejh/hugo-theme-mini/pull/96) Een iets minder historische gebeurtenis, maar van een even insignificant niveau!


Dit lijkt me een mooie gelegenheid om mijn overwegingen bij het uitzoeken van een thema (zie [hier](/blog/21/06/overwegingen-bij-het-uitzoeken-van-een-thema/) en [hier](/blog/21/06/meer-overwegingen-bij-het-uitzoeken-van-een-thema/)) af te ronden. Of toch in elk geval: voorlopig af te ronden.


## Wat mij tegenhield


We eindigden vorige blog met dat ik overwoog om *mini* als thema te gebruiken voor *dotkarl*. De oplettende lezer zal opgemerkt hebben dat van dat plan uiteindelijk niets terechtgekomen is. 


Er waren enkele issues die me tegenhielden het thema te gebruiken. (1) Het thema brak woorden willekeurig af. (2) De links hadden veel witruimte. (3) Er was geen ondersteuning voor [*i18n*](https://en.wikipedia.org/wiki/Internationalization_and_localization).


Het eerste twee issues zijn inmiddels gefixt. De eerste dus door mij! Joepie! Het derde issue liet wat langer op zich wachten vanwege een [merge conflict](https://docs.github.com/en/github/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts). Maar [Hang Jiang](https://github.com/nodejh), de ontwikkelaar van *mini*, was erg dankbaar toen ik dat conflict verwerkt had, en liet een kwartier nadat ik de boel geresolved had al weten de wijziging mee te willen nemen.


## Het alternatief


Desalniettemin is *mini* van de baan als vervanger voor *tale*. De reden is eigenlijk heel eenvoudig: ik heb met wat [custom CSS](https://github.com/EmielH/tale-hugo#additional-css-files) het beste van beide werelden kunnen verenigen.


Met *mini* als inspiratiebron, heb ik *dotkarl* een wat smallere kolom gegeven. Dat geeft het geheel een wat volwassener uitstraling, volgens mij. 


Het nadeel daarvan is overigens wel dat het wat moeilijker is geworden om tabellen en code snippets netjes weer te geven. Maar het esthetisch plezier van mijn wijziging weegt daar ruimschoots tegenop, als je het mij vraagt.


Daarnaast heb ik nu mijn eigen variant van het *mini*-logo op de homepagina, namelijk: mijn hoofd. (N.B. [Géén punthoofd!](/blog/21/04/hoe-mijn-profielfoto-me-een-punthoofd-bezorgde/)) Ik stel het me graag zo voor: die cirkel is een *dot* en mijn hoofd een *karl*, en zo komen vorm en inhoud netjes bijeen. Maar dat is eigenlijk allemaal maar blabla, natuurlijk, zo eerlijk kan ik er ook wel weer over zijn.


## Lessen


Heeft dit verhaal nog een moraal? Nou, misschien zoiets:


- **Je hoeft niet de boel volledig om te gooien om iets naar je smaak te krijgen.** Kijk goed om je heen en kijk hoe je de elementen die je bevallen in kan passen in datgene wat je al hebt. Vraag jezelf altijd af: is een volledig nieuwe oplossing mijn tijd waard, of kan ik ongeveer hetzelfde voor elkaar krijgen met een fractie van de inzet? Daarom:

- **Omarm beperkingen**: ze nopen tot eenvoudige oplossingen. Soms is bloggen, net als software ontwikkelen, compromissen sluiten. Uiteindelijk bleek ik met [nog geen veertig regels CSS](https://github.com/dotkarl/my-software-development-blog/blob/main/static/custom.css) te bereiken wat ik oorspronkelijk met een compleet nieuw thema wilde bewerkstelligen. Dat is, als het op compromissen aankomt, lang geen slechte deal, dunkt me.
