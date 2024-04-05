---
MOOC: "[[Programmation]]"
Langage: SQL
Type: 
tags:
  - status_finish
  - note_permanent
---
La [[Notion de clause|clause]] `WHERE` permet de filtrer le résultat. En effet, pour qu'un n-uplet fasse partit du résultat, il faut qu'il vérifie la clause `WHERE`.
→ Il peut utiliser des opérateurs logiques (`AND`, `OR`, `NOT`)
→ Il peut utiliser des outils de comparaison
→ Il peut être comparé à `NULL` : `val{IN|IN NOT} NULL`
→ Il peut être comparé à une appartenance de même type : `val {IN|IN NOT}(val1, ...)`
→ Il peut être comparé à un intervalle du même type : val {BETWEEN | NOT BETWEEN } val1 and val2 `val {BETWEEN | NOT BETWEEN } val1 and val2`