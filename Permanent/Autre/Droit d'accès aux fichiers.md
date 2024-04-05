---
MOOC: "[[Autre]]"
Sujet: Systèmes d'exploitation
Type: 
tags:
---
Le droit d'accès aux fichiers détermine qui peut consulter, modifier ou exécuter un fichier. Il comprend les informations suivantes :

- **Nom** : Le nom du fichier.
- **Type** : Le type du fichier (par exemple, répertoire, fichier, lien symbolique).
- **Taille** : La taille du fichier en octets.
- **Date** : La date de création ou de dernière modification du fichier.
- **Propriétaire (UID)** : L'utilisateur qui a créé le fichier.
- **Groupe (GID)** : Le groupe d'utilisateurs auquel le fichier appartient.
- **Permission / Droits d'accès** : Les autorisations qui déterminent qui peut lire, écrire ou exécuter le fichier.

Pour afficher ces informations, la commande `ls -l` est utilisée. Par exemple, le résultat de cette commande affiche les permissions, le propriétaire du fichier, le groupe de fichiers, etc.

**Exemple :**
```bash
toto@transit:~$ ls -l /users/info/pub/1a/R1.04/tp-fichiers/ total 80 
-rw-r--r-- 1 bonnaudl info 14859 Sep 9 2013 Avare.txt drwxr-xr-x 2 bonnaudl info 4096 Oct 11 19:42 dossier 
-rw-r--r-- 1 bonnaudl info 413 Sep 30 11:29 Essai.class 
-rw-r--r-- 1 bonnaudl info 131 Sep 30 11:27 Essai.java 
-rwxr-xr-x 1 bonnaudl info 17 Oct 25 11:25 essai-script 
-rw-r--r-- 1 bonnaudl info 430 Oct 8 13:25 Prg.class 
-rw-r--r-- 1 bonnaudl info 153 Oct 3 13:13 Prg.java 
-rw-r--r-- 1 bonnaudl info 282 Oct 3 13:11 Proverbes.txt
```

Il existe de nombreuses [[Permissions et droits d'accès]]