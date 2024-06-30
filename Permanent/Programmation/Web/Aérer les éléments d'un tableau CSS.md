---
MOOC: "[[Programmation]]"
Langage: Web
Type: Tableau
tags:
---
### Aérer les éléments
Il est possible d'ajouter de l'espace autour des éléments de la grille en utilisant la propriété `gap` :
```css
.conteneur {
    display: grid;
    grid-template-columns: 200px 200px 200px;
    grid-template-rows: 100px 150px 200px;
    gap: 10px;
}