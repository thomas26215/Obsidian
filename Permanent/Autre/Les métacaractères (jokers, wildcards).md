---
MOOC: "[[Autre]]"
Sujet: Systèmes d'exploitation
Type: 
tags:
  - status_finish
  - note_permanent
---
Ils permettent de manipuler plusieurs entrées avec une seule commande
**Les jokers** :
- `cp -r tp* /media/tot/MaCle/` : Prend tous les répertoires qui commencent par tp dans le répertoire MaCle
- `cp -r tp* /media/tot/MaCle/` : Prend tous les fichiers qui commencent par tp et qui a un charactère en plus (tp1, tp2)
- `cp -r tp[12] /media/tot/MaCle/` : Récupère les deux premiers tp

- * Remplace une suite quelconque
- ? Remplace un seul charactère
- [] Remplace un charactère parmis ceux présents dans les charactères

Un joker peut être utilisé au début, au milieu d'un chemin ou tout seul

> Le tilde `~` n'a pas la même utilisation en fonction de son emplacement : Au début, c'est le homedir, autre, c'est un caractère normal

- **Copier tous les fichiers finissant par txt** : `cp *.txt essai*`
- **La même commande peut donner un résultat très différent** : `cp * .txt essai*`
- **Commande pour supprimer les fichiers de backup** : `rm *~`
- **La même commande avec espace** : `rm * ~` <mark style="background: #FF5582A6;">NE PAS TAPER CETTE COMMANDE, CATASTROPHIQUE</mark>