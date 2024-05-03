---
MOOC: "[[Programmation]]"
Langage: SQL
Type: Abstrait
tags: []
---
1. **1ère Forme Normale (1FN)** : Cela signifie que chaque information dans une base de données doit être simple et ne pas être un mélange de plusieurs choses. En d'autres termes, chaque donnée doit représenter une chose unique du monde réel. Par exemple, dans une base de données d'informations sur les élèves, le nom et le prénom d'un élève ne devraient pas être mélangés dans une seule cellule. Ils devraient être séparés.
2. **2ème Forme Normale (2FN)** : Pour être en 2FN, une base de données doit être en 1FN, et en plus, toutes les informations qui ne font pas partie de l'identifiant d'une entité (comme un numéro d'identification unique) doivent dépendre entièrement de cet identifiant. En d'autres termes, chaque information doit être directement liée à la chose qu'elle décrit. Par exemple, si tu as une base de données d'achats, le prix d'un article doit dépendre de l'identifiant de cet article, et non d'autres informations.
3. **3ème Forme Normale (3FN)** : Pour être en 3FN, une base de données doit être en 2FN, et en plus, chaque information qui ne fait pas partie de l'identifiant d'une entité ne doit pas dépendre d'autres informations qui ne font pas partie de cet identifiant. En d'autres termes, chaque information doit être indépendante des autres. Par exemple, si tu as une base de données d'employés, le salaire d'un employé ne doit pas dépendre du département dans lequel il travaille, car le département n'est pas une partie de l'identifiant de l'employé.