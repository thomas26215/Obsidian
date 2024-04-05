---
MOOC: "[[Cours]]"
Ressource: "R1.06 : Mathématiques discrètes"
Cours: "Cours 2 : La base de l'arithmétique"
Date: 2023-11-21
tags: 
Complete: true
Learned: true
---
[[La division euclidienne]]
[[Les nombres premiers]]

[[Décomposition en facteurs premiers]]
[[Le PGCD]]
[[Le PPCM]]

[[Algorithme d'Euclide]]
[[Tableau d'Euclide Bézout]]
# Equation diophentienne
Résoudre $11x+7y=1$, c'est trouver tous les couples $(x,y)\in\Z$ vérifiant l'équation
## Première étape : Trouver une solution particulière
Méthode pour trouver une solution particulière : [[Tableau d'Euclide Bézout]]

| a   | b   | r   | q   | u   | v   |
| --- | --- | --- | --- | --- | --- |
| 11  | 7   | 4   | 1   | 1   | -1  |
| 7   | 4   | 3   | 1   | -1  | 2   |
| 4   | 3   | 1 (c'est lui)  | 1   | 2   | 3   |
| 3   | 1   | 0   |     |     |     |
$11*2+7*(-3)=1$

## Deuxième étape : Equation homogène
$L_1\space11x+7y=1$
$L_2\space 11*2+7*(-3)=1$
$⇒ 11(x-2)+7(y+3)=0 ⇔ 11(x-2)=-7(y+3)$

Donc $11|7(y+3)$ Or $pgcd(11, 7)=1$ donc $11|(y+3)$ d'après le lemme de Gauss et $y+3=11k ⇔ y=11k-3$
En replongeant dans l'équation homogène, nous obtenons $11(x-2)=-7*11k ⇔ x-2=-7k ⇔ x=-7k+2$.

## Troisième étape : Vérifications
Vérifions $(-7k+2, 11k-3)$ solutions de l'équation :
$11*(-7k)+7*11k=1$


---
**Questions :**
1. Donner les propriétés des divisions euclidiennes
2. En langage logique, comment s'écrit *b divise a* ?
3. Qu'est ce que la transposition de la division ?
4. Que se passe-t'li si $q$ divise $a$ et $b$ ?
5. Qu'est ce qu'un nombre premier ?
6. Comment prouver facilement qu'un grand nombre est premier ou non ?
7. Qu'est ce que la décomposition en facteurs de nombre premier ?
8. Qu'est ce que le PGCD ? et le PPCM ?
9. Deux nombres non nuls $a$ et $b$ premiers entre eux. Que vaut $pgcd(a,b)$ ?
10. Donner les propriétés du $pgcd$
11. Qu'est ce que l'algorithme d'Euclide ?