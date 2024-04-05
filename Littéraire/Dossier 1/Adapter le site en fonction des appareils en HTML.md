**Media Queries = diff maquettes pour diff appareils**
⇒ Ca indique quand on doit utilise quelles propriétés CSS
Synthaxe :
```css
@media screen and (max-width: 1200px){
	/*Insérer propriétés CSS ici, avec less sélecteurs*/
}
```
⇒ Ne sera appliqué que si écran < 1200 px
`min-width` + `max-width` = Points de rupture (*breakpoints*) ⇒ Points où design change

Nécessaire de rajouter en HTML balise `<meta name=viewport" content="width=device-width, initial-scale=1.0">`
⇒ On demande que viewport du nav s'adapte à surface d'affichage de l'écran. Affichage correct sur mobile
> Tel mobile ont resolution proche d'HD. Si pas de balise meta viewport, affichage du site sera même que sur un écran de cette taille. On y verrait pas grand chose. Avec cette balise, affichage = 390x844 pixels

Plusieurs règles :
- `height` = hauteur zone d'affichage
- `width` = largeur zone d'affichage
- `orientation` = Orientation périphérique
- `media` = type d'écran de sortie
	- `screen` = ecran classique
	- `all` = tout type de média
	- `print` = imprimante
Règles peuvent être combinées avec :
- `only` = uniquement
- `and` = et
- `not` = non
**Voici qqs exemples** :
```css
@media screen and (max-width: 1280px) /*Sur les écrans plus petits que 1280px*/
@media all and (min-width: 1024px) and (max-width: 1280 px) /*Pout tout type d'écran entre 1024 et 1280px
```

Utilise minimum + maximum pour que site d'adapte en fonction des résolutions :
- `min-width` = largeur minimale
- `min-height` = hauteur minimale
- `max-width` = largeur maximale
- `max-height` = hauteur maximale

`overflow` permet de couper ce qui dépasse d'un paragraphe :
- `visible` = (par défaut) reste visible hors du bloc volontairement
- `hidden` = simplement caché
- `scroll` = Caché, mais barre de défilement pour pouvoir voir le reste
- `auto` = C'est navigateur qui décide si il met des barres de défilement si besoin