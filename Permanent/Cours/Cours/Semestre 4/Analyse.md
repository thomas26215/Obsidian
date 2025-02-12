# Théorie des graphes et réseaux de transport

## 1. Introduction

La théorie des graphes est un domaine mathématique étudiant les relations entre objets. Elle s'applique notamment à la modélisation des réseaux de transport.

## 2. Notions de base en théorie des graphes

- **Graphe** : Couple G = (S,A) où S est l'ensemble des sommets et A l'ensemble des arêtes.
- **Graphe orienté** : Arêtes avec direction (appelées arcs).
- **Chemin** : Séquence de sommets reliés par des arêtes.
- **Cycle** : Chemin dont le premier et dernier sommet sont identiques.
- **Degré d'un sommet** : Nombre d'arêtes incidentes.
- **Connexité** : Existence d'un chemin entre toute paire de sommets.

## 3. Réseaux de transport

### 3.1 Définition

Un réseau de transport est un graphe orienté G = (S,A,c) où :
- S : ensemble des sommets (points de transit)
- A : ensemble des arcs (liaisons)
- c : fonction de capacité c : A → R+

Propriétés :
- Sommet source (e) : uniquement des arcs sortants
- Sommet puits (s) : uniquement des arcs entrants

### 3.2 Notion de flot

Un flot f : A → R+ vérifie :
1. Contrainte de capacité : ∀(i,j) ∈ A, f(i,j) ≤ c(i,j)
2. Conservation du flot : ∀x ∈ S\{e,s}, Σf(a)_entrant = Σf(a)_sortant
3. Valeur du flot v(f) : quantité totale source-puits

### 3.3 Définition 3

Quand $f$ est un flot, $f(a)$ est le flux de l'arc $a$. La valeur du flot est $$\forall(f)=\sum_{(e, i)\in A}f(e, i)=\sum_{(i, s)\in A}f(i, s)$$
C'est cette quantité que l'on cherche à maximiser

### 3.4 Définition
$f$ un flot dans un réseau de transport $G=(S, A, c)$ :
- Un arc $(i, j)$ est saturé si $f(i, j) = c(i, j)$
- Un flot est dit complet si tous les chemins de $e$ à $s$ ont un arc saturé
- Un flot est dit maximal si sa valeur est maximale

## 4. Problème du flot maximum

Objectif : trouver un flot de valeur maximale.

### 4.1 Algorithme de Ford et Fulkerson (1956)

4. Initialiser le flot à 0
5. Tant qu'il existe une chaîne élémentaire admissible e-s :
   - Calculer m = min(min(c(a) - f(a)) pour a ∈ U, min(f(a)) pour a ∈ V)
   - Augmenter le flot de m sur U, diminuer de m sur V
6. Flot maximal atteint sans chaîne admissible

**Chaînes élémentaire admissible** : Pour tout arc $a$ de la chaîne :
1. $a\in U =>  f(a) < c(a)$ 
2. $a\in V => f(a) > 0$
## 5. Théorème de la coupe minimale

Coupe : ensemble d'arcs (Y, Ȳ) avec e ∈ Y et s ∉ Y

**Théorème** : Valeur du flot maximum = capacité de la coupe minimale

## 6. Couplage maximal dans un graphe biparti

### 6.1 Définitions

**Graphe biparti** : Un graphe $G = (S, A)$ est dit biparti si l'on peut séparer l'ensemble des sommets $S$ en deux parties disjointes $U$ et $V$ telles que :
- $U \cup V = S$ (tous les sommets sont répartis entre $U$ et $V$),
- $U \cap V = \varnothing$ (les deux ensembles sont disjoints),
- chaque arête de $A$ relie un sommet de $U$ à un sommet de $V$.
**Couplage** : Arêtes sans sommet commun - Un ensemble de d'arêtes tels que 2 à 2 non adjacents
**Couplage maximal** : Tel que si on ajoute une arête $A$ à $C$, $C \cup A$ n'est plus un couplage
**Couplage maximum** : Plus grand nombre d'arêtes. 
**Couplage parfait** : Couvre tous les sommets

### 6.2 Théorème des Mariages (ou Lemme des Mariages ou Théorème de Hall)

Le théorème des mariages est un résultat fondamental en combinatoire et en théorie des graphes. Il donne une condition nécessaire et suffisante pour l'existence d'un système de représentants distincts dans une famille d'ensembles finis.

