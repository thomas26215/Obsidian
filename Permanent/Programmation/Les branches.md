---
MOOC: "[[Programmation]]"
Langage: Git
Type: 
tags:
---
Quand on fait un git init, on est automatiquement sur la branche init, la branche de base. Cependant, il est possible de travailler sur d'autres branches afin de travailler sur des versions en parallèles. Le risque qu'il pourrait y avoir est que quand je travaille sur quelque chose (exemple : modifier le style css d'une page ...) et que je souhaite publier une petite modification rapidement, et bien je suis bloqué  car je suis en train de travailler sur mon nouveau style

- `git branch nom` = Créer une nouvelle branche
- `git checkout nom` = Sauter d'une ranche à l'autre
- `git branch -d nom` = Supprimer une branche

Une fois que les modifications sur les différentes brahes ont été terminées, il faut maintenant les ramener à la branche courante, de base la branche master. Pour faire une fusion, il faut tout d'abord que je me situe sur la branche sur laquelle je souhaite faire la fusion. Il faut ensuite que j'exécute la commande `git merge nom_branche`, avec `nom_branch` le nom de la branche avec laquelle je souhaite fusionner. Ainsi, on remarque que les modifications faites sur la branche extenerne sont ajoutée à la branche actuelle. On peut maintenant supprimer la branche externe (`git branch -d nom`)
Si mes deux branches ont avancées (Plusieurs commit sur les deux branches) et que je souhaite fusionner ces dernières, il va y avoir un auto-merging.
Il peut également y avoir des <mark style="background: #FF5582A6;">conflits</mark>. Cela arrive quand il essaye de fusionner les branches mais qu'il n'y arrive pas. Cela arrive généralement quand il y a des modifications sur des fichiers a peu près aux mêmes endroits. Pour les résoudre, il faut enlever les commentaires et garder uniquement le code que je souhaite envoyer