---
MOOC: "[[Cours]]"
Ressource: "R5.Real.12 : Infographie"
Cours: TPs
Date:
tags:
Complete: false
Learned: false
---
## 0.1
$A=(x_A, y_A)$, $B=(x_B, y_B)$
$\vec{AB}=(x_B-x_A, y_B-y_A)$

2 vecteurs de même direction sont colinéaires

$\forall k\in R, \vec{v}=k\vec{u}$
=> $x_v=kx_u$
=> $y_v=ky_u$

**Définition** :2 vecteurs sont égaux si ils sont de même direction, même sens et même longueur ou s'ils ont les mêmes coordonnées

**Définition** : Les coordonnées cartésiennes sont des corrdonées sur un plan $x, y$ avec $n$ dimensions. Exemple : $\begin{pmatrix}2\\3\end{pmatrix}$ coordonées cartésiennes de $A$.
**Définition** : Les **coordonnées polaires** définissent la position d’un point dans un plan à partir de **la distance $r$ au centre (origine)** et de **l’angle $\theta$** formé avec une direction de référence (souvent l’axe $x$). Exemple : $(r, \theta)$ coordonnées polaires de $A$.

![[Drawing 2025-11-10 10.16.33.excalidraw]]

![[Drawing 2025-11-10 10.19.14.excalidraw]]



## 0.2
### 0.2.1
Un point est une intersection entre deux droites perpendiculaires
**Question 1**
> **Symétrie centrale** : $x' = -x, y'=-y$ 
> **Ecriture matricielle** : $$\begin{pmatrix}x'\\y'\end{pmatrix}=\begin{pmatrix}-1&0\\0&-1\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}$$
> La matrice avec les chiffres est appelée **Matrice de la symétrie centrale de centre O** = $S_0$
> **Transformation réciproque** : $S_0^{-1} = S_0$

**Question 2**
>**Symétrie centrale** : $x'=2x, y'=3y$
>**Ecriture matricielle** : $$\begin{pmatrix}x'\\y'\end{pmatrix}=\begin{pmatrix}2&0\\0&3\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}$$
>**Transformation réciproque** : $$\begin{pmatrix}x'\\y'\end{pmatrix}=\begin{pmatrix}\frac{1}{2}&0\\0&\frac{1}{3}\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}$$

**Question 3**
>**Symétrie centrale** : $x'=2x, y'=2y$
>**Ecriture matricielle** : $$\begin{pmatrix}x'\\y'\end{pmatrix}=\begin{pmatrix}2&0\\0&2\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}$$
>**Transformation réciproque** : $$\begin{pmatrix}x'\\y'\end{pmatrix}=\begin{pmatrix}\frac{1}{2}&0\\0&\frac{1}{2}\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}$$

**Question 3**
>**Symétrie centrale** : $x'=rcos(\alpha+\theta), y'=rsin(\alpha+\theta)$
>$cos(\alpha+\theta) = cos\alpha cos\theta-sin\alpha sin\theta$
>$sin(\alpha+\theta) = sin\alpha cos\theta+cos\alpha sin\theta$
>Donc : $$\begin{Bmatrix}x'=xcos\theta-ysin\theta\\y'=ycos\theta+xsins\theta\end{Bmatrix}$$
>**Ecriture matricielle** : $$\begin{pmatrix}x'\\y'\end{pmatrix}=\begin{pmatrix}cos\theta&-sin\theta\\sin\theta&cos\theta\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}$$
>**Transformation réciproque** : $$\begin{pmatrix}x'\\y'\end{pmatrix}=\begin{pmatrix}cos\theta&sin\theta\\-sin\theta&cos\theta\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}$$


### 0.2.2
Un point est une intersection entre deux droites perpendiculaires
**Question 1**
> **Symétrie centrale** : $x' = -x, y'=-y, z=-z$ 
> **Ecriture matricielle** : $$\begin{pmatrix}x'\\y'\\z'\end{pmatrix}=\begin{pmatrix}-1&0&0\\0&-1&0\\0&0&-1\end{pmatrix}\begin{pmatrix}x\\y\\z\end{pmatrix}$$
> La matrice avec les chiffres est appelée **Matrice de la symétrie centrale de centre O** = $S_0$
> **Transformation réciproque** : $S_0^{-1} = S_0$

**Question 2**
$$\begin{pmatrix}1&0&0\\0&1&0\\0&0&-1\end{pmatrix}\begin{pmatrix}1&0&0\\0&-1&0\\0&0&1\end{pmatrix}\begin{pmatrix}-1&0&0\\0&1&0\\0&0&1\end{pmatrix}$$

**Roration d'axe $x$** :
$$\begin{pmatrix}1&0&0\\0&cos\theta&-sin\theta\\0&sin\theta&cos\theta\end{pmatrix}$$
$$\begin{pmatrix}1&0&0\\0&cos\theta&sin\theta\\0&-sin\theta&cos\theta\end{pmatrix}$$



