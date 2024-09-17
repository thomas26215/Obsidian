---
MOOC: "[[Programmation]]"
Langage: C++
Type: Les bases
tags:
---
En C++, il n'existe pas de vraies constantes. Il faut à la place utiliser le préprocesseur du compilateur
⇒ `#define TAILLE`

On va donc utiliser l'opérateur `const` :
```cpp
const int TAILLE = 5;
const double PI = 3.14;
const char MESSAGE[] = "Hello World"
```

- `const int *p` ⇒ Le pointeur est modifiable mais la valeur pointée ne l'est pas
- `int * const p` ⇒ Le pointeur n'est pas modifiable mais la valeur pointée si
- `const int * const p` ⇒ Ni le pointeur, ni la valeur ne peuvent être modifiées

`const` est utilisé pour qualifier une référence, c'est à dire une variable entière qui ne peut pas être modifiée
Finalement, on peut l'utiliser pour indiquer qu'une fonction ne modifier pas de l'objet auquel elle s'appliquera. Nous utilisons surtout cela dans [[Les classes | les classes]]