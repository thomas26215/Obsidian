---
MOOC: "[[Programmation]]"
Langage: Web
Type: Tableau
tags:
---
Nous pouvons indiquer la position des éléments dans la grille en utilisant les propriétés suivantes :

- `grid-column-start` : Indique la ligne verticale de départ de l'élément
- `grid-column-end` : Indique la ligne verticale de fin de l'élément
- `grid-row-start` : Indique la ligne horizontale de départ de l'élément
- `grid-row-end` : Indique la ligne horizontale de fin de l'élément

Prenons le HTML suivant :
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
    grid-template-columns: 1fr 1fr 1fr; /* Trois colonnes égales */
    grid-template-rows: repeat(5, 100px); /* Cinq lignes de 100px de hauteur chacune */
    gap: 10px;
}

/* Ajout de bordures pour délimiter visuellement les cellules */
.conteneur > div {
    border: 1px solid black; /* Bordure de 1px en noir */
    padding: 10px; /* Espacement interne pour améliorer la lisibilité */
}

.une {
    grid-column: 1 / 4; /* Prend toute la largeur de la grille (colonne 1 à 4) */
}

.deux {
    grid-column: 1 / 2; /* Prend la première colonne */
    grid-row: 2 / 3; /* Prend la deuxième ligne */
}

.trois {
    grid-column: 2 / 4; /* Prend les colonnes 2 et 3 */
    grid-row: 2 / 3; /* Prend la deuxième ligne */
}

```

![[Pasted image 20240628214641.png]]