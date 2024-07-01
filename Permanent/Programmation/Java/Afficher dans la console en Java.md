---
MOOC: "[[Programmation]]"
Langage: Java
Type: Concret
---
Afin d'afficher en Java, il faut écrire `System.out.print()`. Cela va afficher sans retour à la ligne. Pour pouvoir faire un retour à la ligne, il faut remplacer par `println()`. Dedans, on peut y afficher des variables, des chaînes de charactères.

>[!info]
>A noter que tout ce qui est affichée est automatiquement convertit en chaîne de charactère pour l'affichage.


**Exemple**
```Java
System.out.println("Coucou je m'appelle Thomas et j'ai " + 15 + ans)
System.out.println("Calcul " + 4 + 5)
System.out.println("Calcul" + (4 + 5))
```
**Sortie :**
```
Coucou je m'appelle Thomas et j'ai 15 ans
Calcul 45
Calcul 9
```