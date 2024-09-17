---
MOOC: "[[Programmation]]"
Langage: C++
Type: Classes
tags:
---
Le constructeur porte le nom de la classe. Il faut savoir qu'on peut donner des arguments par défauts au constructeur si l'utilisateur ne les mets pas. Voici comment déclarer le constructeur :
```cpp
MaClasse::MaClasse(int x, int y) : m_x(x), m_y(y){
	//Code supplémentaire
}
```

