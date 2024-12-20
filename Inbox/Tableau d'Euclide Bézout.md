
L'**algorithme d'Euclide étendu** est un outil puissant qui permet de calculer non seulement le **plus grand commun diviseur** (pgcd) de deux entiers, mais aussi de déterminer les coefficients de Bézout associés. Ces coefficients, notés $u$ et $v$, satisfont l'équation :

$$
au + bv = \text{pgcd}(a, b)
$$

### Lien avec le PGCD

1. **Calcul du PGCD** : L'algorithme d'Euclide consiste à effectuer une série de divisions euclidiennes pour réduire progressivement les nombres jusqu'à obtenir un reste nul. Le dernier reste non nul est le pgcd des deux nombres.

2. **Coéfficients de Bézout** : En parallèle au calcul du pgcd, l'algorithme permet de remonter les étapes pour exprimer ce pgcd comme une combinaison linéaire des deux nombres initiaux $a$ et $b$. Cela se fait en isolant chaque reste obtenu lors des divisions successives.

### Obtention des Coefficients $u_i$ et $v_i$

Les coefficients $u_i$ et $v_i$ sont calculés à chaque étape de l'algorithme en utilisant les relations suivantes :

- À chaque étape $i$, les coefficients sont mis à jour selon :

$$
u_i = u_{i-2} - q_i \cdot u_{i-1}
$$
$$
v_i = v_{i-2} - q_i \cdot v_{i-1}
$$

où :
- $q_i$ est le quotient obtenu lors de la division de $a$ par $b$.
- Les indices $i-2$ et $i-1$ se réfèrent aux étapes précédentes dans le tableau.

### Exemple de Tableau

Voici un tableau d'exemple pour clarifier le processus :

| étape i | a    | b   | r   | q   | u   | v   |
| ------- | ---- | --- | --- | --- | --- | --- |
| -1      |      |     |     |     | 1   | 0   |
| 0       |      |     |     |     | 0   | 1   |
| 1       | 1236 | 96  | 84  | 12  | 1   | -12 |
| 2       | 96   | 84  | 12  | 1   | -1  | 13  |
| 3       | 84   | 12  | 0   | 7   | 13  | -1 |

### Conclusion

À la fin de l'algorithme, les valeurs finales de $u$ et $v$ fournissent une solution à l'équation de Bézout, permettant d'exprimer le pgcd comme une combinaison linéaire des deux nombres initiaux. Ce processus est essentiel non seulement pour trouver le pgcd, mais aussi pour résoudre des problèmes liés à la théorie des nombres et à la cryptographie.

---
**Question :**
1. Faire le tableau de Bézout à partir de $pgcd(1236, 96)$
2. En déduire les deux entiers relatifs où $ab+uv=pgcd(a,b)$ et vérifier 

---
**Exercices** :
- [[TD arithmétique#Exercice 2]]
- [[TD arithmétique#Exercice 3]]