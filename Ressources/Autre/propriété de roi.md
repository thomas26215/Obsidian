C'est une propriété très simple et très efficace pour le calcul intégrale et notamment pour le calcul intégrale trigonométrique

### Propriété
Soit $f:[a,b]->\R$ une fonction continue
alors $\int_{a}^{b} f(x) \, \mathrm{d}x$ = $\int_{a}^{b} f(a+b-x) \, \mathrm{d}x$ (Propriété du roi)
Ce que ça dit intuitivement, c'est qu'intégrer de droite à gauche, c la même chose qu'intégrer de gauche à droite
C'est le même principe que pour les sommes (Vrai par commutativité)

### Démonstration
$\int_a^bf(x)dx$ = $\int_{a+b-a}^{a+b-b}f(a+b-u)(-du)$ En faisant un changement de variable : $x=a+b-u$ 
																							                                                   $dx=-du$
                 = $-\int^a_bf(a+b-u)du$        Par linéarité de l'intégrale
				 = $-(-\int^b_af(a+b-u)du)$ par la [[Propriété de symétrie de l'intégrale]]
				 = $\int^b_af(a+b-u)du$
				 = $\int^b_af(a+b-x)dx$ Grâce au cours sur les [[variables muettes]]
	+ cours [[Variables libres]] et [[Variables liées]]