---
MOOC: "[[Programmation]]"
Langage: Java
Type: Exceptions
tags:
---
Toutes les exceptions dérivent le la classe `java.lang.Throwable`. Voici la hiérarchie des exceptions :

```
java.lang.Object
	└── java.lang.Throwable
		├── java.lang.Error
		└── java.lang.Exception
			├── java.lang.RuntimeException
			└── (autres exceptions vérifiées)
```

- `Throwable` : Classe de base pour tous les objets qui peuvent être "lancés" (thrown) comme exceptions.
- `Exception` : Superclasse des exceptions qui peuvent être attrapées et gérées.
- `Error` : Indique des problèmes sérieux qui ne devraient normalement pas être attrapés (ex : `OutOfMemoryError`).