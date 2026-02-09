# Correction du sujet CAPES NSI 2021 - Première épreuve d'admissibilité

## Problème 1 : Points proches dans le plan

### 1. Approche exhaustive

**Question 1** - Fonction `distance(i, j)`

```python
from math import sqrt

def distance(i, j):
    return sqrt((coords_x[j] - coords_x[i])**2 + (coords_y[j] - coords_y[i])**2)
```

**Question 2** - Stockage des flottants

Les flottants sont stockés en mémoire selon la norme IEEE 754, en utilisant :

- 1 bit pour le signe
- 8 bits pour l'exposant (simple précision) ou 11 bits (double précision)
- 23 bits pour la mantisse (simple précision) ou 52 bits (double précision)

Conséquence sur le calcul : Les nombres ne peuvent pas tous être représentés exactement, ce qui entraîne des erreurs d'arrondi. Les opérations arithmétiques peuvent accumuler ces erreurs, rendant les comparaisons d'égalité peu fiables.

**Question 3** - Fonction `plus_proche()`

```python
def plus_proche():
    n = len(coords_x)
    min_dist = distance(0, 1)
    i_min, j_min = 0, 1
    
    for i in range(n):
        for j in range(i+1, n):
            d = distance(i, j)
            if d < min_dist:
                min_dist = d
                i_min, j_min = i, j
    
    return (i_min, j_min)
```

**Question 4** - Complexité

La complexité est **O(n²)**.

Justification : On parcourt toutes les paires de points possibles. Il y a n(n-1)/2 paires, et pour chaque paire on calcule la distance en temps constant. Donc la complexité est en Θ(n²).

### 2. Quelques outils pour s'améliorer

**Question 5** - Analyse de la fonction `tri`

Cette fonction renvoie `None` (car il n'y a pas d'instruction `return`).

Elle effectue un **tri par insertion** de la liste en place (modification directe).

**Invariant de boucle** : À la fin de l'itération i, les éléments `liste[0]`, `liste[1]`, ..., `liste[i]` sont triés dans l'ordre croissant.

**Démonstration** :

- Initialisation (i=0) : Un seul élément est trié
- Conservation : Si les i premiers éléments sont triés, l'élément à la position i est inséré à sa place parmi les i premiers par décalages successifs
- Terminaison : À la fin (i=n-1), tous les éléments sont triés

**Question 6** - Complexité du tri

**Complexité : O(n²)** dans le pire des cas.

**Démonstration** :

- La boucle externe s'exécute n fois
- Pour chaque i, la boucle while peut s'exécuter jusqu'à i fois
- Au total : 0 + 1 + 2 + ... + (n-1) = n(n-1)/2 comparaisons/échanges
- Donc complexité en Θ(n²) dans le pire cas (liste triée en ordre décroissant)

**Question 7** - Tri par abscisses

Il faut remplacer :

```python
while pos > 0 and liste[pos] < liste[pos-1]:
```

par :

```python
while pos > 0 and coords_x[liste[pos]] < coords_x[liste[pos-1]]:
```

**Question 8** - Autre algorithme de tri

**Tri fusion (merge sort)** : complexité O(n log n) dans le pire des cas.

Autres options : tri rapide (quicksort) avec complexité moyenne O(n log n), ou tri par tas (heapsort) avec O(n log n) garanti.

**Question 9** - Fonction `sous_cluster`

```python
def sous_cluster(cl, x_min, x_max):
    # Filtrer la première ligne (triée par x)
    ligne_x = []
    for idx in cl[0]:
        if x_min <= coords_x[idx] <= x_max:
            ligne_x.append(idx)
    
    # Filtrer la seconde ligne (triée par y)
    # en ne gardant que les indices présents dans ligne_x
    ensemble_x = set(ligne_x)
    ligne_y = []
    for idx in cl[1]:
        if idx in ensemble_x:
            ligne_y.append(idx)
    
    return [ligne_x, ligne_y]
```

Complexité : O(taille du cluster) car on parcourt chaque ligne une fois.

**Question 10** - Fonction `mediane`

