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

