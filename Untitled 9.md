---
MOOC: "[[Cours]]"
Ressource: "R2.07 : Mathématiques"
Cours: Cours 2
Date: 
tags: 
Complete: false
Learned: false
---

# Concepts algébriques
## Monoïdes
Structure algébrique $(E,\oplus)$ défini par :
- **$\oplus$ est un loi interne :** Une opération binaire définie sur une ensemble, qui prend deux éléments de cet ensemble et qui renvoie un autre élément de cet ensemble.    *Exemple :* Addition sur les entiers → $\forall a,b\in\mathbb{R}, a+b\in\mathbb{R}$
- **Associativité :** $(\forall x, y, z\in E^3), (x\oplus(y\oplus z)=(x\oplus y)\oplus z) ⇒ x\oplus y\oplus z$
- **Elément neutre :** Il existe un élément $(e\in E)$ tel que pour tout $(x\in E),(x\oplus e=e \oplus x=x)$. En gros, c'est un élément qui n'agit sur rien
  *Exemple* : Elément neutre de + est 0 car $x+0=0$

>[!info]
>Monoïdes abéliens : qui sont des monoïdes où l'opération est commutative, càd que pour tout $(x,y\in E),(x\oplus y=y \oplus x)$

### Application d'un monoïde dans les graphes
Pour appliquer le concept de [[Monoïde|monoïde]] dans les graphes, on utilise les ensembles de opérations suivants :
- $(E)$ : ensemble des chemins possibles
- $(\oplus)$ : peut représenter la composition d'un chemin
- $(e)$ : représente le chemin de longueur nulle ou le chemin qui ne change rien
## Dioïde
Structure algébrique $(E, \oplus$, $\otimes$), $E$ un ensemble non-vide et $\oplus$ et $\otimes$ deux lois, définit par :
- $E$ un ensemble non-vide
- $(E,\oplus)$ un monoïde abélien (On note $z$ son élement neutre)
- $(E,\otimes$) un monoïde abélien (On note $e$ son élement neutre)
- $\otimes$ est **distributive** à $\oplus$
- $z$ est **absorbant** à $\otimes$ ⇒ $\forall x\in E, z\otimes x=x\otimes z=z$
- **Idempotent** : si $\forall x\in\mathbb{D},x\oplus x=x$
- **Propriété d'absorption** : Pour les opérations $\oplus$ et $\otimes$, l'opération $\otimes$ respecte certaines règles d'absorption par rapport à $\oplus$

>[!info] Que signifient $\oplus$ et $\otimes$ ?
>- $\oplus$ permet de choisir le meilleur chemin
>- $\otimes$ sert à calculer la valuation d'un chemin

### Exemple pour définir un dioïde pour un graphe
Pour un graphe, je souhaite calculer le plus court chemin. Voici comment définir le dioïde :
⇒ $(\mathbb{R}^+U\{+\infty\},MIN,+$)
$z=+\infty$
$e=0$
1. Domaine de définition, un graphe est définit dans $R^+$ et on aura aussi besoin de $\infty$
2. $\oplus$ permet de choisir le meilleur chemin, et on souhaite le chemin le plus court, ainsi on définit par MIN
3. $\otimes$ sert à calculer la valuation d'un chemin, et pour choisir le meilleur chemin, on va additionner les valeurs, donc on choisit +-
### Propriétés
- Un élément $e\in\mathbb{D}$ est absorbant pour $\oplus$ si $\forall x\in \mathbb{D},e\oplus x=e$ (**Propriété d'absorption**)
- Si la propriété s'absorption est vérifiée, alors $\oplus$ est item potent ($\forall x\in E, x\oplus x = x$)
- Si $e$ est absorbant pour $\oplus$ alors $\oplus$ est idem potent

#### Preuve de l'idempotence
$\forall(x,y)\in E^2,x\oplus x\otimes y=x$ (Propriété d'absorption)
On suppose que $e$ est absorbant pour $\oplus$ : $\forall x\in E, x\oplus e=e$ 
   $\forall(x,y)\in E^2, x\oplus x \otimes y = x\otimes e\oplus x \otimes y=x\otimes(e\oplus y)=x\otimes e=x$

#### Preuve de la propriété d'idempotence
On suppose ($P$) : $\forall(x,y)\in E^2, x\oplus x\otimes y=x ⇒ \forall x\in E, x\oplus x\otimes e=x ⇒ x\oplus x$ ⇒ $\oplus$ est idem potent
**Conclusion :** P ⇒ $e$ absorbant pour $P$

#### Réciproque Propriété d'absorption 1
On veut montrer que $P$ implique que $e$ est absorbant pour $\oplus$
On suppose ($P$) : $\forall(x,y)\in E^2, x\oplus x\otimes y=x ⇒ \forall y\in E, e\oplus e\otimes y=e ⇒ \forall y\in E, e\oplus y=e$
**Conclusion :** P ⇒ $e$ absorbant pour $P$

#### Preuve
On suppose ($P$) : $\forall(x,y)\in E^2, x\oplus x\otimes y=x ⇒ \forall y\in E, e\oplus e\otimes y=e ⇒ \forall y\in E, e\oplus y=e$

# Les différents algorithmes pour un graphe :
Algo Warshall : gloabal
Algo Ford-Belman : Local : (fixé l'origine)

## Algo Ford-Belman
Soit $G=(S,A,v)$ un graphe simple valuée dans le dioïde $(E, \oplus, \otimes)$
Soit $M$ la matrice d'incidence aux sommets
Soit $k\in\mathbb{N}^*$, $M^k=M\otimes M\otimes...\otimes M=\Pi^k_{i=1}M$
$N^k=\sum^k_{i=1}M^i=M+M^2+...+M^k$ (Pour rappel, $M^*=\sum^\infty_{k=1}M^k$)
**Propriété :** 
1. $n_{ij}^k$ représente la valuation d'un meilleur chemin d'origine $i$ et d'extrémité $j$ ayant au plus $k$ arcs
2. $\oplus$ idem potent ⇒ $N^{(k)}=N^{(k-1)}\otimes(I\oplus M)$ 

<mark style="background: #FF5582A6;">Algorithme :</mark>
1. **Initialisation**
   $L^{(0)}=I\otimes M$ où I est la matrice identité
2. **Itérations**
   $L^{(k)}=L^{(k-1)}\otimes(I\oplus M)$ où $L^{(k)}$ est la ligne de $N{'k}$ correspond au sommet origine choisit
3. **Arrêt**
   Arrêt en stabilisation $L^{(k)}=L^{(k-1)}$ 

## Exemple
### Plus court chemin
0. **Définition :**
   $D=(\mathbb{R}_+U\{+\infty\}, min, +)$ ⇒ [[#Dioïde|Définition d'un dioïde]]
   $A=\mathbb{R}_+U\{\infty\}$
   $a=v(a)$
1. **Propriété d'absorption est validée car** $\forall x\in\mathbb{R}, min(x,0)=0$. Ca sert ç ce que l'algo converge
2. **Propriété d'idempotence validée :** $\forall x\in\mathbb{R}_+, min(x,x)=x$
3. ...
4. On peut donner un sens au coefficient $



## Algo Warshall + plus court chemin
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

