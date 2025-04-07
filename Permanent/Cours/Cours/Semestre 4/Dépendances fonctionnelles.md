R3.04

[[Définition - Base de données]]
Un modèle de données est un ensemble de concepts pouvant décrire la structure d'une [[Définition - Base de données|BDD]]
[[Définition - Schéma d'une base de données]]
[[La normalisation d'une base de données]]

## Dépendance fonctionnelle
Une dépendance fonctionnelle est une relation entre deux attributs d'une relation. Elle est notée $X \rightarrow Y$ où $X$ et $Y$ sont des ensembles d'attributs de la relation. Elle signifie que pour chaque valeur de $X$, il existe une seule valeur de $Y$. Cela signifie également qu'à partir de $X$, on peut déduire $Y$

> [!Example]
> Si on a une relation `Personne` avec les attributs `Nom`, `Prénom` et `Adresse`, on peut dire que `Nom` $\rightarrow$ `Prénom` car pour chaque nom, il n'y a qu'un seul prénom associé.

> [!Example]
> Si on a une relation `R(P, H, S, C, M)` exprimant l'emploi du temps d'un Lycée reposant sur les attributs suivants :
> `P` = Professeur, `H` = Heures, `S`  = Salle, `C` = Classe et `M` = Matière enseignée
> 
> On peut avoir les dépendances fonctionnelles suivantes :
> `P -> M`
> `P,H -> C`
> `H,S -> P`
> `H,C -> S`

# Décomposition d'une relation
## Décomposition binaire
Etant donné une relation R(X, Y, Z), on peut la décomposer suviant la décomposition ({X, Y}, {X, Z}) si il existe deux relations R1 et R2 telles que :
- R1 et R2 sont des projections de R : `R1=R[X,Y], R2=R[X, Z]`
- Le produit de R1 et R2 est R : `R = R1 *(X) R2`
=> Cela signifie qu'il n'y a pas de perte d'informations

**Exemple** : Soit une relation `Personne` avec les attributs `Nom`, `Prénom` et `Adresse`. On peut la décomposer en deux relations `Personne1` avec les attributs `Nom` et `Prénom` et `Personne2` avec les attributs `Prénom` et `Adresse` car `Prénom` est une clé de `Personne` (Nom n'est pas une clé car il peut y avoir plusieurs personnes avec le même nom).

## Décomposition correcte
Une décomposition est correcte s'il n'y a pas de perte d'informations et s'il n'y a pas de perte de DF. Pour savoir si le schéma obtenu est un meilleur schéma, il faut qu'il soit en [[La normalisation d'une base de données|3FN]]


## Propriété des DF
- (DF1) Réflexivité : `Y ⊆ X ⇒ X→Y`
>[!Example]
>**Ex** : `X={prof, bureau};Y ={prof} ⇒ prof,bureau→prof
- (DF2) Augmentation : `X→Y ⇒ X,Z→Y,Z`
> [!Example]
> **Ex** : `prof→bureau ⇒ prof,module→bureau,module`
- (DF3) Transitivité : `(X→Y) ∧ (Y→Z) ⇒ X→Z`
>[!Example]
>**Ex** : `(module→UE) ∧ (UE→formation) ⇒ module→formation`
- (DF4) Pseudo-transitivité : `(X→Y) ∧ (Y,W→Z) ⇒ X,W→Z`
>[!Example]
>**Ex** : `Eleve→Groupe ∧ Module,Groupe→Prof ⇒ Module,Eleve→Prof`
- (DF5) Union : `(X→Y) ∧ (X→Z) ⇒ X→Y,Z`
>[!Example]
>**Ex** : `Module → UE ∧ Module→semestre ⇒ Module→UE,semestre`
- (DF6) Décomposition : `(X→Y) ∧ (Z⊆Y) ⇒ X→Z`
>[!Example]
>**Ex** : `Module→UE,semestre ⇒ Module→UE`