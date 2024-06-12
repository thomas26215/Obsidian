Les commentaires en Java peuvent être de trois types principaux : les commentaires sur une seule ligne, les commentaires multi-lignes et les commentaires Javadoc. Voici un aperçu de la structure de chacun de ces types :

### Commentaires en Java

1. **Commentaires sur une seule ligne**:
   - Utilisez `//` pour les commentaires sur une seule ligne.
   ```java
   // Ceci est un commentaire sur une seule ligne
   int x = 5; // Commentaire à côté du code
   ```

2. **Commentaires multi-lignes**:
   - Utilisez `/* */` pour les commentaires qui s'étendent sur plusieurs lignes.
   ```java
   /*
    * Ceci est un commentaire multi-lignes.
    * Il peut s'étendre sur plusieurs lignes.
    */
   int y = 10;
   ```

3. **Commentaires Javadoc**:
   - Utilisez `/** */` pour les commentaires Javadoc, qui sont utilisés pour générer de la documentation.
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

### Structure d'un Commentaire Javadoc

1. **Description de la Classe ou de la Méthode**:
   - La première ligne ou le premier paragraphe d'un commentaire Javadoc décrit l'objectif ou la fonctionnalité de la classe ou de la méthode.
   ```java
   /**
    * Cette classe représente un exemple de classe.
    * Elle contient une méthode principale.
    */
   ```

2. **Description des Paramètres (`@param`)**:
   - Pour documenter les paramètres d'une méthode, utilisez la balise `@param`.
   ```java
   /**
    * Additionne deux entiers et retourne le résultat.
    *
    * @param a Le premier entier.
    * @param b Le second entier.
    * @return La somme des deux entiers.
    */
   ```

3. **Description de la Valeur de Retour (`@return`)**:
   - Pour documenter ce que la méthode retourne, utilisez la balise `@return`.
   ```java
   /**
    * @return La somme des deux entiers.
    */
   ```

4. **Autres Balises Utilisées dans les Commentaires Javadoc**:
   - `@throws` ou `@exception`: Pour documenter les exceptions lancées par la méthode.
   - `@see`: Pour référencer d'autres méthodes ou classes.
   - `@since`: Pour indiquer depuis quelle version la classe ou méthode existe.
   - `@deprecated`: Pour marquer une classe ou méthode comme dépréciée.

### Exemple Complet de Commentaires en Java

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