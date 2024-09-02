---
MOOC: "[[Medias]]"
Type: Formation
FullName: Déclarez des variables
Numero: "04"
Categorie: Productivite, Programmation
Auteur: 
Lien: https://openclassrooms.com/fr/courses/19980-apprenez-a-programmer-en-c/7669586-declarez-des-variables
tags:
---
# La base
En C, une variable est constituée d'une **valeur** (Ce que ça stocke) et d'un **nom**. Il y a quelque règles à respecter pour le nom des variables :
- Que des minuscules, majuscules et chiffres
- Ca doit commencer par une lettre
- Pas d'espace, mais utilisation de `_`
- Pas d'accents

Voici les différents types de variables :
- Stockers les nombre entiers
	- `signed char`
	- `int`
- Les nombres décimaux
	- `long`
	- `float`
	- `double`
Il existe aussi les types de variables dites `unsigned` qui ne peuvent que stockes des nombres entiers positifs, mais qui peuvent stocker des nombres deux fois plus grands que les nombres dits `signed`

# Déclarer une variable
Pour déclarer une variables, il suffit simplement de déclarer le type et le nom :
```C
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char *argv[]) // Équivalent de int main()
{
	int nombreDeVies; // Déclarer une variable de type entier qui s'appelle nombreDeVies
	return 0;
}
```
>[!tip]
>Attention, la valeur de la variable par défaut n'est pas `0`. L'emplacement est réservé mais la valeur ne change pas. On n'efface pas ce qui se trouve dans la « case mémoire ». Du coup, votre variable prend la valeur qui se trouvait là avant dans la mémoire, et **cette valeur peut être n'importe quoi** ! Il faut donc penser à initialiser la variable pour ne pas avoir de choses bizarre dans notre programme !
# Affecter une valeur à une variable
Il suffit simplement de faire :
```C
nombreDeVies = 5;
```
Il est également possible pour forcer le fait qu'une variable garde la même valeur toute la durée du programme en utilisant `const`
```C
const int nombre = 5;
```

# Afficher le contenu d'une variable

