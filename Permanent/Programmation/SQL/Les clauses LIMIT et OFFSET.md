---
MOOC: "[[Programmation]]"
Langage: 
Type: 
tags:
---
La [[Notion de clause|clause]] `LIMIT` permet de spécifier la limite de résultats pour la clause `WHERE`.

> Elle peut avoir plus d'intérêt si elle est précédée de la clause `ORDER BY`

**Exemple** :
```SQL
SELECT * FROM relation
[ORDER BY ..] LIMIT nombre_lignes_résultats
```

La clause `OFFSET` spécifie le nombre de n-uplets à ne pas conserver. Les n premiers n-uplets ne seront pas affichés

> Elle peut avoir plus d'intérêt si elle est précédée de la clause [[La clause ORDER BY|ORDER BY]] 

**Exemple** :
```SQL
SELECT * FROM relation
[ORDER BY ..] [LIMIT ..] OFFSET decalage
```
