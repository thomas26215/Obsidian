# Introduction

**Question A**
> $2u_1-u_2=2(2,0,1)-(1,0,2) = (4-1,0-0,2-2)=(3,0,0)$
> 
> $u_1-u_2+u_3=(2,0,1)-(1,0,2)+(2,2,2)=\begin{pmatrix}2-1+2\\0-0+2\\1-2+2\end{pmatrix} = (3,2,3)$

**Question B**
> $\begin{pmatrix} 2a+b+2c=0\\2c=2\\a+2b+2c=0 \end{pmatrix}=\begin{pmatrix} b = -2a-2 \\ c = 1 \\ a + 2(-2a-2)+2=0 \\  \end{pmatrix} = \begin{pmatrix} b = -2a-2 \\ c=1 \\ a-4a-4+2=0 \\\end{pmatrix}=\begin{pmatrix} -\frac{1}{3} \\ c=1\\ a=\frac{2}{3} \\\end{pmatrix}$

**Question C**


# Exercice 3
**Question 1**
>$\begin{pmatrix}a+3c=0\\2b+7c=0\\a+2b+c=0\end{pmatrix}=\begin{pmatrix} a=-3c \\ b=-\frac{7}{2}c \\a+2b+c=0 \end{pmatrix} = \begin{pmatrix} a=-3c \\ b=-\frac{7}{2}c \\ (-3c)+2(-\frac{7}{2}c)+c=0 \end{pmatrix} = \begin{pmatrix} a=-3c \\ b=-\frac{7}{2}c \\ -3c-7c+c=-9c=0 \end{pmatrix} = \begin{pmatrix} a=-3c \\ b=-\frac{7}{2}c \\ c=0 \end{pmatrix} = \begin{pmatrix} a=0 \\ b=0 \\ c=0 \end{pmatrix}$

**Question 2**
> $\begin{pmatrix} a+c=0 \\ b+c=0 \\ b+c=0 \end{pmatrix}=\begin{pmatrix} a=-c \\ b=-c \\ b=-c \end{pmatrix} = \begin{pmatrix} a=-c \\ b=-c \\ c=\text{libre} \end{pmatrix} = \begin{pmatrix} a=-t \\ b=-t \\ c=t \end{pmatrix} = \begin{pmatrix} a=b \\ a=-c \\ c=\text{libre} \end{pmatrix}, \quad t \in \mathbb{R}$

**Question 3**
> $\begin{pmatrix}2a+b+c=0 \\ -a+2b-8c=0 \\ 3a-b+9c=0\end{pmatrix} = \begin{pmatrix}b=-2a-c\\-a+2(-2a-c)-8c=0\\3a-(-2a-c)+9c=0\end{pmatrix}\begin{pmatrix}b=c-2a\\a=-2c\\-10c+10c=0\end{pmatrix}=\begin{pmatrix}b=0-2*0=0\\a=-2*0=0\\0=0\end{pmatrix}$


# Exercice 4
**Question 1**
> $u_1=(0,1,0),u_2=(1,0,0)$
> $\{u_1,u_2\}$ est libre et non génératrice

**Question 2**
> $\{(1,0,0),(0,1,0),(0,0,1),(1,1,1)\}$ et une famille liée et génératrice de $\mathbb{R}$

# Exercice 5

**Question 1**
> - $0\in F$ car $0+0-2*0=0$
> - Soit $u_1\in(x_1,y_1,z_1)\in F$, on a $x_1+y_1-2z_1$, soit $u_1\in(x_2,y_2,z_2)\in F$, on a $x_2+y_2-2z_2$ 
> - $u_1+u_2=(x_1+x_2,y_1+y_2,z_1+z_2)\in F$
> - Or $(x_1+x_2)+(y_1+y_2)-2(z_1+z_2)=(x_1+y_1-2z_1)+(x_2+y_2-2z_2)=0+0=0$ donc $u_1+u_2\in F$ 
> - $\forall \lambda\in\mathbb{R},\lambda u_1=(\lambda x_1, \lambda y_1, \lambda z_1)$ et $\lambda x_1+\lambda y_1-2\lambda z_1=\lambda(x_1+y_1-2z_1)=\lambda*0=0$ donc $\lambda u\in F$
> => $F$ est un sous espace vectoriel de $\mathbb{R}³$ donc F est un sous espace vectoriel

> **On cherche une base**
> $F=\{(x,y,z)\in\mathbb{R}, x+y-2z=0\}$
> $$F=\{\begin{pmatrix} -y+2z \\ y\\ z\end{pmatrix},y\in\mathbb{R},z\in\mathbb{R}\}=\{y\begin{pmatrix} -1 \\ 1\\0 \end{pmatrix}+z\begin{pmatrix}2 \\0 \\ 1\end{pmatrix},y\in\mathbb{R},z\in\mathbb{R}\}=vect(\{(-1, 1, 0),(2,0,1\})$$
> De plus $(-1, 1, 0)$ n'est pas colinéaire si $(2, 0, 1)$ donc $B=\{(-1, 1, 0),(2,0,1)\}$ est une base de $F$

# Exercice 6
**Question 1**
> Les conditions $x-y=0$ et $z-t=0$ impliquent que $y=z$ et $z=t$. Donc tout vecteur de $E$ peut s'écrire sous la forme $(x,x,z,z)$ où $x$ et $z$ sont des réels quelconques.
> 
> Une base de $E$ est $B_E=\{(1,1,0,0),(0,0,1,1)\}$
> 
> Ces deux vecteurs sont linéairement indépendants et engendrent $E$. En effet :
> - $(1,1,0,0)$ représente le cas où $x=y=1$ et $z=t=0$
> - $(0,0,1,1)$ représente le cas où $x=y=0$ et $z=t=1$

---

- Pour trouver une base, nous devons choisir des vecteurs qui :
    - Respectent ces conditions (x = y et z = t)
    - Sont linéairement indépendants
    - Peuvent générer tous les vecteurs de E par combinaison linéaire
- Un choix naturel est :
    - v1 = (1, 1, 0, 0) : ce vecteur représente le cas où x = y = 1 et z = t = 0
        
    - v2 = (0, 0, 1, 1) : ce vecteur représente le cas où x = y = 0 et z = t = 1
        
- Ces deux vecteurs forment une base car :
    - Ils respectent les conditions x = y et z = t
    - Ils sont linéairement indépendants (aucun n'est multiple de l'autre)
    - Toute combinaison av1 + bv2 = (a, a, b, b) peut générer n'importe quel vecteur de E