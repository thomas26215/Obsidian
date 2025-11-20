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


