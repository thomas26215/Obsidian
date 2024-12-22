---
MOOC: "[[Autre]]"
Thème: Systèmes d'exploitation
Sujet:
tags:
---

Pour pouvoir utiliser une variable dans le shell en demandant la variable à l'utilisateur, il faut utiliser une notation particulière. En effet, il faut utiliser les noms de variable `$1`, `$2`, ..., `$9`. Les paramètres sont passés au script depuis la ligne de commande du script vers les variables.

**Exemple :**

```Shell
#! /bin/bash
rm "$1.class" "$1.java"
```

Commande utilisée : `$ ./menage-java toto`

A l'exécution, le shell remplace `$1` par `toto` :
⇒ `rm toto.class toto.java`

