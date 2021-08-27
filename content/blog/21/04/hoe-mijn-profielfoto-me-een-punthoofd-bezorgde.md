---
title: "Hoe mijn punthoofd me een punthoofd bezorgde"
date: 2021-04-19T07:45:11+02:00
draft: false
comments: true
tags: ["dotkarl", "hugo", "image processing", "leermoment", "web development"]
summary: "Op deze blog bevindt zich op dit moment één afbeelding. Het is een afbeelding van mijn hoofd. Best een aardige afbeelding, al zeg ik het zelf (maar misschien ben ik bevooroordeeld). 


Ik ben een goed uur uur met die afbeelding bezig geweest. Laat me je vertellen waarom."
---

Op deze blog bevindt zich op dit moment één afbeelding, [hier zo](/about). Het is een afbeelding van mijn hoofd. 


{{<figure src="/images/profile-picture-sm.jpg" width="300" alt="Mijn profielfoto, zoals te zien op de Over mij-pagina">}}


Best een aardige afbeelding, al zeg ik het zelf. Maar misschien ben ik bevooroordeeld.


Ik ben een goed uur uur met die afbeelding bezig geweest.


## Poging #1


Niet om ‘m daar te krijgen, hoor. Ik heb wel ‘ns wat documentatie in Markdown geschreven, dus dat had ik zo rond:


```markdown
![alt text](/path/to-image.jpg)
```


Maar dat leverde dit op:


![Mijn profielfoto, maar dan net zo breed als de hele pagina](/images/profile-picture-sm.jpg)


Veel te groot! Dat kon en moest beter. 


## Poging #2


Maar om dat voor elkaar te krijgen had ik iets langer voor nodig. Geen goed uur, hoor - stel je voor! Wie even Googlet, stuit vanzelf op de [shortcode](https://gohugo.io/content-management/shortcodes/) die je in staat stelt om [de dimensies van een afbeelding in te stellen](https://gohugo.io/content-management/shortcodes/#figure):


```html
<figure src="/path/to-image-sm.jpg" width="300" height="300" alt="alt text">
```


Maar het probleem met die code is dat de afbeelding niet mooi schaalt. Als ik de breedte van mijn browser verklein, dan gaan de verhoudingen van de afbeelding op een gegeven moment goed uiteen lopen. 


{{<figure src="/images/profile-picture-sm.jpg" width="200" height="300" alt="Mijn profielfoto, met scheve verhoudingen">}}


Ik krijg er een punthoofd van, zou je kunnen zeggen.


## Poging #3


Met dat punthoofd van me ben ik wat langer bezig geweest. Ik heb gespeeld met [*image processing*](https://gohugo.io/content-management/image-processing/). En ik vond een uitstekende blog van Alex Lakatos over [hoe je daarmee de performance van je website kunt verbeteren](https://alexlakatos.com/web/2020/07/17/hugo-image-processing/).


Om daar mee aan de slag te gaan, moest ik de boel wel een beetje omgooien. Ik verplaatste mijn afbeelding uit de [static map](https://gohugo.io/content-management/static-files/), naar een algemene assets-map, naar een specifieke map voor de Over mij-pagina. Ik speelde wat met de code die ik had gevonden, voegde variabelen toe om met hoogte en breedte te kunnen spelen. 


Meestal veroorzaakte ik build errors. Op de momenten dat ik dat niet deed, schaalde mijn afbeelding alsnog niet goed. Hoe verder het uur vorderde, hoe meer ik wegzakte in steeds complexere code.


Ik kreeg er letterlijk een punthoofd van. 


## De oplossing


(Ervaren webontwikkelaars zijn vast en zeker naar het beeldscherm aan het schreeuwen nu.) 


Waar de oplossing vandaan kwam, weet ik niet eens meer. Ik deed het gewoon, en voordat ik de pagina opnieuw bouwde (websites in Hugo, inclusief content, worden op build time gegenereerd), wist ik dat het zou werken. Al mijn problemen verdwenen zodra ik me realiseerde dat ik de hoogte van een afbeelding helemaal niet op *hoef* te geven. Zo dus:


```html
<figure src="/path/to-image.jpg" width="300" alt="alt text">
```


En zie: een afbeelding, 300 pixels breed. En hij schaalt mooi mee als ik de breedte van mijn scherm aanpas.


## Lessen


- **De oplossing is vaak simpeler dan je denkt.** Als je merkt dat je veel code moet schrijven voor iets wat voor je gevoel een simpel probleem moet zijn, dan is de kans groot dat je iets over het hoofd hebt gezien. Verlies jezelf niet in steeds complexere code. Neem een moment om afstand te nemen van waar je mee bezig bent en breng de aannames die je doet in kaart. Veroorzaakt het framework je punthoofd, of doe je het zelf?
