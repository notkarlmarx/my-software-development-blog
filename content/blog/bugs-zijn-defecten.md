---
title: "Bugs zijn defecten"
author: "Karl van Heijster"
date: 2024-08-31T20:00:58+02:00
draft: true
comments: true
tags: ["bugs", "software ontwikkelaar (rol)", "teamcultuur", "verantwoordelijkheid"]
summary: "Een softwareontwikkelaar is: iemand die defecten fixt die hij zelf heeft geïntroduceerd."
---

# Karl overdenkt een metafoor #12


<br>


Een softwareontwikkelaar is: iemand die defecten fixt die hij zelf heeft geïntroduceerd. (Bedenk: de kleinste eenheid in de softwareontwikkeling is het team.)


{{< asterisk >}}


Een softwareontwikkelaar introduceert *defecten*. Een ontwikkelaar introduceert geen [*bugs*](/tags/bugs/ "Blogs met de tag 'bugs'"). Bugs zijn beestjes die onze code in zijn komen vliegen, een natuurfenomeen waar we helemaal niets aan doen. (En zo verpietert onze code net als onze tuin na een insectenplaag.)


De term "bug" heeft – bedoeld of onbedoeld – een connotatie: dat het defect iets is dat extern is aan ons en ons handelen. 


Maar, afgezien van [de allereerste bug](https://nl.wikipedia.org/wiki/Bug_(technologie) "'Bug (technologie)', Wikipedia"), is een bug niet een beestje dat in de raderen van de code is gekomen. Een bug is: we zeiden dat het zou werken, maar het werkt niet. Het systeem is defect.


Een softwareontwikkelaar introduceert *defecten*.[^1]


{{< asterisk >}}


*It’s not a bug, it’s a feature* – dat is de aloude grap.


Of het een defect is of niet is afhankelijk van hoe we de correcte werking definiëren -- en daarover kan verschil van mening bestaan. (Soms wil je als ontwikkelaar uitroepen: snappen ze dan niet dat het *zo* werkt?)


Soms is een bug een feature. Dan zeggen we: het systeem is niet bedoeld om *zo* te werken, maar we snappen waarom je wil dat het zo werkt.


Een verschuiving in ons perspectief kan van een bug een feature maken, of andersom. 


Maar alleen als we bereid zijn dat te doen. Of iets een bug of een feature is, is ook een politieke vraag.


{{< asterisk >}}


Voor de melder van de bug is het om het even wie de bug heeft geïntroduceerd. Schuld draagt een team als geheel (– en dus ook de [verantwoordelijkheid](/tags/verantwoordelijkheid/ "Blogs met de tag 'verantwoordelijkheid'")).


Een ontwikkelteam is als een sportteam. In de sport wint of verliest een team als geheel, al kunnen sommige spelers nog zo goed zijn.


Bugs introduceren is net zozeer een teamsport als bugs fixen.


{{< asterisk >}}


Een gedeelde verantwoordelijkheid kan alleen worden gedragen door een [cultuur](/tags/teamcultuur/ "Blogs met de tag 'teamcultuur'"). Is de cultuur zwak, dan is gedeelde verantwoordelijkheid geen verantwoordelijkheid.


Bugs ontstaan (ook, niet uitsluitend) wanneer ontwikkelaars zeggen: -- niet mijn probleem. Een systeem rot wanneer er niet voor wordt gezorgd. 


Als ontwikkelaars zeggen: niet mijn probleem, dan bedoelen ze: dat is *zijn* probleem. Het tweetal (*n*-tal) opereert niet als team, als geheel. Er is onderlinge verdeeldheid, men werkt niet *samen*.


Een team dat niet [samenwerkt](/tags/samenwerking/ "Blogs met de tag 'samenwerking'") is gewoon een groep mensen.


{{< asterisk >}}


Een systeem rot wanneer er niet voor wordt [gezorgd](/tags/zorg/ "Blogs met de tag 'zorg'"). -- De metafoor (het [mentaal model](/tags/mentaal-model/ "Blogs met de tag 'mentaal model'")) van de tuin. Beestjes leven in het hoge gras.


Vlak voordat ik met vakantie ging, gooide ik een dertigtal classes weg uit onze codebase: dode code, of op sterven na. En vlak voordat mijn vakantie eindigde, haalde ik het onkruid tussen de tuintegels vandaan (en verwoestte daarmee de huizen van tientallen bugs, beestjes).[^2]


Soms moet je in de code *snoeien*. De beste manier om bugs te voorkomen is te versimpelen.


{{< asterisk >}}


Bugs verschuilen zich in complexiteit -- dat betekent: we overzien defecten in complexe omgevingen. (Bugs zijn defecten.)


Bugs leggen defecten bloot: in de werking van onze code, in haar ontwerp, en in onze werkwijze. 


Produceren teams waarin er wordt samengewerkt (waarin er als team wordt geopereerd) meer of minder bugs? Vraag jezelf af: wat is de [eerste oorzaak](https://en.wikipedia.org/wiki/Unmoved_mover "'Unmoved mover', Wikipedia") van de bug?


{{< asterisk >}}


Als het onze verantwoordelijkheid is om correcte software op te leveren, dan is de aanwezigheid van bugs (c.q. defecten) het bewijs van ons tekortkomen.


Maar: software wordt ontwikkeld door mensen, en omdat mensen inherent imperfect zijn, zal onze code hoe dan ook bugs bevatten.


Voorkomen is beter dan genezen, jazeker -- maar soms is het pragmatischer te zeggen: *snel* genezen is in dit geval de best mogelijke handelswijze.


{{< asterisk >}}


De beste manier om bugs te voorkomen is te versimpelen. Soms betekent dat: zes mapping-classes terugbrengen naar twee, of twee mapping-classes uitbreiden naar zes (dat is de grap).


Simpel vanuit welk oogpunt? -- Voor ons ontwikkelaars? Voor onze gebruikers? Voor de organisatie (zoals wanneer de software de bedrijfsprocessen versimpelt)?


Soms, als we het leven van onze gebruikers versimpelen, maken we ons ontwikkelaarsleven moeilijker -- en andersom natuurlijk ook. Het is als [de eerste regel van softwarearchitectuur](https://deviq.com/laws/laws-software-architecture "'Laws of Software Architecture', DevIQ"): alles is een afweging (*trade-off*).


(Maar dat beeld suggereert dat ontwikkelaars en eindgebruikers tegenover elkaar staan -- dat kan niet kloppen. De gewenste (?) metafoor zou het volgende beeld moeten overbrengen: ontwikkelaars en eindgebruikers zij aan zij.)


{{< asterisk >}}


Als bugs schuilen in complexiteit, is de aanwezigheid van bugs een aanwijzing dat we ons 't leven moeilijk (de code complex) hebben gemaakt. 


[Neal Ford](https://nealford.com/) zegt (in [*The Productive Programmer*](https://nealford.com/books/productiveprogrammer.html)): "*Developers are drawn to complexity like moths to a flame, often with the same outcome.*"


Bugs zijn over het algemeen het gevolg van beslissingen die *ontwikkelaars* nemen -- soms bewust, vaker onbewust. Slechts af en toe zijn bugs het gevolg van inconsistente gebruikerswensen.


Hoe het ook zij, de verantwoordelijkheid om het defect te voorkomen of elimineren, ligt bij de ontwikkelaar.


{{< asterisk >}}


Softwareontwikkelaars zijn geen ongediertebestrijders. Een team dat grote gedeelten van haar tijd kwijt is aan het oplossen van bugs (repareren van defecten), rest twee keuzes: de bron van het probleem aanpakken -- of van carrière wisselen.


[^1]: Deze gedachten zijn niet origineel, [ik steel ze](https://www.youtube.com/watch?v=9iLxR1h2208 "'Technical Neglect - Kevlin Henney - NDC London 2024', YouTube") ongetwijfeld van [Kevlin Henney](https://kevlinhenney.medium.com/ "Kevlin Henney @ Medium").

[^2]: Karl-de-dichter schreef er een haiku over, ['Tuin'](/blog/21/09/vijf-plus-een-haikus-over-software-ontwikkeling/ "'Vijf+1 haiku's over software ontwikkelen'"): *mijn code is mijn / tuin, ik ben vooral onkruid / aan het wieden dus*. 
