---
title: "Testbuilderbuilder"
author: "Karl van Heijster"
date: 2021-07-26T19:31:46+02:00
draft: true
comments: true
tags: []
summary: ""
---

Drie manieren om objecten te instantiëren in tests:


1. Ze handmatig new'en
2. Object Mother (factory methods)
3. TestBuilders


Khorikov verkiest Object Mothers boven TestBuilders, omdat de laatste onderhoudsintensief zijn. Je bent veel bezig met plumbing code schrijven om een klein beetje leesbaarheid te winnen.


Maar: het patroon is in principe voor elk object hetzelfde. Dit zou je dus moeten kunnen automatiseren. Je zou een `TestBuilderBuilder` moeten kunnen uitprogrammeren.


Eerste versie:
- Input: een bepaald Type
- Output: een string-representatie van een TestBuilder voor dat Type


Deze string kun je in een .cs-file plakken en dan heb je een TestBuilder zonder er al te veel moeite voor te hebben hoeven doen.
