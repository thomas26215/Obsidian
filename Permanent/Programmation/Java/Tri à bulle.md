---
MOOC: "[[Programmation]]"
Langage: Java
Type: Algorithmes de tri
tags:
---
Le principe de ce système est de placer le plus grand élément à droite de la liste. En fait, pour une liste de taille `t`, nous allons parcourir `i` fois la liste. Pour chaque parcours de la liste, nous allons parcourir itérativement chaque élément de la liste jusqu'à l'indice `t-i` et si l'élément actuel est plus grand que l'élément suivant, nous allons échanger les deux éléments. Le principe est que une fois que l'élément le plus grand est mis à droite, on y touche plus. et on fait ca jusqu'à ce que tous les éléments sont triés
En conclusion, cela permet de faire remotner progressivement les éléments les plus grands vers la fin de la liste.
![[Pasted image 20231113090322.png]]

---
**Links :**
[[Tri à bulles amélioré en Java]]