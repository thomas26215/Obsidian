---
MOOC: "[[Cours]]"
Ressource: "R3.02 : Développement efficace"
Cours: "Cours 0 : La récursivité"
Date: 
tags: 
Complete: false
Learned: false
---
$n!=(n-1)!*n$
On peut écrire une fonction pour calculer la factorielle en utilisant de la récursivité :
```Cpp
void Factorielle(int n){
	while(n > 0){
		return Factorielle(n-1)*n;
	}
}
```

Pour écrire une fonction récursive ou une procédure récursive pour résoudre une problème, il faut imaginer qu'elle existe déjà et qu'elle calcule la réponse au problème <mark style="background: #ADCCFFA6;">P</mark>
Il faut exprimer la résolution du problème <mark style="background: #ADCCFFA6;">P</mark> sur des données <mark style="background: #FF5582A6;">D</mark> en fonction de la résolution du même problème sur des données réduites <mark style="background: #D2B3FFA6;">d</mark> plus petites
Il faut trouver une <mark style="background: #FFB86CA6;">dt</mark> pour laquelle on connaît trivialement la réponse au problème
Il faut s'assurer que les données convergent vers les données <mark style="background: #FFB86CA6;">dt</mark>

Généralement, les problèmes récursifs sont rangés en deux classes
- Pour résoudre le problème initial sur les données, il suffit de résoudre le problème sur des données plus petites
- Pour résoudre le problème initial sur des données, il faut résoudre deux fois le problème sur des données d1 et d2 et utiliser le résultat pour un résultat sur <mark style="background: #ADCCFFA6;">D</mark>
