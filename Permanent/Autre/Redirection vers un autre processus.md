---
MOOC: "[[Autre]]"
Sujet: Systèmes d'exploitation
Type: 
tags:
  - status_finish
  - note_permanent
---
Il est possible d'utiliser une commande qui agit sur une autre commande, de la même manière qu'en SQL avec les sous-requêtes. Ce processus s'appelle un tube qui est une redirection vers un autre processus et la forme générale est `COMMANDE1 | COMMANDE2`. Ainsi, la commande 1 ne sera pas directement affichée mais sera soumise aux contraintes de la commande 2
**Par exemple**, si je souhaite afficher le nombre d'éléments de mon répertoire courant, il faut que je fasse la commande `ls -l . | wx`. En effet, la commande `ls -l` me permet d'afficher les éléments de mon répertoire courant. Cependant, elle est redirigée vers le processus `wc`, qui lui va compter les éléments.

**Autre exemple** : `cat ma-liste-de-films | sort`
**Forme plus courte** : `sort ma-liste-de-films`
**Combinaison avec redirection** : `cat ma-liste-de-films | sort > ma-liste-de-films-triées`

Voici les filtres les plus courants :
- `sort` : Permet de trier par ordre alphabétique
- `greps, head, tail` : Extraire des lignes
- `cut` : Extraire des colonnes
- `wc` : Compter