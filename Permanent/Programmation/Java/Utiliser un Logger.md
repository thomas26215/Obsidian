---
MOOC: "[[Programmation]]"
Langage: Java
Type: Logger
tags:
---
Pour utiliser un logger, il faut spécifier le niveau de log suivit du message. Il existe plusieurs niveau de log :
- `SEVERE` (Plus haute valeur)
- `WARNING`
- `INFO`
- `CONFIG`
- `FINE`
- `FINER`
- `FINEST` (Plus petite valeur)

Voici comment l'utiliser :
```java
public static void main(String[] args){
		Logger.log(Level.INFO, "This is an info message");
	}
```