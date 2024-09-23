Très bien, utilisons la loi binomiale pour résoudre ce problème.

Rappel du problème :

Nous cherchons la probabilité de gagner au moins une fois le jackpot en jouant 2 fois par semaine pendant 80 ans, sachant que la probabilité de gagner à chaque tirage est très faible.

Hypothèses :

La probabilité de succès (gagner le jackpot) à chaque tirage est .

Le nombre de tirages  est  tirages en 80 ans.


Nous allons utiliser la loi binomiale pour modéliser cette situation, qui est définie par :

P(X = k) = \binom{n}{k} p^k (1 - p)^{n - k}

 est la variable aléatoire représentant le nombre de fois où tu gagnes le jackpot,

 est le nombre de succès (victoires) que l’on veut,

 est le nombre d’essais (nombre de tirages),

 est la probabilité de succès pour un essai.


Ici, nous cherchons la probabilité de gagner au moins une fois sur 8 320 tirages. Cela revient à calculer :

P(X \geq 1) = 1 - P(X = 0)

Calcul de  :

La probabilité de ne pas gagner lors d'un tirage est , donc la probabilité de ne jamais gagner sur 8 320 tirages est :

$P(X = 0) = (1 - p)^{n} = \left(1 - \frac{1}{139\,838\,160}\right)^{8\,320}$

Maintenant, on peut utiliser cette valeur pour trouver la probabilité de gagner au moins une fois :

$P(X \geq 1) = 1 - \left(1 - \frac{1}{139\,838\,160}\right)^{8\,320}$

Je vais effectuer le calcul pour obtenir cette probabilité.

