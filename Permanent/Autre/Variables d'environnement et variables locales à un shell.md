---
MOOC: "[[Autre]]"
Thème: Systèmes d'exploitation
Sujet:
tags:
---

Les variables d'environnement sont disponibles pour tous les processus et sont transmises d'un processus parent à ses enfants. Elles ont généralement des noms en majuscules et peuvent modifier le comportement de certains logiciels.

Les variables locales à un shell sont définies uniquement pour ce processus shell particulier, et ses processus enfants n'en héritent pas. Elles ont généralement des noms en minuscules.

Pour transformer une variable locale en une variable d'environnement, vous pouvez utiliser la commande `export NOM_DE_VARIABLE`.

Pour définir directement une variable d'environnement, utilisez `export NOM_DE_VARIABLE=VALEUR`.

La commande shell pour lister toutes les variables est la variable `env`

L'une des variables d'environnement les plus courantes est `PATH`, qui spécifie les répertoires où le shell recherche les programmes ou scripts à exécuter.

Il faut savoir qu'un variable n'a pas besoin d'être déclarée contrairement à [[Les variables en Java|Java]]. D'ailleurs, le type de la variable est interprétée selon son contexte, comme en Python. Ainsi, la déclaration / affectation d'un variable se fait sous cette forme : `fichier="/tmp/toto"`. Attention, il ne doit pas y a avoir d'espace entre le nom de la variable et la valeur. Enfin, l'utilisation d'un variable est constamment d'un `$`

**Exemple de script contenant des variables** :

```shell
#! /bin/bash
variable="toto"
echo "la variable est $variable"
```

⇒ **Résultat :** `la variable est toto`

Il est tout à fait possible d'[[Fournir une variable à un script shell|appeler des variables directement lors de l'appel du script]] dans le shell

