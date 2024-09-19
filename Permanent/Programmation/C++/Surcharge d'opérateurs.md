---
MOOC: "[[Programmation]]"
Langage: C++
Type: Surchage
tags:
---
Il est possible de faire un surcharge d'opérateurs sur un objet. Voici le prototype de la fonction :
```Cpp
//Fichier.h
class MaClasse{
public:
	inline bool operator==(int autre){ //Surcharge pour la condition d'égalité
		return this->m_int == autre;
	}
	inline void operator=(int autre){
		this->m_int = autre;
	}
	inline bool operator<(int autre){
		this->m_int < autre;
	}
	...
private:
	...
	int m_int;
};
```

>[!info]
>Nous utilisons ici la fonction [[Inline]] pour code les fonctions directement dans le fichier `.h`


- Ici, nous surchargons les opérateurs en définissant des fonctions spéciales. Il suffit d'écrire `typeRenvoie operateur@(type autre)` où
	- `@` est l'opérateur à surchager (`>`, `<`, `!=`, ...)
	- `autre` qui est passé en paramètres est l'objet qui va être utilisé lors de l'opération, de type `type`
- **Portée** : La surcharge s'applique uniquement aux objets de la classe où elle est définie.
- **Exemple :** `void operateur=(int autre){this->m_int = autre}`
	- `operateur=` : L'opérateur à modifier est l'opérateur d'affectation
	- `int autre` ⇒ Ca veut dire que l'affectation est faite avec un entier
	- Nous faisons ensuite ce qui se passe dans la fonction

Il existe certaines surcharges spéciales, comme la surchage de l'opérateur de flux de sortie et la surchage de l'opérateur de flux d'entrées