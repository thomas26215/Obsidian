---
Type de ressource: programmation
Langage: Kotlin
tags: []
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
- `val` : Immuables (on ne peut pas le modifier une fois initialisé). Variable pointe toujours sur la même réf mémoire
- `var` : Muable (on peut le modifier une fois initialisé). Variable pointe vers 1 réf mémoire, mais pourra être remplacée par une autre si nécessaire
> Kotlin invite toujours à déclarer les variables en immuables, pour rendre le code le + proche pssible de la programmation fonctionnelle et éviter les effets de bords<

Kotlin est un[[langage statiquement typés]], cependant, comme les dévs ont souhaités offrir les avantages de lisibilité des langages "[[langage dynamiquement typés]]" mais sans leurs inconvénients, c'est au moment de la compilation que les variables sont automatiquement déduits (comme en Python)
Cependant, il y a toujours la possilité d'indiquer le type de variable : 
`val name: String = "Thomas"` <=> `val name = "Thomas"`
`val age: int = 17` <=> `val age = 17`
De plus, pas besoin de points virgules !

### Initialisation
Il est possible d'initialiser la variables sans leurs assigner une valeur directement de la même manière qu'en Java
**Exemple** :
```Kotlin
val message: String
if(isUserHappy()){
	message = "Je suis heureux de l'entendre !"
}
else{
	message = "Qu'est ce qu'il ne va pas :("
}
```
Ceci est également une introduction aux [[Fonctions - Kotlin]]
On voit bien ici que la variable *message* a été initialisée à la ligne 1 mais qu'une valeur n'a été assignée qu'à la ligne 3 / 6

### Réductions des erreurs
Kotlin est un langage dit "sûr". Il évite d'ailleurs le problème le plus courant  grâce au *NullSafety* : le [[Gestion des valeurs nulles (Null Safety)]] 

### Affichage facile
Nous avons la possibilité de manipuler plus aisément les variables `String` : en utilisant `$` afin de faire référence à une variable directement à l'intérieur d'une autre :
**Exemple**
```Kotlin
val name = "Thomas"
print("Je m'appelle $name") //Affiche Je m'appelle Thomas
```
### Les constantes
En Java, pour déclarer une variable constante, on utilisait le mot clé `static`:
```Java
public static final String name = "Thomas";
```
Attention, en Kotlin, le mot-clé `static` n'existe plus !
Voici le code remplaçant :
```Kotlin
const val name: String = "Thomas"
```
Le mot clé `const` permet de définir une constante. Bien évidemment, elle ne pourra pas être modifiée lors de l'éxecution du programme
