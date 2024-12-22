---
MOOC: "[[Autre]]"
Thème: Systèmes d'exploitation
Sujet:
tags:
---

- **Entrée** : un fichier ou un répertoire du SF (Système de fichiers)
- **Répertoire racine** : Le répertoire `/`
- **Répertoire père** : Le répertoire auquel cette entrée appartient. Chaque entrée à un répertoire père hormis racine. Dans la commande shell, on peut y accéder par `..`
- **Répertoire personnel** d'un utilisateur : Le répertoire qui lui est réservé pour stocker ses données. Dans un shell, on peut désigner celui-ci par `~`
- **Répertoire courant** : Celui dans lequel on est actuellement. Dans le shell, on le désigne par `.`. Par défaut, c'est le répertoire personnel

Quand on construit un chemin, on énumère la liste des répertoires qu'il faut traverser au sein du SF et il y a deux points de départs possible :

- `/` : Chemin absolu. On part du répertoire racine
- `.` : Chemin relatif. On part du répertoire courant
  Les différents répertoires qui séparent sont énumérés, séparés par `/`
