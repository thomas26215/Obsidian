En C++, nous représentons généralement les classes dans deux fichiers distincts :
- Le fichier header qui sert à indiquer les prototypes des fonction de la classe
- Le fichier cpp qui va indiquer les corps de fonction de la classe

Voici comment se définit le fichier header :

```cpp
#ifndef POINT2D_H
#define POINT2D_H
#include <iostream>

class Point2D{
public:
	Point2D(int x = X_DEFAUt, int y = Y_DEFAUT);
	~Point2D(); // destructeur
	int getX() const;
	int getY() const;
	void deplacerDe(int dx, int dy);
	void afficher(std::ostream & sortie = std::cout);
	static int getNbInstances();
private:
	int m_x;
	int m_y;
	static int nbInstances;
	static int X_DEFAUT;
	static int Y_DEFAUT;
};
#endif
```

**Voici quelques remarques :**
- Nous devons inclure les 3 directives suivantes : `ifndef`, `define` et `endif` afin d'empêcher l'inclusion multiple d'un même fichier en-tête dans une unité de compilation
- Nous séparons les fonctions/attributs publics des privés (`public:` et `private:`)
- Nous avons [[Le constructeur|le constructeur]] : `Point2D(...);` qui définit certaines choses de bases si elles ne sont pas rentrées
- Nous avons [[Le destructeur|le destructeur]] : `~Point2D();`
- Nous avons des [[Les constantes|fonctions constantes]] : Nous devons préciser les fonctions constantes quand elles ne modifient pas les attributs à l'intérieur de la fonction
- Nous avons des [[L'appel de méthodes|fonctions]] normales
- Nous avons les variables constantes et non constantes qui sont tous privés
- Nous avons les attributs de la fonction qui sont tous précédés de `m_` pas convention (`int m_attribut1; int m_attribut2; ...`)


Il suffit maintenant de compléter les classes dans le fichier `cpp` :

```cpp
#include "Point2D.h"
#include <iostream>
using namespace std;

Point2D::Point2D(int x, int y) : m_x(x), m_y(y){
	nbInstances++;
}
Point2D::~Point2D(){
	nbInstances--;
	cout << "Un point a été supprimé";
}
...
// Autres fonctions

```

Quelques points à noter :
- On peut initialiser les attributs dans le constructeur après `:`
- Le destructeur est appelé automatiquement quand l'objet n'existe plus

Il est également possible d'utiliser la méthode [[Inline|inline]] pour les fonctions 

Enfin, une classe doit être sous [[La forme canonique de Coplien|forme canonique de Coplien]]