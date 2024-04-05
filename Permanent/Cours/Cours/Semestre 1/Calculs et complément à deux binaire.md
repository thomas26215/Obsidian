---
MOOC: "[[Cours]]"
Ressource: "R1.03 : Architecture des ordinateurs (données et instructions)"
Cours: "Cours 2 : Entiers relatifs et complément à deux"
Date: 
tags: 
Complete: false
Learned: false
---
# Entiers relatifs
Il est tout à fait possible d'afficher des nombres relatifs en binaire. Pour cela, il faut modifier l'utilité du poids fort, et il n'affichera plus un nombre, mais le signe du chiffre. Par exemple :
`<%00000001>deux = <1>dix`
`%10000001>deux = <-1>dix`
L'avantage est donc de pouvoir afficher des nombres relatifs. Cependant, il y a un inconvénient à cette méthode, en effet, le nombre de combinaisons est réduite pour afficher un nombre. Ainsi, pour afficher des entiers naturels, il était possible de les afficher de **0 à 255** mais avec les nombres relatifs, cette valeur s'étend de **-127 à 127**.
La notation est également changée :
`<%00000001>deux` ⇒ `<%00000001>±||`

# Complément à deux

Le complément à deux est une méthode couramment utilisée en informatique pour représenter les nombres négatifs de manière binaire, facilitant ainsi les opérations arithmétiques. Voici comment cela fonctionne, en reprenant votre exemple :

Considérons la notation `<%00110100>Compl.2`. Cela représente un nombre en complément à deux.

- Pour le nombre positif $00001010_2$, son complément à deux serait identique à sa représentation binaire actuelle.
    
- Pour le nombre négatif $-00001010_2$, pour obtenir son complément à deux, on inverse tous les bits (passage de 1 à 0 et vice versa) et on ajoute 1 au résultat. Cela donne $11110110$​.

On peut maintenant y appliquer les méthodes basiques de calcul binaire (Addition, Soustraction)

**Il faut savoir qu'un nombre relatif en complément à 2 et un nombre entier en  base deux ne pourront jamais être calculés ensemble ! Pour que deux nombres puissent être calculés ensemble, il doivent être de la même base. C'est le même principe qu'on ne peut pas calculer ensemble un nombre base deux et un nombre base 10**

<mark style="background: #FF5582A6;">Compléter avec les trois méthodes</mark>

# Opération arithmétique avec le complément à deux
## Addition
Même principe que pour les additions.
`<27>dix = <%00011011>`
`<-45>dix = <%11010011>`
`<27>dix + <-45>dix = <%00011011> + <%11010011>`
**Complément à deux = inverser résultat**

## Soustraction
La soustraction en binaire suit un processus similaire à celui utilisé dans d'autres systèmes numériques, mais avec quelques différences notables. Contrairement à la soustraction décimale où la retenue est de 10, la soustraction binaire utilise une retenue de 2. De plus, lorsqu'il est nécessaire d'emprunter (prendre une retenue) lors de la soustraction, on emprunte une valeur de 1 au lieu de 10 comme dans le système décimal.

## Le débordement
<mark style="background: #FF5582A6;">Compléter</mark>

---
**Questions :**
1. Quelle est la notation d'un entier relatif en binaire ?
2. Comment est représenté le signe ?
3. Quel est l'inconvénient ?
4. Quelle est la notation du complément à deux ?
5. Pourquoi utilise-t-on le complément à deux ?
6. Donner le complément à deux de $00001010_2$ et de $-00001010_2$
7. Peut on calculer un complément à deux avec un nombre base 2 ? Avec une virgule fixe ? Pourquoi ?
8. Avec le complément à deux, comment faire une addition ?
9. Avec le complément à deux, comment faire une soustraction ? Calculer 45 - 27
10. Qu'est ce que le débordement ? Calculer 45 - 27