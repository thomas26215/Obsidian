---
MOOC: "[[Programmation]]"
Langage: Web
Type: CSS
tags:
---
En agençants nos attrivuts sur la même, ligne on remarque que les blocs ont tendances à vouloir d'écraser pour prendre l'espace nécessaire. Cependant, avec l'attribut `flex-wrap`, il est possible de légèrement modifier le comportement des blocs :
- `nowrap` : Par de retour à la ligne
- `wrap` : Retour à la ligne si plus de place
- `wrap-reverse` : Les éléments vont à la ligne, mais sont en sens inverseas
**Exemple :**
```CSS
.container{
	display: flex;
	flex-wrap: wrap-reverse
}
```
---
**Links :**
[[Le principe du Flexbox]]