---
MOOC: "[[Cours]]"
Ressource: "R3.04 : C++"
Cours: "Cours 1 : Introduction"
Date: 
tags: 
Complete: false
Learned: false
---
# Les types références
En C++, on peut utiliser des paramètres référence *&*
La syntaxe reste trompeyse car le signe de référence *&* reste le même que celui de l'opérateur de calcul d'adresse :
```C
void permuteEntiers(int &a, int &b){
	int c = a;
	a = b;
	b = c;
}
int main(){
	int i = 5;
	int j = 6;
	permuteEntiers(i, j);
	return 0;
}
```

Une variable / paramètre référence est un pionteur automatiquement déréférencé quand on le manipule. Elle pointe toujours sur la même variable au cours de sa vie
```C
int i = 5;
int & ref_i = i; //ref_i sera toujours un référence à i !

/* ------ */

void permuteEntiers(int & a, int & b){
	
}
int i = 5; i j = 6;
permuteEntiers(i, j);
```



---
Il est possible de surcharger une fonction en C++
⇒ Il faut tout de même qu'il aient une signature différente (nom fonction + paramètres)

---
Il est possible de mette une valeur par défaut dans les paramètres (dans le cas ou rien n'est rentré) :
```C
int f1(int x, int y = 4){
	//y vaut 4 si rien n'est rentré
	...
}
```

---
# Lire et écrire sur le terminal
```C
#include <iostream>
using namespace std;

cout << "Coucou" << endl; //Ecrire "coucou" dans le terminal
cin >> variable; //Demander à l'utilisateur une valeur pour la variable
```


---
# Classe
```C
/* Ficher .h */
class Point2D{
public:
	Point2D(int x = X_DEFAUT, int y = Y_DEFAUT); // Constructeur
	~Point2D(); // Destructeur
	int getX() const;
	int getY() const;
	void DeplacerDe(int dx, int dy);
	void afficher(std::ostream & sorte = std::cout);
	static int getNbInstances();
private:
	int m_x; // Attributs d'instance, préfixés par m_ par convention
	int m_x;
	static int nbInstance; //attributs de classe
	static const int X_DEFAUT; // Constantes de classe
	static const int Y_DEFAUT;
}
```

Devant chaque nom de méthode, on doit préciser le nom de la classe

```C
/* Fichier .cpp */
#include "Point2D.h"
#include <iostream>

Point2d::Point2D(int x, int y){
	//Une instance de plus
	nbInstances++;
}
Point2d::~Point2D(){
	//Une instance de moins
	nbInstances--;
}
int Point2d::getX(à const){
	//
}
int Point2d::getY() const{
	//
}
...
```

---
# Le cycle de vie des objets
Un objet est alloué (on lui donne un espace mémoire). S'il a un constructeur, le constructeur va être appelé.

>[!warning] Le constructeur
>son rôle n'est pas d'alloué mais d'initialiser

Voici comment se présente un constructeur :
```Cpp
Point2D::Point2D(int x = 0, int y = 0) : m_x(x), m_y(y){
	...
}
```

3 façons de fabriquer des objets :
- statique (rarement utilisé)
- allocation automatique : dans la pile (stack) et supprimé automatiquement à la fin du bloc d'instructions (fonction généralement) ⇒ `T nomObjet; // appel du const. par défaut s'il existe`
- allocation dynamique : Dans le tas (pile) Ils sont crées par un appel de l'opérateur `new` et doivent êtres détruits explicitement par l'opérateur `delete`
	- `T* pointeurObject = new T(<paramètres d'un constructeur>);`
	- `T* pointeurObject = new T;` ⇒ Si le constructeur existe par défaut

---
Les méthodes ne modifiant pas les objets dont êtres suivies de `const` : Le pointeur `this` d'une méthode d'instance constante est de type `const T*`

---
Le rôle du destructeur est de faire du ménage : il veillera à libérer la mémoire afin d'éviter que celle-ci ne soit perdue (fuite mémoire)
⇒ `MaClasse :: ~MaClasse()`

---
Pour qu'une classe soit bien écrite, il faut :
- Un constructeur par défaut ⇒ `Image(const std::string & nom = "une image");`
```cpp
Image::image(...) : m_nom(nom), m_hauteur(hauteur), m_largeur(largeur){
	...
}
```
- Un constructeur par recopie ⇒ `Image(const Image & image);`
```cpp
Image::image(const Image & image){
	if(image.m_contenu != nullptr){
		this->m_contenu = new unsigned char(m_hauteur * m*largeur);
		memcpy(this->m_contenu, image.m_contenu, m_hauteur * m_largeur);
	}else{
		this->m_contenu=nullptr;
	}
}
```
- Une opération d'affectation ⇒ `Image & operateor=(const Image & image);`
- Un destructeur ⇒ `~Image();`