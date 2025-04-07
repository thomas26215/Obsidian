---
MOOC: "[[Mathématiques]]"
Thème: Algèbre linéaire
Sujet: Bases et dimensions
tags: 
Complete: 
Learned:
---
Une **base** d'un espace vectoriel est un ensemble de vecteurs à la fois linéairement indépendants et générateurs de cet espace. Autrement dit :

- Les vecteurs sont indépendants
- Toute combinaison linéaire possible dans l'espace peut être obtenue à partir de ces vecteurs

> [!Example] <mark style="background: #00c49a;">Soit $F = {(x, y, z) \in \mathbb{R}^3 \mid x + y - 2z = 0}$. Déterminer une base de $F$.</mark>
> On sait $x+y-2z=0 <=> x = -y+2z$. Ainsi :
> $$F=\{\begin{pmatrix} -y+2z \\ y\\ z\end{pmatrix},y\in\mathbb{R},z\in\mathbb{R}\}=\{y\begin{pmatrix} -1 \\ 1\\0 \end{pmatrix}+z\begin{pmatrix}2 \\0 \\ 1\end{pmatrix},y\in\mathbb{R},z\in\mathbb{R}\}=vect(\{(-1, 1, 0),(2,0,1\})$$
> De plus $(-1, 1, 0)$ n'est pas colinéaire si $(2, 0, 1)$ donc $B=\{(-1, 1, 0),(2,0,1)\}$ est une base de $F$