```python
def mediane(cl):
    n = len(cl[0])
    # L'abscisse médiane est celle du point au milieu (ou juste avant)
    indice_median = (n - 1) // 2
    idx_point = cl[0][indice_median]
    return coords_x[idx_point]
```

Complexité : O(1) car accès direct à un élément.

### 3. Méthode sophistiquée

**Question 11** - Fonction `gauche`

```python
def gauche(cl):
    n = len(cl[0])
    # Nombre de points à gauche (arrondi supérieur si impair)
    nb_gauche = (n + 1) // 2
    
    # Indices des points à gauche (première moitié triée par x)
    indices_gauche_x = cl[0][:nb_gauche]
    
    # Filtrer la ligne y
    ensemble_gauche = set(indices_gauche_x)
    indices_gauche_y = [idx for idx in cl[1] if idx in ensemble_gauche]
    
    return [indices_gauche_x, indices_gauche_y]
```

**Question 12** - Justification de la bande centrale

Si M₁ est dans G et M₂ dans D avec d(M₁, M₂) < d₀ :

- M₁ a une abscisse ≤ x₀, donc x₁ ≤ x₀
- M₂ a une abscisse ≥ x₀, donc x₂ ≥ x₀
- d(M₁, M₂) < d₀ implique |x₂ - x₁| < d₀

Si x₁ < x₀ - d₀, alors x₂ - x₁ > x₂ - (x₀ - d₀) ≥ x₀ - (x₀ - d₀) = d₀, contradiction. Si x₂ > x₀ + d₀, alors x₂ - x₁ > (x₀ + d₀) - x₁ ≥ (x₀ + d₀) - x₀ = d₀, contradiction.

Donc x₁ ∈ [x₀ - d₀, x₀] et x₂ ∈ [x₀, x₀ + d₀], donc les deux points sont dans [x₀ - d₀, x₀ + d₀].

**Question 13** - Fonction `bande_centrale`

```python
def bande_centrale(cl, d0):
    x0 = mediane(cl)
    return sous_cluster(cl, x0 - d0, x0 + d0)
```

Complexité : linéaire (appel à `sous_cluster` qui est linéaire).

**Question 14** - Distance maximale dans la liste triée par y

Considérons un rectangle de dimensions 2d₀ × d₀ (largeur 2d₀, hauteur d₀).

**Par l'absurde** : supposons qu'il contienne au moins 9 points avec des distances toutes ≥ d₀.

On peut diviser ce rectangle en 8 carrés de côté d₀/2. Par le principe des tiroirs, au moins deux points sont dans le même carré. La distance maximale dans un carré de côté d₀/2 est d₀√2/2 < d₀ (pour la diagonale). Contradiction.

Donc le rectangle contient au plus 8 points.

Dans la liste triée par ordonnées, deux points M₁ et M₂ de la bande centrale à distance < d₀ ont leurs ordonnées qui diffèrent de moins de d₀. Le rectangle de hauteur d₀ contenant ces deux points contient au plus 8 points. Donc dans la liste triée par y, ils sont séparés d'au plus 7 éléments (ou 6 autres éléments entre eux).

**Question 15** - Fonction `fusion`

```python
def fusion(cl, d0):
    n = len(cl[1])  # Utiliser la liste triée par y
    min_dist = d0
    
    # Parcourir tous les points dans l'ordre des y
    for i in range(n):
        idx_i = cl[1][i]
        # Ne regarder que les 7 points suivants maximum
        for j in range(i+1, min(i+8, n)):
            idx_j = cl[1][j]
            # Vérifier que la différence en y n'est pas trop grande
            if coords_y[idx_j] - coords_y[idx_i] >= d0:
                break
            d = distance(idx_i, idx_j)
            if d < min_dist:
                min_dist = d
    
    return min_dist
```

**Complexité** : O(n) où n est la taille du cluster.

- Boucle externe : n itérations
- Boucle interne : au plus 7 itérations (constante)
- Donc O(7n) = O(n)

**Question 16** - Fonction `distance_minimale`

