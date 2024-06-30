---
MOOC: "[[Programmation]]"
Langage: Java
Type: Commentaires
tags:
---
```java
/**
 * Classe Exemple pour démontrer les commentaires Java et Javadoc.
 * Cette classe contient des exemples de commentaires de différentes sortes.
 */
public class ExampleClass {

    // Champ d'exemple
    private int value;

    /**
     * Constructeur de la classe ExampleClass.
     *
     * @param value La valeur initiale à attribuer au champ.
     */
    public ExampleClass(int value) {
        this.value = value;
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

    /**
     * Méthode principale qui sert de point d'entrée pour l'application.
     *
     * @param args Les arguments de ligne de commande.
     */
    public static void main(String[] args) {
        // Création d'une instance de ExampleClass
        ExampleClass example = new ExampleClass(10);

        // Appel de la méthode add et affichage du résultat
        System.out.println("Addition de 5 et 3 : " + example.add(5, 3));
    }
}
```

En utilisant ces structures de commentaires et Javadoc, vous pouvez non seulement rendre votre code plus lisible mais aussi générer automatiquement de la documentation à l'aide de l'outil Javadoc.