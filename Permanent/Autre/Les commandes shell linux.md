---
MOOC: "[[Autre]]"
Thème: Systèmes d'exploitation
Sujet:
tags: []
---

Un shell est un interpréteur qui réalise une interface entre l'utilisateur et le système d'exploitation permettant de gérer le système de fichiers, de lancer des processus .. C'est aussi un langage de programmation qui permet d'écrire des programmes plus ou moins complexes allant de l'enchaînement automatiques de commandes sous linux à de véritables programmes structurés

[[L'arborescence linux standard]]

**Commandes** :

- `ls` : Liste le contenu du répertoire courant
  ⇒ Peut aussi liste contenu d'un autre répertoire : `ls ./R1.04`
- `ls -l` : Liste de manière détaillée le répertoire courant
- `pwd` : affiche le nom absolu du répertoire courant
- `history` : Affiche l'historique des commandes
- `mkdir nom_dossier` : Créer un dossier
- `rmdir nom_dossier` : Supprime un dossier
- `cd nom` : Déplace répertoire courant vers celui spécifié
- `cp -r dossier fichier dossier` : Permet de copier un fichier du dossier 1 vers le dossier 2
- `mv FICHIER DOSSIER` : Déplace un le fichier vers le dossier
- `rm nom_fichier` : Supprimer un fichier
- `rm -r ENTREE` : Supprime répertoires et fichiers avec tout leurs contenu
- `cat fichier` : Lire le fichier dans la console
- `cat ma-liste*` : Concaténer tous les fichiers en un seul
- `echo ~` : Permet de réaliser un affichage
- Il est possible de lancer un logiciel depuis la commande : Il suffit de taper son nom en minuscule
- `date` : Affiche la date et l'heure
- `man LOGICIEL` : Affiche le manuel du logiciel passé en paramètres
- Pour pouvoir arrêter une commande qui a été lancée depuis le shell, il faut faire Ctrl + C
- Pour pouvoir effacer l'écran, il faut faire Ctrl + l
    > **Sensible à la casse. Minuscule et majuscule != même** > **Il y a aussi de l'autocomplétion**

La composition d'une commande : Logiciel → Espace → Eventuels arguments → Caractère de fin de ligne
**Exemple de commande** :
ls (logiciel) → -l (argument a) → -a (argument 2)

- **ls** : liste les fichiers
- **-l** : en format long
- **-a** : y compris les fichiers cachés
- Pas d'autres arguments : Liste le répertoire courant
