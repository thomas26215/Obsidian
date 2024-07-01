---
MOOC: "[[Programmation]]"
Langage: Kotlin
Type: Basics
tags:
---
Les variables Kotlin sont assez différentes de celles de Java
En effet, En Java, nous avons l'habitude de déclarer nos variables comme ceci :
`String question = "Quel est ton nom ?;"`
`int number = 1;`
Cependant, les variables Kotlin ne sont pas déclarées de la même manière.
Voici trois exemple de déclarations qu'il peut exister :
`val question = "Quel est ton prénom ?"`
`val question: String = "Quel est ton prénom ?"`
`var question: String = Quel est ton prénom ?"`

Comme on peut le voir, on peut déclarer des variables grâce aux mots-clés `var` et `val` :
- `val` : Immuables (on ne peut pas le modifier une fois initialisé)
- `var` : Muable (on peut le modifier une fois initialisé)