```python
def distance_minimale(cl):
    n = len(cl[0])
    
    # Cas de base : 2 ou 3 points
    if n == 2:
        return distance(cl[0][0], cl[0][1])
    if n == 3:
        d1 = distance(cl[0][0], cl[0][1])
        d2 = distance(cl[0][0], cl[0][2])
        d3 = distance(cl[0][1], cl[0][2])
        return min(d1, d2, d3)
    
    # Diviser
    cl_gauche = gauche(cl)
    cl_droite = droite(cl)
    
    # Récursion
    d_gauche = distance_minimale(cl_gauche)
    d_droite = distance_minimale(cl_droite)
    d0 = min(d_gauche, d_droite)
    
    # Fusion : chercher dans la bande centrale
    bande = bande_centrale(cl, d0)
    d_bande = fusion(bande, d0)
    
    return min(d0, d_bande)
```

**Question 17** - Équation de récurrence

À chaque appel sur un cluster de taille n :

- On divise en 2 sous-clusters de taille n/2 : 2 appels récursifs → 2C(n/2)
- On effectue des opérations linéaires : `gauche`, `droite`, `bande_centrale`, `fusion` → O(n)

Donc : **C(n) = 2C(n/2) + O(n)**

**Question 18** - Résolution de la récurrence

Pour n = 2^k, posons C(2^k) = f(k).

f(k) = 2f(k-1) + c·2^k pour une constante c.

En développant :

- f(k) = 2f(k-1) + c·2^k
- f(k) = 2[2f(k-2) + c·2^(k-1)] + c·2^k = 4f(k-2) + 2c·2^k
- f(k) = 2^i·f(k-i) + i·c·2^k

Pour i = k : f(k) = 2^k·f(0) + k·c·2^k = O(2^k) + k·c·2^k = O(k·2^k)

Donc C(n) = O(log n · n) = **O(n log n)**.

---

## Problème 2 : Composantes connexes et biconnexes

### 4. Site Internet et bases de données

**Question 19** - Différence Internet/Web

- **Internet** : réseau mondial d'ordinateurs interconnectés utilisant le protocole TCP/IP. C'est l'infrastructure physique et logique.
- **Web** (World Wide Web) : service fonctionnant sur Internet, basé sur HTTP/HTTPS, permettant de consulter des pages web via des navigateurs.

Le Web est un service parmi d'autres sur Internet (comme l'email, FTP, etc.).

**Question 20** - Conséquences du RGPD

1. **Consentement explicite** : Le site doit obtenir le consentement clair et explicite des utilisateurs pour collecter et traiter leurs données personnelles.
    
2. **Droit d'accès et de suppression** : Les utilisateurs doivent pouvoir accéder à leurs données, les modifier ou demander leur suppression.
    

Autres conséquences possibles : obligation d'informer en cas de fuite de données, désignation d'un DPO, minimisation des données collectées, durée de conservation limitée.

**Question 21** - Nombre de ressources de type cours

```sql
SELECT COUNT(*) 
FROM ressources 
WHERE type = 'cours';
```

**Question 22** - Analyse de la requête

Cette requête renvoie le titre de la dernière ressource téléchargée et le nom de la personne qui l'a téléchargée.

Explication :

- Jointure entre `chargement`, `ressources` et `comptes`
- Tri par date décroissante
- Limitation au premier résultat (le plus récent)

Note : Il y a une faute de frappe dans la requête (`ressouces` au lieu de `ressources`).

**Question 23** - Triplets (x, y, n)

```sql
SELECT chargement.id_u AS x, ressources.owner AS y, COUNT(*) AS n
FROM chargement
JOIN ressources ON ressources.id = chargement.id_r
GROUP BY chargement.id_u, ressources.owner;
```

**Question 24** - Table des couples de E

```sql
SELECT c1.id_u AS x, c2.id_u AS y
FROM chargement c1
JOIN ressources r1 ON r1.id = c1.id_r
JOIN chargement c2 ON c2.id_r IN (
    SELECT id FROM ressources WHERE owner = c1.id_u
)
JOIN ressources r2 ON r2.id = c2.id_r
WHERE r1.owner = c2.id_u AND c1.id_u < c2.id_u
GROUP BY c1.id_u, c2.id_u

UNION

SELECT c2.id_u AS x, c1.id_u AS y
FROM chargement c1
JOIN ressources r1 ON r1.id = c1.id_r
JOIN chargement c2 ON c2.id_r IN (
    SELECT id FROM ressources WHERE owner = c1.id_u
)
JOIN ressources r2 ON r2.id = c2.id_r
WHERE r1.owner = c2.id_u AND c1.id_u < c2.id_u
GROUP BY c1.id_u, c2.id_u;
```

