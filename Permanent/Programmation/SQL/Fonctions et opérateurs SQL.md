Une fonction d'agrégat calcule une valeur unique à partir d'un ensemble de valeurs. Voici les différentes fonctions d'agrégat :
- `count(*)` : Nombre de lignes en entrées
- `count(expression)` : Nombre de lignes pour lesquelles `expression` n'est pas `NULL`
- `count(DISTINCT expression)` Nombre de valeurs différentes de expression
- `max(expression)` maximum des valeurs non null de expression
- `min(expression)`
- `avg(expression)` : La moyenne des valeurs non null de expression
- `sum(expression)` : La somme des valeurs non null de expression

Fonctions et calcul de date et heure
- `age(d)` : L'âge qu'aurait aujourd'hui une personne née à la date d
- `current_age` : date courante | `current_time` : heure courante
- `now()` : date et heure de l'instant présent