Les Grids nous permettent de créer des tableaux visuels. Il faut pour cela utiliser la propriété `display: grid;` :
```css
.conteneur{
	display: grid;
}
```
Il y a ensuite quelques éléments à préciser afin de représenter correctement le tableau :
- `grid-template-columns`  :Le nombre de colonnes, ainsi que la largeur de chacune d'entre elles
- `grid-template-rows` : 
> Dans la div `container` sera compris les différentes divs `box`. Il est nécessaire de mettre la propriété `display-grid` dans la div `container` avant d'ajouter d'autres propriétés correspondante liées à cette div ou aux autres divs `box`

#### 1 - Définir la largeur
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

Il est possible d'indiquer le nombre de colonnes. Pour cela, il suffit d'utiliser la propriété `grid-template-columns` suivit des tailles différentes colonnes :
```css
.conteneur{
	display: grid;
	grid-template-columns: 200pd, 150px, 300px;
}
```
Ainsi, la grid sera composée de 3 colonnes qui auront respéctivement les tailles `200px`, `150px` et `300px`.
On remarque ici que l'on a même pas besoin de spécifier le nombre de colonnes nécessaires, les calcul se fait tout seul

Il est également possible de spécifier la largeur des éléments de la même manière. Cependant, il faut utiliser la propriété `grid-template-rows`.

### Aérer les éléments
Il est possible d'ajouter de l'espace autour des éléments de la grille en utilisant la propriété `gap` :
```css
.conteneur {
    display: grid;
    grid-template-columns: 200px 200px 200px;
    grid-template-rows: 100px 150px 200px;
    gap: 10px;
}
```

### Mesurer ses colonnes
Afin de réaliser des choses plus complexes avec les grids, il est possible d'indiquer un point de départ et un point d'arrivée pour nos éléments avec les propriétés suivantes :
- `grid-columns-start` : Indique la ligne verticale de départ de l'élément
- `grid-columns-end` : Indique la ligne verticale de fin de l'élément
- `grid-columns-start` : Indique la ligne horizontale de départ de l'élément
- `grid-columns-end` : Indique la ligne horizontale de fin de l'éléments

Changeons un peu la structure de base de notre projet :
```html
<div class="conteneur">
    <div class="une">🐸 Élément 1</div>
    <div class="deux">🦊 Élément 2</div>
    <div class="trois">🦄 Élément 3</div>
    <div class="quatre">🐶 Élément 4</div>
    <div class="cinq">🐨 Élément 5</div>
    <div class="six">🐒 Élément 6</div>
    <div class="sept">🦆 Élément 7</div>
    <div class="huit">🐙 Élément 8</div>
    <div class="neuf">🐋 Élément 9</div>
</div>
```

```css
.conteneur {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 100px 100px 100px 100px 100px;
    grid-gap: 10px;
}
```

### Mesurer les colonnes
Si on prend la première div : `.une`
Si on considère que la partie la plus à gauche est de valeur 1 et que la valeur la plus à droite est de valeur 4. Ainsi, pour que la div `.une` prenne toute la longueur, il faut faire :
```css
.une{
	grid-column-start: 1;
	grid-column-end: 4;
}
```
Il est aussi possible d'écrire :
```css
.une{
	grid-column: 1/4;
}
```
Il est ainsi plus facile de mesurer ses éléments. C'est le même pour l'attribut `grid-row`