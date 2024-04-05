---
MOOC: "[[Autre]]"
Sujet: Systèmes d'exploitation
Type: 
tags:
---
Les droits d'accès aux fichiers se divisent en trois catégories d'utilisateurs :

- **u (user)** : Désigne la personne qui a créé le fichier ou le répertoire.
- **g (group)** : Les membres du groupe d'utilisateurs auquel le fichier appartient.
- **o (others)** : Les autres utilisateurs.

Pour chaque catégorie d'utilisateur, il y a trois types de permissions :

- **r (read)** : Autorise la lecture du fichier.
- **w (write)** : Autorise l'écriture dans le fichier.
- **x (execute)** : Autorise l'exécution du fichier (pour les fichiers exécutables) ou la traversée du répertoire.

En combinant ces catégories d'utilisateurs et ces types de permissions, on obtient un total de 9 autorisations possibles pour chaque entrée (fichier ou répertoire).

Pour changer les combinaisons, il existe le logiciel `chmod`.
⇒ `chmod [-R] [QUI] + | - PERM ENTREE`
- `QUI`
	- A qui s'applique le changement de permissions
	- Chaîne fabriquée avec les caractères `u` `g` `o` (ou chaîne vidéo)
- `PERM`
	- Quelle permission on veut ajouter ou enlever
	- Chaîne fabriquée avec les caractères `r` `w` `x` `X`

**Exemples pour un fichier** :
- `chmod g+r f1` : Autorise les membres du groupe de `f1`
- `chmod o-w f1` : Interdit aux autre d'écrire dans `f1`
- `chmod go-rwx` : Interdit aux non-propriétaires tous les accès à `f1`