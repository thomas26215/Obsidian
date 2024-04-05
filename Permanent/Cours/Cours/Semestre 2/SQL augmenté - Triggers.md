---
MOOC: "[[Cours]]"
Ressource: "R2.06 : SQL"
Cours: "Cours 5 : SQL augmenté - Triggers"
Date: 2024-03-12
tags: 
Complete: false
Learned: false
---
# Variables
En plus du bloc BEGIN et END, il existe le bloc DECLARE afin de déclarer des variables
**Exemple :**
- `nom type;`
- `nom type := expression;`
- `nom CONSTANT type := expression;`

- Les types sont les mêmes que pour les attributs de table
	1) Les n-uplets
		- `RECORD`
		- `nom_table`
	2) Pour une variable simple :
		- `nom_table.nom_att%TYPE`
## Instructions
- `var := val;`
- `IF ... THEN ... ELSIF ... THEN ... ELSE ... ENF IF;`
- `FOR ... IN[REVERSE] ... LOOP...END LOOP;`
- `WHILE...LOOP...END LOOP`
- `IF ... WHERE`
- `FOR..SUM, AVG..`

Il est possible de faire des mélanges :
- `IF EXISTS(SELECT ...) THEN ... END IF;`
- `FOR var1,var2 IN SELECT ... LOOP ... END LOOP;`

## Variable prédéfinie FOUND
⇒ Statut du résultat d'une requête
→ Positionné par la dernière exécution de :
- `SELECT ... INTO`
- `UPDATE`, `INSERT`, `DELETE`
- `FOR`