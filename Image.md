---
MOOC: "[[Mathématiques]]"
Thème: Algèbre linéaire
Sujet: Transformations linéaires
tags: 
Complete: 
Learned:
---
#### **Définition de l'image d'une application linéaire**
Soit $f : E \to F$ une application linéaire entre deux espaces vectoriels $E$ et $F$. L'**image** de $f$, notée $\text{Im}(f)$, est l'ensemble des vecteurs de $F$ qui peuvent s'écrire comme l'image d'un vecteur de $E$ par $f$.  
Matériellement, cela s'écrit :
$$
\text{Im}(f) = \{v \in F \mid \exists u \in E, v = f(u)\}.
$$

Autrement dit, l'image correspond à l'ensemble des "résultats possibles" obtenus en appliquant $f$ à tous les vecteurs de $E$.

#### **Propriétés de l'image**
1. **Sous-espace vectoriel :**  
   L'image de $f$ est toujours un sous-espace vectoriel de $F$. Cela signifie que :
   - Si $v_1, v_2 \in \text{Im}(f)$, alors $v_1 + v_2 \in \text{Im}(f).$
   - Si $v \in \text{Im}(f)$ et $\lambda \in K$ (le corps des scalaires), alors $\lambda v \in \text{Im}(f).$

2. **Lien avec la matrice associée :**  
   Si $f$ est représentée par une matrice $A$ dans une base donnée, alors l'image de $f$ correspond à l'espace engendré par les colonnes de la matrice $A$ :
   $$
   \text{Im}(f) = \text{Vect}(c_1, c_2, \dots, c_n),
   $$
   où $c_i$ sont les colonnes de la matrice.

3. **Dimension de l'image :**  
   La dimension de l'image, appelée **rang** de l'application linéaire, est égale au nombre de colonnes indépendantes de la matrice associée :
   $$
   \dim(\text{Im}(f)) = \text{rang}(A).
   $$

> [!Example]
> 1. Soit l'application linéaire suivante :
>    $$
>    f(x, y, z) = (x + y, y - z).
>    $$
>    La matrice associée à cette application est :
>    $$
>    A =
>    \begin{pmatrix}
>        1 & 1 & 0 \\ 
>        0 & 1 & -1
>    \end{pmatrix}.
>    $$
>    Les colonnes sont :
>    $$
>    c_1 = (1, 0), \quad c_2 = (1, 1), \quad c_3 = (0, -1).
>    $$
>    Pour déterminer une base de l'image, on vérifie si ces colonnes sont linéairement indépendantes. Après réduction échelonnée ou calcul direct du rang, on trouve que les vecteurs $c_1$ et $c_2$ sont indépendants. Une base de l'image est donc :
>    $$
>    \text{Base de l'image} : \{(1, 0), (1, 1)\}.
>    $$
>    La dimension de l'image est donc égale à 2.
> 
> 2. Si $f : P_2(\mathbb{R}) \to P_1(\mathbb{R})$ est définie par :
>    $$
>    f(ax^2 + bx + c) = bx + c,
>    $$
>    alors l'image correspond à tous les polynômes du type $bx + c$ dans $P_1(\mathbb{R})$. L'espace engendré est donc :
>    $$
>    \text{Im}(f) = P_1(\mathbb{R}).
>    $$
>    Une base de l'image est donnée par :
>    $$
>    \{x, 1\}.
>    $$
> 
