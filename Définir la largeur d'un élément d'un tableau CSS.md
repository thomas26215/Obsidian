---
MOOC: "[[Programmation]]"
Langage: Web
Type: Tableau
tags:
---
Prenons le code HTML suivant :
```html
<div class="conteneur">
    <div class="box">🐸 Élément 1</div>
    <div class="box">🦊 Élément 2</div>
    <div class="box">🦄 Élément 3</div>
    <div class="box">🐶 Élément 4</div>
    <div class="box">🐨 Élément 5</div>
    <div class="box">🐒 Élément 6</div>
    <div class="box">🦆 Élément 7</div>
    <div class="box">🐙 Élément 8</div>
    <div class="box">🐋 Élément 9</div>
</div>
```

Dans le code précédant, nous avons initialisé la grid pour la classe conteneur. Ainsi, tous les éléments se trouvant à l'intérieur sont les éléments de la grid. Dans le code présent, tous les éléments de la classe `box` sont présent dans la catégorie `conteneur`. Il est possible de les modifier :
```css
.box{
	height: 150px;
}
```
Tous les éléments de classe `box` présents dans la grid de classe `conteneur` seront de hauteur `150px`. 

Il est également possible d'indiquer le nombre de colonnes. Pour cela, il suffit d'utiliser la propriété `grid-template-columns` suivit des tailles différentes tailles des colonnes :
```css
.conteneur{
	display: grid;
	grid-template-columns: 200pd, 150px, 300px;
}
```
Ainsi, la grid sera composée de 3 colonnes qui auront respéctivement les tailles `200px`, `150px` et `300px`.
On remarque ici que l'on a même pas besoin de spécifier le nombre de colonnes nécessaires, les calcul se fait tout seul

Il est également possible de spécifier la largeur des éléments de la même manière. Cependant, il faut utiliser la propriété `grid-template-rows`.