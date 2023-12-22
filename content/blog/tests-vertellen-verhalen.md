---
title: "Tests vertellen verhalen"
author: "Karl van Heijster"
date: 2023-12-16T22:49:10+01:00
draft: true
comments: true
tags: ["intentie van code", "testen"]
summary: "Op een dag schoot me het idee te binnen: een test vertelt een verhaal. In een test gebeurt er -- iets. Een test kent een (a) subject dat (b) in een bepaalde situatie (c) een bepaalde handeling verricht met (d) een bepaalde uitkomst. (-- Ik heb nooit gezegd: een test vertelt een *goed* verhaal.)"
---

Op een dag schoot me het idee te binnen: een test vertelt een verhaal. In een test gebeurt er -- iets. Een test kent een (a) subject dat (b) in een bepaalde situatie (c) een bepaalde handeling verricht met (d) een bepaalde uitkomst.


(a) Het subject is het systeem dat wordt getest. Het systeem kan alles beslaan van een éénregelige functie tot een aaneenreiging van modules. -- We kunnen mijmeren over een enkelvoudige gedachte of een episch avontuur neerpennen. 


(b) De situatie waarin het subject zich bevindt, wordt in de *Arrange*-sectie van de test beschreven. Het is de context waarbinnen het subject handelt. Die context kan zich beperken tot het systeem zelf, maar het kan ook de objecten omschrijven waarmee deze interacteert.


(c) De handeling is de *Act*-sectie van de test. Als een goede hoofdpersoon onderneemt ons subject actie; hij stuwt het narratief voorwaarts -- één stap voorwaarts, om precies te zijn. Tests zijn kortverhalen, eenakters.


(d) De uitkomst van de handeling is vastgelegd in de *Assert*-sectie van de test. Een handeling kan positieve of negatieve gevolgen hebben (bijvoorbeeld: het object is succesvol opgeslagen, of juist niet) -- of destructieve (in deze situatie wordt er een *exception* opgegooid). De wereld van het verhaal is aan het eind niet meer dezelfde als aan het begin.


Tests zeggen: *als* deze code dit doet in deze situatie, *dan* zal dit het geval zijn.[^1] Zoals verhalen ons lessen kunnen voorspiegelen over ons eigen gedrag, vertellen tests ons wat de gevolgen zullen zijn van een bepaald gebruik van de code.


En de verhaalmetafoor kan nog verder opgerekt worden. Een test is onderdeel van een testsuite. Je zou kunnen zeggen: elke test is een hoofdstuk of een scène of een kortverhaal in een groter geheel. Elke scène brengt een nieuw aspect aan het licht in het grotere verhaal dat over de code verteld wordt. Naarmate er meer verhalen over de code verteld worden, leer je de aard ervan steeds beter kennen.


Maar anders dan traditionele vertellingen kennen de scènes geen onderlinge samenhang. Tests zijn atomair: ze staan op zichzelf. De uitkomst van de ene scène mag niet als input dienen voor de volgende. 


Een meeslepend epos levert dat niet op. Het overkoepelende verhaal van een testsuite is, zou je kunnen zeggen, postmodern. Maar ik heb nooit gezegd: een test vertelt een *goed* verhaal, een spannend verhaal, een inzichtelijk verhaal. Tests geven ons geen inzicht in de menselijke ziel. -- Maar ze geven ons wel een inzicht in onze codebase. 


Net als traditionele verhalen, vertellen ze ons aan de hand van concrete situaties iets wat die situaties zelf overstijgt.


[^1]: De verhaalmetafoor doet een causale interpretatie van die *als dan*-constructie oplichten. Ik spreek hier dus niet van de logische interpretatie die ook in termen van *~(p ∧ ~q)* kan worden uitgedrukt.
