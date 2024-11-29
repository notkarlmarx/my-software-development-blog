---
title: "Testen jullie private methods?"
author: "Karl van Heijster"
date: 2024-11-29T09:46:54+01:00
draft: true
comments: true
tags: ["testbaarheid", "testen", "unit tests"]
summary: "\"Ja en nee. De testcode is geschreven om de logica te testen die in die `private` method zit. Dus in die zin testen we de `private` method. Maar we testen de `private` method niet door deze direct aan te roepen, nee.\" -- \"Hm.\" -- \"Er zit een verborgen veronderstelling in je vraag. Namelijk: dat een stuk code alleen wordt getest als deze direct wordt aangeroepen. Maar er is een verschil tussen de code die wordt *aangeroepen* door een test, en de code die erdoor *getest* wordt.\""
---

"Testen jullie `private` methods?"


"Ja, wij wel."


"Hoe? Maak je die dan `public` zodat de test erbij kan?"


"Op sommige plekken in de code hebben we zo'n [`InternalsVisibleToAttribute`](https://learn.microsoft.com/en-us/dotnet/api/system.runtime.compilerservices.internalsvisibletoattribute?view=net-9.0 "'InternalsVisibleToAttribute Class', Microsoft documentatie") staan. Dan kunnen we de method op `internal` zetten. Anders kunnen we er niet bij voor onze unittests."


"Dat vind ik zo lelijk."


"Ja, wij ook."


"En jullie?"


"Of wij `private` methods testen?"


"Ja."


"Ja. Maar: niet direct."


"Hoe bedoel je?"


"We testen zulke code wel, maar niet door die methods direct aan te roepen. We testen zulke code via de publieke interface."


"Maar dan test je die interface, niet die `private` method."


"Ja en nee. De testcode is geschreven om de logica te testen die in die `private` method zit. Dus in die zin testen we de `private` method. Maar we testen de `private` method niet door deze direct aan te roepen, nee."


"Hm."


"Er zit een verborgen veronderstelling in je vraag, volgens mij. Namelijk: dat een stuk code alleen wordt getest als deze direct wordt aangeroepen. Maar er is een verschil tussen de code die wordt *aangeroepen* door een test, en de code die erdoor *getest* wordt."


"Hm."


"De test heeft als *expliciet* doel het stuk code te testen die in die private method zit. Maar *impliciet* test deze veel meer, namelijk alle code die erdoor wordt aangeroepen."


"Als je het zo wil zien, ja."


"Het klinkt inefficiënt."


"In zekere zin is het dat ook. Althans, je voert meer instructies uit dan strikt noodzakelijk om de logica te testen, in die zin is het inefficiënt. Maar in andere zin is het juist efficiënter, omdat ik niet elke keer mijn tests hoef te herschrijven als ik refactor."


"Hm."


"Je klinkt niet helemaal overtuigd."


"Ik weet het niet."


"Het is een subtiel punt. Misschien is het wel op het pedante af, geen idee. Maar een test hoeft niet gekoppeld te zijn aan de structuur van een stukje code om dat stukje code te testen. Sterker nog: liever niet."


"Hm."


"Wij houden het gewoon bij dat `InternalsVisibleToAttribute`, denk ik."
