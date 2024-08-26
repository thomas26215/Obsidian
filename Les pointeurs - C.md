Un pointeur en C stocke l'adresse mémoire d'une autre variable
Il y a plusieurs avantages : la manipulation de chaînes de tableaux, une allocation dynamique de memoire ou bien passer des données de référence aux tableaux

# Créer un pointeur
Pour créer un pointeur, il fait faire `int &pointeur = NULL`. Comme pour les variables, il est important d'initialiser les pointeurs. Cependant, on ne les initialisé pas avec les valeur 0 mais avec `NULL` (==Attention a bien l'écrire en majuscules==)
> [!info] Utilité
> Cela va réserver une place en mémoire mais au lieu de stocker une variable, on stocke l'adresse d'une autre variable

Maintenant, pour indiquer l'adresse d'une autre variable au pointeur, il faut faire : `pointeur = *variable`
Cela donne ça :
```C
int age = 10;
int *pointeurSurAge; // 1) signifie "Je crée un pointeur"
pointeurSurAge = &age; // 2) signifie "pointeurSurAge contient l'adresse de la variable age"
```
