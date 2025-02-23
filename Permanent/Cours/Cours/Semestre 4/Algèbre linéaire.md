# Espaces Vectoriels et Applications Linéaires

## 1. L'Espace $\mathbb{R}^n$

L'espace $\mathbb{R}^n$ est constitué de n-uplets de réels, où chaque élément peut être interprété comme un vecteur. Par exemple :

- **$\mathbb{R}^2$** : Ensemble des couples $(x_1, x_2)$ représentant des points dans le plan.
- **$\mathbb{R}^3$** : Ensemble des triplets $(x_1, x_2, x_3)$ représentant des points dans l'espace tridimensionnel.

De manière générale, un élément de $\mathbb{R}^n$ peut être écrit sous la forme :

$$
\begin{pmatrix}
X_1 \\
X_2 \\
\vdots \\
X_n
\end{pmatrix}
$$

### Opérations dans $\mathbb{R}^n$

Pour deux vecteurs $u = \begin{pmatrix} U_1 \\ U_2 \\ \vdots \\ U_n \end{pmatrix}$ et $v = \begin{pmatrix} V_1 \\ V_2 \\ \vdots \\ V_n \end{pmatrix}$ de $\mathbb{R}^n$, les opérations suivantes sont définies :

- **Somme** : $u + v = \begin{pmatrix} U_1 + V_1 \\ U_2 + V_2 \\ \vdots \\ U_n + V_n \end{pmatrix}$

- **Produit par un scalaire** : $\lambda u = \begin{pmatrix} \lambda U_1 \\ \lambda U_2 \\ \vdots \\ \lambda U_n \end{pmatrix}, \quad \text{où } \lambda \in \mathbb{R}$

- **Vecteur nul** : $\vec{0} = \begin{pmatrix} 0 \\ 0 \\ \vdots \\ 0 \end{pmatrix}$

- **Opposé d'un vecteur** : $-u = \begin{pmatrix} -U_1 \\ -U_2 \\ \vdots \\ -U_n \end{pmatrix}$

## 2. Définition d'un Espace Vectoriel

Un espace vectoriel sur un corps $\mathbb{K}$ (souvent $\mathbb{K} = \mathbb{R}$ ou $\mathbb{K} = \mathbb{C}$) est un ensemble non vide $E$ muni de deux opérations :

1. Une **loi de composition interne** : $E \times E \to E$, $(u,v) \mapsto u + v$
2. Une **loi de composition externe** : $\mathbb{K} \times E \to E$, $(\lambda,u) \mapsto \lambda u$

Ces opérations doivent satisfaire les propriétés suivantes :

- **Associativité** : $(u + v) + w = u + (v + w)$ pour tous $u, v, w \in E$
- **Commutativité** : $u + v = v + u$ pour tous $u, v \in E$
- **Élément neutre** : Il existe un vecteur nul $\vec{0} \in E$ tel que $u + \vec{0} = u$ pour tout $u \in E$
- **Opposé** : Pour tout $u \in E$, il existe $-u$ tel que $u + (-u) = \vec{0}$
- **Distributivité** :
  - $\lambda(u + v) = \lambda u + \lambda v$, pour tous $\lambda \in \mathbb{K}$, $u, v \in E$
  - $(\lambda + \mu)u = \lambda u + \mu u$, pour tous $\lambda, \mu \in \mathbb{K}$, $u \in E$
  - $(\lambda\mu)u = \lambda(\mu u)$ pour tous $\lambda, \mu \in \mathbb{K}$, $u \in E$
- **Élément neutre de la multiplication scalaire** : $1u = u$ pour tout $u \in E$, où $1$ est l'élément neutre dans $\mathbb{K}$

## 3. Exemples d'Espaces Vectoriels

- L'espace $\mathbb{R}^n$ des n-uplets de réels est un espace vectoriel sur $\mathbb{R}$
- L'ensemble des polynômes à coefficients dans un corps $\mathbb{K}$, noté $\mathbb{K}[X]$, est un espace vectoriel
- L'ensemble des matrices de taille $n\times p$ à coefficients dans $\mathbb{K}$, noté $\mathcal{M}_{n,p}(\mathbb{K})$, est un espace vectoriel
- L'ensemble des fonctions d'un ensemble $A$ dans un corps $\mathbb{K}$, noté $\mathcal{F}(A,\mathbb{K})$, est un espace vectoriel

