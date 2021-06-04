---
title: "Enums, Switch Statemens en SOLID - Deel 6"
author: "Karl van Heijster"
date: 2021-06-04T08:24:18+02:00
draft: false
comments: true
tags: ["clean code", "enums", "refactoren", "SOLID", "switch statements"]
summary: "De conclusie van onze refactorslag rondom een op een enum gebaseerd switch statement! Ik hoop de afgelopen weken aan te hebben getoond hoe het gebruik van SOLID-principes je code beter onderhoudbaar kan maken. Vandaag concluderen we met de vraag: moet je morgen meteen dit patroon uit je code base refactoren?"
---

# Conclusie

De afgelopen weken heb ik een [stuk code](https://github.com/notkarlmarx/RefactorExercises/blob/master/RefactorExercises/EnumSwitch/Original/ClaimsHelper.cs) gerefactord om meer in lijn te zijn met [SOLID-principes](https://en.wikipedia.org/wiki/SOLID). Door gebruik te maken van [*Single-Responsiblity*](/blog/21-05-07-enums-switch-statements-en-solid-2), [*Dependency inversion*](/blog/21-05-14-enums-switch-statements-en-solid-3) en het [*Open-closed* principe](/blog/21-05-21-enums-switch-statements-en-solid-4), hebben we de code makkelijker onderhoudbaar gemaakt, zonder de [performance](/blog/21-05-28-enums-switch-statements-en-solid-5) van die code te hoeven offeren. De conclusie is dus duidelijk: verwerk de SOLID-principes in je code!


Zeker als het op nieuwe code aankomt, heb je geen excuus om SOLID niet mee te nemen in je ontwerpproces. Maar hoe zit het met bestaande code? Moet je alles laten vallen waar je mee bezig bent, en je bestaande code base onder handen nemen om alle enum-gebaseerde switch statements eruit te refactoren?


## Wat je je af moet vragen vóórdat je gaat refactoren


Die vraag is moeilijk met een "ja" of "nee" te beantwoorden. Eigenlijk is het antwoord hier hetzelfde als altijd in softwareontwikkelland: [*it depends*](https://medium.com/swlh/the-golden-rule-of-software-engineering-9faaaab85e78). Ga voor jezelf de volgende punten eens na.


### Is de code geunittest? 


Zo ja, mooi! De aanwezigheid van unittests is een voorwaarde voor elke refactorslag. 


Zo nee, doe het dan alsjeblieft niet. Het aantal applicaties dat om zeep geholpen is door goedbedoelde "verbeteringen" aan de code base is ontelbaar, en een gebrek aan unittests is eigenlijk altijd debet daaraan. Als je niet snel en makkelijk kunt controleren of je code hetzelfde blijft functioneren na een wijziging, is deze onderneming eenvoudigweg te risicovol.


### Verandert de code vaak? 


Zo ja, doen! Als je veel in de code moet werken, dan is het de moeite waard om ervoor te zorgen dat deze zo onderhoudbaar mogelijk is. Bovendien hoef je voor deze refactorslag niet apart tijd voor vrij te maken, je kunt deze meenemen tijdens het implementeren van een nieuwe feature. 


Let er wel op dat je dan altijd in twee stappen werkt: eerst refactoren en dan pas de nieuwe feature implementeren. Door beide tegelijkertijd te doen, maak je het jezelf - en je teamgenoten die je code zullen reviewen! - alleen maar moeilijker. (Je ziet: ook in het proces van software ontwikkelen bestaat er een *Single-Responsibility* principe!)


Verandert de code echter niet of nauwelijks, laat het dan voor wat het is. Lelijke werkende code is aan het eind van de dag misschien lelijk, maar hij werkt wel. Zo lang de code geen ontwikkelaar in de weg zit, is het eenvoudigweg niet de moeite waard eraan te komen.


### Is de impact van de refactorslag groot? 


Heb je niet één plek met een enum-gebaseerd switch statement, maar wel tien? (Belangrijk is dat het daarbij ook tien keer om dezelfde enum gaat.) Dan kan een refactorslag de moeite waard zijn. 


Maar let op: hoe groter de impact van je codewijzigingen, hoe beter beslagen je ten ijs moet komen. De toegevoegde waarde van je refactorslag neemt toe met de hoeveelheid code die je opschoont, maar hetzelfde geldt voor de risico's. Wie één switch statement breekt, mag één switch statement repareren. Wie er tien tegelijkertijd breekt...


Zorg ervoor dat je haalbare doelen stelt. Het enige dat erger is dan een brok lelijke code, is een half opgepoetst brok lelijke code. Halve refactorslagen houden de slechte kanten van de oorspronkelijke code in stand én voegen extra onderhoudslast toe in de vorm van een tweede oplossing.


### Past het opschonen van de code binnen de prioriteiten je stakeholders op dit moment hebben? 


Zo ja, ruim dan absoluut tijd in om je code base continu op te schonen. Jijzelf, je collega's en uiteindelijk je stakeholders zullen je er dankbaar voor zijn.


Nadert er echter een deadline, en kun je je Product Owner er met geen mogelijkheid van overtuigen dat refactoring zich op dit moment loont? Laat het voor nu dan wat het is. Focus je op dit moment op de belangrijkste zaken. 


Je hoeft het daar echter niet bij te laten zitten. Breng ondertussen de impact en waarde van je voorgestelde refactorslag in kaart, zodat je je PO op een later moment kunt overtuigen om dit alsnog te prioriteren. Hoe je dat aanpakt? [*Refactoring at Scale*](https://www.oreilly.com/library/view/refactoring-at-scale/9781492075523/) van Maude Lemaire is een uitstekend boek over alles wat bij grootschalige refactoring komt kijken. 


## Nog één dingetje...


Daarmee komen we aan het eind van deze reeks blogs. Zoals altijd: wie de code in al haar iteraties nog eens na wil kijken, kan terecht op [GitHub](https://github.com/notkarlmarx/RefactorExercises).


Er zit me alleen nog één dingetje dwars aan de uiteindelijke implementatie. En dat is die verdomde naam, `ClaimsHelper`, die ik (in aangepaste vorm) heb overgenomen uit onze eigen code base. Het valt misschien buiten het domein van de SOLID-principes, maar in hemelsnaam... [noem je classes geen `...Helper`](/blog/21-04-23-neem-afscheid-van-helpers/)! 


Heb jij een betere suggestie voor de naam van deze class?


## Meer in deze reeks

1. [De casus](/blog/21-04-30-enums-switch-statements-en-solid-1)
2. [Het *Single-Responsibility* principe](/blog/21-05-07-enums-switch-statements-en-solid-2)
3. [Het *Dependency inversion* principe](/blog/21-05-14-enums-switch-statements-en-solid-3)
4. [Het *Open-closed* principe](/blog/21-05-21-enums-switch-statements-en-solid-4)
5. [SOLID en performance](/blog/21-05-28-enums-switch-statements-en-solid-5)
6. **Conclusie**


***TODO: Andere blogs aanpassen***
