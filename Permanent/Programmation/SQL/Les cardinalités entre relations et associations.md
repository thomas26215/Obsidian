---
MOOC: "[[Programmation]]"
Langage: SQL
Type: Abstrait
tags: []
---
**Les cardinalités** sont des règles qui indiquent combien de fois certaines choses peuvent être reliées entre elles. Les cardinalités sont représentées par un couple de valeurs : **(min, max)**.
1. **min** : Cette valeur peut être 0, 1 ou n (indéfini) et cela indique combien d'occurences de l'entité peuvent être liées à l'association au minimum
2. **max** : Cette valeur peut être 1 ou n (indéfini) et cela indique combien d'occurences de l'entité peuvent être liées à l'association au minimum
**Exemples :**
`Patient(NSS, NomPatient, Prénom, DateNaissance, DateNaissance, Adresse, Antecedants)`
`Ordonnance(NumOrdonnance, Prescriptions)`
Et association `Etablie_Pour`
- **PATIENT → Prescrit_Pour** : Un patient peut ne jamais se faire prescrire d'ordonnance (**min = 0**) mais peut aussi s'en faire prescrire une infinité (**max = n**)
- **ORDONNANCE → Prescrit_Pour** : Une ordonnance est prescrite pour un et un seul patient (**min = 1** et **max = 1**)