**Rotation d'axe $z$**
$$\begin{pmatrix}cos\theta&-sin\theta&0\\sin\theta&cos\theta&0\\0&0&1\end{pmatrix}$$



## TD 2

### Partie 1

**Définition** : $\begin{pmatrix}x\\y\end{pmatrix}$ coordonnées cartésiennes
- En 2D, $(x,y,1)$ : coordonnées homogènes
- En 3D, $(x,y,z,1)$ coordonnées homogènes en 3D

**Question 3**
> $$\begin{pmatrix}x'\\y'\\1\end{pmatrix}=\begin{pmatrix}1&0&2\\0&1&3\\0&0&1\end{pmatrix}\begin{pmatrix}x\\y\\1\end{pmatrix}$$


### Partie B
**Exercice**
> $$\begin{pmatrix}a&b&c\\d&e&f\\g&h&i\end{pmatrix}\begin{pmatrix}0&2&2\\0&0&2\\1&1&1\end{pmatrix}=\begin{pmatrix}c&2a+c&2a+2b+c\\f&2d+f&2d+2e+f\\i&2g+i&2g+2h+i\end{pmatrix}=\begin{pmatrix}2&3&3\\1&1&2\\1&1&1\end{pmatrix}$$
> => $$\left\{\begin{array}{ll}c=2\\2a+c=3\\2a+2b+c=3\\f=1\\2d+f=1\\2d+2e+f=2\\i=1\\2g+i=1\\2g+2h+i=1\end{array}\right.$$
> ---
>$$\left\{\begin{array}{ll}c=2\\a=\frac{1}{2}\\b=0\\f=1\\d=0\\e=\frac{1}{2}\\i=1\\g=0\\h=0\end{array}\right.$$
>Donc $$\begin{pmatrix}\frac{1}{2}&0&2\\0&\frac{1}{2}&1\\0&0&1\end{pmatrix}$$

**Question 1**
> $(2, 6, -2)$

**Question 2**
> $(2, 6, -2, 4)$ => $(\frac{2}{4}, \frac{6}{4}, \frac{-2}{4})$ 

**Question 3**
> $(3, 1, 2)$ => $(3, 1, 2, 1)$ ou $(6, 2, 4, 2)$ ou $(-9, -3, -6, -3)$

**Question 4**
> $$\begin{pmatrix}x'\\y'\\z'\\1\end{pmatrix}=\begin{pmatrix}1&0&0&3\\0&1&0&1\\0&0&1&4\\0&0&0&1\end{pmatrix}\begin{pmatrix}x\\y\\z\\1\end{pmatrix}$$
> $$T^=\begin{pmatrix}1&0&0&-3\\0&1&0&-1\\0&0&1&-4\\0&0&0&1\end{pmatrix}$$

**Question 5**
> $$S=S^{-1}\begin{pmatrix}-1&0&0&0\\0&-1&0&0\\0&0&-1&0\\0&0&0&1\end{pmatrix}$$

**Question 6**
> $W=S*T$
> $$\begin{pmatrix}-1&0&0&-3\\0&-1&0&-1\\0&0&-1&-4\\0&0&0&1\end{pmatrix}$$

**Question 7**
> $$\begin{pmatrix}-1&0&0&-3\\0&-1&0&-1\\0&0&-1&-4\\0&0&0&1\end{pmatrix}\begin{pmatrix}1&0\\2&2\\3&1\\1&1\end{pmatrix}=\begin{pmatrix}-4&-3\\-3&-3\\-7&-5\\1&1\end{pmatrix}$$
> $B'=(-4, -3, -7)$ 


### Problème

**Question 1**
> $$S=\begin{pmatrix}-1&0&0\\0&-1&0\\0&0&1\end{pmatrix}$$

**Question 2**
> $$T=\begin{pmatrix}1&0&-2\\0&1&10\\0&0&1\end{pmatrix}$$

**Question 2**
> $$H=\begin{pmatrix}\frac{1}{2}&0&0\\0&\frac{1}{2}&0\\0&0&1\end{pmatrix}$$

**Question 3**
> Matrice à calculer : $H*T*S$
> $$\begin{pmatrix}-\frac{1}{2}&0&-1\\0&-\frac{1}{2}&5\\0&0&1\end{pmatrix}$$

**Question 4**
> $$\begin{pmatrix}-\frac{1}{2}&0&-1\\0&-\frac{1}{2}&5\\0&0&1\end{pmatrix}\begin{pmatrix}1&6&-3&2\\1&2&-3&6\\1&2&-1&2\end{pmatrix}=\begin{pmatrix}-\frac{3}{2}&-5&\frac{5}{2}&-3\\-\frac{1}{2}&9&-\frac{7}{2}&7\\1&2&-1&2\end{pmatrix}$$

**Question 6**
> Pour revenir au carré initial, il faut faire $S^{-1}*T^{-1}*H^{-1}$
> $$S^{-1}=\begin{pmatrix}-1&0&0\\0&-1&0\\0&0&1\end{pmatrix}$$
> $$T^{-1}\begin{pmatrix}1&0&2\\0&1&-10\\0&0&1\end{pmatrix}$$
> $$H^{-1}=\begin{pmatrix}2&0&0\\0&-2&0\\0&0&1\end{pmatrix}$$
> $$Matrice=\begin{pmatrix}-2&0&-2\\0&-2&10\\0&0&1\end{pmatrix}$$


# TD 3

![[Drawing 2025-12-08 10.06.38.excalidraw]]
## 1

$A:(2, 1) -> O\vec{A}:(2, 1)$
$B:(-1, 2) -> O\vec{B}:(-1, 2)$ 

## 2
$\vec{O}:\begin{pmatrix}x_0-x_A\\y_0-y_A\end{pmatrix}=(-2, -1)$ 
## 3
$\vec{AB}=\begin{pmatrix}-3\\1\end{pmatrix}$ 
## 4
$\vec{M}: \begin{pmatrix}x-2\\y-1\end{pmatrix}$. $x_1=x_0-2, y_1=y_0-1$ 
## 5
$\vec{M}: \begin{pmatrix}x_0+1\\y_0-2\end{pmatrix}$. $x_2=x_0+1, y_2=y=0-2$ 
## 6
On fait une translation de vecteurs $\vec{OA}(2, 1)$ 

---
Passage de $R_0$ à $R_1$ par la translation de vecteur $O\vec{A}:(2, 1)$ 
$R_o -H_{01}-> R_1$ 
$X_0=H_{01}X_1$ où $H_{01}=\begin{pmatrix}1&0&2\\0&1&1\\0&0&1\end{pmatrix}$ 
$X_1=H^{-1}_{01}=H_{01}X_0=H_{10}X_0$ où $H_{10}=\begin{pmatrix}1&0&-2\\0&1&-1\\0&0&1\end{pmatrix}$

## 7
Translation de vecteurs $(-2, -1)$ 

## Obtention de matrices de transformations géométriques quelconques

Passage de $R_0$ à $R_1$
Une translation de vecteur $\vec{OC}:(a, b)$
$R_0 -H_{01}- R_1$ 
$X_0=H_{01}X_1$ où $H_{01}=\begin{pmatrix}1&0&a \\0&1&b\\0&0&1\end{pmatrix}$
Dans $R_1$, $X'_1=R{x,0}X_1$ où $R_{c, 0}=\begin{pmatrix}cos\theta&-sin\theta&0\\sin\theta&cos\theta&0\\0&0&1\end{pmatrix}$
$X'0=H_{01}R_{c, 0}H_{10}X_0$




# TD 4

## Partie 1

### Projections paralleles obliques

Connues : $M=(x, y, z)$ et $\vec{v}(a, b, c)$ 
On cherche $M':(x', y', z')$ et $k$

$\vec{MM'}=k\vec{v}$
$z'=0$


$$\left\{\begin{array}{ll}x'-x=ka \\ y'-y=kb \\ z'-z=kc \\z'=0\end{array}\right.=\left\{\begin{array}{ll}x'=x-\frac{a}{c}z\\y'=y-\frac{b}{c}z\\k=-\frac{z}{c}\\z'=0\end{array}\right.$$

$$\begin{pmatrix}x'\\y'\\z'\\1\end{pmatrix}\begin{pmatrix}1&0&-\frac{a}{c}&0\\0&1&-\frac{b}{c}&0\\0&0&0&0\\0&0&0&1\end{pmatrix}\begin{pmatrix}x\\y\\z\\1\end{pmatrix}$$

### Projections perspectives

## Question 1


$$SOBJ=\begin{pmatrix}1&2&2&1&2&2&1&1\\1&1&2&2&2&1&1&2\\-2&-2&-2&-2&-3&-3&-3&-3\\1&1&1&1&1&1&1&-1\end{pmatrix}$$
## Question 2

$$\begin{pmatrix}1&0&-2&0\\0&1&1&0\\0&0&0&0\\0&0&0&1\end{pmatrix}SPBJ=\begin{pmatrix}5&6&6&5&8&8&7&7\\-1&-1&0&0&-1&-2&-2&-1\\0&0&0&0&0&0&0&0\\1&1&1&1&1&1&1&1\end{pmatrix}$$

## Question 3

$$\begin{pmatrix}3&0&0&0\\0&3&0&0\\0&0&0&0\\0&0&-1&3\end{pmatrix}SPBJ=\begin{pmatrix}3&6&6&3&6&6&3&3\\3&3&6&6&6&3&3&6\\0&0&0&0&0&0&0&0\\5&5&5&5&6&6&6&6\end{pmatrix}=\begin{pmatrix}3/5&6/5&6/5&3/5&1&1&1/2&1/2\\3/5&3/5&6/5&6/5&1&1/2&1/2&1\end{pmatrix}$$