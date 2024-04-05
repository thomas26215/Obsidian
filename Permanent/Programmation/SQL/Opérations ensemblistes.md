**Forme générale** :
```SQL
SELECT ...
{UNION|INTERSECT|EXCEPT}[ALL|DISTINCT]
SELECT ...
[ORDER BY ...][OFFSET ...][LIMIT ...];
```
Les opérateurs ensemblistes `UNION`, `INTERSECT`, `EXCEPT` permettent de construire un résultat à partir de deux instructions `SELECT`
Il y a quelques contraintes :
- Les deux instructions `SELECT` doivent avoir le même nombre de colonnes
- Le type d'une colonne du premier `SELECT` doit être compatible avec le type de colonne de même rang de deuxième `SELECT`

## UNION
L'opérateur ensembliste `UNION` permet de combiner le résultat envoyé par deux clauses `SELECT`. Autrement dit, pour qu'un n-uplet apparaisse dans le résultat, il doit appartenir au résultat d'au moins un des deux `SELECT`
**Exemple** :
```SQL
SELECT .. FROM ..
WHERE ..
UNION
SELECT .. FROM ..
WHERE ..
```

## INTERSECT
l'opérateur `INTERSECT` va nous permettre de récupérer le résultat des résultats présent dans le premier `SELECT` ET dans le deuxièe `SELECT`

## EXCEPT

L'opérateur ensembliste `EXCEPT` va retourner en résultat le résultat du premier `SELECT` mais ceux qui sont présents dans le deuxième `SELECT` ne seront pas affichés même s'ils sont présents dans le premier `SELECT`

**Exemple** :
```SQL
SELECT .. FROM ..
WHERE ..
EXCEPT
SELECT .. FROM ..
WHERE ..
```