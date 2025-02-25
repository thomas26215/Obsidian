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

**Question 2**
> Pour compléter la base de $E$ en une base de R^4, nous devons ajouter deux vecteurs linéairement indépendants entre eux et indépendants des vecteurs de $B_E$. Un choix possible est $(1,0,0,0)$ et $(0,1,0,0)$
> Ainsi, une base complète de $\mathbb{R}^4$ est :  $B_{\mathbb{R}^4} = \{(1,1,0,0), (0,0,1,1), (1,0,0,0), (0,1,0,0)\}$
> Cette base contient 4 vecteurs linéairement indépendants qui engendrent $\mathbb{R^4}$.

# Exercice 7
**Question 1**
> $F=\{(x,y,z)\in\mathbb{R}³:x-2y+z=0\}$
> $G=Vect(u_1,u_2)$, où $u_1=(1,2,1),u_2=(2,1,3)$
> 
> => **Equation de $F$** : $F$ est définit par l'équation $x-2y+z=0$. Cela signifie donc que tout vecteur $v=(x,y,z)\in F$ satisfait cette équation
> 
> **=> Base de $G$** : $G=Vect(u_1,u_2)$, donc tout vecteur $x\in G$ peut s'écrire comme une combinaison linéaire : $$w=au_1+bu_2=a(1,2,1)+b(2,1,3),a,b\in\mathbb{R}$$ Cela donne : $$w=\begin{pmatrix}a+2b\\2a+b\\a+3b\end{pmatrix}$$
> 
> **=> Intersection $F\cap G$** : Pour que $w\in F\cap G$, il faut que $w\in G$ et que $w=(x,y,z)$ satisfasse aussi l'équation de $F:x-2y+z=0$. Substituons les coordonnées de $w=(a+2b, 2a+b, a+3b)$ sans l'équation de $F:x-2y+z=0$. Cela donne $(a+2b)-2(2a+b)+(a+3b)=0$.
> Simplifions : $a+2b-4a-2b+a+3b=0 <=> -2a+3b=0$
> 
> **=> Résolution du système** : On obtient une relation entre $a$ et $b$ : $-2a+3b=0$. Soit $a=\frac{3}{2}b$. En remplaçant cette relation dans l'expressions de $w=(a+2b,2a+b,a+3b)$, on exprime les vecteurs de l'intersection $F\cap G$ en fonction de $b$ : $$w=\begin{pmatrix}\frac{3}{2}b+2b\\2(\frac{3}{2}b)+b\\\frac{3}{2}b+3b\end{pmatrix}$$
> En calculant chacune des composantes :
> 1. $a+2b=\frac{3}{2}b+2b=\frac{7}{2}b$
> 2. $2a+b=2(\frac{3}{2}b)+b=3b+b=4b$
> 3. $a+2b=\frac{3}{2}b+3b=\frac{9}{2}b$
> 
> Ainsi, tout vecteur de $f\cap G$ s'écrit comme $w=b(\frac{7}{2}, 4, \frac{9}{2})$

# Exercice 8

**Exercice 1**
> Bah exo 7 frère

**Exercice 2**
> **=> Dimension des sous-espaces** : La dimension de $F$ est égale à 2 car l'équation $x-2y+z=0$ représente un plan dans $\mathbb{R}³$. La dimension de $G$ est égale à 2 car ses générateurs $(u_1, u_2)$ sont linéairement indépendants
> 
> **=> Utilisation de la formule de Grassmann** : La formule pour la dimension de la somme est donnée par $dim(F+G)=dim(F)+dim(G)-dim(F\cap G)$
> On sait que $dim(F)=2, dim(G)=2$
> 
> **=> Déterminer $F\cap G$** : Un vecteur dans $F \cap G$ doit appartenir à la fois à $F$ et à $G$.
> Autrement dit, il doit une combinaison linéaire des générateurs de $G$, tout en satisfaisant l'équation du plan définissant $F:x-2y+z=0$
> 
> **Exression générale d'un vecteur dans $G$** : Tout vecteur dans $G$ s'écrit comme : $w=au_1+bu_2=a(1,2,1)+b(2,1,3)$. Cela donne $w=(a+2b,2a+b,a+3b)$
> 
> **Condition pour appartenir à $F$** : Pour que ce vecteur appartiennt aussi à $F$, il doit satisfaire l'équation $x-2y96z=0$. Substituons les coordonnées de ce vecteur dans cette équation : $(a+2b)-2(2a+b)+(a+3b)=0$. En simplifiant : $a+b2-4a-2b+a+3b=0, -2a+3b=0$.
> On obtient une relation entre les coefficients : $a=\frac{3}{2}b$
> 
> **=> Dimension de l'intersection** : Puisque nous avons trouvé une seule relation linéaire entre les coefficients, cela signifie que l'intersection est un sous-espace vectoriel de dimension 1. Ainsi, $dim(F\cap G)=1$
> 
> **=> Calculer la dimension de la somme** : En appliquant la formule de grassmann : $dim(F+G) = dim(F)+dim(G)-dim(F\cap G)$. On obtient donc $dim(F+G)=2+2-1=3$
> Puisque la dimension de la somme est égale à cette de l'espace ambiant ($\mathbb{R}^3$), on conclut que $F+G=\mathbb{R}^3$
> 
> => **Ainsi, F+G=$\mathbb{R}^3$**