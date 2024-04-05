### La différence entre les blocks et les inline
Les balises HTML peuvent se ranger en deux types de catégorie :
- `block` : Ces types de balises créent généralement un retour à la ligne avant et après
- `inline` : Ce type de balise va obligatoirement se trouver à l'intérieur d'une balise `block`
> En réalité, il existe bien d'autres types de catégories mais se sont des catégories mineures, et donc inintéressantes pour le moment

![[Différences block-inline HTML.png|500]]
Ici, les boîtes sont les unes en dessous des autres. Mais on peut également les imbriquer comme les blocs `<section>` dans le bloc `<main>`

### Les balises universelles
Il existe des balises qui n'ont aucun sens particulier : C'est les balises `<span>` (de type bloc) et `<div>` (de type inline).
⇒ **L'intérêt de ces balises est qu'on peut leur associer un `id` ou  une `class` pour le CSS quand aucune balise ne convient**
> Il ne faut pas abuser de ces balises. Des balises adaptées peuvent exister !

### Dimensionner les éléments
Grâce au CSS, il est possible de modifier la largeur du block grâce à la propriété `width` et la hauteur grâce à la propriété `hieght`. Les valeurs sont exprimées en `px` (pixels) ou en `%`
⇒ **Par défaut, un bloc a une largeur de 100%**
```css
p{
	width: 50%
	height: 50dp
}
```
> Les pourcentages sont utiles quand le design doit s'adapter automatiquement à la résolution d'écran du visiteur


### Donner une marge aux éléments
Il est possible de donner une marge extérieure grâce à la propriété `padding` ainsi qu'une marge intérieure grâce au `padding`!
![[exemple marging padding.png|375]]

**Exemple** :
```css
p{
	width: 350px;
	background-color: #F1C864;
	text-align: justify;
	pagging: 16px;
	margin: 50px;
}
```
Ici, cela signifie que le texte sera réduit de `16px` par rapport à son contenant mais aussi que le contenant sera à une distance de `50px` de tout contenant

Cependant, ce code-la va modifier la distance de tous les bords, mais il est possible de ne modifier qu'un bord :
- `top` : haut
- `bottom` : bas
- `left` : gauche
- `right` : droite
![[exemple margin padding  spécifiés.png|375]]
