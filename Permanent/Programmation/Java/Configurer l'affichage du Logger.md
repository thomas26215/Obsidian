---
MOOC: "[[Programmation]]"
Langage: Java
Type: Logger
tags:
---
Il est possible de modifier l'affiche du log en mettant un message personnalisé. Voici un exemple de code qui permet de modifier le message du Log :
```java
// Configuration du logger
static {
	System.setProperty("java.util.logging.SimpleFormatter.format", "[%1$s] %4$-10s | (%3$s) %2$-15s | %5$s\n");
}
```
1. La date de production du log
2. La source si elle est connue ou bien le nom du logger
3. Nom du logger
4. Niveau du log
5. Message du log
6. L'exception associée si elle est spécifiée