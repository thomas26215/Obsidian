---
MOOC: "[[Programmation]]"
Langage: Java
Type: Concret
---
Afin d'afficher en Java, il faut écrire `System.out.print()`. Cela va afficher une chaîne de charactères sans retour à la ligne. Pour pouvoir faire un retour à la ligne, il faut remplacer par `println()`. Dedans, on peut y afficher des variables, des chaînes de charactères.

>[!info]
>A noter que tout ce qui est affichée est automatiquement convertit en chaîne de charactère pour l'affichage.

>[!info] Concaténer des chaînes de charactères
>L'opérateur `+` permet de coller des chaînes de charactères (`sout("Je m'appelle" + "Thomas")` ⇒ Je m'appelle Thomas))

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