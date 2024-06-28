---
MOOC: "[[Programmation]]"
Langage: Web
Type: Tableau
tags:
---
Pour créer un tableau en CSS, il faut utiliser la propriété `display: grid` :
```css
.conteneur{
	display: grid;
}
```
Il y a ensuite quelques propriétés à préciser afin de représenter correctement le tableau :
- `grid-template-columns`  : Cette propriété nous permet de préciser le nombre de colonnes, ainsi que la largeur précise de chacune d'elles (*Exemple :*  `grid-template-columns: 100px 200px;` ⇒ De colonne ; la première 100px et la deuxième 200px)
- `grid-template-rows` : Cette propriété nous permet de préciser le nombre de lignes, ainsi que la largeur précise de chacune d'elles
> Dans la div `container` sera compris les différentes divs `box`. Il est nécessaire de mettre la propriété `display-grid` dans la div `container` avant d'ajouter d'autres propriétés correspondante liées à cette div ou aux autres divs `box`

![[Les valeurs pour un tableau CSS]]