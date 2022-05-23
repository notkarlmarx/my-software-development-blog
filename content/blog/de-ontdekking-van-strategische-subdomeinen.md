---
title: "De ontdekking van strategische subdomeinen"
author: "Karl van Heijster"
date: 2022-05-23T07:29:05+02:00
draft: true
comments: true
tags: ["domain-driven design", "leermoment", "software ontwikkelaar (rol)", "strategische subdomeinen", "verantwoordelijkheid", "waarde"]
summary: "Ik schreef één keer eerder over Domain-Driven Design - en in die blog gaf ik onmiddellijk toe niks van het onderwerp te weten. Precies daarom nam ik me voor om *Learning Domain-Driven Design* van Vlad Khononov op te pakken. En met succes, want al meteen in het eerste hoofdstuk leerde ik iets nieuws: het bestaan van strategische subdomeinen."
---

Ik schreef [één keer eerder](/blog/21/08/domain-driven-design-en-ludwig-wittgenstein/) over Domain-Driven Design (DDD) - en in die blog gaf ik onmiddellijk toe niks van het onderwerp te weten. Precies daarom nam ik me voor om [*Learning Domain-Driven Design*](https://www.oreilly.com/library/view/learning-domain-driven-design/9781098100124/) van [Vlad Khononov](https://vladikk.com/) op te pakken.[^1]


En met succes, want al meteen in het eerste hoofdstuk leerde ik iets nieuws: het bestaan van strategische subdomeinen. - Huhwattisdat? Om dat te snappen, moet je je softwareontwikkelaarspet even afzetten, en een businessanalistenpet op je kruintje plaatsen. 


## Kern, generiek en ondersteunend


Elk bedrijf opereert binnen een bepaald domein. Dat kan bijvoorbeeld [toetsontwikkeling](https://www.cito.nl/) zijn, of [het aanbieden van films en series](https://www.netflix.com/nl/), of [het verkopen van je gegevens aan de hoogste bieder](https://www.facebook.com/). Dat ene ding, datgene waar het bedrijf om bekend staat, is hun kernsubdomein (*core subdomain*). Het is hetgeen het bedrijf onderscheidt van zijn concurrenten.


Maar hoewel een bedrijf altijd een bepaald domein als zijn *core business* heeft, opereert het nooit binnen exact één domein. Er zijn altijd randzaken die net zo goed moeten worden afgehandeld. 


Dat zijn ofwel generieke problemen die uitbesteed kunnen worden - zoals authenticatie van gebruikers - ofwel specifieke problemen die weinig onderscheidende waarde leveren voor het bedrijf - zoals het uitvoeren van [CRUD-operaties](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) op bepaalde businessentiteiten. De eerste set problemen behoren tot het generieke (*generic*), de tweede tot het ondersteundende (*supporting*) subdomein.


Alles wat een bedrijf doet, valt onder één van die drie subdomeinen: kern, generiek of ondersteunend. Ze worden "strategisch" genoemd, omdat ze verband houden met de strategie van het bedrijf.


## Hiërarchie


Waarom is dit belangrijk om als softwareontwikkelaar te weten? Omdat de aard van het subdomein de aarde van de softwareoplossing bepaalt. In de hiërarchie van waar als softwareontwikkelaar je tijd (en het geld van je opdrachtgever) aan wil besteden, staat het kernsubdomein bovenaan, en het generieke domein onderaan. Anders gezegd: je zet de nieuwste technieken in voor het kernsubdomein, en bewezen patronen voor het ondersteunende domein. Naar generieke subdomeinen kijk je het liefst geeneens, die besteed je uit. 


Een voorbeeld verheldert die uitspraak misschien. Een tijd geleden sprak ik een oud-studiegenoot van me, die niet zolang daarvoor een carrièreswitch gemaakt had van filosofiedocent naar de IT-afdeling van een Nederlandse universiteit.


Hij vertelde over de applicaties die zijn team ontwikkelde (en die ik - sorry! - vrijwel onmiddellijk allemaal vergat). Maar één ding is me wel bijgebleven. Hij vertelde dat hij onlangs de opdracht op zich had genomen een [rijke teksteditor](https://weblearn.ox.ac.uk/portal/help/TOCDisplay/content.hlp?docId=whatistherichtexteditor) te bouwen. Daar was hij twee of drie weken mee bezig geweest, en toen besloot men dat project te schrappen en een open source-oplossing te gebruiken.


Een goede keus, als je het mij vraagt. Dat vond ik toen hij me dat verhaal vertelde, en dat vind ik nu nog steeds. Maar waarom? - Destijds vond ik het moeilijk er de woorden voor te vinden. Maar de notie van strategische subdomeinen heeft me die nu gegeven. 


Het bouwen van een rijke teksteditor is geen onderdeel van het kerndomein van een universiteit. Sterker nog, zo'n editor is onderdeel van een generiek subdomein. Het is een standaardprobleem waar standaardoplossingen beschikbaar voor zijn. Het is een probleem dat je oplost door zo'n standaardpakket in te kopen, tegen nota bene een fractie van de kosten van het zelfstandig ontwikkelen van een eigen oplossing.


### Ondersteunen


Uit die anekdote is het misschien verleidelijk om de les te trekken: oplossingen in het generieke domein koop je in, oplossingen in het kerndomein ontwikkel je zelf. Maar die vlieger gaat niet op. Het kerndomein is datgene wat een bedrijf onderscheidt van zijn concurrenten, maar wat dat is, hoeft niet per se op het vlak van software te liggen.


Een bedrijf kán zich onderscheiden door het gebruik van *cutting edge* [machine learning-algoritmen](/blog/22/02/hoe-machines-leren/), zeker. Maar het kan datzelfde ook doen op het gebied van klantvriendelijkheid, of de goedkope prijs van haar diensten. De software van zo'n bedrijf - dat waar jij als ontwikkelaar je ziel en zaligheid in legt - kan volledig in het ondersteunende en generieke domein vallen.


Let op: daar is niets mis mee! Het lezen van *Learning Domain-Driven Design* deed mij beseffen dat mijn team en ik inderdaad in het ondersteunende domein vallen. Het kerndomein van onze werkgever, ligt 'm niet in de *software* die ze gebruikt om toetsen te construeren: het zit 'm in de expertise waarmee die toetsen geconstrueerd worden.


## Gevolgen


Die realisatie heeft belangrijke gevolgen voor de software die ik ontwikkel - ontwikkel als ondersteuner, zogezegd. Hij hoeft niet gebruik te maken van de aller-, allernieuwste technieken, of heel ingewikkelde businesslogica te implementeren. Integendeel: mijn software moet zo eenvoudig mogelijk zijn binnen de kaders van de businessprocessen. 


Dat betekent ook: eenvoud propageren naar de business toe. Als de business *pusht* om een oplossing te ontwikkelen die nodeloos complex is - eentje van het kaliber zou-het-niet-tof-zijn-als -, is het je taak als ontwikkelaar-ondersteuner om tegengas te geven. 


Opnieuw levert de notie van strategische subdomeinen hier de taal. Waarom vraag je aan ontwikkelaars om complexe, *cutting edge* - en loeidure - oplossingen te ontwikkelen, als ze niet de waarde leveren waar jullie een strategisch voordeel mee behalen ten opzichte van de concurrent? - Dáárom is het als ontwikkelaar belangrijk om kennis te nemen van DDD.



[^1]: Het [beruchte boek](https://www.dddcommunity.org/book/evans_2003/) van [Eric Evans](https://www.domainlanguage.com/) durfde ik nog niet aan. Je begint ook niet aan [*Kritik der reinen Vernunft*](https://nl.wikipedia.org/wiki/Kritik_der_reinen_Vernunft) zonder eerst een goede inleiding in het denken van [Kant](https://plato.stanford.edu/entries/kant/) gelezen te hebben!
