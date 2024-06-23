---
title: "Wat zegt deze code?"
author: "Karl van Heijster"
date: 2024-06-22T21:26:54+02:00
draft: true
comments: true
tags: ["bedrijfscultuur", "betekenis", "code lezen", "communicatie", "eerlijke functies", "filosofie", "functioneel programmeren", "intentie van code", "kernwaarden", "LINQ", "naamgeving", "objectgeoriënteerd programmeren", "refactoren", "teamcultuur", "technische schuld", "verantwoordelijkheid", "werkplezier", "zorg"]
summary: "De namen in onze code -- van variabelen, velden, methoden, parameters -- beschrijven wat de code doet. De naam van een class beschrijft haar wezen: `integer`, `Url`, `ResourceHelper`. Anders dan bij mensen gaat de existentie van code niet vooraf aan haar essentie. Code is bepaald, bepaald door haar functie. Wat die functie is, weet een goede programmeur in een naam te vangen."
---

"Wat zegt deze code?" -- Of: wat zegt het dat het zegt? -- De functie heet `Add`, hij telt dingen bij elkaar op. -- Kortom: naamgeving. -- Er is een filosofische traditie die teruggaat tot [Plato](https://plato.stanford.edu/entries/plato/ "'Plato', Stanford Encyclopedia of Philosophy"), die zegt dat je een ding pas echt kent als je de naam ervan kent. In de naam ligt het wezen van het ding vervat.


Natuurlijk: wat is een naam? Volgens [Russell](https://plato.stanford.edu/entries/russell/ "'Bertrand Russell', Stanford Encyclopedia of Philosophy") een verkorte [beschrijving](https://plato.stanford.edu/entries/descriptions/ "'Descriptions', Stanford Encyclopedia of Philosophy") (hij reserveerde de term "*proper names*" dan ook voor iets wat wij geen naam zouden noemen). "Plato" betekent -- onder andere -- "de leraar van Aristoteles". (Maar dat zorgt voor problemen, want we kunnen ons indenken dat Plato ook *niet* de leraar van Aristoteles had kunnen zijn. Is die hypothethische Plato dan geen Plato? -- Jawel, zegt [Kripke](https://en.wikipedia.org/wiki/Saul_Kripke "'Saul Kripke', Wikipedia"), en introduceert de notie van de [starre verwijzer](https://plato.stanford.edu/entries/rigid-designators/ "'Rigid Designators', Stanford Encyclopedia of Philosophy").)


De namen in onze code -- van variabelen, velden, methoden, parameters -- beschrijven wat de code doet. De naam van een class beschrijft haar wezen: `integer`, `Url`, [`ResourceHelper`](https://www.karlvanheijster.com/blog/21/04/neem-afscheid-van-helpers/ "'Neem afscheid van helpers'"). Anders dan bij mensen (*dixit* [Sartre](https://plato.stanford.edu/entries/sartre/ "'Jean-Paul Sartre', Stanford Encyclopedia of Philosophy")) gaat de existentie van code niet vooraf aan haar essentie.[^1] Code is bepaald, bepaald door haar functie. Wat die functie is, weet een goede programmeur in een naam te vangen.


## Liegen


Maar naamgeving is moeilijk. We zijn in staat tot fouten, tot miskarakterisaties. Een naam zegt niet altijd alles. Noem een kip een eend, het blijft een kip. (-- `Duck.Cuckoo()` voelt niet juist.)


Onze code kan liegen -- het kan het ene zeggen en het ander doen. 


```cs
public int Add(int a, int b) => a - b;
```


Of zeggen en verzwijgen -- ook in de wereld van code bestaan halve waarheden.


```cs
public int Add(int a, int b) 
{
    _mailServer.Send("Calculation performed!");
    return a + b;
}
```


"Wat zegt deze code?" -- Het zegt wat het zegt  -- maar taal is goedkoop (*talk is cheap*), een goedkoop signaal.


## Daden


"Wat zegt deze code?" Dat kan ook betekenen: wat toont haar vorm? Eén van de grote openbaringen van het functioneel programmeren was, voor mij, het idee van de [*eerlijke functie*](/tags/eerlijke-functies/ "Blogs met de tag 'eerlijke functies'"), het idee dat je aan de signatuur van een functie moet af kunnen lezen wat ze doet.


De methoden in [LINQ](/tags/linq/ "Blogs met de tag 'LINQ'") voldoen mooi aan die eis: `(IEnumerable<T>, Func<T, bool>) -> IEnumerable<T>`, `(IEnumerable<T>, Func<T, R>) => IEnumerable<R>`.[^2] (LINQ is dan ook een zuiver stuk functionele C#.)


De signatuur van de functie zegt de lezer alles wat het moet weten over de functie (-- al zegt een signatuur natuurlijk ook niet alles. De gelogen `Add` van hierboven heeft dezelfde in- en outputparameters van een optelfunctie. Logisch, want het zijn dezelfde parameters als die van de aftrekfunctie die het feitelijk is. Ook functionele code kan bugs bevatten!) -- of in elk geval alles wat een signatuur over kan brengen.


Je zou `Add` ook in het objectgeoriënteerde paradigma kunnen forceren.


```cs
public interface IAddable
{
    void Add(int b);
}

public class Number : IAddable
{
    private int _a;

    public int A => _a;

    public Number() { }

    public Number(int a)
    {
        _a = a;
    }

    public void Add(int b);
    {
        _a = _a + b;
    }
}
```

Afgezien van de weinig elegante opzet, is er niets mis met deze implementatie. Maar merk op dat de signatuur van `Add` niet langer vertelt wat het feitelijk doet: `int -> void`. Dat inputparameter `b` een rol speelt in het produceren van een nieuw getal, is aan het zicht onttrokken. Het is een geëncapsuleerd stukje logica geworden.


(Dat toont waarin het objectgeoriënteerde en het functionele paradigma in verschillen. Het objectgeoriënteerde probeert de lezer te helpen door informatie te verbergen, het functionele door juist alle informatie te presenteren.[^3] -- Welke methode spreekt je het meest aan?)


Middels haar signatuur kan een functie een hint geven van wat het doet.[^4] "Wat zegt deze code?" -- Om het antwoord daarop te krijgen, moet je kijken wat het *doet*. Geen woorden maar daden -- oftewel: laat de daden voor zich spreken (*actions speak louder than words*).


## Toestand


"Wat zegt deze code?" -- Soms dit: de programmeur dacht op het moment van schrijven niet aan dit eenvoudiger alternatief. Misschien stond hij op moment van schrijven aan het begin van zijn carrière. Of was hij allang tevreden toen de code deed wat het moest doen. -- En misschien betekent dat: de programmeur was moe, hij was verkouden en de baby huilde de hele nacht.


Code is een weergave van de toestand van de persoon die haar schreef. Soms is dat de gemoedstoestand, andere keren is het het vaardigheidsniveau. 


Regelmatig vertelt code over de mate waarin een programmeur het probleem heeft begrepen. Verweven code vertelt van een programmeur die het probleem nog niet ver genoeg geanalyseerd heeft (*to decompose*, een probleem uiteenleggen in kleinere problemen). Omslachtige code vertelt over ontbrekende verbindingen tussen ideeën. Gedupliceerde code kan op een missende abstractie wijzen.


Een tijd terug kwam ik een stuk code tegen dat *a* omzette naar *b*, en *b* daarna aanpaste (*b'*) op basis van *c*. Waarom? -- Omdat de aanpassing van *b* een latere toevoeging was. De code gaf impliciet aan in welke volgorde ze geschreven was.


En dat signaleert dat de programmeur niet voldoende tijd heeft genomen om zijn code te [refactoren](/tags/refactoren/ "Blogs met de tag 'refactoren'"). De volgorde waarin code opgebouwd is, is accidenteel -- irrelevant voor haar lezer. Een gevolg van continu refactoren is dat de code er altijd uitziet alsof ze van begin af aan zo bedoeld was. (Ik refactorde de code om *b* te construeren op basis van *a* en *c*.)


Code vertelt me iets over mijn relatie tot mezelf. Gun ik mezelf om in een makkelijk werkbare codebase te werken? ([Kent Beck](https://www.kentbeck.com/) maakt dit punt; zie ook [deze blog] (GROTE_REFACTORSLAGEN_ONDERMIJNEN_VERTROUWEN).)


## Cultuur


"Wat zegt deze code?" -- Ze zegt dus ook iets over de context, de cultuur waarin ze tot stand is gekomen. Want waarom heeft de programmeur de code niet gerefactord? Misschien: omdat hij onder grote tijdsdruk stond. Omdat de feature *nu* af moest, omdat het project al over budget was, omdat *we anders die grote klant verliezen!*


Soms zegt code: deze organisatie geeft meer om snelheid dan om kwaliteit. -- En soms is dat ook de juiste keuze. ["Technische schuld" is niet *per se* een negatieve term.](/blog/21/11/bewuste-technische-schuld/ "'Bewuste technische schuld'") Je kunt nu schulden maken -- als investering in de toekomst. Het is slechts ("slechts"?) zaak de schuld structureel en tijdig af te lossen. Het werkelijke probleem met technische schuld is *onbeheerde* technische schuld ("*unmanaged technical debt*", [Kevlin Henney](https://kevlinhenney.medium.com/ "Kevlin Henney @ Medium") wijst op dit punt). -- Anders gezegd: het probleem is niet de schuld, het is de terugbetaalstrategie, of het gebrek daaraan.


De grap is natuurlijk: teams die aandacht hebben voor de kwaliteit van hun code, leveren sneller. Omdat ze niet continu bugs hoeven te fixen. Omdat ze de structuur van hun code continu aanpassen aan nieuwe wensen, in plaats van die wensen in een achterhaalde structuur te wrotten.


Want code kan ook zeggen: het team -- want het is een *team effort*! -- besteedt zorg en aandacht aan haar codebase. De naamgeving is helder, de vorm communiceert intentie, de programmeur weet waar hij mee bezig is -- de code is [gereviewd](/tags/code-reviews/ "Blogs met de tag 'code reviews'") (achteraf of middels [*pair programming*](/tags/pair-programming/ "Blogs met de tag 'pair programming'")) en [getest](/tags/testen/ "Blogs met de tag 'testen'") (vooraf of achteraf, maar [liever vooraf](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'")); de uitrol is onmiddellijk zodat enige fouten die er *desondanks* in zijn geslopen meteen kunnen worden opgelost.


De code is een uiting van de [ontwikkelcultuur van een team](/tags/teamcultuur/ "Blogs met de tag 'teamcultuur'").[^5] Je kunt aan de code aflezen wat het team belangrijk vindt -- en per extensie de softwareontwikkelafdeling, en per extensie de [organisatie](/tags/bedrijfscultuur/ "Blogs met de tag 'bedrijfscultuur'"). Wat is belangrijk: dat er op de deadline tien dingen half af zijn, of dat de belangrijkste drie precies doen wat ze moeten doen? -- De keus is aan ons, aan ons ontwikkelaars (zie ook [deze blog](/blog/23/12/formuleer-je-kernwaarden/ "'Formuleer je kernwaarden'").)


## Meer dan je denkt


"Wat zegt deze code?" -- Een naïef antwoord zou zijn: de code is een uitdrukking van dat wat zich in het hoofd van de haar schrijver afspeelde op het moment van schrijven. (En de code produceert vervolgens een betekenisgeheel in het hoofd van degene die het leest.) 


Maar dat laat onverklaard waarom de code me iets kan vertellen over alles waar de schrijver *niet* aan dacht, niet bewust althans. Alle aannames, inhoudelijk en vormelijk, die werden gedaan op het moment dat de code uit de vingers vloeide, *zit in de code* zonder dat die daar bewust in is gestopt.


("[De auteur is dood](https://en.wikipedia.org/wiki/The_Death_of_the_Author "'The Death of the Author', Wikipedia")," in de woorden van [Roland Barthes](https://en.wikipedia.org/wiki/Roland_Barthes "'Roland Barthes', Wikipedia").)


Code zegt meer dan je denkt. En dat toont dat code meer is dan "het jasje" dat we onze gedachten aan moeten trekken om ze te communiceren aan een ander. Zoals [Hilary Putnam](https://en.wikipedia.org/wiki/Hilary_Putnam "'Hilary Putnam', Wikipedia") ooit zei: "*Cut the pie any way you leaking, "meanings" just ain't in the* head!"


[^1]: Al kunnen onze eerste pogingen tot naamgeving het wezen van de code missen.

[^2]: Respectievelijk `Where` en `Select`.

[^3]: Maar zie [deze blog](/blog/23/06/objectgeorienteerd-programmeren-draait-niet-om-objecten/ "'Objectgeoriënteerd programmeren draait niet om objecten'") voor een overeenkomst tussen beide paradigma's.

[^4]: Uiteraard zijn signaturen niet de enige manieren waarop de vorm van code haar verhaal kan vertellen. De manieren waarop objecten aan elkaar gekoppeld zijn, vertelt eveneens een verhaal. Zie [deze](/blog/24/01/overerving-compositie-en-dependency-injection/ "'Overerving, compositie en dependency injection'") en [deze blog](/blog/24/01/symmetrische-en-asymmetrische-overerving/ "'Symmetrische en asymmetrische overerving'").

[^5]: Maar de relatie werkt twee kanten op. Tegelijkertijd *maakt* de code de cultuur. Een slordige codebase nodigt uit tot slordigheid; een opgeruimde tot opruimen. Je gaat niet nonchalant om met zorgvuldig geconstrueerde code -- tenzij je een betere oplossing vindt, en dan kieper je de oude code ongenadig weg.