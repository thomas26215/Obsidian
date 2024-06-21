---
MOOC: "[[Programmation]]"
Langage: Java
Type: Outillage
tags:
---
L'outillage d'une fonction est le fait de compte le nombre de comparaisons qu'il y a..
**Exemple :**
```Java
private static void fonction(){
	int nbComparaisons = 0;
	...
	...
	if(...){// Comparaison
		nbComparaisons++;
	}
	if(...){//Comparaison
		nbComparaisons++;
	}
	...
	if(...){
		nbComparaison++;	
	}
	while(if faux){
		//Pas de comparaison car déja fait dans le if. Car on exécture le while que si le if est faux. Donc a on a déja fait la comparaison dans le if
	}
}
```

Ici, seul le nombre de comparaisons est renvoyé. Si l'on souhaite en même temps renvoyer une valeur, il faut utiliser une classe générique