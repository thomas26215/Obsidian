# Théorie des graphes et réseaux de transport

## 1. Introduction

La théorie des graphes est un domaine des mathématiques qui étudie les relations entre des objets. Elle trouve de nombreuses applications, notamment dans la modélisation de réseaux de transport.

## 2. Notions de base en théorie des graphes

**Graphe** : Un graphe G est un couple (S,A) où S est un ensemble de sommets et A un ensemble d'arêtes reliant ces sommets.

**Graphe orienté** : Les arêtes ont une direction (on parle alors d'arcs).

**Chemin** : Séquence de sommets reliés par des arêtes.

**Cycle** : Chemin dont le premier et le dernier sommet sont identiques.

**Degré d'un sommet** : Nombre d'arêtes incidentes à ce sommet.

**Connexité** : Un graphe est connexe s'il existe un chemin entre toute paire de sommets.

## 3. Réseaux de transport

### 3.1 Définition

Un réseau de transport est modélisé par un graphe orienté G = (S,A,c) où :
- **S** est l'ensemble des sommets (points de transit).
- **A** est l'ensemble des arcs (liaisons entre les points).
- **c** est une fonction de capacité c : A → R+

**Propriétés importantes** :
- Il existe un sommet source (e) qui n'a que des arcs sortants.
- Il existe un sommet puits (s) qui n'a que des arcs entrants.

### 3.2 Notion de flot

Un flot **f** dans un réseau de transport est une fonction f : A → R+ qui vérifie :

1. **Contrainte de capacité** : \( \forall (i,j) \in A, f(i,j) \leq c(i,j) \)
2. **Conservation du flot** : \( \forall x \in S \setminus \{e,s\}, \sum f(a)_{entrant \ en \ x} = \sum f(a)_{sortant \ de \ x} \)
3. La **valeur du flot** \( v(f) \) est la quantité totale transitant de la source au puits.

## 4. Problème du flot maximum

Le problème consiste à trouver un flot de valeur maximale dans le réseau.

### 4.1 Algorithme de Ford et Fulkerson (1956)

1. Initialiser le flot à 0.
2. Tant qu'il existe une **chaîne admissible** d'extrémités e et s :
   - Calculer \( m = \min(\min(c(a) - f(a)) \text{ pour } a \in U, \min(f(a)) \text{ pour } a \in V) \)
   - Augmenter le flot de \( m \) sur les arcs de \( U \) et le diminuer de \( m \) sur les arcs de \( V \).
3. Le flot obtenu est maximal quand il n'y a plus de chaîne admissible.

## 5. Théorème de la coupe minimale

Une coupe est un ensemble d'arcs (Y, \( \bar{Y} \)) où \( e \in Y \) et \( s \notin Y \).

**Théorème** : La valeur du flot maximum est égale à la capacité de la coupe minimale.

## 6. Couplage maximal dans un graphe biparti

### 6.1 Définitions

- **Graphe biparti** : Graphe dont les sommets peuvent être séparés en deux ensembles U et V tels que chaque arête relie un sommet de U à un sommet de V.
- **Couplage** : Ensemble d'arêtes sans sommet commun.
- **Couplage maximum** : Couplage contenant le plus grand nombre d'arêtes possible.
- **Couplage parfait** : Couplage qui couvre tous les sommets de U et V.

### 6.2 Théorème de Hall (lemme des mariages)

Un graphe biparti G = (U \cup V, A) admet un couplage parfait si et seulement si pour tout sous-ensemble X de U, le nombre de sommets de V adjacents à X est supérieur ou égal à la cardinalité de X.

### 6.3 Lien avec les flots

Le problème du couplage maximum peut être résolu en le transformant en un problème de flot maximum.

## 7. Transversaux dans les graphes

- **Transversal** : Ensemble de sommets T tel que toute arête du graphe a au moins une extrémité dans T.
- **Transversal minimum** : Transversal de cardinalité minimale.

**Théorème de König** : Dans un graphe biparti, la cardinalité du couplage maximum est égale à celle du transversal minimum.

## 8. Problème d'affectation

Le problème d'affectation consiste à affecter n tâches à n personnes en minimisant le coût total. Il peut être résolu par l'**algorithme de Kuhn** (méthode hongroise).

### 8.1 Algorithme de Kuhn (Méthode hongroise)

1. **Réduction du coût** en soustrayant le minimum de chaque ligne et colonne.
2. **Encadrement et barrage des zéros**.
3. **Marquage des lignes et colonnes**.
4. **Itération** jusqu'à obtention d'un couplage parfait.

Cet algorithme garantit une affectation optimale en temps polynomial.
