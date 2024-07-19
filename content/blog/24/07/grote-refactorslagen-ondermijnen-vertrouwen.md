---
title: "Grote refactorslagen ondermijnen vertrouwen"
author: "Karl van Heijster"
date: 2024-07-19T07:55:35+02:00
draft: false
comments: true
tags: ["boeken", "leermoment", "professionaliteit", "refactoren", "software ontwikkelaar (rol)", "software ontwikkelen", "stakeholders", "verantwoordelijkheid", "vertrouwen", "werkplezier"]
summary: "Wat een stakeholder betreft is een grote refactorslag een enorme kostenpost zonder aantoonbaar resultaat. Een team dat erop staat niet verder te kunnen werken zonder eerst een hele tijd heel veel geld uit te geven -- nota bene zonder daar iets voor terug te geven! --, ondermijnt het vertrouwen dat de stakeholder hen daarmee geeft."
---

Het primaire uitgangspunt van [Kent Becks](https://www.kentbeck.com/) nieuwste boek[^1], [*Tidy First?*](https://www.oreilly.com/library/view/tidy-first/9781098151232/ "Kent Beck, 'Tidy First?: A Personal Exercise in Empirical Software Design', O'Reilly Media, 2023"), luidt als volgt:


> "Software development is an exercise in human relationships."


*Tidy First?* gaat over de relatie die een ontwikkelaar heeft tot zichzelf. De mate waarin ontwikkelaars hun codebase bijhouden, vertelt iets over die relatie. Gunnen ze het zichzelf te werken in een omgeving die hun geen onnodige frustratie oplevert? Of gaat de deadline altijd voor, en accepteren ze het dat hun werk nu eenmaal moeizaam en onplezierig is? 


Ontwikkelaars in de eerste categorie ruimen hun code regelmatig op, vaak voordat ze een nieuwe feature implementeren (en soms erna). Ontwikkelaars in de tweede categorie doen dat niet -- en dragen de gevolgen.


## Stakeholders


Maar die persoonlijke relatie is natuurlijk niet de enige die een rol speelt in softwareontwikkeling. Als ontwikkelaars hebben we ook een relatie tot onze teamgenoten, bijvoorbeeld, en tot onze stakeholders. En het is die laatste relatie die de persoonlijke vaak verstoort. 


Want waarom kiezen zoveel ontwikkelaars ervoor om hun code niet bij te houden? Omdat stakeholders roepen om nieuwe features, omdat ze hameren op deadlines, soms zelfs omdat ze ontwikkelaars expliciet verbieden te investeren in de kwaliteit van hun code. (-- Een tijd terug sprak ik iemand op een usergroep die zei: "Wij mogen van onze stakeholders geen tests schrijven." Ik moest lachen om niet te huilen.)


De persoonlijke relatie gaat in dat geval ten koste aan het onderhouden van de goede banden met de stakeholders. -- Althans, dat is wat ontwikkelaars in zulke situaties zichzelf wijsmaken. Want wie de relatie met zichzelf verstoort, heeft geen stabiele basis om een goede band met een ander aan te kunnen gaan. Softwareteams die nooit hun code onderhouden, zullen uiteindelijk ontevreden en cynisch worden, en daardoor ondermaats werk leveren waarmee ze de relatie met hun stakeholders op losse schroeven zetten. 


Je moet eerst voor jezelf kunnen zorgen voordat je voor een ander kunt zorgen. Je moet eerst durven zeggen: *nee*, het is belangrijker om deze code *eerst* op te schonen en *dan* pas de nieuwe feature te implementeren. De kosten die een stakeholder daar *nu* voor betaalt zijn maar een fractie van de kosten die diegene ervoor zou betalen als we het niet zouden doen. 


## Afweging


Maar dat je dit moet *durven* zeggen, betekent natuurlijk niet dat je dit altijd moet zeggen. Het vraagteken in *Tidy First?* verwijst nu precies naar het maken van die afweging. Ruim ik deze code eerst op *of niet*? Op basis waarvan maak ik die afweging? In welke gevallen ruim ik juist niet op, en ga ik meteen door naar de implementatiefase? 


Want het is niet zo dat de persoonlijke relatie altijd voorrang heeft boven die met je stakeholders. (Uitspraken met "altijd" en "nooit" erin zijn verdacht in softwareontwikkelland. Het antwoord is meestal (!): *it depends*.) Het doel is een gezonde balans te creëren tussen de verschillende soorten relaties.


Dat punt landde bij mij pas echt toen Beck in [een aflevering](https://open.spotify.com/episode/6XHBSDSSuH0xBDz1LeiAUE?si=b3ae437b513f406d "'SE Radio 615: Kent Beck on Tidy First?', Spotify") van [*Software Engineering Radio*](https://se-radio.net/) de volgende vraag kreeg: "Waarom focus je je in je boek op het opruimen van kleine stukken code vóór het implementeren van een nieuwe feature? Waarom zouden we onze code niet beter in één keer op kunnen ruimen met grote refactorslagen?"


Zijn antwoord was: "Omdat dit de relatie met je stakeholders beschadigt." En hij heeft gelijk. Als je een grote refactorslag uitvoert, dan heeft de stakeholder aan het eind van de rit -- een sprint, een maand, een halfjaar later -- precies hetzelfde systeem als voorheen, vanuit zijn perspectief in elk geval. Erger nog, dat is de uitkomst *in het beste geval*. Want het komt regelmatig voor dat zulke grote verbouwingen gepaard gaan met regressiebugs.


Wat een stakeholder betreft is een grote refactorslag een enorme kostenpost zonder aantoonbaar resultaat. Een team dat erop staat niet verder te kunnen werken zonder eerst een hele tijd heel veel geld uit te geven -- nota bene zonder daar iets voor terug te geven! --, ondermijnt het vertrouwen dat de stakeholder hen daarmee geeft.


## Balans


Beck geeft toe dat grote refactorslagen vanuit technisch oogpunt bezien (i.e. bezien vanuit je persoonlijke relatie tot de code) soms efficiënter kunnen zijn. Maar de schade die dat toebrengt aan de relatie met je stakeholders weegt niet op tegen dat voordeel.


Kleine refactorings brengen daarentegen geen schade aan die relatie. Voor de stakeholder voelt de oplevering van een nieuwe feature die is voorafgegaan door een minimale opschoonbeurt, hetzelfde als de oplevering van een nieuwe feature *tout court*. Want een stakeholder heeft niet de technische achtergrond om te kunnen oordelen dat die feature die je in tweeënhalve dag hebt opgeleverd, ook best in twee dagen had kunnen coderen.


Tegelijkertijd houdt zo'n opschoonbeurt de code wel netjes genoeg om op een prettige manier te kunnen blijven werken in de code. De relaties zijn in balans. En wanneer zowel de ontwikkelaars als de stakeholders tevreden zijn, wordt de beste software ontwikkeld. 


[^1]: Of liever: van zijn nieuwste boekenreeks, want *Tidy First?* is het eerste deel in een geplande trilogie.
