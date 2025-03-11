---
MOOC: "[[Mathématiques]]"
Thème: Algèbre linéaire
Sujet: Fondements mathématiques
tags: 
Complete: false
Learned: false
---
Une partie $F$ d'un espace vectoriel $E$ est appelée un **sous-espace vectoriel** si :

1. $F$ est non vide (contient le vecteur nul)
2. $F$ est stable par addition : si $u,v \in F$, alors $u+v \in F$
3. $F$ est stable par multiplication scalaire : si $u \in F$ et $\lambda \in \mathbb{K}$, alors $\lambda u \in F$

> [!Example]
> <mark style="background: #00c49a;">Soit $F = {(x, y, z) \in \mathbb{R}^3 \mid x + y - 2z = 0}$. Montrer que F est un sous-espace vectoriel de $\mathbb{R}^3$</mark>
> - $0\in F$ car $0+0-2*0=0$
> - Soit $u_1\in(x_1,y_1,z_1)\in F$, on a $x_1+y_1-2z_1$, soit $u_1\in(x_2,y_2,z_2)\in F$, on a $x_2+y_2-2z_2$ 
> - $u_1+u_2=(x_1+x_2,y_1+y_2,z_1+z_2)\in F$
> - Or $(x_1+x_2)+(y_1+y_2)-2(z_1+z_2)=(x_1+y_1-2z_1)+(x_2+y_2-2z_2)=0+0=0$ donc $u_1+u_2\in F$ 
> - $\forall \lambda\in\mathbb{R},\lambda u_1=(\lambda x_1, \lambda y_1, \lambda z_1)$ et $\lambda x_1+\lambda y_1-2\lambda z_1=\lambda(x_1+y_1-2z_1)=\lambda*0=0$ donc $\lambda u\in F$
> => $F$ est un sous espace vectoriel de $\mathbb{R}³$ donc F est un sous espace vectoriel

> [!propriete]
> Si $F$ est un sous-espace vectoriel de $E$, alors $F$ est lui-même un [[Espace vectoriel|espace vectoriel]] pour les lois induites par celles de $E$