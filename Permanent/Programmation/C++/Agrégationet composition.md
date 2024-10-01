---
MOOC: "[[Programmation]]"
Langage: C++
Type: Relations entre éléments
tags:
---
[[Composition]] : L'élément contenu sera un attribut qui fera partit intégrante de l'agrégat (agrégation par valeur ou interne)
```Cpp
#include "ClasseB.h"

class ClasseA{
public:
	ClasseA():monObjetB(...){} //Passé par référence. Si objetA détruit, pas objetB
private:
	ClasseB monObjetB;
}
```


[[Agrégation]] : L'agrégat contient soit un attribut référence, soit un pointeur vers l'élément associé
```cpp
#include
```