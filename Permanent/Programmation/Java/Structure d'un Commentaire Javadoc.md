---
MOOC: "[[Programmation]]"
Langage: Java
Type: Commentaires
tags:
---
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

![[Exemple complet de commentaires JavaDoc]]