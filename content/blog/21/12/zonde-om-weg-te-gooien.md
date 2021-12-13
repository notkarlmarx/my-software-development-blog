---
title: "Zonde om weg te gooien?"
author: "Karl van Heijster"
date: 2021-12-13T08:13:08+01:00
draft: false
comments: true
tags: ["clean code", "Concorde-effect", "refactoren", "samenwerking", "software ontwikkelen", "technische schuld", "waarde"]
summary: "Laatst kwam ik tijdens het refactoren een stuk code tegen dat alleen maar werd gebruikt in unittests. Dat maakt me erg verdrietig, en om dat verdriet niet te hoeven voelen, donderde ik dat stuk code weg zodat ik er nooit meer naar om zou hoeven kijken. Een collega van me maakte bezwaar toen hij mijn *pull request* bekeek. En, eerlijk is eerlijk, niet helemaal onterecht. Er was veel moeite in deze feature gestopt, zei hij. Was het niet zonde om deze code zonder omzien te verwijderen?"
---

Laatst kwam ik tijdens het refactoren een stuk code tegen dat alleen maar werd gebruikt in unittests. Dat maakt me erg verdrietig, en om dat verdriet niet te hoeven voelen, donderde ik dat stuk code weg zodat ik er nooit meer naar om zou hoeven kijken.


Ongebruikte code voegt geen waarde toe, maar wel onderhoudslast. Het verwijderen van die code heeft dus een netto positief effect: dezelfde lusten tegenover minder lasten.


## Zonde?


Toch maakte een collega van me bezwaar toen hij mijn *pull request* bekeek. En, eerlijk is eerlijk, niet helemaal onterecht. Er was veel moeite in deze feature gestopt, zei hij. (Door hem nota bene, geen wonder dat uitgerekend hij in opstand kwam!) Was het niet zonde om deze code zonder omzien te verwijderen?


Ja, gaf ik toe. Maar ook: nee. 


Het was zonde, daar had hij gelijk in, maar niet omdat de code verwijderd werd. Het was zonde dat er destijds überhaupt tijd in was gestoken. En het was zonde dat die tijd niet gebruikt was om te valideren of er eigenlijk wel behoefte was aan de feature in kwestie.


## Overmaat aan enthousiasme


Waarom hadden we dat niet gedaan? Een situatie als deze ontstaat wanneer een overmaat aan enthousiasme en een gebrek aan een plan elkaar ontmoeten. Onze Product Owner (PO) barst van ambitie, en dat is zowel zijn sterke als zijn zwakke kant. (Zie ook [deze blog](/blog/21/07/de-kwestie-autorisatie/).) Hij had een prachtig idee voor een feature waarbij metadata op hoog niveau wordt gespecificeerd om vervolgens te worden overgeërfd door alle onderliggende objecten. 


Maar hij had er weinig oog voor hoeveel behoefte er voor die feature was - of liever: behoefte op dat moment. Nu ja, nog niet bijster veel, bleek, want de feature zat al maanden ongebruikt in onze applicatie en nog nooit had iemand erom gevraagd. De boel stond ergens in een hoek maar te verstoffen.


(Overigens zijn het niet alleen PO's die voor situaties als deze zorgen. Ook ontwikkelaars hebben er soms een handje van features te willen ontwikkelen omdat *zij* die cool vinden, niet omdat de gebruikers daar om vragen. En soms zijn het de gebruikers zelf (!) die hameren op bepaalde functionaliteit, om er vervolgens niet meer naar om te kijken zodra de boel ontwikkeld is.)


## Nieuwe inzichten


En toch, is het niet zonde om de domeinkennis die mijn collega met pijn en moeite in code heeft vastgelegd zomaar terzijde te schuiven? Nee, en daar zijn twee redenen voor.


Ten eerste is de code misschien wel verwijderd, maar niet verdwenen. De feature is vastgelegd in onze [*source control*](https://en.wikipedia.org/wiki/Version_control) en kan dus altijd terug worden gehaald, mocht dat nodig zijn.


Maar zal het nodig zijn? Het is, ten tweede, maar de vraag of de manier waarop de boel destijds geprogrammeerd was, ook echt de beste was. Niet dat de code slecht opgezet was, meer omdat deze niet strookte met nieuwe inzichten. Het was niet voor niets dat ik deze code tijdens een refactorslag tegenkwam: de opzet van de feature botste met een architecturele beslissing die het team onlangs had genomen. 


Om de feature naar behoren te laten werken, zou hij sowieso moeten worden omgebouwd. Zoals ik al zei: geen waarde, wel onderhoudslast. In wezen is het niets meer dan *legacy code* - en zulke code ben je liever kwijt dan rijk.


## Gehecht


Waarom had mijn collega dan toch het gevoel dat de code beter bewaard zou kunnen blijven? Het antwoord is simpel: omdat hij er veel pijn en moeite in had gestoken! Het is een bekend psychologisch gegeven dat het moeilijker is om afscheid te nemen van zaken naarmate je er meer moeite in hebt gestoken. Je raakt eraan gehecht, niet omdat het iets oplevert, maar omdat het je al zoveel gekost heeft. Dit wordt ook wel het [Concorde-effect](https://nl.wikipedia.org/wiki/Sunk_costs) genoemd.


Dat ik uiteindelijk degene was die de code weggooide, en niet mijn collega, had dus niet alleen te maken met het feit dat ik toevallig de refactorslag voor mijn rekening had genomen. Deze episode toont een nauwelijks gedocumenteerd voordeel van werken in een team: je spreidt het risico te gehecht te raken aan bepaalde oplossingen. 


Want op korte termijn doet het misschien pijn, maar op lange termijn mag je maar blij zijn dat je collega's zo oneerbiedig met je code omspringen.
