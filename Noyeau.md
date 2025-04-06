---
MOOC: "[[Mathématiques]]"
Thème: Algèbre linéaire
Sujet: Transformations linéaires
tags:
---

#### **Définition du noyau d'une application linéaire**
Soit $f : E \to F$ une application linéaire entre deux espaces vectoriels $E$ et $F$. Le **noyau** de $f$, noté $\ker(f)$, est l'ensemble des vecteurs de $E$ qui sont envoyés sur le vecteur nul de $F$ par $f$.  
Matériellement, cela s'écrit :
$$
\ker(f) = \{ u \in E \mid f(u) = 0_F \}.
$$

Le noyau est donc l'ensemble des solutions de l'équation homogène associée à $f$. Par définition, il est inclus dans $E$ :
$$
\ker(f) \subseteq E.
$$

#### **Propriétés du noyau**
1. **Sous-espace vectoriel :**  
   Le noyau de $f$ est toujours un sous-espace vectoriel de $E$. Cela signifie que :
   - Si $u, v \in \ker(f)$, alors $u + v \in \ker(f).$
   - Si $u \in \ker(f)$ et $\lambda \in K$ (le corps des scalaires), alors $\lambda u \in \ker(f).$

2. **Critère d'injectivité :**  
   L'application linéaire $f$ est injective si et seulement si son noyau est réduit au vecteur nul :
   $$
   f \text{ injective } \iff \ker(f) = \{0_E\}.
   $$

3. **Lien avec la matrice associée :**  
   Si $f$ est représentée par une matrice $A$ dans une base donnée, alors le noyau de $f$ correspond à l'ensemble des solutions du système homogène suivant :
   $$
   A X = 0.
   $$
   La dimension du noyau est donnée par le nombre de colonnes de la matrice moins son rang :
   $$
   \dim(\ker(f)) = n - \text{rang}(A),
   $$
   où $n$ est le nombre de colonnes de la matrice.

> [!Example]
> 1. Soit l'application linéaire suivante :
>    $$
>    f(x, y, z) = (x + y, y - z).
>    $$
>    Le noyau de cette application est donné par les vecteurs $$(x, y, z)$$ tels que :
>    $$
>    x + y = 0, \quad y - z = 0.
>    $$
>    En résolvant ce système, on obtient :
>    $$
>    x = -y, \quad z = y.
>    $$
>    Ainsi, le noyau est l'ensemble des vecteurs de la forme :
>    $$
>    (-y, y, y) = y(-1, 1, 1), \quad y \in K.
>    $$
>    Une base du noyau est donc :
>    $$
>    \{(-1, 1, 1)\}.
>    $$
> 
> 2. Si $$f : P_2(\mathbb{R}) \to \mathbb{R}^2$$ est définie par :
>    $$
>    f(ax^2 + bx + c) = 
>    \begin{pmatrix}
>        a + 3c \\ 
>        a - c
>    \end{pmatrix},
>    $$
>    alors le noyau est donné par les polynômes tels que :
>    $$
>        a + 3c = 0, \quad a - c = 0.
>    $$
>    En résolvant ce système, on trouve que $$a = c = 0.$$ Le noyau est donc constitué des polynômes de la forme :
>    $$
>        bx, \quad b \in \mathbb{R}.
>    $$
>    Une base du noyau est donc :
>    $$
>        \{x\}.
>    $$