Ou plus simplement :

```sql
SELECT DISTINCT t1.x, t1.y
FROM (
    SELECT c.id_u AS x, r.owner AS y
    FROM chargement c
    JOIN ressources r ON r.id = c.id_r
) t1
JOIN (
    SELECT c.id_u AS x, r.owner AS y
    FROM chargement c
    JOIN ressources r ON r.id = c.id_r
) t2 ON t1.x = t2.y AND t1.y = t2.x
WHERE t1.x < t1.y

UNION

SELECT DISTINCT t1.y AS x, t1.x AS y
FROM (
    SELECT c.id_u AS x, r.owner AS y
    FROM chargement c
    JOIN ressources r ON r.id = c.id_r
) t1
JOIN (
    SELECT c.id_u AS x, r.owner AS y
    FROM chargement c
    JOIN ressources r ON r.id = c.id_r
) t2 ON t1.x = t2.y AND t1.y = t2.x
WHERE t1.x < t1.y;
```

### 5. Composantes connexes

**Question 25** - Fonction `adjacences`

```python
def adjacences(n, li):
    # Initialiser avec des listes vides
    result = [[] for _ in range(n)]
    
    # Ajouter chaque arête
    for (x, y) in li:
        if y not in result[x]:
            result[x].append(y)
        if x not in result[y]:
            result[y].append(x)
    
    return result
```

**Question 26** - Type et application de `parcours`

**Type** : Liste d'objets `Arbre`.

**Application sur g_ex_b** :

En partant de 0, exploration en profondeur :

- 0 → 1 → 4 (feuille)
- 0 → 1 → 8 (feuille)
- 0 → 2 → 3 → 6 → 5 (feuille)

Représentation :

```
Arbre(0)
├── Arbre(1)
│   ├── Arbre(4)
│   └── Arbre(8)
├── Arbre(2)
└── Arbre(3)
    └── Arbre(6)
        └── Arbre(5)

Arbre(7)
└── Arbre(9)
```

**Nom du parcours** : Parcours en profondeur (DFS - Depth-First Search).

**Question 27** - Complexité de `parcours`

Chaque sommet est visité exactement une fois (marqué dans `deja_vu`). Pour chaque sommet, on parcourt sa liste de voisins. Au total, on parcourt chaque arête deux fois (une fois dans chaque sens).

- Parcours des sommets : O(|V|)
- Parcours des arêtes : O(|E|)

**Complexité totale : O(|V| + |E|)**

**Question 28** - Définition de la connexité

Un graphe G(V, E) est **connexe** si et seulement si pour toute paire de sommets (u, v), il existe un chemin reliant u à v.

Autrement dit : le graphe est en un seul "morceau", tous les sommets sont accessibles depuis n'importe quel autre sommet.

**Question 29** - Fonction `connexe`

```python
def connexe(listes_adjacences):
    foret = parcours(listes_adjacences)
    # Le graphe est connexe ssi la forêt ne contient qu'un seul arbre
    return len(foret) == 1
```

**Question 30** - Fonction `composantes_connexes`

```python
def composantes_connexes(p_graphe):
    result = []
    
    def extraire_sommets(arbre):
        """Extrait récursivement tous les sommets d'un arbre"""
        sommets = [arbre.sommet]
        for child in arbre.children:
            sommets.extend(extraire_sommets(child))
        return sommets
    
    # Pour chaque arbre de la forêt
    for arbre in p_graphe:
        composante = extraire_sommets(arbre)
        result.append(composante)
    
    return result
```

**Question 31** - Limitation de la récursivité en Python

Python a une **limite de profondeur de récursion** (par défaut environ 1000). Pour des graphes avec des chaînes très longues, la fonction récursive risque de dépasser cette limite et provoquer une erreur `RecursionError`.

Solution : utiliser une approche itérative avec une pile explicite.

