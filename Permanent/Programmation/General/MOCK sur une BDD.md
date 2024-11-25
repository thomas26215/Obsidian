---
MOOC: "[[Programmation]]"
Langage: General
Type: MOCK
tags:
---
![[MOCK]]


Si nous voulons tester une fonction nécessitant une connexion à un BDD. La fonction peut dépendre d'une BDD mais la BDD n'est pas le focus ici. Nous ne voulons pas tester la base de données ou une connexion à celle-ci, mais nous voulons juste tester une fonction qui dépend ce cette chose

Au lieux de founir une connexion réelle à la BDD, nous pouvons fournir une fausse BDD à notre fonction. Certes, une connexion réelle à la BDD rendrait notre test plus *réel*, mais fournir une fausse BDD est considérée comme une interaction mockée, car elle simule quelque chose avec lequel notre fonction intéragit

Nous avons également des données mockées qui sont des fausses données utilisées pour les tests. Par exemple, la fausse BDD était juste pour que nous puissions commencer à tester notre fonction

Une fois que nous avons toutes les interactions dont notre fonction dépend, il faut réellement la tester. Pour se faire, on passe des entrées et on attend certaines sorties. Les entrées ont certes besoins de données, mais ce ne doit pas nécessairement être des données réelles de notre vraie base de données. Ainsi, nous pouvons utiliser des données mockées → Des fausses données