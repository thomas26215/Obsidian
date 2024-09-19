---
MOOC: "[[Programmation]]"
Langage: C++
Type: Surchage
tags:
---
Il existe deux principales surchages d'opérateurs :
1. **La surcharge d'opérateur de flux de sortie**
Voici son implémentation :
```Cpp
std::ostream & operateur << (std::ostream & sortie, const EntierContraint & ec){
	cout << "coucou";
	return sortie;
}
```
1. La fonction prend deux paramètres :
	- `std::ostream & sortie` : une référence au flux d'entrée (Il n'y a pas de rentrer explicitement le flux d'entrée dans l'appel de la fonction, ça le fait tout seul)
	- `const EntierContraint & ec` : Une référence à l'entier constant EntierContraint à afficher
2. On affiche simplement `coucou` sur la sortie standard
3. La fonction retourne la référence au flux de sortie, ce qui permet les appels de chaîne

>[!info] Utilisation
>On déclarer un objet `EntierContraint entier();`
>=> Maintenant, quand on fait `cout << entier;`, cela affiche **"coucou"**

2. **La surcharge d'opérateur de flux d'entrée**
Même principe que précédemment :
```Cpp
std::istream& operator >>(std::istream & entree, const EntierContraint & ec){
	cout << "Rentrez un chiffre";
	cin >> m_int;
	return entree;
}
```

Utliisation :
```Cpp
EntierContraint();
cin >> entierContraint;
```