### 6. Graphes biconnexes

**Question 32** - Graphe biconnexe ⇒ connexe

Si G est biconnexe, alors :

- Soit |V| ≤ 2 : dans ce cas, G est trivialement connexe
- Soit |V| ≥ 3 : pour toute paire (x, y), il existe un cycle élémentaire contenant x et y, donc en particulier un chemin de x à y.

Donc G est connexe.

**Question 33** - Exemple de graphe connexe mais pas biconnexe

Un graphe en "chaîne" : 0 — 1 — 2

Ce graphe est connexe mais pas biconnexe car le sommet 1 est un point d'articulation (si on le retire, le graphe n'est plus connexe). Il n'existe pas de cycle contenant 0 et 2.

**Question 34** - Points d'articulation de G'ex

Points d'articulation : **3, 6, 8**

- Retirer 3 déconnecte {0,1,2} de {4,5,6,7,8,9,10,11,12}
- Retirer 6 déconnecte {0,1,2,3,4,5} de {7,8,9,10,11,12}
- Retirer 8 déconnecte {0,1,2,3,4,5,6,7} de {9,10,11,12}

**Question 35** - Point d'articulation ⇒ non biconnexe

Si x est un point d'articulation, alors G{x} (G privé de x) n'est pas connexe. Il existe donc deux composantes connexes C₁ et C₂ dans G{x}.

Soient y ∈ C₁ et z ∈ C₂. Tout chemin de y à z dans G passe nécessairement par x. Il ne peut donc pas exister de cycle élémentaire contenant y et z (un tel cycle permettrait d'aller de y à z sans passer par x).

Donc G n'est pas biconnexe.

**Question 36** - Pas de point d'articulation ⇒ biconnexe

1. **Existence d'une chaîne** : Puisque G est connexe (car sans point d'articulation avec |V| ≥ 3 implique connexe), il existe un chemin de x à y, qu'on peut représenter comme une chaîne (x₀ = x, x₁, ..., xₖ = y).
    
2. **Cycle contenant x₀ et x₁** :
    
    - Si on retire x₁, le graphe reste connexe (car x₁ n'est pas un point d'articulation)
    - Donc il existe un chemin P de x₀ à x₂ ne passant pas par x₁
    - La chaîne (x₀, x₁, x₂) ∪ P⁻¹ forme un cycle contenant x₀ et x₁
    - On peut extraire un cycle élémentaire de ce cycle
3. **Récurrence** : Supposons qu'il existe un cycle élémentaire C contenant x₀ et xᵢ.
    
    **Cas 1** : C contient xᵢ₊₁
    
    - Alors C contient déjà x₀ et xᵢ₊₁
    
    **Cas 2** : C ne contient pas xᵢ₊₁
    
    - En retirant xᵢ₊₁, le graphe reste connexe
    - Il existe donc un chemin P de x₀ à xᵢ₊₂ ne passant pas par xᵢ₊₁
    - Soit C' le sous-chemin de C allant de x₀ à xᵢ
    - Le chemin (C', xᵢ, xᵢ₊₁, xᵢ₊₂) ∪ P⁻¹ forme un cycle contenant x₀ et xᵢ₊₁
    - On peut en extraire un cycle élémentaire
4. **Conclusion** : Par récurrence, il existe un cycle élémentaire contenant x₀ = x et xₖ = y. Donc G est biconnexe.
    

**Question 37** - Déterminer un point d'articulation

Pour vérifier si un sommet v est un point d'articulation :

1. Effectuer un parcours en profondeur depuis v
2. Effectuer un parcours en profondeur depuis un voisin de v en marquant v comme déjà visité
3. Si tous les sommets (sauf v) sont visités, alors v n'est pas un point d'articulation
4. Sinon, v est un point d'articulation

Alternative plus efficace : lors du DFS, v est un point d'articulation ssi :

- v est racine et a au moins 2 enfants dans l'arbre DFS
- v n'est pas racine et a un enfant dont le sous-arbre ne peut pas remonter au-dessus de v

**Question 38** - Algorithme pour déterminer si G est biconnexe

**Algorithme** :

1. Vérifier que G est connexe (sinon, pas biconnexe)
2. Parcourir tous les sommets v
3. Pour chaque v, vérifier s'il est un point d'articulation (méthode Q37)
4. Si aucun point d'articulation trouvé : G est biconnexe
5. Sinon : G n'est pas biconnexe

**Complexité** : O(|V| · (|V| + |E|))

- |V| sommets à tester
- Pour chaque sommet : un DFS en O(|V| + |E|)

Avec l'algorithme optimisé (calcul simultané de tous les points d'articulation) : **O(|V| + |E|)**.

