---
MOOC: "[[Programmation]]"
Langage: C++
Type: Classes
tags:
---
Nous avons vu quand pour utiliser [[Permanent/Programmation/C++/Les classes|une classe]], il faut définir le prototype dans le fichier `.h` et décrire la fonction dans le fichier `.cpp`. Cependant, il se peut peut que de toutes méthode fassent très peu de lignes. On peut alors les décrire directement dans le `.h` en utilisant `inline` :

```h
#ifndef FICHIER_H
#define FICHIER_H

class demo{
public
	...
	...
	inline int getX(){return m_x}
	inline int getY(){return m_y}
	...
	...
}
```