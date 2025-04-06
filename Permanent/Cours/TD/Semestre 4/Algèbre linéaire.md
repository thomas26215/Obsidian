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


# Exercice 9

**Question 1**
> $F=\{(x,y,z\in\mathbb{R}^3|x-2y+z=0\}$
> $G=\{(x,y,z)\in\mathbb{R}^3|2x-y+2z=0\}$
> 
> **Base de F :** On peut exprimer $x$ en fonction de $y$ et $z$ : $x=2y-z$
> $$\begin{pmatrix}x\\y\\z\end{pmatrix}=\begin{pmatrix}2y-z\\y\\z\end{pmatrix}=y(2,1,0)+z(-1,0,0)$$
> Ainsi : $B_F=\{(2,1,0),(-1,0,0)\}$
> 
> ---
> 
> **Base de G :** On peut exprimer $y$ en fonction de $x$ et $z$ : $y=2x+2z$
> $$\begin{pmatrix}x\\y\\z\\\end{pmatrix}=\begin{pmatrix}x\\2x+2z\\z\end{pmatrix}=x(1,2,0)+z(0,2,1)$$
> Ainsi : $B_G=\{(1,2,0),(0,2,1)\}$

**Question 2**
> $dim(F) = 2$ (car la base de $F$ a deux vecteurs)
> $dim(G)=2$ (car la base de $G$ a deux vecteurs)
> 
> **Calcul d'intersection :** On doit trouver un vecteur appartenant à $F$ et $G$. Un vecteur appartenant $F$ et $G$ vérifie :
> $$\left\{\begin{array}{l}x-2y+z=0\\2x-y+z=0\end{array}\right.=\left\{\begin{array}{l}x-2y+z=0\\-3y=0 <=> y=0\end{array}\right.=\left\{\begin{array}{l}x+z=0\\y=0\end{array}\right.$$
> Ainsi, tout vecteur est de la forme $(x,0,-x)=x(1,0,-1)$. Ainsi, $F\cap G=Vect\{(1,0,-1)\}$ => $dim(F\cap G)=1$
> Donc, d'après la formule de Grassmann, $dim(F+G)=2+2-1=3$ et puisque $dim(F+G)=3$ et que l'espace ambiant est $\mathbb{R}^3$, $F+G=\mathbb{R}^3$

**Question 3**
> Pour que 2 sous espaces soient supplémentaires, il faut que $F+G=\mathbb{R}^3$ et que $F\cap G=\{0\}$
> On a déjà montré que $F+G=\mathbb{R}^3$ et que $F\cap G=vect\{(1,0,-1\}$. Ainsi, l'intersection n'est pas réduite à un vecteur nul

# Exercice 10
**Question 1**
> Pour démontrer que $vect(\vec{u_1}, \vec{u_2})=vect(\vec{v_1},\vec{v_2})$, on doit démontrer que tout vecteur de la base $(\vec{v_1,v_2})$ peut être exprimé comme une combinaison linéaire des vecteur de la base $(\vec{u_1},\vec{u_2})$ et inversement
> 
> On exprime $v_1$ et $v_1$ en fonction $u_1$ et $u_2$ : On cherche des scalaires $a,b,c,d$ tels que $v_1=au_1+bu_2$ et $v_2=cu_1+du_2$
> $$\begin{Bmatrix}2a+b=3\\3a-b=7\\-a-2b=0\end{Bmatrix}\space et\space \begin{Bmatrix}2c+d=3\\3c-d=7\\-c-2d=-7\end{Bmatrix}$$
> ---
> **Résolution pour $v_1$ :** $\begin{Bmatrix}2a+b=3\\3a-b=7\\-a-2b=0\end{Bmatrix}\space=\begin{Bmatrix}-4b+b=3\\3a-b=7\\a=-2b\end{Bmatrix}\space$
> => (2) $3a-b=7 <=> 3*2-(-1)=7 <=> 7=7$
> Donc $v_1=2u_1+u_2$
> ---
> **Résolution pour $v_2$** : $\begin{Bmatrix}2c+d=3\\3c-d=7\\-c-2d=-7\end{Bmatrix}=\begin{Bmatrix}5c=5 <=> c = 1\\d=3c <=> d=3\\-c-2d=-7\end{Bmatrix}$
> => $-1-2*3=-7 <=> -1-6 = -7 <=> -7 = -7$
> Donc $v_2=u_1+3u_2$
> ---
> **Ainsi :** n'importe quel vecteur pouvant être écrit en combinaison linéaire de $v_1,v_2$ peut
> également être écrit en combinaison linéaire de $u_1$ et $u_2$
>  ---
> **Exprimer $u_1$ et $u_2$ en fonction de $v_1$ et $v_2$ :**
> On a déjà $\vec{v_1} = 2\vec{u_1} + \vec{u_2}$ et $\vec{v_2} = \vec{u_1} + 3\vec{u_2}$.
> Réarrangeons la première équation : $\vec{u_2} = \vec{v_1} - 2\vec{u_1}$
> 
> Substituons dans la deuxième équation :  
> $\vec{v_2} = \vec{u_1} + 3(\vec{v_1} - 2\vec{u_1})$  
> $\vec{v_2} = \vec{u_1} + 3\vec{v_1} - 6\vec{u_1}$ 
> $\vec{v_2} = 3\vec{v_1} - 5\vec{u_1}$
> 
> Réarrangeons :  
> $5\vec{u_1} = 3\vec{v_1} - \vec{v_2}$  
> $\vec{u_1} = \frac{3}{5}\vec{v_1} - \frac{1}{5}\vec{v_2}$
> 
> Maintenant, substituons cette expression de $\vec{u_1}$ dans l'équation pour $\vec{u_2}$ :  
> $\vec{u_2} = \vec{v_1} - 2(\frac{3}{5}\vec{v_1} - \frac{1}{5}\vec{v_2})$  
> $\vec{u_2} = \vec{v_1} - \frac{6}{5}\vec{v_1} + \frac{2}{5}\vec{v_2}$  
> $\vec{u_2} = -\frac{1}{5}\vec{v_1} + \frac{2}{5}\vec{v_2}$
> 
> Ainsi, nous avons exprimé $\vec{u_1}$ et $\vec{u_2}$ en fonction de $\vec{v_1}$ et $\vec{v_2}$ :  
> $\vec{u_1} = \frac{3}{5}\vec{v_1} - \frac{1}{5}\vec{v_2}$  
> $\vec{u_2} = -\frac{1}{5}\vec{v_1} + \frac{2}{5}\vec{v_2}$
> 
> Cette correction montre que chaque vecteur de la base $(\vec{u_1}, \vec{u_2})$ peut être exprimé comme une combinaison linéaire des vecteurs de la base $(\vec{v_1}, \vec{v_2})$, complétant ainsi la démonstration que $\text{vect}(\vec{u_1}, \vec{u_2}) = \text{vect}(\vec{v_1}, \vec{v_2})$.
>  

**Question 2**
> Soit $x=(2,-7,-7)$ et $y=(2,7,7)$. On peut vérifier si on peut les écrire comme combinaison linéaire de $*u_1$ et $u_2$

**Question 3**
>$w=v_1+3v_2$   $(x_v, y_v)=(1,3)$
>$v_1=2u_1-u_2$
>$v_2=u_1+3u_2$
>=> Donc $w=2u_1-u_2+3u_1+9+u_2=5u_1+8u_2$ donc $(x_u,y_u)=5,8)$ 
>$$P=\begin{pmatrix}2 && 1\\-1 && 3\end{pmatrix}$$.
>$$P\begin{pmatrix}x_v\\y_v\end{pmatrix}=P\begin{pmatrix}x_u\\y_u\end{pmatrix}$$
>$B=\{u_1,u_2\}$ $B'=\{v_1,v_2\}$

# Exercice 11

> $B=\{u_1,u_2,u_3\}$ et $B'=\{w_1,w_2,w_3\}$
> $P_{BB'}=\begin{pmatrix}w_1&&w_2&&w_3\end{pmatrix}$

# Exercice 12

Rappel : pour chaque application, il faut vérifier les deux propriétés fondamentales des application linéaires :
- **Additivité** : $f(u+v)=f(u)+f(v)$
- **Homogénéité** : $f(cu)=cf(u)$

**Exercice 1**
> $(x,y,z)->x,y,z-1)$
> 
> **Test du vecteur nul** : $f(0,0,0) = (0,0,-1 \space!= (0,0,0))$ 
> Ainsi, non linéaire

**Exercice 2**
> **Expression matricielle** : $$\begin{pmatrix}1&0&0\\0&1&0\\-2&1&1\end{pmatrix}\begin{pmatrix}x\\y\\z\end{pmatrix}$$
> Ainsi, linéaire car représentable comme une matrice

**Exercice 3**
> **Contre-exemple avec l'additivité** :
> Soient $u=(1,0,0)$ et $v=(0,1,0)$
> - $f(u)=(1,0,0)$
> - $f(v)=(1,1,0)$
> - $f(u+v)=f(1,1,0)=(2,2,1)$
> - $f(u)+f(v)=(2,1,0) \space != f(u+v)$
> Ainsi, non linéaire

**Exercice 4**
> **Expression matricielle** : $$\begin{pmatrix}1&0&-1\\1&1&0\\0&0&0\end{pmatrix}\begin{pmatrix}x\\y\\z\end{pmatrix}$$
> Ainsi, linéaire

# Exercice 15
> Pour déterminer une matrice, on applique $f$ aux vecteurs de la base canonique de $\mathbb{R}^3$ à savoir $e_1=(1,0,0), e_2=(0,1,0), e_3=(0,0,1)$
> - f(e_1)=f(1,0,0)=(1+2*0,0,1+0)=(1,0,1)$ 
> - f(e_2)=f(0,1,0)=(0+2*1,1,0+0)=(2,1,0)$
> - f(e_3)=f(0,0,1)=(0+2*0,0,1+0)=(0,0,1)$
> 
> La matrice de $f$ dans la base canonique de $\mathbb{R}^3$ est donc : $$\begin{pmatrix}1&2&0\\0&1&0\\1&0&1\end{pmatrix}$$

**Exercice 2.a**
> Le noyeau est l'ensemble des vecteurs $v=(x,y,z)$ tels que $Av=0$. Cela revient à résoudre le système linéaire suivant :
> $$\begin{pmatrix}1&2&0\\0&1&0\\1&0&1\end{pmatrix}\begin{pmatrix}x\\y\\z\end{pmatrix}=\begin{pmatrix}0\\0\\0\end{pmatrix}$$
> 
> Ce qui donne les équations suivantes :
> - $x+2y=0$
> - $y=0$
> - $x+z=0$
> En résolvant le système, on trouve que $x=0, y=0, z=0$ donc le noyeau est réduit au vecteur nul : $ker(f) = \{(x,y,z)^r:x=y=z=0\}$
> La base du noyeau est donc $B_{ker(f)}=\{\}$

**Exercice 2.b**
> L'image est engendrée par les colonnes de la matrice $A$ : $$\begin{pmatrix}1&2&0\\0&1&0\\1&0&1\end{pmatrix}$$
> Les colonnes sont $v_1=(1,0,1), v_2=(2,1,0), v_3=(0,0,1)$
> On vérifie leur dépedance linéaire : $v_1+v_2+v_3=(1,0,1)+(2,1,0)+(0,0,1)=(3,1,2)$
> Nous avons vérifié que les colonnes sont linéairement indépendantes donc une base est constitué de ces 3 vecteurs :
> $$B_{Im(f)}=\{(1,0,1),(2,1,0),(0,0,1)\}$$
> Comme la dimension de l'image est 3 et que la dimension de l'espace de départ est 3, on a bien $dim(Im(f))=dim(\mathbb{R}^3)=3$ et donc $f$ est surjective

# Exercice 16
**Question 1**
> Soit $B=(e_1, e_2, e_3)$ une base de $\mathbb{R}^3$ et $T$ une application linéaire de $\mathbb{R}^3$ dans $\mathbb{R}^3$ telle que :
> - $T(e_1)=T(e_3)=e_3$
> - $T(e_2)=-e_1+e_2+e_3$
> 
> Pour trouver le noyau de $T$, on cherche les vecteurs  $v=xe_1+ye_2+ze_3$ tels que $T(v)=0$.
> $T(v)=T(xe_1+ye_2+ze_3)=xe_3+y(-e_1+e_2+e_3)+ze_3=-ye_1+ye_2+(x+y+z)e_3$
> Pour que $T(v)=0$, on doit avoir $-y=0$, $y=0$ et $x+y+z=0$
> Cela implique que $x=0$, $x+z=0$ et $x=-z$. Ainsi, les vecteurs du noyau sont de la forme $xe_1-xe_3=x(e_1-e_3)$
> Une base du noyau est donc $(e_1-e_3)$

**Exercice 2**
> La matrice A est formée des coordonnées des vecteurs $T(e_1), T(e_2), T(e_3)$ dans la base $B$.
> - $T(e_1)=e_3=0e_1+0e_2+1e_3$
> - $T(e_2)=-e_1+e_2+e_3=-1e_1+1e_2+1e_3$
> - $T(e_3)=e_3=0e_1+0e_2+1e_3$
> Donc la matrice est : $$A=\begin{pmatrix}0&-1&0\\0&1&0\\1&1&1\end{pmatrix}$$

**Exercice 3.a**
> Calculer $e_1, e_2, e_3$ en fonction de $u_1, u_2, u_3$
> On a le système :
> - $u_1=e_1-e_3$
> - $u_2=e_1-e_2$
> - $u_3=-e_1+e_2+e_3$
> 
> On peut exprimer $e_1, e_2, e_3$ en fonction de $u_1, u_2, u_3$ en résolvant ce système :
> - $e_1=\frac{1}{2}(u_1+u_2-u_3)$
> - $e_2=\frac{1}{2}(u_1+u_3)$
> - $e_3=\frac{1}{2}(u_1-u_2+u_3)$
> 
> Ainsi, nous avons exprimé les vecteurs $e_1, e_2, e_3$ en fonction de $u_1, u_2, u_3$

**Exercice 3.b**
> On veut $T_(u_1), T_(u_2)$ et $T(u_3)$ dans la base $U=\{u_1, u_2, u_3\}$ 
> - $T(u_1)=T(e_1-e_3)=T(e_1)-T(e_2)=e_3-e_3=0$
> - $T(u_2)=T(e_1-e_2)=T(e_1)-T(e_2)=e_3-(-e_1+e_2+e_3)=-e_1-e_2=u_2$
> - $T(u_3) = ...$
> $$A=\begin{pmatrix}0&-1&0\\0&1&0\\1&1&1\end{pmatrix}$$
> $$P_{BV}=\begin{pmatrix}1&1&-1\\0&-1&1\\-1&0&1\end{pmatrix}$$
> $$Pˆ{-1}_{BU}=\begin{pmatrix}1&1&0\\1&0&1\\1&1&1\end{pmatrix}$$
> $$D=\begin{pmatrix}0&0&0\\0&1&0\\0&0&1\end{pmatrix}$$

# Exercice 17
**Exercice 1**
> La matrice est de dimension $3*2$ ce qui signifie donc qu'elle représente une équation linéaire de $\mathbb{R}ˆ3$ dans $\mathbb{R}ˆ2$ telle que $f(x, y, z) = (
> 2x-y, y-z)$

**Exercice 2**
> La matrice est de dimension $2*3$ ce qui signifie qu'elle représente une équation linéaire de $\mathbb{R}ˆ2$ dans $\mathbb{R}ˆ3$ telle que $g(x,y,z)=(x+y, x-y, 2x+3y)$

**Exercice 3**
> $gof = g(f(x)) = g(f((x,y,z))) <=> g((2x-y, y-z) <=> (2x-y)+(y-z), (2x-y)-(y-z), 2(2x-y)-(y-z)+3(y-z) <=> 2x-y, 2x-y_0-y+z, 4x+z-3z <=> 2x-z, 2x-2y+z, 4x+y-3z$
> Ainsi :
> - $f(1,0,0)=(2,2,4)$
> - $f(0,1,0)=(0, -2, 1)$
> - $f(0,0,1)=(-1, 1, -3)$
> Donc $$P=\begin{pmatrix}2&0&-1\\2&-2&1\\4&1&-3\end{pmatrix}$$

**Exercice 4 :**
> ![[Drawing 2025-03-25 13.47.26.excalidraw]]

**Exercice 5 :**
> $gof((x,y,z))=0<=>\begin{Bmatrix}x=\frac{z}{2}\\y=z\\0=0\end{Bmatrix}$
> $Ker(gof)=\{(x,y,z)\in\mathbb{R}ˆ{3}; x=\frac{y}{2}, y=z\}=\{(\frac{z}{2}, z, z), z\in\mathbb{R}\}=vect(\{\frac{z}{2},1,1\})$
>
> $$gof((x, y, z))=(a, b, c)<=>\begin{Bmatrix}2x-z=a\\2x-2y+z=b\\4x+y-3z=c\end{Bmatrix}<=>\dots<=>\begin{Bmatrix}2x-y=a\\-2y+2z=b-a\\0=-5a+b+2c\end{Bmatrix}$$
> $Im(gof)=\{(a,b,c)\in\mathbb{R}ˆ3, -5a+b+2c=0)\}\{(a, 5a-2c, c), a\in\mathbb{R}\}=vect(\{(1,5,0),(0,-2,1)\})$ 

**Exercice 18**
> Soit $B=\{}

---

# Questions
D'accord, voici la reconstitution des énoncés des exercices à partir des solutions fournies dans le document `paste.txt`. Je vais reformuler les questions en utilisant les informations contenues dans les réponses.

**Exercice 1**

- **Question A:** Soit $u_1 = (2, 0, 1)$, $u_2 = (1, 0, 2)$, et $u_3 = (2, 2, 2)$. Calculer $2u_1 - u_2$ et $u_1 - u_2 + u_3$.
    
- **Question B:** Résoudre le système d'équations linéaires suivant :  
    $\begin{cases} 2a + b + 2c = 0 \ 2c = 2 \ a + 2b + 2c = 0 \end{cases}$
    

**Exercice 3**

- **Question 1:** Résoudre le système d'équations linéaires suivant :  
    $\begin{cases} a + 3c = 0 \ 2b + 7c = 0 \ a + 2b + c = 0 \end{cases}$
    
- **Question 2:** Résoudre le système d'équations linéaires suivant :  
    $\begin{cases} a + c = 0 \ b + c = 0 \ b + c = 0 \end{cases}$
    
- **Question 3:** Résoudre le système d'équations linéaires suivant :  
    $\begin{cases} 2a + b + c = 0 \ -a + 2b - 8c = 0 \ 3a - b + 9c = 0 \end{cases}$
    

**Exercice 4**

- **Question 1:** Soit $u_1 = (0, 1, 0)$ et $u_2 = (1, 0, 0)$. La famille ${u_1, u_2}$ est-elle libre ? Est-elle génératrice de $\mathbb{R}^3$ ?
    
- **Question 2:** La famille ${(1, 0, 0), (0, 1, 0), (0, 0, 1), (1, 1, 1)}$ est-elle libre ? Est-elle génératrice de $\mathbb{R}^3$ ?
    

**Exercice 5**

- **Question 1:** Soit $F = {(x, y, z) \in \mathbb{R}^3 \mid x + y - 2z = 0}$. Montrer que F est un sous-espace vectoriel de $\mathbb{R}^3$. Déterminer une base de F.
    

**Exercice 6**

- **Question 1:** Soit $E = {(x, y, z, t) \in \mathbb{R}^4 \mid x - y = 0, z - t = 0}$. Déterminer une base de E.
    
- **Question 2:** Compléter la base de E en une base de $\mathbb{R}^4$.
    

**Exercice 7**

- **Question 1:** Soient $F = {(x, y, z) \in \mathbb{R}^3 \mid x - 2y + z = 0}$ et $G = \text{Vect}(u_1, u_2)$, où $u_1 = (1, 2, 1)$ et $u_2 = (2, 1, 3)$. Déterminer l'intersection $F \cap G$.
    

**Exercice 8**

- **Question 2:** Déterminer la dimension de F, la dimension de G, la dimension de l'intersection $F \cap G$, et la dimension de la somme $F + G$. En déduire si $F + G = \mathbb{R}^3$. (Note: Cet exercice fait référence à l'Exercice 7 pour la définition de F et G)
    

**Exercice 9**

- **Question 1:** Soient $F = {(x, y, z) \in \mathbb{R}^3 \mid x - 2y + z = 0}$ et $G = {(x, y, z) \in \mathbb{R}^3 \mid 2x - y + z = 0}$. Déterminer une base de F et une base de G.
    
- **Question 2:** Calculer la dimension de F, la dimension de G, la dimension de l'intersection $F \cap G$, et la dimension de la somme $F + G$. En déduire si $F + G = \mathbb{R}^3$.
    
- **Question 3:** F et G sont-ils supplémentaires ?
    

**Exercice 10**

- **Question 1:** Soient $\vec{u_1} = (2, 3, -1)$ et $\vec{u_2} = (1, -1, -2)$. Soient $\vec{v_1} = (3, 7, 0)$ et $\vec{v_2} = (3, 7, -7)$. Démontrer que $\text{vect}(\vec{u_1}, \vec{u_2}) = \text{vect}(\vec{v_1}, \vec{v_2})$. (Note : Il est possible qu'il y ait une erreur dans l'énoncé de cet exercice. Voir l'analyse de l'énoncé).
    
- **Question 2:** Soit $x = (2, -7, -7)$ et $y = (2, 7, 7)$. Peut-on écrire $x$ et $y$ comme combinaisons linéaires de $\vec{u_1}$ et $\vec{u_2}$ ?
    

Ces énoncés ont été reconstitués au mieux à partir des réponses fournies.


---

D'accord, voici les corrections détaillées pour chaque exercice que j'ai donné précédemment.

## Corrections des Exercices

## Exercice 1 : Sous-espaces et Bases

1. **Définir et Montrer :**
    
    - Pour montrer que $F$ est un sous-espace vectoriel de $E$, il faut vérifier trois conditions :
        
        1. Le vecteur nul $(0, 0, 0)$ appartient à $F$ : $0 + 0 + 0 = 0$, donc c'est vrai.
            
        2. $F$ est stable par addition : Si $(x_1, y_1, z_1) \in F$ et $(x_2, y_2, z_2) \in F$, alors $x_1 + y_1 + z_1 = 0$ et $x_2 + y_2 + z_2 = 0$. En additionnant, $(x_1 + x_2) + (y_1 + y_2) + (z_1 + z_2) = 0$, donc $(x_1 + x_2, y_1 + y_2, z_1 + z_2) \in F$.
            
        3. $F$ est stable par multiplication scalaire : Si $(x, y, z) \in F$ et $\lambda \in \mathbb{R}$, alors $x + y + z = 0$. Donc $\lambda x + \lambda y + \lambda z = \lambda(x + y + z) = 0$, donc $(\lambda x, \lambda y, \lambda z) \in F$.
            
    - Conclusion : $F$ est un sous-espace vectoriel de $E$.
        
2. **Base de F :**
    
    - Comme $x + y + z = 0$, on peut écrire $z = -x - y$. Donc tout vecteur de $F$ est de la forme $(x, y, -x - y) = x(1, 0, -1) + y(0, 1, -1)$.
        
    - La famille ${(1, 0, -1), (0, 1, -1)}$ est une base de $F$.
        
    - La dimension de $F$ est 2.
        
3. **Vecteur Spécifique :**
    
    - Pour $v = (1, -1, 0)$, on a $1 + (-1) + 0 = 0$, donc $v \in F$.
        

## Exercice 2 : Familles Libres et Génératrices

1. **Famille Libre :**
    
    - On cherche à résoudre $\alpha u + \beta v + \gamma w = 0$, soit $\alpha(1, 0, 1) + \beta(0, 1, 1) + \gamma(1, 1, 2) = (0, 0, 0)$. Cela donne le système :
        
        - $\alpha + \gamma = 0$
            
        - $\beta + \gamma = 0$
            
        - $\alpha + \beta + 2\gamma = 0$
            
    - En substituant les deux premières équations dans la troisième, on obtient $(-\gamma) + (-\gamma) + 2\gamma = 0$, ce qui est toujours vrai. Donc il y a une infinité de solutions. Par exemple, $\alpha = 1$, $\beta = 1$, $\gamma = -1$.
        
    - Conclusion : La famille ${u, v, w}$ n'est pas libre.
        
2. **Famille Génératrice :**
    
    - Puisque la famille n'est pas libre, elle ne peut pas être une base de $\mathbb{R}^3$. Pour savoir si elle est génératrice, on peut calculer le rang de la matrice formée par les vecteurs $u$, $v$ et $w$. Si le rang est 3, alors la famille est génératrice. Sinon, elle ne l'est pas. La matrice est :
        
        (101011112)\begin{pmatrix} 1 & 0 & 1 \\ 0 & 1 & 1 \\ 1 & 1 & 2 \end{pmatrix}101011112
    - Le déterminant de cette matrice est 0, donc le rang est inférieur à 3. La famille n'est pas génératrice.
        
3. **Base de E :**
    
    - On peut extraire une base en prenant deux vecteurs linéairement indépendants parmi ${u, v, w}$. Par exemple, ${u, v}$ est une base du sous-espace engendré par ${u, v, w}$.
        

## Exercice 3 : Indépendance Linéaire

1. **Vérification :**
    
    - On cherche à résoudre $\alpha v_1 + \beta v_2 + \gamma v_3 = 0$, soit $\alpha(1, 0, 1, 0) + \beta(0, 1, -1, 0) + \gamma(1, 1, 1, 1) = (0, 0, 0, 0)$. Cela donne le système :
        
        - $\alpha + \gamma = 0$
            
        - $\beta + \gamma = 0$
            
        - $\alpha - \beta + \gamma = 0$
            
        - $\gamma = 0$
            
    - De ce système, on déduit que $\alpha = 0$, $\beta = 0$ et $\gamma = 0$.
        
    - Conclusion : La famille ${v_1, v_2, v_3}$ est libre.
        
2. **Extension :**
    
    - Pour compléter cette famille en une base de $\mathbb{R}^4$, on peut ajouter le vecteur $(0, 0, 0, 1)$. La famille ${v_1, v_2, v_3, (0, 0, 0, 1)}$ est une base de $\mathbb{R}^4$.
        

## Exercice 4 : Sous-espace Défini par un Système

1. **Nature de F :**
    
    - Pour montrer que $F$ est un sous-espace vectoriel, on vérifie :
        
        1. $(0, 0, 0) \in F$ car $0 - 0 + 0 = 0$ et $0 + 0 - 0 = 0$.
            
        2. Si $(x_1, y_1, z_1) \in F$ et $(x_2, y_2, z_2) \in F$, alors $(x_1 - y_1 + z_1) + (x_2 - y_2 + z_2) = 0$ et $(x_1 + y_1 - z_1) + (x_2 + y_2 - z_2) = 0$, donc $F$ est stable par addition.
            
        3. Si $(x, y, z) \in F$ et $\lambda \in \mathbb{R}$, alors $\lambda x - \lambda y + \lambda z = 0$ et $\lambda x + \lambda y - \lambda z = 0$, donc $F$ est stable par multiplication scalaire.
            
    - Conclusion : $F$ est un sous-espace vectoriel de $\mathbb{R}^3$.
        
2. **Base de F :**
    
    - On a le système :
        
        - $x - y + z = 0$
            
        - $x + y - z = 0$
            
    - En additionnant les deux équations, on obtient $2x = 0$, donc $x = 0$. En substituant dans la première équation, on a $-y + z = 0$, donc $y = z$.
        
    - Donc $F = {(0, y, y) \mid y \in \mathbb{R}}$. Une base de $F$ est ${(0, 1, 1)}$.
        

## Exercice 5 : Combinaison Linéaire et Générateurs

1. **v est-il combinaison linéaire de u1 et u2?**
    
    - On cherche $\alpha$ et $\beta$ tels que $v = \alpha u_1 + \beta u_2$, soit $(1, 1, 1) = \alpha(1, 2, 1) + \beta(1, 0, 2)$. Cela donne le système :
        
        - $\alpha + \beta = 1$
            
        - $2\alpha = 1$
            
        - $\alpha + 2\beta = 1$
            
    - De la deuxième équation, on a $\alpha = \frac{1}{2}$. En substituant dans la première équation, on a $\beta = \frac{1}{2}$. En substituant dans la troisième équation, on a $\frac{1}{2} + 2(\frac{1}{2}) = \frac{3}{2} \neq 1$.
        
    - Conclusion : $v$ ne peut pas s'écrire comme une combinaison linéaire de $u_1$ et $u_2$.
        
2. **Base?**
    
    - $u_1$ et $u_2$ ne sont pas colinéaires donc ils forment une base de vect(u1, u2), de dimension 2.
        
    - Pour savoir si $(u_1, u_2)$ est une base de $\mathbb{R}^3$, il faudrait que ce soit une famille libre et génératrice de $\mathbb{R}^3$. Or on a vu que ce n'est pas le cas.
        
    - Conclusion : $(u_1, u_2)$ n'est pas une base de $\mathbb{R}^3$
        

J'espère que ces corrections t'aideront à te préparer pour ton contrôle. N'hésite pas si tu as d'autres questions.

### Citations:

1. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/49351872/4a0f9b34-da93-4f4c-9501-9ef2448c2bde/paste.txt](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/49351872/4a0f9b34-da93-4f4c-9501-9ef2448c2bde/paste.txt)

---

Réponse de Perplexity: pplx.ai/share