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
- **Elément neutre :** Il existe un élément $(\forall e\in E)$ tel que pour tout $(x\in E),(x\oplus e=e \oplus x=x)$. En gros, c'est un élément qui n'agit sur rien
*Exemple* : Elément neutre de + est 0 car $x+0=0$




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

#### Théorème
Soit $(E, \oplus, \otimes)$ un dioïde :
- $e$ est absorbant pour $\oplus$ si la propriété d'absorption est vérifiée ([[#Réciproque Propriété d'absorption 1]])
- Si la propriété s'absorption est vérifiée, alors $\oplus$ est item potent ($\forall x\in E, x\oplus x = x$) ([[#Preuve de l'idem potent|preuve]])
- Si $e$ est absorbant pour $\oplus$ alors $\oplus$ est idem potent

#### Preuve de l'idem potent
$\forall(x,y)\in E^2,x\oplus x\otimes y=x$ (Propriété d'absorption)
1. On suppose que $e$ est absorbant pour $\oplus$ : $\forall x\in E, x\oplus e=e$ 
   $\forall(x,y)\in E^2, x\oplus x \otimes y = x\otimes e\oplus x \otimes y=x\otimes(e\oplus y)=x\otimes e=x$

#### Réciproque Propriété d'absorption 1
On suppose ($P$) : $\forall(x,y)\in E^2, x\oplus x\otimes y=x ⇒ \forall y\in E, e\oplus e\otimes y=e ⇒ \forall y\in E, e\oplus y=e$
**Conclusion :** P ⇒ $e$ absorbant pour $P$


#### Preuve
On suppose ($P$) : $\forall(x,y)\in E^2, x\oplus x\otimes y=x ⇒ \forall x\in E, x\oplus x\otimes e=x ⇒ x\oplus x$ ⇒ $\oplus$ est idem potent
**Conclusion :** P ⇒ $e$ absorbant pour $P$

### Preuve
On suppose ($P$) : $\forall(x,y)\in E^2, x\oplus x\otimes y=x ⇒ \forall y\in E, e\oplus e\otimes y=e ⇒ \forall y\in E, e\oplus y=e$

### Exemple pour définir un monoïde pour un graphe
Pour un graphe, je souhaite calculer le plus court chemin. Voici comment définir le dioïde :
⇒ $(R^+U\{+\infty\},MIN,+$)
$z=+\infty$
$e=0$
1. Domaine de définition, un graphe est définit dans $R^+$ et on aura aussi besoin de $\infty$
2. $\oplus$ permet de choisir le meilleur chemin, et on souhaite le chemin le plus court, ainsi on définit par MIN
3. 
4. $\otimes$ sert à calculer la valuation d'un chemin, et pour choisir le meilleur chemin, on va additionner les valeurs, donc on choisit +-

## Remplir le graphe pour déterminer le plus court chemin
Pour déterminer le plus court chemin d'un graphe, il faut tout d'abord définir le dioïde ([[Graphes#Exemple pour définir un monoïde pour un graphe|Exemple de définition]]) 
Ensuite il y plusieurs étapes :
### Initialisation
La matrice initiale $G_0$ correspond à la matrice d'adjacence aux arcs du graphe

 ### Relaxation des distances
Maintenant, passons à l'étape de relaxation des distances. À chaque étape $G_x$, où $x$ est déterminé par la taille de la matrice carrée, nous faisons ce qui suit :

- Tout d'abord, nous remplissons la colonne $x$ de la matrice en copiant simplement la colonne $x$ de la matrice précédente, $G_{x-1}$.
- Ensuite, pour chaque ligne de cette colonne que nous venons de remplir, si la valeur dans cette cellule est $\infty$ (ce qui signifie qu'il n'y a pas de lien direct entre les nœuds), alors nous recopions simplement la ligne de la matrice précédente.
- Enfin, pour les cellules vides (c'est-à-dire les cellules pour lesquelles nous n'avons pas encore de valeur), nous regardons la valeur $D[i][j]$ (la distance entre les nœuds $i$ et $j$). Nous la mettons à jour en prenant le minimum entre sa valeur actuelle et la somme des distances entre $i$ et $k$ et entre $k$ et $j$, où $k$ est un autre nœud du graphe.

C'est ainsi que l'algorithme de Warshall fonctionne pour trouver les chemins les plus courts entre tous les nœuds d'un graphe.



# Les différents algorithmes :
Algo Warshall : gloabal
Algo Ford-Belman : Local : (fixé l'origine)

## Algo Ford-Belman
Soit $G=(S,A,v)$ un graphe simple valuée dans le dioïde $(E, \oplus, \otimes)$
Soit $M$ la matrice d'incidence aux sommets
Soit $k\in\mathbb{N}^*$, $M^k=M\otimes M\otimes...\otimes M=\Pi^k_{i=1}M$
$N^k=\sum^k_{i=1}M^i=+M^2+...+M^k$ (Pour rappel, $M^*=\sum^\infty_{k=1}M^k$)
**Propriété :** 
1. $n_{ij}^k$ représente la valuation d'un meilleur chemin d'origine $i$ et d'extrémité $j$ ayant au plus $k$ arcs
2. $\oplus$ idem potent ⇒ $N^{(k)}=N^{(k-1)}\otimes(I\oplus M)$ 

<mark style="background: #FF5582A6;">Algorithme de Ford-Belman :</mark>
$L^{(k)}=L^{(k-1)}\otimes(I\oplus M)$ où $L^{(k)}$ est la ligne de $N{'k}$ correspond au sommet origine choisit
Arrêt en stabilisation $L^{(k)}=L^{(k-1)}$ 