### 7. Algorithme efficace pour les points d'articulation

**Question 39** - Valeurs de `prefixe` pour G'ex

En partant de 0, avec voisins triés :

```
prefixe = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
```

Ordre de visite : 0, 1, 2, 6, 7, 11, 10, 5, 3, 8, 12, 4, 9

**Question 40** - Descendance dans l'arbre

Si (i, j) ∈ E et prefixe[i] < prefixe[j], alors :

- i a été visité avant j
- Lors de la visite de i, si j n'était pas encore visité, alors j est découvert depuis i (ou un descendant de i)
- Donc j est dans le sous-arbre enraciné en i
- j est un descendant de i

**Question 41** - Valeurs de ord[i] pour G'ex

Pour chaque sommet i, ord[i] = min des prefixe[j] pour j ∈ V(D(i)).

```
ord[0] = 1
ord[1] = 1
ord[2] = 1
ord[3] = 1
ord[4] = 1
ord[5] = 1
ord[6] = 1
ord[7] = 7
ord[8] = 1
ord[9] = 1
ord[10] = 6
ord[11] = 7
ord[12] = 9
```

**Question 42** - Fonction `points_articulation`

```python
def points_articulation(listes_adjacences):
    arbre, prefixe = parcours(listes_adjacences)
    ord_values = calcule_ord(listes_adjacences)
    
    points_art = []
    
    # Cas particulier de la racine
    if len(arbre.children) >= 2:
        points_art.append(arbre.sommet)
    
    # Parcourir tous les autres sommets
    def verifier_arbre(noeud):
        for child in noeud.children:
            # Si un fils j vérifie ord[j] >= prefixe[noeud.sommet]
            if ord_values[child.sommet] >= prefixe[noeud.sommet]:
                if noeud.sommet != arbre.sommet:  # Pas la racine
                    points_art.append(noeud.sommet)
            # Récursion
            verifier_arbre(child)
    
    verifier_arbre(arbre)
    
    # Éliminer les doublons
    return list(set(points_art))
```

**Question 43** - Composantes biconnexes de G'ex

Composantes biconnexes :

- {0, 1, 2, 3, 5, 6}
- {3, 4, 8, 9}
- {6, 7, 10, 11}
- {8, 12}

**Question 44** - Algorithme pour les composantes biconnexes

**Algorithme** :

1. Effectuer un DFS et calculer prefixe et ord pour chaque sommet
2. Utiliser une pile pour mémoriser les arêtes visitées
3. Lors du parcours :
    - Empiler chaque arête visitée
    - Quand on trouve un point d'articulation v avec un fils w tel que ord[w] ≥ prefixe[v] :
        - Dépiler toutes les arêtes jusqu'à (v, w) inclus
        - Ces arêtes forment une composante biconnexe
4. À la fin, les arêtes restantes forment une dernière composante

**Complexité** : O(|V| + |E|) (linéaire)

- Un seul DFS
- Chaque arête est empilée et dépilée au plus une fois


---

# Notions à connaître - CAPES NSI 2021

## Algorithmique et Complexité

### Complexité algorithmique

- **Notation O, Θ, Ω** : définitions et utilisation
- **Complexité dans le pire cas, cas moyen**
- **Analyse de complexité** : boucles simples, boucles imbriquées
- **Équations de récurrence** : méthode de résolution (substitution, arbre de récursion)
- **Complexité des algorithmes classiques** : recherche, tri, parcours de graphes

### Paradigmes algorithmiques

- **Diviser pour régner** : principe, exemples (tri fusion, algorithme des points proches)
- **Algorithmes gloutons**
- **Programmation dynamique**
- **Force brute / recherche exhaustive**

