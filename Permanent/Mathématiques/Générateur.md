
## Notation
On note $(\mathbb{Z}/n\mathbb{Z})^X$ l'ensemble des éléments inversibles de $\mathbb{Z}/n\mathbb{Z}$ pour tout entier $n > 2$. 

### Sous-groupe Généré par $a$
Soit $<a>$ le sous-groupe constitué des éléments suivants :

$$ 
<a> = \{ 1, a, a^2, a^3, ... \}
$$

### Définitions
- **Ordre de $a$** : Le nombre d'éléments distincts dans $<a>$.
- **Générateur** : Un élément $g$ est un générateur de $(\mathbb{Z}/n\mathbb{Z})^\times$ si et seulement si :

$$
<g> = (\mathbb{Z}/n\mathbb{Z})^X 
$$

<mark style="background: #BBFABBA6;">Exemple Générateur</mark> : 
> ⇒ On se place dans $(\mathbb{Z}/15\mathbb{Z})^X$
> $\Phi(15)=\Phi(3*5)=2*4=8$
> $(\mathbb{Z}/15\mathbb{Z})^X=\{\bar{1}, 2, 4, 7, 8, 11, 13, 14\}$ ⇒ Tous les nombres premiers avec $15$ ⇔ $pgcd(6, 15) != 1$
> $<2> = \{\bar{1}, \bar{2}, \bar{4}, \bar{8\}}$
> Element inversible dans $\mathbb{Z}/15\mathbb{Z}$
> Donc l'ordre de R est égal à 4
> Nombre d'éléments : $\#<2> != \Phi(15)$
> Donc $<2>$ n'est pas un générateur de $(\mathbb{Z}/15\mathbb{Z})^X$

> ⇒ On se place sur $(\mathbb{Z}/13\mathbb{Z})^X$
> $\Phi(13) = 12$
> $(\mathbb{Z}/13\mathbb{Z})^X=\{\bar{1}, \bar{2}, \bar{3}, \bar{4}, \bar{5}, \bar{6}, \bar{7}, \bar{8}, \bar{9}, \bar{10}, \bar{11}, \bar{12}\}$ ⇒ Tous les nombres premiers avec $12$
> $<2>=\{\bar{1}, \bar{2}, \bar{3}, \bar{4}, \bar{5}, \bar{6}, \bar{7}, \bar{8}, \bar{9}, \bar{10}, \bar{11}, \bar{12}\}$
> $=(\mathbb{Z}/13\mathbb{Z})^*$ 
> Donc $<2>$ est un générateur