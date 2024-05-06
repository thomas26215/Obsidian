---
MOOC: "[[Cours]]"
Ressource: "R2.09 : Mathématiques"
Cours: Graphes
Date: 
tags: 
Complete: false
Learned: false
---
**La base :**
G(S, A, V)
- S : Sommet ⇒ L'ensemble des points du graphe
- A : Arc ⇒ L'ensemble des traits reliant les différents points
- V : Valuation des arc

La **multiciplé** d'un arc est le nombre d'arcs d'un point à un autres
[[Drawing 2024-05-06 00.12.26.excalidraw]]
Multiplicité d'un arc =>
- (1,2) ⇒ 2
- (2,3) ⇒ 0
- (4,3)

En prenant ce graphe :
[[Drawing 2024-05-06 00.17.56.excalidraw]]
**Matrice d'adjacence aux sommets** :

|     | 1   | 2   | 3   | 4   |
| --- | --- | --- | --- | --- |
| 1   | -   | a   | c   | d   |
| 2   | -   | -   | b   | -   |
| 3   | -   | -   | -   | e   |
| 4   | -   | -   | -   | -   |

**Matrice booléenne** :

|     | 1   | 2   | 3   | 4   |
| --- | --- | --- | --- | --- |
|     | 0   | 0   | 1   | 1   |
|     | 0   | 0   | 1   | 0   |
|     | 0   | 0   | 0   | 1   |
|     | 0   | 0   | 0   | 0   |
**Matrice d'incidence aux arcs :**

|     | a   | b   | c   | d   | e   | f   |
| --- | --- | --- | --- | --- | --- | --- |
| 1   | 1   | 0   | 1   | 1   | 0   | 1   |
| 2   | -1  | 1   | 0   | 0   | 0   | -1  |
| 3   | 0   | -1  | -1  | 0   | 1   | 0   |
| 4   | 0   | 0   | 0   | -1  | 1   | 0   |
**Vocabulaire :**
- <mark style="background: #BBFABBA6;">Chemin</mark> : Une suite d'arc ($a_1,...a_ n$) avec $T(a_i)=I(a_{i+1}),\forall i\in[1..n-1]$
  $I[a_1]$ = origine du point
  $T[a_n]$ = terminale du point
  $N$ = Longueur du point
	- <mark style="background: #FF5582A6;">Chemin simple</mark> ⇒ Arcs distincts : 1,2,3
	- <mark style="background: #FF5582A6;">Chemin élémentaire</mark> ⇒ Sommets distincts
	- <mark style="background: #FF5582A6;">Circuit</mark> ⇒ Chemin élémentaire de même extrémités terminales
- <mark style="background: #BBFABBA6;">Chaîne</mark> = Arc sans sens
   