---
MOOC: "[[Programmation]]"
Langage: SQL
Type: 
tags:
  - "#note_permanent"
  - status_finish
---
La requête `select` permet d'obtenir des informations à partir des [[Définition - relation|relations]] de la [[Définition - Base de données|BD]]. On dit qu'elle interroge la base de données.
→ Le résultat d'une requête `select` est un ensemble de n-uplets, dont certains peuvent être identiques
→ Pour qu'elle puis s'affiche, la requête doit se terminer par `;`
→ On peut modifier son résultat à partir de sous-requêtes

Voila la forme minimale d'une requête
```SQL
SELECT colonne_résultat
FROM relations
[{UNION|INTERSECT|EXEPT}select];
```