### Structures de données

- **Listes** : manipulation, complexité des opérations (append, accès, parcours)
- **Matrices** : représentation par listes de listes
- **Piles et files** : principe, utilisation
- **Arbres** : structure, parcours (profondeur, largeur)
- **Graphes** : représentations (matrice d'adjacence, listes d'adjacences)

## Tri et Recherche

### Algorithmes de tri

- **Tri par insertion** : principe, invariant, complexité O(n²)
- **Tri fusion (merge sort)** : principe, complexité O(n log n)
- **Tri rapide (quicksort)** : principe, complexité moyenne O(n log n)
- **Tri par tas (heapsort)** : principe, complexité O(n log n)
- **Comparaison des algorithmes de tri** : stabilité, complexité spatiale

### Invariants de boucle

- **Définition** : propriété vraie avant et après chaque itération
- **Utilisation** : démonstration de correction d'algorithmes
- **Méthode** : initialisation, conservation, terminaison

## Théorie des Graphes

### Définitions de base

- **Graphe orienté / non orienté**
- **Sommets, arêtes** (ou arcs)
- **Degré d'un sommet**
- **Chemin, chaîne, cycle**
- **Cycle élémentaire** : tous les sommets distincts

### Propriétés des graphes

- **Graphe connexe** : tout sommet accessible depuis tout autre
- **Composante connexe** : sous-ensemble maximal connexe
- **Graphe biconnexe** : pour toute paire de sommets, il existe un cycle élémentaire les contenant
- **Point d'articulation** : sommet dont la suppression déconnecte le graphe

### Algorithmes sur les graphes

- **Parcours en profondeur (DFS)** : principe, arbre de parcours, complexité O(|V| + |E|)
- **Parcours en largeur (BFS)** : principe, applications
- **Détection de composantes connexes**
- **Détection de points d'articulation** : algorithme de Tarjan
- **Composantes biconnexes** : algorithme, complexité linéaire

### Représentations des graphes

- **Matrice d'adjacence** : avantages, inconvénients, complexité spatiale O(|V|²)
- **Listes d'adjacences** : avantages, complexité spatiale O(|V| + |E|)
- **Conversion** entre représentations

## Géométrie Algorithmique

### Distance et métrique

- **Distance euclidienne** : formule √[(x₂-x₁)² + (y₂-y₁)²]
- **Propriétés** : symétrie, inégalité triangulaire

### Problèmes géométriques

- **Paire de points les plus proches** :
    - Approche naïve O(n²)
    - Diviser pour régner O(n log n)
- **Enveloppe convexe**
- **Points dans un rectangle**

### Techniques

- **Tri par coordonnées** : x, y
- **Médiane** : définition, calcul en O(1) sur liste triée
- **Bande centrale** : optimisation pour diviser pour régner

## Bases de données et SQL

### Modèle relationnel

- **Table, attribut, enregistrement**
- **Clé primaire, clé étrangère**
- **Relations entre tables**

### Langage SQL

- **SELECT** : projection, sélection
    
    ```sql
    SELECT attribut1, attribut2 FROM table WHERE condition
    ```
    
- **Fonctions d'agrégation** : COUNT, SUM, AVG, MIN, MAX
- **GROUP BY** : regroupement
- **ORDER BY** : tri (ASC, DESC)
- **LIMIT** : limitation du nombre de résultats
- **JOIN** : jointure entre tables (INNER JOIN, LEFT JOIN, etc.)
- **UNION** : union de résultats
- **WHERE** : conditions de filtrage

### Requêtes avancées

- **Sous-requêtes** : dans WHERE, FROM
- **Jointures multiples**
- **Agrégations avec GROUP BY et HAVING**

## Réseaux et Web

### Concepts fondamentaux

- **Internet** : réseau mondial d'ordinateurs, protocole TCP/IP, infrastructure
- **Web** : service sur Internet, protocole HTTP/HTTPS, pages web, navigateurs
- **Différence Internet/Web** : Internet est l'infrastructure, Web est un service
- **Client-serveur** : architecture

### Protocoles

- **TCP/IP** : base d'Internet
- **HTTP/HTTPS** : protocole du Web
- **DNS** : résolution de noms de domaine