## 4. Sous-Espace Vectoriel

### Définition

Une partie $F$ d'un espace vectoriel $E$ est appelée un **sous-espace vectoriel** si :

1. $F$ est non vide (contient le vecteur nul)
2. $F$ est stable par addition : si $u,v \in F$, alors $u+v \in F$
3. $F$ est stable par multiplication scalaire : si $u \in F$ et $\lambda \in \mathbb{K}$, alors $\lambda u \in F$

### Propriété

Si $F$ est un sous-espace vectoriel de $E$, alors $F$ est lui-même un espace vectoriel pour les lois induites par celles de $E$

## 5. Combinaisons Linéaires et Sous-Espace Engendré

### Combinaison Linéaire

Soit une collection de vecteurs $\{v_1, v_2, ..., v_n\}$ dans un espace vectoriel $E$. Une combinaison linéaire de ces vecteurs est une expression sous la forme :

$$
v = \lambda_1v_1 + \lambda_2v_2 + ... + \lambda_nv_n
$$

où les scalaires $\lambda_i \in \mathbb{K}$ sont appelés les coefficients.

### Sous-Espace Engendré

L'ensemble des combinaisons linéaires des vecteurs $\{v_1,\dots,v_n\}$ forme un sous-espace vectoriel noté :

$$
\text{Vect}(v_1,\dots,v_n) = \left\{\sum_{i=1}^{n}\lambda_iv_i \mid \lambda_i \in \mathbb{K}\right\}
$$

## 6. Indépendance Linéaire

Un ensemble de vecteurs $\{u_1, ..., u_q\}$ est dit **linéairement indépendant** si l'équation suivante admet uniquement la solution triviale :

$$
\sum_{i=1}^{q}\lambda_i u_i = \vec{0}
$$

ce qui implique que $\lambda_i = 0$ pour tout $i$.

Si une solution non triviale existe (c'est-à-dire où au moins un coefficient est non nul), alors les vecteurs sont dits **linéairement dépendants**.

## 7. Base et Dimension

### Base

Une **base** d'un espace vectoriel est un ensemble de vecteurs à la fois linéairement indépendants et générateurs de cet espace. Autrement dit :

- Les vecteurs sont indépendants
- Toute combinaison linéaire possible dans l'espace peut être obtenue à partir de ces vecteurs

### Dimension

La **dimension** d'un espace vectoriel correspond au nombre maximal d'éléments linéairement indépendants qu'il peut contenir. On note cette dimension par :

$$
\dim(E)
$$

## 8. Applications Linéaires

### Définition

Soient deux espaces vectoriels $V$ et $W$ sur le même corps $\mathbb{K}$. Une application $f : V \to W$ est dite **linéaire** si elle respecte les deux propriétés suivantes :

1. $f(u + v) = f(u) + f(v)$, pour tous $u,v \in V$
2. $f(\lambda u) = \lambda f(u)$, pour tout scalaire $\lambda \in \mathbb{K}$ et tout vecteur $u \in V$

### Noyau et Image

- Le **noyau** de $f$, noté $\ker(f)$, est l'ensemble des vecteurs envoyés sur le vecteur nul :

$$
\ker(f) = \{x \in V \mid f(x) = \vec{0}\}
$$

- L'**image** de $f$, notée $\text{Im}(f)$, est l'ensemble des valeurs atteintes par $f$ :

$$
\text{Im}(f) = \{f(x) \mid x \in V\}
$$

### Propriétés

- Le noyau de $f$ est un sous-espace vectoriel de $V$
- L'image de $f$ est un sous-espace vectoriel de $W$

## 9. Théorème du Rang

Pour une application linéaire $f : V \to W$, on a la relation suivante entre la dimension du noyau et celle de l'image :

$$
\dim(V) = \dim(\ker(f)) + \dim(\text{Im}(f))
$$
