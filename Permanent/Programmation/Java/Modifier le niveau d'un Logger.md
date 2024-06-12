---
MOOC: "[[Programmation]]"
Langage: Java
Type: Logger
tags:
---
Il est possible de modifier le niveau d'un logger pour qu'il ne puisse afficher que des logs de niveau supérieurs (Fiche sur le niveau des logs). Voici le moyen de le faire :
```java
static{
	LOGGER.setLevel(Level.WARNING);
}
```
On peut le définir à plusieurs niveaux : `OFF`, `SEVERE`, `WARNING`, `INFO`, `ONFIG`, `FINE`, `FINER`; `FINEST`, `ALL`