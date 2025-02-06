R3.04

[[Définition - Base de données]]
Un modèle de données est un ensemble de concepts pouvant décrire la structure d'une [[Définition - Base de données|BDD]]
[[Définition - Schéma d'une base de données]]
[[La normalisation d'une base de données]]

## Dépendance fonctionnelle
Une dépendance fonctionnelle est une relation entre deux attributs d'une relation. Elle est notée $X \rightarrow Y$ où $X$ et $Y$ sont des ensembles d'attributs de la relation. Elle signifie que pour chaque valeur de $X$, il existe une seule valeur de $Y$.

**Exemple** : Si on a une relation `Personne` avec les attributs `Nom`, `Prénom` et `Adresse`, on peut dire que `Nom` $\rightarrow$ `Prénom` car pour chaque nom, il n'y a qu'un seul prénom associé.

# Décomposition d'une relation
## Décomposition binaire
Etant donné une relation R(X, Y, Z), on peut la décomposer en deux relations R1(X, Y) et R2(Y, Z) si Y est une clé de R.

**Exemple** : Soit une relation `Personne` avec les attributs `Nom`, `Prénom` et `Adresse`. On peut la décomposer en deux relations `Personne1` avec les attributs `Nom` et `Prénom` et `Personne2` avec les attributs `Prénom` et `Adresse` car `Prénom` est une clé de `Personne` (Nom n'est pas une clé car il peut y avoir plusieurs personnes avec le même nom).

## Décomposition correcte
Une décomposition est correcte si on peut retrouver la relation initiale en faisant un produit cartésien des relations obtenues et si le schéma obtenu est équivalent au schéma de la relation initiale. Cela est possible uniquement si :
- Les relations obtenues sont disjointes (pas d'attributs en commun)

## Propriété des DF
Soit une relation R(X, Y, Z) et une dépendance fonctionnelle X $\rightarrow$ Y. Si on décompose R en R1(X, Y) et R2(Y, Z), alors la dépendance fonctionnelle X $\rightarrow$ Y est conservée.
- Réflexivité : Si Y ⊆ X, alors X → Y est conservée (DF1)
- Augmentation : Si X → Y est conservée, alors XZ → YZ est aussi conservée pour tout Z (DF2)
- Transitivité : Si X → Y et Y → Z sont conservées, alors X → Z est aussi conservée (DF3)

