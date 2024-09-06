---
MOOC: "[[Cours]]"
Ressource: "R3.16 : C"
Cours: "Cours 1 : Présentation du langage"
Date: 
tags: 
Complete: false
Learned: false
---
Langage compliqué. Important pour enseignement des cours de système (quand on veut parler en [[Instructions bas nivaux|bas niveau]])
On a besoin de gérer la mémoire nous-même

# Pourquoi C ?
- [[Codage assembleur|Assembleur]] trop compliqué
- Bas niveau
- Portabilité (notamment par rapport à l'assembleur)

Codage système
- Recherche dans les années 60
- 1973 UNIX
- 1980 → standard
- 1989 → ANSIC
⇒ C99 dans ce cours


Standardisé :
- Syntaxe
- Bibs standards
- (modèle mémoire)

Code de base :
```C
#include<stdio.h>
#include <stdlib.h>

int main(void){
	printf("Hello World");
	return EXIT.SUCCESS;
}
```

Il faut maintenant traduire ce que j'ai écrit en code machnie grâce à un [[Compilateur]]
⇒ GCC, clang, deux compilateurs différents (donne deux codes machines [assembleur] différents mais produit le même résultat)

[[Les principaux mots-clés en C]]
[[Structure]]
[[Les fonctions en C]]