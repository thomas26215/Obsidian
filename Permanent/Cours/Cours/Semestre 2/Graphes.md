---
MOOC: "[[Cours]]"
Ressource: "R2.07 : Mathématiques"
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


# Algorithe de Warshall
Il est utilisé pour trouver la fermeture transitive d'un graphe orienté. Cela signifie qu'il détermine si un chemin existe entre deux noeuds pour tous les paires de noeurs dans le graphe

## Monoïde
Structure algébrique $(E,\oplus)$ défini par :
- **$\oplus$ est un loi interne**
- **Opération binaire interne :** $\forall(x, y \in E)$, $(x \oplus y\in E)$
- **Associativité :** Pour tous $(x, y, z\in E^3), (x\oplus(y\oplus z)=(x\oplus y)\oplus z) ⇒ x\oplus y\oplus z$
- **Elément neutre :** Il existe un élément $(\forall e\in E)$ tel que pour tout $(x\in E),(x\oplus e=e \oplus x=x)$

Il existe aussi des monoïdes abéliens, qui sont des monoïdes où l'opération est commutative, càd que pour tout $(x,y\in E),(x\oplus y=y \oplus x)$

## Application dans les graphes
Pour appliquer le concept de [[Monoïde|monoïde]] dans les graphes, on utilise les ensembles de opérations suivants :
- $(E)$ : ensemble des chemins possibles
- $(\oplus)$ : peut représenter la composition d'un chemin
- $(e)$ : représente le chemin de longueur nulle ou le chemin qui ne change rien

## Dioïde
Structure algébrique $(E, \oplus$, $\otimes$), $E$ un ensemble non-vide et $\oplus$ et $\otimes$ deux lois, définit par :
- $E$ un ensemble non-vide
- $(E,\oplus)$ un monoïde abélien (On note $z$ son élement neutre)
- $(E,\otimes$) un monoïde abélien (On note $e$ son élement neutre)
- $\otimes$ est distributive à $\oplus$
- $\oplus$ est absorbant à $\otimes$ ⇒ $\forall x\in E, z\otimes x=x\otimes z=z$ 
>[!info] Que signifient $\oplus$ et $\otimes$ ?
>- $\oplus$ permet de choisir le meilleur chemin
>- $\otimes$ sert à calculer la valuation d'un chemin
### Exemple pour définir un monoïde pour un graphe
Pour un graphe, je souhaite calculer le plus court chemin. Voici comment définir le dioïde :
⇒ $(R^+U\{+\infty\},MIN,+$)
1. Domaine de définition, un graphe est définit dans $R^+$ et on aura aussi besoin de $\infty$
2. $\oplus$ permet de choisir le meilleur chemin, et on souhaite le chemin le plus court, ainsi on définit par MIN
3. $\otimes$ sert à calculer la valuation d'un chemin, et pour choisir le meilleur chemin, on va additionner les valeurs, donc on choisit +


   
