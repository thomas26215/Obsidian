---
MOOC: "[[Programmation]]"
Langage: 
Type: 
tags:
---
Une classe template est une classe générique qui fonctionne avec différents types. Voici la structure générale de la classe :
```Cpp
template <Typename T>
class maClasse{
public:
	MaClasse(T valeur);
	T getDonnee() const;
private:
	T donnee;
};

template <typename T>
T maClasse<T>::methode(){
	...
}
```
- `T` représente ma variable de type générique, qui sera donc remplacée par `int`, `float` ...
- Nous écrivons le corps des fonction directement dans le fichier `.h`

Maintenant, nous pouvons utiliser cette classe générique dans le code :
```cpp
maClasse<int>* objetA = new maClasse<int>();
maClasse<float>* objetB = new maClasse<float>();
```