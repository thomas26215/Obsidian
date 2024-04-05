---
MOOC: "[[Cours]]"
Ressource: S1.02
Cours: Evaluation du coût d'un algorithme
Date: 2023-11-27
tags: 
Complete: false
Learned: false
---
Un [[Définition - Algorithme|algorithme]] efficace consomme peu de ressources. Pour cela, on évalue **l'espace mémoire** utilisé par celui-ci et **le temps requis** par l'algorithme pour fournir la solution. Il est généralement assez simple de déterminer l'espace mémoire maximal utilisé par l'algorithme mais il cependant plus difficile de déterminer la performance de l'alrogithme, critère qui retiendra le plus notre attention car c'est la plus important pour mesurer l'efficacité de l'alrogithme

Pour mesurer le temps requis d'un algorithme sur un ensemble $D_n$, $n$ la taille des données, on note $coût_A(d)$ le coût  en temps de l'algorithme $A$ sur la donnée $d$

Pour évaluer la compléxité de l'algorithme, on évalue le pire cas possible, celui qui prendrait le plus de temps pour que l'algorithme le résous. On le note $Tworst(n)$
→ Le calcul se fait $Tworst(n)=max(coût_A(d); d\in D_n)$
C'est le même principe pour évaluer celui qui prend le moins de temps

La complexité en moyenne se calcule par $T_{avg}(n)=\sum _{d\in D_n}p(d)*coût_A(d)$ 

**La notion aymptotique** est le temps d'exécution exprimés à l'aide la notation asymptotique qui regroupe différents tps d'éxecutions indépendemment du matériel ou du logiciel

Il existe 3 types de classe de complexité :
- **Les classes constantes** : Quelle que soit la taille des données, le temps de l'a lgorithme est constant
- **Les classes $log(n)$** : réduit la taille des données à chaque itération (diviser pour régner)
- $nlog(n)$ : Tri fusion
- **Classe $n^2$** : Deux boules imbriquées

On note :
- $O$ le pire des cas
- $\Omega$ Le pire des cas
- $\Theta$ Quand l'alrgorithme a une même classe de coput dans le pire et dans le meilleur des cas

Pour évaluer la complexité d'un algorithme, ici, le tri d'un vecteur en prenant comme baromètre le nombre de compraisons effectuées entre deux éléments de ce vecteur, il y a plusieurs étapes (**Tri bulle amélioré**) :
1. Identifier les instructions donnant lieu à une comparaison (Ici 1 comparaison du `if`)
2. Trouver les facteurs d'influence sur le nombre de comparaisons. Sur notre cas, il y en a 3 :
	1. **vInt** déja trié : boucle `while` executée une fois, provocant `n-1` exécutions de la boucle `for`
	   ⇒ `n-1` comparaisons effectuées
	2. **vInt** déja trié : `(n-(i+1))` comparaisons
	3. présence de doublons = aucune influence
3. Exprimer la relation entre le nombre de comparaisons effectuées et la taille du vecteur
	- **Meilleur des cas :** $n-1$ comparaisons
	- **pire des cas** : $(n-(i+1))$ comparaisons pour la boucle for
	  Nombre de comparaisons = $1+2+3+...+(n-2)+(n-1)=\sum^{n-1}_{i=1}i=(n-1)*n/2$
	- ⇒ Nombre de comparaisons entre $n-1$ et $(n-1)*n/2$
4. Il faut en déduire la classe de complexité de l'algorithme
	- **Linéaire** pour le pire des cas : $n-1 → \Omega(n)$
	- **Quadratique** pour le meilleure des cas : $(n-1)*n/2 → O(n^2)$

--- 
**Questions :**
1. Comment définit un algorithme efficaces ?
2. Quels critères sont pris en compte pour juger de l'efficacité d'un algorithme ?
3. Comment mesurer le temps d'un algorithme ?
4. Comment calculer la complexité d'un algorithme ?
5. Qu'est ce que la notion asymptotique ?
6. Comment évaluer de la complexité d'un algorithme ? Expliquer avec l'algorithme de tri à bulle amélioré, en prenant en baromètre le nombre de comparaisons entre deux éléments de ce vecteur.
