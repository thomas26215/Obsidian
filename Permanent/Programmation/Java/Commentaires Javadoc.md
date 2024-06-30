---
MOOC: "[[Programmation]]"
Langage: Java
Type: Commentaires
tags:
---
Utiliser `/** */` pour les commentaires Javadoc, qui sont utilisés pour générer de la documentation.
```java
/**
* Cette classe représente un exemple de classe.
* Elle contient une méthode principale.
*/
public class ExampleClass {

   /**
	* Méthode principale qui sert de point d'entrée pour l'application.
	*
	* @param args Les arguments de ligne de commande.
	*/
   public static void main(String[] args) {
	   System.out.println("Hello, world!");
   }

   /**
	* Additionne deux entiers et retourne le résultat.
	*
	* @param a Le premier entier.
	* @param b Le second entier.
	* @return La somme des deux entiers.
	*/
   public int add(int a, int b) {
	   return a + b;
   }
}
```

![[Structure d'un Commentaire Javadoc]]