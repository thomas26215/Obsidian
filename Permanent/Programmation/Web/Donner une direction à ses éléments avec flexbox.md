---
MOOC: "[[Programmation]]"
Langage: Web
Type: CSS
tags:
---
D'après la note [[Le principe du Flexbox]], on remarque, que l'attribut `flex` va automatiquement agencer les blocs sur une même ligne. Cependant, il est possible de modifier cela grâce à la propriété `flex-direction` avec l'une des valeurs suivantes :
- `row` : Organisés sur une ligne
- `column` : Organisés sur une colonne
- `row-reverse` : Organisé sur une ligne, mais en sens inverse
- `column-reverse` : Organisé sur un colonne en sens inverse
**Exemple :**
```CSS
.container{
	display: flex;
	flex-direction: column-reverse;
}
```
---
**Links :**
[[Le principe du Flexbox]]
[[Aligner sur l'axe principale avec flexbox]]
[[Aligner sur l'axe secondaire avec flexbox]]