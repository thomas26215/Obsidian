# Les tableaux a valeur deifnie
Il est possible de créer un tableau en C. Voici la méthode :
```C
int tableau[TAILLE]; //Créer un tableau de TAILLE entiers
tableau[0] = 10; //Modification du premier élément
```

Il est possible de passee un tableau en référence aux fonctions :
```C
void fonction(int *tableau, ...){
   ...
}
```

>[!Info] Pourquoi passe-t'on le tableau dans la fonction en tant que pointeur ?
>Il faut savoir que quand on passe un tableau dans une fonction, il se transforme automatiquement en un [[Les pointeurs - C|pointeur]] vers son premier élément, et c'est plus efficace que de copier tout le tableau. Cela permet également de modifier le tableau original. Cependant, il est tout de même possible de le passer en copie en faisant : `void fonction(int tableau[TAILLE]){}`. Le tableau est toujours passe en référence en tant que pointeur vers le premier élément, mais il a été copié vers un autre endroit de la mémoire pour ne pas modifier le tableau original

# Les tableau dynamiques
Il est possible de créer des tableaux donc on ne connait pas la taille des la compilation.
