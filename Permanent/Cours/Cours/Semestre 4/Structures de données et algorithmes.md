# Caractéritiques d'un jeu
- Présence d'un adversaire introduisant élément d'incertitude
- Les jeux intéressants sont très complexes
- Le but est de gagner, de déterminer le prochain coup à jouer
- Les coups doivent être évalués selon leur valeur

L'environnement des jeux considéré est complétement observable, déterministe, dynamisue, discret à tour de rôle, multi-agent et et un jeu à somme nulle

Un programme de jeu comprend un générateur de mouvement, une fonction de test d'arrêt, une fonction d'évaluation et un stratégie de contrôle
Pour formaliser le processus de recherche du meilleur coup, on utilise un arbre de décision appelé **Arbre de Jeu** construit pour chaque position p comme suit :
- La position p consitue la racine de l'arbre
- Si les coups sont possibles, à partir de la position p, donnent les positions $p_1, ..., p_n$, alors $p$ a comme fils $p_1, ..., p_n$
- Les neouds correspondants auc positions finales sont les feuilles de l'arbre de jeu

# Retour sur la récursivité
## Principes de base
Une fonction récursive est une fonction qui s'appelle elle-même
**Exemple :** Factorielle
```Java
int Factorielle(int n) {
    if(n == 0) {
        return 1;
    }return Factorielle(n-1)*n
}
```

Autre exemple classique : **Arbre de Fibonacci**

## Algorithmes de retour en arrière
Egalement appelé *backtracking*, c'est un algorithme qui explore toutes les possibilités. Quand l'algorithme se retrouve dans un cul de sac, il revient en arrière et explore une nouvelle solution

# Recherche graphe dans les jeux
## Un coup
On suppose que les deux joueurs exécutent alternativement un seul coup

## Minimax
Deux joueurs :
- MAX : Le joueur à qui on veut faire gagner la partie. Il va toujours tenter de maximiser son avantage
- MIN : Le joueur adverse. Il tente de minimiser l'avantage de joueur MAX
=> Les deux joueurs veulent gagner. Les deux joueurs ont exactement la même vision que son adversaires

**Exemple** : On peut voir ce processus d'association des valeurs aux noeurs intermédiaire, valeurs marquées en *italiques*
Les scores sont toujours en fonction du joueur MAX. +100 si MAX gagne, -100 si MIN gagne

Un algorithme qui impémente le joueur MAX comportera les phases suivantes :
1. Construire l'arbre de jeu pour P niveaux à partir de la configuration initiale
2. Visiter l'arbre de jeu par niveaux en remontant des noeuds terminaux jusqu'à la racine
3. Quand on réussit à associer une valeur à la racine (appelé valeur MiniMax), on fait le choix de coup qui mène vers le fils qui a cette valeur maximale
4. S'il y a plusieurs fils qui ont la même valeur, alors on en choisit un au hazard ou
    1. Celui qui conduit à la victoire ou
    2. Celui qui conduit à une situation finale dans le plus petit nombre de coups ou
    3. Un autre critère selon les spécificités de jeu

```Java
Algorithme diapo 78
```

##
