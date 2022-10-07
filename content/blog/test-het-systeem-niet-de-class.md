---
title: "Test het systeem, niet de class"
author: "Karl van Heijster"
date: 2022-10-07T13:29:40+02:00
draft: true
comments: true
tags: ["DRY", "leermoment", "software ontwikkelen", "test-driven development", "testen", "teststrategie", "unit tests"]
summary: "Het is belangrijk om vast te stellen dat er een bug in het systeem was geslopen, ondanks dat de functionaliteit die de bug veroorzaakte *ogenschijnlijk* gedekt was door tests. Waarom \"ogenschijnlijk\"? De class die de serialisatie voor zijn rekening nam, werd wel getest, maar alleen in isolatie en niet in de context van het systeem. - Vraag je af wat de implicatie daarvan is. Het betekent dat onze tests bewezen dat een class naar behoren werkt. Of het systeem als geheel naar behoren werkt, dat kunnen we op basis van de tests niet concluderen. Terwijl dat juist is waar het om gaat! "
---

Ik heb al vaker over testen via de voordeur geschreven ([hier](/blog/22/06/testen-via-de-voordeur/), [hier](/blog/22/09/tests-als-vangnet/) en [hier] (LINK_NAAR_WAT_IS_EEN_UNIT)), dus je zou denken: zo langzamerhand zal 'ie wel uitgeluld zijn. Maar nee hoor!


Laatst nam ik een devbugje over van een collega - zo iemand ben ik - die op dat moment al midden in de ontwikkeling van een volgende feature zat. Wat de precieze bug was, ben ik alweer vergeten, maar ik weet nog dat het iets met het [serialiseren](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/serialization/) van een [C#-object](https://www.w3schools.com/cs/cs_classes.php) naar [JSON](https://www.json.org/json-en.html) te maken had. Ik herinner me dat heel goed, want die collega zei nog: "Werkt dat nou nog niet goed? Ik heb toch een hele tijd met die serialisatie zitten te kloten!"


## Tests


En dat had zijn sporen nagelaten in de codebase - in goede zin! Want mijn collega had een handvol tests toegevoegd waarin een object werd geserialiseerd naar JSON (waarvoor mijn complimenten!), en die tests slaagden als een pientere eindexamenscholier. Dus ik reproduceerde handmatig de bug en voegde een test toe met daarin de het dienstweigerende object en de verwachte JSON.


Het idee achter die aanpak is tweeledig. Ten eerste helpt zo'n test om de bug niet elke keer handmatig te hoeven reproduceren. Op die manier hoef ik tijdens het coderen van een oplossing alleen maar de test af te trappen, in plaats elke keer opnieuw de applicatie op te starten en de foutconditie met het handje te reproduceren. Ten tweede helpt het om de bug te voorkomen, zodra deze verholpen is. In die zin dient de test [als vangnet](/blog/22/09/tests-als-vangnet/) voor de volgende keren.


Het is een vorm van Test-Driven Development (TDD) - of liever: het *is* TDD. Het enige verschil met de standaardvoorbeelden is dat het hier wordt toegepast op een bug in plaats van een feature.


## Geslaagd!


Logischerwijs verwachtte ik een falende test. Maar wat schetste mijn verbazing: de test slaagde! Het object serialiseerde netjes naar de verwachte JSON. Dus startte ik de applicatie opnieuw op, reproduceerde de foutconditie met het handje - en kreeg een foutmelding om mijn oren!


Wat was hier in hemelsnaam aan de hand? Om dat te snappen, moet je iets weten over de bug - en over de test. 


De bug ontstond doordat er iets misging bij het serialiseren van het object. De code riep [`JsonConvert.SerializeObject`](https://www.newtonsoft.com/json/help/html/t_newtonsoft_json_jsonconvert.htm) - met een onverwachte uitkomst tot gevolg. De test testte in isolatie of het object in kwestie geserialiseerd kon worden. Hij riep `JsonConvert.SerializeObject` aan - en slaagde.


Achteraf bezien is het verbazingwekkend dat ik het niet meteen zag. De eerste aanroep, die in onze code, serialiseerde het object zonder de optionele [`JsonSerializerSettings`](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonSerializerSettings__ctor.htm) mee te geven. Die in de test daarentegen, maakte gebruik van de centraal gedefinieerde `JsonSerializerSettingsFactory`. Deze wordt door de hele codebase overal gebruikt om consistente serialisatie te bewerkstelligen - behalve op de plek waar de bug ontstond.


Enfin, je kunt wel raden dat de bug daarna binnen een handomdraai was gefixt.


## Lessen


Ik geloof dat er een paar lessen uit deze episode kunnen worden getrokken. De eerste is van architecturele aard. Het loont zich om een wrapper te schrijven die de huidige aanroepen naar `JsonConvert` encapsuleert. Daar kunnen automatisch de juiste `JsonSerializerSettings` worden toegevoegd, wat het effectief onmogelijk maakt voor ontwikkelaars om deze nog te vergeten toe te voegen. Het zorgt er ook voor dat de `JsonSerializerSettingsFactory` niet meer door de hele applicatie heen aangeroepen hoeft te worden. Zo'n wrapper helpt dus ook om onze applicatie meer [DRY](/tags/dry/) te maken.


De tweede is van test...uele aard? - is dat hoe je dat zegt? Enfin, de tweede gaat over tests. Het is belangrijk om vast te stellen dat er een bug in het systeem was geslopen, ondanks dat de functionaliteit die de bug veroorzaakte *ogenschijnlijk* gedekt was door tests. Waarom "ogenschijnlijk"? De class die de serialisatie voor zijn rekening nam, werd wel getest, maar alleen in isolatie en niet in de context van het systeem.


Vraag je af wat de implicatie daarvan is. Het betekent dat onze tests bewezen dat een class naar behoren werkt. Of het systeem als geheel naar behoren werkt, dat kunnen we op basis van de tests niet concluderen. - Terwijl dat juist is waar het om gaat! 


Idealiter wil je op basis van je testsuite kunnen zeggen: alles werkt, rol maar uit naar productie. Maar willen tests die functie kunnen vervullen, dan moet je geen implementatiedetails in isolatie testen. Je moet het systeem zoveel mogelijk als geheel testen. Test óók daarom [via de voordeur](/blog/22/06/testen-via-de-voordeur/).
