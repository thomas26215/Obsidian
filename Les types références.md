---
MOOC: "[[Programmation]]"
Langage: C++
Type: Bases
tags:
---
En C++n quand on passe un objet en référence à une fonction, il faut le passer par valeur. Ainsi, quand une procédure a besoin de modifier une valeur passer en paramètres, il lui faut un pointeur sur l'objet à modifier
```cpp
void additionner(int a, int b, int* resultat){
	*resultat = a + b;
}

int main(){
	int resultat = 0;
	additionner(10, 20, &resultat);
}
```
Une référence peut en fait être considéré comme un alias




L'opérateur de déréférencement :
- Il est possible de déclarer un pointeur : `int* pointeur`. Il faudra cependant obligatoirement utiliser L'adresse d'une variable pour l'initialiser ou le modifier
- Pour accéder à la valeur pointée : `*pointeur = 10;`
L'adresse :
- Pour obtenir l'adresse d'une variable : `int* pointeur = &variable` L'adresse de la variable au pointeur
- Dans une déclaration de référence : `int& r = i` Déclare r comme référence à i
- Les références `&` ne peuvent pas être nulles, contrairement aux pointeurs