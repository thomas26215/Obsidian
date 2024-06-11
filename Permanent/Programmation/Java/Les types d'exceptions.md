---
MOOC: "[[Programmation]]"
Langage: Java
Type: Exceptions
tags:
---
**2 grandes catégories d'exceptions :**
- **Checked exceptions** : Exceptions devant être déclarées dans la signature d'une méthode avec le mot-clé `throws` si elles ne sont pas gérées à l'intérieur de la méthode.
	Elles sont vérifiées au moment de la compilation
	- *Exemple :* `IOException` ou `SQLException`
- **Unchecked exceptions** : Exceptions n'étant pas obligées d'être déclarées ou gérées. Dérivées de la classe `Runtime Exception` et vérifiées au moment de l'éxecution.
	- *Exemple* `NullPointerException`, `ArrayIndexOutOfBoundsExceptions`

Se référer au fichier [[La hiérarchie des exceptions]]