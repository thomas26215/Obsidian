---
MOOC: "[[Cours]]"
Ressource: "R5.04 : Qualité algorithmique"
Cours: "Cours 1 :"
Date:
tags:
Complete: false
Learned: false
---
# Efficacité d’un algorithme

L’efficacité d’un algorithme est évaluée en fonction des ressources qu’il consomme, principalement :  
- **L’espace mémoire utilisé**,  
- **Le temps d’exécution** (le plus souvent le critère principal).

---

# Mesure du temps requis

Soit un algorithme $A$ traité sur un ensemble de données $D_n$ de taille $n$.  
On note $T_A(d)$ le temps d’exécution de $A$ sur la donnée $d$.

Trois mesures usuelles :  
- $T_{worst}(n) = \max_{d \in D_n} T_A(d)$, la complexité dans le pire des cas,  
- $T_{best}(n) = \min_{d \in D_n} T_A(d)$, la complexité dans le meilleur des cas,  
- $T_{avg}(n) = \sum_{d \in D_n} P(d) \cdot T_A(d)$, la complexité moyenne, avec $P(d)$ la probabilité d’apparition de la donnée $d$.

On a toujours :  
$T_{best}(n) \leq T_{avg}(n) \leq T_{worst}(n)$

---

# Exemple de fonction RechMax

Pour la recherche du maximum dans un tableau $V[1..n]$ non vide :  
- Meilleur cas (maximum au premier élément) :  
$T_{best} = a_b n + b_b$  
- Pire cas (maximum au dernier élément) :  
$T_{worst} = a_w n + b_w$

où $a_b, b_b, a_w, b_w$ sont des constantes réelles positives dépendant de la machine et du logiciel.

Cet algorithme a une complexité en temps constante dans le meilleur cas ($\Omega(1)$) et linéaire dans le pire cas ($O(n)$).

---

# Analyse détaillée vs analyse asymptotique

- **Analyse détaillée** :  
  Compte précisément chaque opération, très longue à établir mais précise.  
- **Analyse asymptotique** :  
  Approche simplifiée pour estimer la croissance du temps d’exécution en fonction de $n$, en ignorant constantes et termes de plus faible ordre.

---

# Comptage du coût

1. Chaque itération d’une boucle compte pour 1.  
2. Le coût des blocs internes est multiplié par le nombre d’exécutions.  
3. Pour les instructions conditionnelles, on compte la branche la plus coûteuse.  
4. Chaque instruction élémentaire compte pour 1.

---

# Somme arithmétique

$\sum_{i=1}^n i = \frac{n(n+1)}{2} = \frac{n^2}{2} + \frac{n}{2}$

Plus généralement :

$\sum_{i=inf}^{sup} i = \frac{(sup + inf)(sup - inf + 1)}{2}$

---

# Notations asymptotiques

## Notation $O(g(n))$ (Grand O)

Elle donne une borne supérieure asymptotique pour la complexité dans le pire cas.

La fonction $f(n)$ est dans $O(g(n))$ s’il existe des constantes $c > 0$ et $n_0 \geq 0$ telles que :  
$\forall n \geq n_0, \quad f(n) \leq c \cdot g(n)$

C’est-à-dire que $g(n)$ domine $f(n)$ asymptotiquement.

---

## Notation $\Omega(g(n))$ (Grand Oméga)

Elle donne une borne inférieure asymptotique.

La fonction $f(n)$ est dans $\Omega(g(n))$ s’il existe $c > 0$ et $n_0$ tels que :  
$\forall n \geq n_0, \quad f(n) \geq c \cdot g(n)$

---

## Notation $\Theta(g(n))$ (Thêta)

Elle définit une bornes asymptotiques à la fois supérieures et inférieures.  
$f(n) \in \Theta(g(n))$ si et seulement si $f(n) \in O(g(n))$ et $f(n) \in \Omega(g(n))$, autrement dit :  
$\exists c_1, c_2 > 0, \exists n_0, \quad \forall n \geq n_0, \quad c_1 g(n) \leq f(n) \leq c_2 g(n)$

On dit alors que $g(n)$ donne une estimation asymptotique précise de $f(n)$.

---

## Notations supplémentaires (moins courantes)

- $o(g(n))$ : signifie que $f(n)$ croît plus lentement que $g(n)$ (limite supérieure non serrée).   
- $\omega(g(n))$ : signifie que $f(n)$ croît plus vite que $g(n)$ (limite inférieure non serrée).

---

# Exemples classiques de complexité

| Classe de complexité   | Description                     | Exemple typique                 |
|-----------------------|--------------------------------|--------------------------------|
| $O(1)$                | Temps constant                 | Accès à un tableau             |
| $O(\log n)$           | Temps logarithmique            | Recherche dichotomique         |
| $O(n)$                | Temps linéaire                 | Parcours d’un tableau          |
| $O(n \log n)$         | Temps quasi-linéaire           | Tri rapide (QuickSort)         |
| $O(n^2)$              | Temps quadratique              | Tri à bulles, tri par insertion|
| $O(2^n)$              | Temps exponentiel              | Problèmes combinatoires naïfs  |
| $O(n!)$               | Temps factoriel                | Permutations complètes         |

---

# Remarque importante sur l’analyse asymptotique

L’analyse asymptotique élimine les constantes et les termes moins significatifs pour ne garder que l’ordre de grandeur dominant de la fonction de coût. Cela permet de comparer la croissance des algorithmes indépendamment de la machine utilisée ou des détails d’implémentation.

Cependant, pour des petites valeurs de $n$, un algorithme asymptotiquement moins performant peut être plus rapide à cause de petites constantes cachées.

---

# Exemple explicite

Si $T_A(n) = \frac{1}{8} n^2 - 64 n + 8$ et $T_B(n) = 1789 n + 1968$, alors :  
$T_A(n) = \Theta(n^2), \quad T_B(n) = \Theta(n)$

Bien que $T_B$ soit meilleur asymptotiquement, pour $n < 14825$, la complexité effective de $T_A$ peut être meilleure.

---

# Résumé des propriétés

| Notation | Sens                         | Borne pour $f(n)$          |
|----------|------------------------------|----------------------------|
| $O$      | Borne supérieure asymptotique | $f(n) \leq c \cdot g(n)$ |
| $\Omega$ | Borne inférieure asymptotique | $f(n) \geq c \cdot g(n)$ |
| $\Theta$ | Borne asymptotique exacte      | $c_1 g(n) \leq f(n) \leq c_2 g(n)$ |



