---
MOOC: "[[Programmation]]"
Langage: Web
Type: Tableau
tags:
---
Ici, nous avons un *exemple* de code CSS qui permet de diviser les colonnes d'un tableau en CSS.
- **`.grid`** : Nous avons la mise en page d'un tableau (`display: grid`) avec un espace de 10px entre les éléments de la grille (`gap: 10px`) et la grille aura une colonne et occupera toute la largeur disponible (`grid-template-colummns: 1fr;`)
- **`@media`** : Cette règle s'appliquant pour tous les appareils qui ont plus de 1025px de largeur (` screen and (min-width: 1025px)`)  réorganise les éléments de la grille en 2 colonnes (`grid-template-columns: 1fr 1fr;`)

```CSS
.grid{
	display: grid;
	gap: 10px;
	grid-template-colummns: 1fr;
}
.grid article{
	background-color: silver;
}
@media screen and (min-width: 1025px){
	.grid{
		grid-template-columns: 1fr 1fr;
	}
}
```

---
**Links :**
[[Adapter le site en fonction des appareils en HTML]]
[[CSS - Des tableaux visuels avec les Grids !]]