## Données et confidentialité

### RGPD (Règlement Général sur la Protection des Données)

- **Consentement explicite** : obligation d'obtenir l'accord de l'utilisateur
- **Droit d'accès** : consultation de ses données
- **Droit de rectification** : modification de ses données
- **Droit à l'effacement** : suppression ("droit à l'oubli")
- **Portabilité des données**
- **Notification des violations** : obligation d'informer en cas de fuite
- **Privacy by design** : protection dès la conception
- **DPO** (Data Protection Officer) : délégué à la protection des données

## Représentation des données

### Nombres flottants

- **Norme IEEE 754** :
    - 1 bit de signe
    - Bits d'exposant (8 en simple précision, 11 en double)
    - Bits de mantisse (23 en simple précision, 52 en double)
- **Limitations** :
    - Erreurs d'arrondi
    - Nombres non représentables exactement
    - Problèmes de comparaison d'égalité
- **Conséquences** : accumulation d'erreurs dans les calculs

## Programmation Python

### Structures de base

- **Listes** :
    
    - Création : `[x] * n`, `[... for ... in ...]`
    - Accès : `li[k]`, modification : `li[k] = x`
    - Ajout : `li.append(x)`
    - Taille : `len(li)`
    - Slicing : `li[a:b]`
- **Matrices** (listes de listes) :
    
    - Création : `[[x for j in range(p)] for i in range(n)]`
    - Accès : `mat[i][j]`
    - Dimensions : `len(mat)` lignes, `len(mat[0])` colonnes

### Fonctions et récursivité

- **Définition** : `def fonction(params):`
- **Return** : valeur de retour (None par défaut)
- **Récursivité** : fonction qui s'appelle elle-même
- **Limite de récursion en Python** : environ 1000 (RecursionError)
- **Alternative itérative** : utilisation d'une pile explicite

### Programmation orientée objet

- **Classes** : `class NomClasse:`
- **Constructeur** : `def __init__(self, ...)`
- **Attributs** : `self.attribut`
- **Méthodes** : `def methode(self, ...)`
- **Instanciation** : `objet = NomClasse(...)`

### Imports et modules

- **Import de fonctions** : `from math import sqrt`
- **Import de module** : `import math` puis `math.sqrt()`

### Variables et portée

- **Variables globales** : accessibles partout
- **Variables locales** : limitées à une fonction
- **nonlocal** : accès à une variable d'une fonction englobante
- **global** : modification d'une variable globale

### Compréhensions

- **Listes** : `[expr for item in iterable if condition]`
- **Ensembles** : `{expr for item in iterable}`
- **Dictionnaires** : `{key: value for item in iterable}`

### Structures de données avancées

- **set** : ensemble, opérations rapides de recherche
- **Utilisation** : éliminer les doublons, test d'appartenance en O(1)

## Preuves et démonstrations

### Méthodes de preuve

- **Preuve directe** : déduction logique
- **Preuve par récurrence** :
    - Initialisation : vrai pour n₀
    - Hérédité : si vrai pour n, alors vrai pour n+1
    - Conclusion : vrai pour tout n ≥ n₀
- **Preuve par l'absurde** : supposer le contraire et montrer une contradiction
- **Preuve par contraposée** : pour prouver A ⇒ B, montrer non B ⇒ non A

### Invariants

- **Invariant de boucle** : propriété maintenue à chaque itération
- **Utilisation** : prouver la correction d'algorithmes
- **Structure** : initialisation, conservation, terminaison

## Notions transversales

### Optimisation

- **Compromis temps/espace** : mémoire vs rapidité
- **Prétraitement** : calculs préalables pour accélérer
- **Mémoïsation** : stockage de résultats intermédiaires

### Bonnes pratiques

- **Nommage** : variables explicites
- **Commentaires** : explication du code
- **Modularité** : fonctions réutilisables
- **Tests** : vérification du bon fonctionnement

### Cas particuliers

- **Cas de base** : dans les algorithmes récursifs
- **Cas limites** : listes vides, graphes à 1 ou 2 sommets
- **Gestion des erreurs** : validation des entrées