#### Énoncé du Théorème

Soient $F$ et $G$ deux ensembles finis, et une application $c : F \to \mathcal{P}(G)$, où $c(f) \subseteq G$ représente les choix possibles pour chaque élément $f \in F$. Le théorème énonce que :

> Il existe une fonction injective $\phi : F \to G$ telle que $\phi(f) \in c(f)$ pour tout $f \in F$, si et seulement si, pour tout sous-ensemble $F_0 \subseteq F$, on a :
>
> $|c(F_0)| \geq |F_0|,$
>
> où $c(F_0) = \bigcup_{f \in F_0} c(f)$.

#### Interprétation Matrimoniale

Dans un contexte de mariage :

*   $F$ représente un ensemble de filles.
*   $G$ représente un ensemble de garçons.
*   Chaque fille a une liste de garçons acceptables (donnée par l'application $c(f)$).

Le théorème garantit qu'il est possible de marier chaque fille à un garçon de sa liste, sans qu'aucun garçon ne soit marié à plus d'une fille, si et seulement si la **condition de mariage** est satisfaite : pour tout groupe de filles, la réunion de leurs listes contient au moins autant de garçons que le nombre de filles dans ce groupe.

### Applications

Le théorème des mariages a des implications importantes dans :

*   **Théorie des graphes** : Il est utilisé pour déterminer l'existence d'un couplage parfait dans un graphe biparti.
*   **Optimisation combinatoire** : Résolution de problèmes d'affectation.
*   **Algorithmes** : Construction d'algorithmes efficaces pour trouver des couplages maximaux ou parfaits.

## 6.4 Le Principe de Transversale dans les Graphes

Le concept de transversale dans les graphes est un élément important de la théorie des graphes.
Une transversale (aussi appelée couverture par sommets) dans un graphe $G = (V, E)$ est un sous-ensemble $T$ de sommets de $V$ tel que chaque arête du graphe est incidente à au moins un sommet de $T$. En d'autres termes, une transversale est un ensemble de sommets qui "couvre" toutes les arêtes du graphe.

### Caractéristiques Principales
*   **Définition Formelle** : Pour un graphe $G = (V, E)$, une transversale $T \subseteq V$ satisfait la condition que pour toute arête $e \in E$, $T \cap e \neq \emptyset$.
*   **Objectif** : L'idée est de trouver un ensemble minimal de sommets qui touche toutes les arêtes du graphe.
*   **Transversale Minimale** : On cherche souvent à déterminer la transversale de taille minimale, c'est-à-dire celle contenant le moins de sommets possible tout en couvrant toutes les arêtes.
### Applications et Propriétés
1.  **Problème d'Optimisation** : Le problème de trouver une transversale minimale est un problème classique d'optimisation en théorie des graphes.
2.  **Relation avec les Couplages** : Il existe une relation importante entre les transversales et les couplages dans un graphe. Pour tout transversal $T$ et tout couplage $M$ d'un graphe $G$, on a $|T| \geq |M|$.
3.  **Complémentarité** : Si $W$ est un stable (ensemble de sommets deux à deux non adjacents) dans $G$, alors $V - W$ est une transversale dans $G$.
4.  **Algorithmes** : Il existe des algorithmes pour calculer les transversales minimales d'un graphe, comme l'algorithme MTMiner (Minimal Transversals Miner).
Le concept de transversale est fondamental en théorie des graphes et trouve des applications dans divers domaines de l'informatique et de l'optimisation combinatoire.

### 6.3 Lien avec les flots
Couplage maximum résolvable par flot maximum.

## 7. Transversaux dans les graphes

- **Transversal** : Ensemble T de sommets touchant toutes les arêtes
- **Transversal minimum** : De cardinalité minimale

**Théorème de König** : |Couplage maximum| = |Transversal minimum| (graphes bipartis)

## 8. Problème d'affectation

Affecter n tâches à n personnes en minimisant le coût total.

### 8.1 Algorithme de Kuhn (Méthode hongroise)

3. Réduction du coût
4. Encadrement et barrage des zéros
5. Marquage des lignes et colonnes
6. Itération jusqu'au couplage parfait

Garantit une affectation optimale en temps polynomial.

---

**Définition** : 
