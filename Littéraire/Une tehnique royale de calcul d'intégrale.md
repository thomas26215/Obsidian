Notre objectif étant de calculer l'intégrale suivante :
$$\int_{\frac{\pi}{6}}^{\frac{\pi}{3}}\frac{1}{1+(tan(x))^{2013}}dx$$ ⇒ **Il est possible d'utiliser la propriété du Roi**.
>[!info]
>En effet, il est compliqué de trouver une primitive de cette fonction car une primite d'une puissance $2013$ est compliquée à trouver. Et changements de variables infructueuses de la part d'Axel

Voici à quoi ressemble la propriété
>Soit $f :[a, b] → \mathbb{R}$  une fonction continue
>Alors : $$\int_a^bf(x)dx=\int_a^bf(a+b-x)dx$$
>Cela indique implicitement qu'on peut intégrer de droite à gauche comme de gauche à droite

Ce changement de sens est aussi souvent utilisés dans la calcul de somme pour débloquer certaines situations
**Résultats analogue pour les sommes :**
>$$\sum_{k=a}^bf(k)=\sum_{k=a}^bf(a+b-k)$$

**Démonstration de la propriété du Roi :**
>$$\int_a^bf(x)dx=\stackrel{\tiny\text{x=a+b-u, dx=-du}}{\boxed{\displaystyle\int_{a+b-a}^{b+b-a} f(a+b-u) -du}}=-\int_b^af(a+b-u)du=-[-\int_b^af(a+b-u)du]=\int_a^bf(a+b-u)du=\int_a^bf(a+b-x)dx$$

Comment appréhender le changement de variable ?
> - Changement de variable proposé : $x = a + b - u ⇔  u = a+b-x$ 
> 	- Quand $x = a$ (borne indérieure) : $a+b-x=a+b-a=b$
> 	- Quand $x=b$ (borne supérieure) : $a+b-x=a+b-b=a$
> - De plus, quand $x$ augmente, $d$ diminue, donc $dx=-du$ (Quand on différencie l'équation)


Petit corrolaire avant de se lancer dans le problème :
> Soit $f:[0;\frac{\pi}{2}] → \mathbb{R}$ une fonction continue
> Alors : $$\int_0^{\frac{\pi}{2}}f(cos(x))dx = \int_0^\frac{\pi}{2}f(cos(\frac{\pi}{2}-x))dx=\int_0^{\frac{\pi}{2}}f(cos(\frac{\pi}{2}cos(x)+sin(\frac{\pi}{2})sin(x))dx=\int_0^{\frac{\pi}{2}}f(sin(x))dx$$
> **Ainsi :**
> $$\int_0^{\frac{\pi}{2}}cos^n(x)dx=\int_0^{\frac{\pi}{2}}sin^n(x)dx\space\forall n\in\mathbb{N}$$
> Quelques formules trigonométriques pour mieux comprendre :
> - $cos(x)=cos(\frac{\pi}{2}-x)$ pour $x$ entre $0$ et $\frac{\pi}{2}$
> - $cos(A-B)=cos(A)cos(B)+sin(A)sin(B)$
> - $cos(\frac{\pi}{2})=0$ et $sin(\frac{\pi}{2})=1$


En l'appliquant à notre problème :
$$\int_{\frac{\pi}{6}}^{\frac{\pi}{3}}\frac{1}{1+tan(x)^{2013}}dx$$
> Pour savoir qu'il faut utiliser la propriété du Roi, c'est que nous savons que $\frac{\pi}{6}+\frac{\pi}{3} = \frac{\pi}{2}$ et nous avons des fonctions trigonométriques
> 
> Ainsi, en appliquant notre formule :
> 
> $$\int_{\frac{\pi}{6}}^{\frac{\pi}{3}}\frac{1}{1+tan(x)^{2013}}dx = \int_{\frac{\pi}{6}}^{\frac{\pi}{3}}\frac{1}{1+tan(\frac{\pi}{2}-x)^{2013}}dx$$
> Car $\frac{\pi}{3}+\frac{\pi}{6}=\frac{\pi}{2}$. Egalement, quand la somme des bornes vaut $\frac{\pi}{2}$ et que l'on a des fonctions trigonométriques, il est judicieux de penser à cette propriété
> 
> $$\int_{\frac{\pi}{6}}^{\frac{\pi}{3}}\frac{1}{1+tan(\frac{\pi}{2}-x)^{2013}}dx=\int_{\frac{\pi}{6}}^{\frac{\pi}{3}}\frac{1}{1+\frac{1}{tan(x)^{2013}}}dx$$
> Car $tan(\frac{\pi}{2}-x)=\frac{sin(\frac{\pi}{2}-x)}{cos(\frac{\pi}{2}-x)}=\frac{cos(x)}{sin(x)}=\frac{1}{tan(x)}$
> 
> $$\int_{\frac{\pi}{6}}^{\frac{\pi}{3}}\frac{1}{1+\frac{1}{tan(x)^{2013}}}dx=\int_{\frac{\pi}{6}}^{\frac{\pi}{3}}\frac{tan(x)^{2013}}{1+tan(x)^{2013}}dx$$
> Donc :
> $$2I=\int_{\frac{\pi}{6}}^{\frac{\pi}{3}}\frac{1+tan(x)^{2013}}{1+tan(x)^{2013}}dx = \int_{\frac{\pi}{6}}^{\frac{\pi}{3}}dx=\frac{\pi}{6} ⇔ I=\frac{\pi}{12}$$



