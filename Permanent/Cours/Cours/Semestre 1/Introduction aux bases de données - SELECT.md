---
MOOC: "[[Cours]]"
Ressource: "R1.05 : Introduction aux bases de données et SQL"
Cours: "Cours 2 : Introduction aux bases de données - SELECT"
Date: 2023-09-19
tags:
  - status_toReformulate
  - note_cours
Complete: true
Learned: true
---
[[La requête SELECT]]
[[Notion de clause]]

Voici ce qui est étudié dans ce cours :

```SQL
SELECT colonnes_resultats FROM relations
[WHERE condition ]
[GROUP BY condition]
[HAVING condition_sur_groupes]
[ORDER BY critère_tri_résultat]
[LIMIT nombre_lignes_résultats]
[OFFSET décalage]
[{UNION|INTERSECT|EXEPT}select];
```

[[La clause DISTINCT]]
[[La clause WHERE]]
[[La clause ORDER BY]]
[[Les clauses LIMIT et OFFSET]]
[[Fonctions et opérateurs SQL]]
[[Opérations ensemblistes]]

# Les groupements SQL
La clause `GROUP BY` sert à regrouper les lignes qui ont les mêmes valeurs dans une ou plusieurs colonnes.

**Exemple** :
```SQL
SELECT count(*)
FROM lecture
GROUP BY theme
```
Originallement, la requête va compter le nombre total de livres dans la relation lecture. Cependant, la clause `GROUP BY` m'indique qu'il faut que je sépare par thème. Ainsi, ca ne me renverra pas une seule ligne avec le nombre total de lignes, mais plusieurs lignes avec le nombre de livres par `theme`

# HAVING
La clause `HAVING` suit généralement une requête `GROUP BY`. Cela permet de quels sous groupes doivent être conservés.

**Exemple** :
```SQL
SELECT count(*)
FROM lecture
GROUP BY theme
HAVING count(*) > 2
```
Ici, la requête me permet de récupérer les nombre de livres par thème (cf Clause GROUP BY). Cependant, la clause `HAVING` m'indique que je dois avoir au moins deux livres présents dans la catégorie pour que la ligne s'affiche

# Sous-requête
Une sous requête est une requête intégrée dans une requête plus grande. La sous-requête est effectuée avant la requête principale, et le résultat de la sous-requête est utilisée dans la colonne principale