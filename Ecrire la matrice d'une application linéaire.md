La matrice d'une application linéaire est une représentation de cette application qui te permet de calculer facilement l'image d'un vecteur par cette application en faisant une simple multiplication matricielle.

**Les étapes pour trouver la matrice d'une application linéaire :**

1. **Choisir les bases :**
    - Tu dois avoir une base pour l'espace de départ (l'espace où vivent les vecteurs que tu transformes). On l'appelle souvent la base de départ.
    - Tu dois aussi avoir une base pour l'espace d'arrivée (l'espace où vivent les vecteurs transformés). On l'appelle la base d'arrivée.
    - Dans beaucoup d'exercices, on te dit d'utiliser les bases canoniques. C'est souvent le plus simple. Si on parle de R², la base canonique est ((1, 0), (0, 1)). Pour R³, c'est ((1, 0, 0), (0, 1, 0), (0, 0, 1)), etc.
2. **Calculer les images des vecteurs de la base de départ :**
    - Prends chaque vecteur de la base de départ et calcule son image par l'application linéaire. C'est-à-dire, applique la transformation à chaque vecteur de la base.
3. **Exprimer les images dans la base d'arrivée :**
    - Chaque image que tu as calculée à l'étape précédente est un vecteur de l'espace d'arrivée. Tu dois exprimer ce vecteur comme une combinaison linéaire des vecteurs de la base d'arrivée. Les coefficients de cette combinaison linéaire seront les coordonnées du vecteur image dans la base d'arrivée.
4. **Construire la matrice :**
    - Les coordonnées que tu as trouvées à l'étape 3 deviennent les colonnes de la matrice. La première colonne correspond aux coordonnées de l'image du premier vecteur de la base de départ, la deuxième colonne aux coordonnées de l'image du deuxième vecteur, et ainsi de suite.

> [!Example]
> Prenons un exemple concret pour illustrer tout ça. Supposons que tu as l'application linéaire `f : R² -> R³` définie par `f(x, y) = (x + y, x - y, 2x)`. (C'est l'application f1 de l'exercice 13).
> 1. **Bases :**
>     - Base de départ (R²) : On choisit la base canonique `((1, 0), (0, 1))`.
>     - Base d'arrivée (R³) : On choisit la base canonique `((1, 0, 0), (0, 1, 0), (0, 0, 1))`.
> 2. **Calcul des images :**
>     - `f(1, 0) = (1 + 0, 1 - 0, 2 * 1) = (1, 1, 2)`
>     - `f(0, 1) = (0 + 1, 0 - 1, 2 * 0) = (1, -1, 0)`
> 3. **Expression dans la base d'arrivée :**
>     - Comme on a choisi la base canonique pour R³, c'est très facile ici. Les coordonnées sont directement les composantes du vecteur :
>         - (1, 1, 2) = 1 * (1, 0, 0) + 1 * (0, 1, 0) + 2 * (0, 0, 1) -> Coordonnées : (1, 1, 2)
>         - (1, -1, 0) = 1 * (1, 0, 0) + (-1) * (0, 1, 0) + 0 * (0, 0, 1) -> Coordonnées : (1, -1, 0)
> 4. **Construction de la matrice :**
>     - On prend les coordonnées qu'on a trouvées et on les met en colonnes :
> - text
>     `|  1  1 | |  1 -1 | |  2  0 |`
> - Voilà, c'est la matrice de l'application linéaire `f` dans les bases canoniques.
