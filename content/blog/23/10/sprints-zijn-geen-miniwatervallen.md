---
title: "Sprints zijn geen miniwatervallen"
author: "Karl van Heijster"
date: 2023-10-27T06:54:46+02:00
draft: false
comments: true
tags: ["agile ontwikkeling", "scrum", "waterval"]
summary: "Een tijd geleden viel ik midden in een discussie over de zin en de onzin van Scrum. De ene partij vond Scrum een vooruitgang ten opzichte van de traditionele manier van werken. De andere partij vond Scrum onzin. Ik vond z'n argumenten tegen Scrum onzin."
---

Een tijd geleden verkondigde ik het evangelie van [de edele kunst van het pull request](/talks/de-edele-kunst-van-het-pull-request/) tijdens een pizzasessie bij [4Dotnet](https://www.4dotnet.nl/). Voor aanvang van de presentatie viel ik midden in een discussie over de zin en de onzin van [Scrum](/tags/scrum/ "Blogs met de tag 'scrum'"). De ene partij vond Scrum een vooruitgang ten opzichte van de traditionele manier van werken. De andere partij vond Scrum onzin.


Ik vond z'n argumenten tegen Scrum onzin.


Zelden heb ik zoveel misvattingen over Scrum in zo'n korte tijd gehoord. "Volgens Scrum moet ik mijn planningssessie van twee uur vol maken, ook als we na vijf minuten klaar zijn." Nee, alle sessies in Scrum zijn getimeboxt. Je mag niet langer dan twee uur plannen, korter is geen probleem. "Volgens Scrum mag ik pas na twee weken mijn code releasen." Er is vanuit Scrum bezien niets wat je tegenhoudt eerder te releasen. "Volgens Scrum moet ik mijn stakeholders pas inlichten over mijn voortgang bij de Sprint Review. Volgens Scrum mag ik alleen tijdens de Retrospective ons proces proberen te verbeteren." Dat Scrum voorschrijft elke Sprint expliciet tijd te reserveren voor deze doeleinden, betekent niet dat dit de *enige* momenten zijn waarop je ermee aan de slag mag gaan.


## Managers


Natuurlijk komt deze kritiek niet uit de lucht vallen. Uit de context van de discussie kon ik opmaken dat deze onzinnige voorschriften uit de koker van managers kwamen die weinig begrepen hadden van de methodologie waarvan ze *hun interpretatie* de teams door de strot duwden. 


Scrum komt voort uit de [Agile filosofie](/tags/agile-ontwikkeling/ "Blogs met de tag 'agile ontwikkeling'"). Managers die die filosofie niet omarmen, zien en behandelen Scrum als een dogma. Ze vormen een [cargocultus](https://nl.wikipedia.org/wiki/Cargocult "'Cargocult', Wikipedia") die de methodologie naar de letter volgt (of wat zij als de letter ervaren), zonder de geest ervan te begrijpen -- of te willen begrijpen. (Zie ook [deze blog](/blog/22/02/de-rol-van-user-stories/ "'De rol van user stories'").)


Scrum terzijde schuiven omwille van interpretaties die de essentie van Scrum missen, is als zeggen dat [Nietzsches filosofie](https://plato.stanford.edu/entries/nietzsche/ "'Friedrich Nietzsche', Stanford Encyclopedia of Philosophy") inherent kwaadaardig is, omdat [de nazi's ermee aan de haal gingen dankzij van de selectieve lezing van zijn zus](https://en.wikipedia.org/wiki/Influence_and_reception_of_Friedrich_Nietzsche#Nietzsche_and_fascism "'Nietzsche and fascism' in 'Influence and reception of Friedrich Nietzsche', Wikipedia"). Het doelwit van kritiek is niet Scrum; het is de onzinnige interpretatie die sommige managers eraan geven.


## Waterval


De belangrijkste -- en meest gehoorde -- misvatting over Scrum is echter deze: *Scrum is gewoon waterval, maar dan elke twee weken.*


Volgens [de watervalopvatting van softwareontwikkeling](https://en.wikipedia.org/wiki/Waterfall_model "'Waterfall model', Wikipedia") verloopt het proces van idee naar productiecode volgens welonderscheiden fases. Eerst worden er requirements verzameld. Dan wordt op basis van die requirements een ontwerp uitgetekend. Dan wordt er op basis van dat ontwerp code geschreven. Dan wordt er op basis van die code getest of er aan de requirements is voldaan. Waterval is een sequentieel proces: elke stap in het proces kan pas worden gestart als de vorige is afgerond.


Dat dit proces in de praktijk totaal ongeschikt blijkt om software mee te ontwikkelen, is voor veel managers niet van belang. Het idee heeft een intuïtieve aantrekkingskracht, en omdat ze zelf hun handen niet vuil te hoeven maken aan de code, vinden ze dat dit is hoe we systemen moeten bouwen. 


Maar in de praktijk kunnen we niet op voorhand een systeem volledig specificeren, en daardoor zijn onze ontwerpen imperfect. De code die op basis daarvan wordt geschreven, mist zo haar doel. En het ergst van al is dat de tests pas helemaal op het eind komen, waardoor we niet in staat zijn om de code op basis van nieuwe inzichten tijdig te refactoren.


## Feedbackcyclus


Mensen die zeggen dat Scrum ons voorschrijft om elke Sprint de watervalcyclus te doorlopen, zijn van mening dat het de lange feedbackcyclus is die ervoor zorgt dat watervalprojecten mislukken. Hun oplossing is: laten we elke Sprint een deel van de requirements verzamelen, een deel van de applicatie uittekenen, een deel van de code schrijven, en dat deel testen -- in die volgorde.


Dat is ontegenzeggelijk een vooruitgang ten opzichte van de traditionele waterval. En het is inderdaad hoe veel Scrumteams hun werk organiseren.


Maar het is een misvatting om te denken dat Scrum *voorschrijft* dat er binnen een Sprint op deze manier wordt gewerkt. Sterker nog, wie Scrum in het licht ziet van de Agile filosofie die haar achtergrond vormt, weet dat dit onmogelijk de bedoeling kan zijn geweest van haar bedenkers.


## Projectie


Waterval plaatst analisten, architecten, programmeurs en testers in silo's en verbiedt hen nog net niet ooit met elkaar te praten. Agile draait daarentegen om continue communicatie.[^1] Het plaatst individuen in deze rollen bij elkaar met het expliciete doel hen doorlopend met elkaar te laten samenwerken. 


Requirements verzamelen, ontwerpen, coderen en testen zijn geen welonderscheiden processtappen. Ze informeren en versterken elkaar. [Test-Driven Development is een ontwerpdiscipline](/blog/22/08/test-driven-development-is-een-ontwerpdiscipline/) (zie ook [deze blog](/blog/22/09/tests-als-ontwerpmiddel/ "'Tests als ontwerpmiddel'")). De code die het oplevert kan en moet gebruikt worden om feedback te verzamelen, en de requirements zo wat scherper te krijgen. Softwareontwikkeling is geen sequentieel, maar een iteratief proces (zie ook [deze blog](/blog/21/07/incrementele-versus-iteratieve-ontwikkeling/ "'Incrementele versus iteratieve ontwikkeling'")).


Het idee dat Scrum geen radicale breuk vormt met de traditionele manier van softwareontwikkeling, dat elke Sprint een miniwaterval is, is een misvatting. Het projecteert de traditionele manier van werken op Scrum, in plaats van Scrum te bezien in het licht van de Agile filosofie waar het uit voortkomt.


## Agile


Alle bashing van Scrum terzijde, waren we het op dit punt met elkaar eens. Een Agile manier van werken is de sleutel tot succesvol software ontwikkelen (of in elk geval: succesvoller dan haar voorganger), niet Scrum *an sich*.


Een terechte kritiek luidt dan ook als volgt: de verkondigers van Scrum hebben de indruk gewekt dat je de problemen van waterval kan omzeilen *zonder de achterliggende denk- en werkwijze fundamenteel te veranderen*. Als je maar in Sprints werkt en [Reviews](/tags/sprint-review/ "Blogs met de tag 'sprint review'") en [Retro's](/tags/sprint-retrospective/ "Blogs met de tag 'sprint retrospective'") en [Planningsessies](/tags/sprint-planning/ "Blogs met de tag 'sprint planning'") houdt, dan komt het wel goed. 


En dat is inderdaad een probleem waar veel organisaties tegenaan lopen, getuige de vele managers die, tot frustratie van mijn discussiepartner, hun onzinnige interpretaties van Scrum aan teams blijven opdringen.


[^1]: Het [Agile Manifesto](https://agilemanifesto.org/) spreekt van "individuals and interactions over processes and tools" en "customer collaboration over contract negotiation".
