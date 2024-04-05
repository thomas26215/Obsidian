---
MOOC: "[[Cours]]"
Ressource: "R1.03 : Architecture des ordinateurs (données et instructions)"
Cours: "Cours 3 : Virgule fixe"
Date: 2023-11-27
tags: 
Complete: false
Learned: false
---
# Nombres réels
Il existe deux nombre à virgules (donc qui ont une partie entière et une partie fractionnaire) :
→ Virgule fixe
→ Virgule flottante
On va ici s'intéresser à la notion de nombres réels à virgule fixe

## Notation
### Normale
On écrit un nombre à virgule fixe comme ceci :
`<%001010...101>V.F(x,y)`
Avec `V.F` qui signifie Virgule fixe, $x$ un nombre qui correspond au nombre de bits représentant la partie entière du nombre et $y$ un nombre représentant les bits désignant la partie fractionnaire du nombre.
**Exemple :**
`<18,625>dix` = `<%0001 1010 1010>V.F(8,4)`
Ici, les 8 premiers bits représentent la partie entière du nombre et les 4 derniers bits représentent la partie décimale du nombre
On pourrait aussi le représenter de cette manière :

### Complément à deux
On note un nombre réel en complément à deux comme ceci :
`<%0010 1010, 0110>V.F(8,4).cpt2`
Pour avoir un nombre réel en complément à deux, c'est le même principe que pour les nombres entiers à complément à deux.
**Voici un exemple :**
`<-47,725>dix` = `-<%0010 1111 1100>V.F(8,4)` = `<%1101 0000 0100>V.F(8,4).cpt2`

## Dynamique de codage et bornes de l'intervalles des valeurs codées
On rappelle que la dynamique de codage est la représentation binaire de la plus petite valeur possible et de la plus grande valeur possible.
Ainsi, en prenant la notation `<>V.F(10,6).cpt2`, on a :
→ Plus petite : `<%1000 0000 0000 0000>`
→ Plus grande : `<%0111 1111 1111 1111>`

Les bornes sont $-2^9$ et $2^9-2^6$
La précision du codage est de $2^{-6}$

## Erreur de troncature
Une erreur de troncature est la valeur à coder - valeur codée
**Ex :** `<0,45>dix` = `<%0,01>V.F.(1,2)`. Erreur de troncature = 0,45-0,25=0,2

---
**Links :**
1. Quels sont les deux types de nombres réels ?
2. Comment représenter un nombre réel en binaire en utilisant $x$ et $y$. A quoi correspondent-ils ?
3. Prendre `<18,625>dix` et le représenter en binaire. Faire de même pour `<-18,625>dix`
4. Donner la dynamique de codage et l'intervalles de valeurs codées