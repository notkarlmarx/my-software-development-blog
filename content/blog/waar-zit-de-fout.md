---
title: "Waar zit de fout?"
author: "Karl van Heijster"
date: 2024-09-20T09:54:53+02:00
draft: true
comments: true
tags: ["bugs", "datamigratie", "leermoment", "software ontwikkelen", "test-driven development", "testen", "unit tests"]
summary: "Mijn collega bracht een argument in dat vaak wordt genoemd als ik mensen vertel over testen via de voordeur: maar door de code direct aan te roepen, geven mijn tests onmiddellijk feedback over *waar* de fout zit. Als de tests van *deze* migratie beginnen te falen, dan weet ik zeker dat *daar* de fout zit. En dat scheelt tijd in het debuggen van de code. -- Maar dat laat de volgende vraag onverlet: is een unittest (waarbij \"unit\" wordt opgevat als "eenheid van code") het beste middel om erachter te komen waar de fout zit?"
---

Mijn team gebruikt [Migrations.Json.Net](https://github.com/Weingartner/Migrations.Json.Net "'WeinGartner/Migrations.Json.Net', GitHub") om de modelwijzigingen in onze [NoSQL-database](https://nl.wikipedia.org/wiki/NoSQL "'NoSQL', Wikipedia") [stapje voor stapje te kunnen migreren](/blog/21/09/stapje-voor-stapje-data-migreren/ "'Stapje voor stapje data migreren'") -- al een hele tijd, getuige ook de vele migraties die we in de loop van de tijd hebben geschreven.


Onlangs gebeurde er iets achteraf-grappigs in die hoek. Onze API retourneerde foutcodes: *kan dit object niet serialiseren*. Ik onderzocht: het ging om zus en zulke objecten, in zus en zulke omstandigheden. En inderdaad, daar was onlangs wat in het model gewijzigd, en dus was er een migratie voor geschreven. Dus ik zette een breakpoint aan de top van die migratiecode en stapte door de code heen: alles oké. 


Dus ik [F10'de](https://learn.microsoft.com/en-us/visualstudio/debugger/debugger-feature-tour?view=vs-2022#step-over-code-to-skip-functions "'Step over code to skip functions' in 'First look at the Visual Studio Debugger', Microsoft documentatie") naar de volgende method, een [custom JSON-converter](https://learn.microsoft.com/en-us/dotnet/standard/serialization/system-text-json/converters-how-to?pivots=dotnet-8-0 "'How to write custom converters for JSON serialization (marshalling) in .NET'") -- ineens: boem! Een foutmelding: *kan dit object niet serialiseren*.


## Breakpoint


Dus ik zette een breakpoint aan de top van die converter -- en inderdaad: de [JSON](https://www.json.org/json-en.html) die ik daar binnenkreeg was invalide. Maar... waarom? Want ik had zojuist nog diezelfde structuur geïnspecteerd in de migratiecode, en die leverde het juiste resultaat op. Zat er misscihen een bug, ergens diep verstopt in de [serializer](https://www.newtonsoft.com/JSON/help/html/SerializingJSON.htm "'Serializing and Deserializing JSON', Newtonsoft documentatie") die we gebruikten?


Het was een chaotische dag, ik had een vergadering hier en een vergadering daar. En tussen die vergaderingen door runde ik mijn tests keer op keer, en steeds met hetzelfde resultaat. En elke keer zat ik met mijn handen iets dieper in het haar: waar zat toch de fout? -- Zo kwam het dat ik aan het eind van de dag nog geen stap dichter bij een oplossing was.


En toen zag een collega: het resultaat van *die* migratie wordt overschreven door de *volgende* migratie. -- Ik kon mezelf wel voor mijn kop slaan. Want die volgende migratie had ik geeneens bekeken. En het zou ook niet nodig moeten zijn, want de naam van die class beloofde een modelwijziging in een heel andere hoek af te vangen. Maar een stuk gekopieerde code was meegeglipt, met alle gevolgen van dien.


## Voorkomen


De les hier is natuurlijk: kopieer geen code -- *in godsnaam*, kopieer geen code! Maar dat is niet de les waar ik het over wil hebben. Ik wil het over [tests](/tags/testen/ "Blogs met de tag 'testen'") hebben -- want, dat kunnen mijn collega's beamen, ik wil het meestal over tests hebben.


De vraag die ik na een episode als deze graag mag stellen is: hoe hadden we dit issue kunnen voorkomen? Antwoord: door een test te schrijven. -- Alleen: we hadden tests geschreven. We hadden tests voor de door mij gedebugde migratiecode, en we hadden tests voor de migratie die erop volgde. Als iemand ons had gevraagd: "Werkt de migratiecode correct?", dan hadden we geantwoord: "Jazeker, kijk maar: *hier* zie je dat *deze* migratie de JSON *zus* transformeert (correct), en *daar* zie je dat *die* migratie de JSON *zo* transformeert (eveneens correct)."


Maar: we hadden geen tests geschreven voor de *interactie* tussen beide migraties. Want de correct output van de ene, bleek de incorrecte input van de volgende te zijn. De fout zat 'm niet in één van beide componenten, maar de manier waarop ze met elkaar samenwerken -- dat was waar onze blinde vlek zat. En pas als we die in beeld krijgen, kunnen we deze fouten in de toekomst voorkomen.


## Voordeur


De oplossing die ik voorstelde was: [test via de voordeur](/blog/22/06/testen-via-de-voordeur/ "'Testen via de voordeur'") (zie ook [deze](/blog/22/09/tests-als-vangnet/ "'Tests als vangnet'"), [deze](/blog/22/11/test-het-systeem-niet-de-class/ "'Test het systeem, niet de class'") en [deze blog](/blog/22/12/tests-zijn-specs/ "'Tests zijn specs'")). In plaats van in onze tests de migratiecode direct aan te roepen, zouden we deze via de serializer moeten aanspreken. De serializer vormt de voordeur via welke de logica in onze migraties wordt ontsloten.


En dit is ook in lijn met het [documenterende aspect van een goede testsuite](/blog/22/09/tests-als-documentatie/ "'Tests als documentatie'"). Tests die via de serializer lopen, communiceren: het doel van de code is deze JSON correct te serialiseren naar ons domeinmodel. Tests die de migratie direct aanspreken, communiceren: het doel van deze code is *deze* JSON correct om te zetten naar *die* JSON. 


Maar dat is maar een implementatiedetail, een tussenresultaat. Het opleveren van de correcte JSON is maar een stapsteen op weg naar het serialiseren ervan, en daarom -- wat mij betreft -- niet de moeite waard om apart te documenteren. Tegelijkertijd laten zulke tests het *eigenlijke* doel van de code impliciet, namelijk het juist kunnen serialiseren naar het domeinmodel.


## Waar zit de fout?


Maar daar was mijn collega het niet mee eens. Hij bracht een argument in dat vaak wordt genoemd als ik mensen vertel over testen via de voordeur: maar door de code direct aan te roepen, geven mijn tests onmiddellijk feedback over *waar* de fout zit. Als de tests van *deze* migratie beginnen te falen, dan weet ik zeker dat *daar* de fout zit. En dat scheelt tijd in het debuggen van de code.


Deze manier van denken houdt nauw verband met het idee dat de *unit* in unittest verwijst naar een eenheid van code (zie [deze blog](/blog/22/11/wat-is-een-unit/ "'Wat is een unit?'")). Maar dat is een problematische notie. Door elke eenheid code direct te testen, maak je het praktisch onmogelijk om te kunnen refactoren -- althans, niet zonder constant je tests ook te moeten herschrijven. Daarnaast is een implicatie van dit idee dat een refactorslag waarbij je een class in tweeën splitst, er op magische wijze voor zorgt dat alle unittests van die class van het ene op het andere moment in integratietests zijn veranderd -- en wat betekent het dan nog om over unit- en integratietests te spreken?


Maar dat laat de volgende vraag onverlet: is een unittest (waarbij "unit" wordt opgevat als "eenheid van code") het beste middel om erachter te komen waar de fout zit? En het antwoord daarop is, volgens mij: nee. Want om unittests die functie te laten spelen, moeten we ze op zo'n manier schrijven dat de tests sterk worden gekoppeld met de code, met alle nadelen van dien.


## Daar zit de fout


Er is een betere manier om erachter te komen waar de fout zit. En dat is door [Test-Driven Development](/tags/test-driven-development/ "Blogs met de tag 'test-driven development'") (TDD) te praktiseren. Want als je TDD't, zou er maar één moment mogen zijn waarop er een test faalt, en dat is op het moment dat je een nieuwe test schrijft (fase *red*). Op elk ander moment (fasen *green* en *refactor*) zouden de tests -- *alle* tests -- moeten blijven slagen.


Voor wie die manier van werken volgt, is het triviaal om aan te wijzen waar de fout in de code zit. *De fout zit in de laatste wijziging* -- altijd en overal. En het oplossen van de fout is dus altijd een kwestie van de laatste wijziging terugdraaien -- en de tests zijn weer groen.


TDD dwingt een ontwikkelaar om zijn code in heel veel heel kleine stapjes te schrijven. Elk stapje is een mogelijke misstap, maar ook: terugkomen van zulke kleine misstappen is een triviale onderneming. Wanneer je unittests zelf (in plaats van *het proces van* unittests schrijven) gaat gebruiken om erachter te komen waar de fout zit, dan is dat een teken dat je te grote stappen neemt in het schrijven van je code. Wanneer je TDD't, verdwijnt de behoefte om al je code direct te testen. 
