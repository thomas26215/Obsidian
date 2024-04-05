---
MOOC: "[[Cours]]"
Ressource: "R1.04 : Introduction aux systèmes d'exploitation\ret à leur fonctionnement"
Cours: Fichier des commandes
Date: 2023-11-04
tags: 
Complete: true
Learned: true
---
# Cours 1

Racine = `/`
Répertoire parent = `..`
Homedir = `~`
Répertoire courant = `.`
Répertoire absolu commence par `/`
Répertoire relatif commence par `.`

`pwd` = logiciel affichant répertoire courant
`echo ~` = Réaliser une affichage en shell (echo("coucou"))
touche FICHIER = Créer un fichier
cat FICHIER = Afficher un fichier dans le shell
rm FICHIER = Supprimer un fichier
cp FICHIER = Copier un fichier
mv FICHIER = Déplacer un fichier
mv ANCIER_NOM NOUVEAU_NOM = Renommer un fichier
ls = afficher le répertoire courant
ls -l = afficher le répertoire courant de façon détaillée
LS != ls
mkdir DOSSIER = Créer un dossier
rmdir DOSSIER = Supprimer un dossier
cd DOSSIER = Se déplacer dans un autre dossier
cp DOSSIER = Copier un dossier
mv SOURCE DESTINATION = Déplacer un dossier
mv ANCIER_DOSSIER NOUVEAU_DOSSIER = Renommer un dossier
history = Historique des commandes effectuées
tab = complétion automatique

Ctrl+c = Interruption de la commande
Lancement de base = en avant plan
kcalk & = lancement en arrière plan

man LOGICIEL = documentation en ligne
man-fr LOGICIEL = documentation en ligne en français
q = quitter le manuel

javac PROGRAMME.java = Compilation d'un programme
java PROGRAMME = compilation du programme compilé (Un nouveau fichier aura été crée)

# Cours 2 : Joker, Processus, Alias du shell, Fichiers cachés
## Joker
`*` = Remplace une suite quelconque de charactères, y compris vide
`[]` = Remplace un unique charactère parmis ceux présents entre les crochets
`?` = Remplace un unique charactère, n'importe lequel

`pstree -u` = Afficher arbres des processus, avec noms de propriétaire.
`ps -ef` = Affiche les  processus sous liste
`ps aux` = Affichage similaire mais avec d'autres attributs
`ps -f -u NOM_LOGIN` = visualiser uniquement ses processus
`top` = 
`plasma-systemmonitor` = Vue graphique des processus (Sélectionner "All processor, Tree")


## Processus
`Ctrl+C` = Arrêter un processus
`Ctrl+Z` = Suspendre un processus (pour taper une nouvelle commande)
`bg` = Met en background (après Ctrl+Z)
`fg` = Met au premier plan
`kill` = tuer un processus

## Alias
alias `RACCOURCI="CHAÎNE QUI SERA SUBSITUEE POUR LE RACCOURCI"` = Définir des raccourcis
Fichier `.bash_aliases` = Alias permanents
`rm -i` = Demande confirmation pour supprimer un fichier

## Questions diverses
`ls -a` = Afficher fichiers cachés
`less FICHIER` = Visualiser le contenu d'un fichier de manière très efficace


# Cours 3 : Redirections, filtres, recherches
## Flux
Flux entrée standard = entrée (clavier) = 0
Flux sortie standard = sortie (écran) = 1
Flux erreur standard = erreur = 2

## Redirection
`COMMANDE > FICHIER` = Met dans le fichier ce qu'affiche la commande
`COMMANDE < FICHIER` = Prend les entrées d'un fichier pour les mettre sur la commande
`COMMANDE1 | COMMANDE2` = On effectue la première commande, et on effectue la deuxième commande sur la première avant affichage (`grep` = compter nb lignes, `wc` Compter nombre d'entrée / charactères)
`sort` = Trier par ordre alphabétique
`grep` = Ne garde que les lignes contenant chaîne de charactères spécifiée
`grep -r` = Chercher récursivement
`wc` = Afficher nombre de lignes affichées
`head` = Affiche n premières lignes
`tail` = Affiche n dernières lignes
`cut -cSELECTION_COLONNES` = Affiche la colonne spécifiée pour chaque ligne
1. `cut -5 fichier` : Affiche le 5e caractère de chaque ligne du fichie
	1. `cut -5-10 fichier`, Affiche du 5e au dixieme caractère
	2. `-cut -5,10 fichier` : Affiche le 5e et le 10e caractère
	3. `-cut c5- fichier` Affiche à partir du 5e
`cut -dSEPARATEUR -f SELECTION_CHAMPS` = délimitateur (<mark style="background: #FF5582A6;">à revoir dans TP</mark>)
`uniq` = Elimine doublons
`getent passwd` = Affiche une liste des utilisateurs connus du système. Chaque ligne contient des infos relatives  à un utilisateur

**Utilisation `grep` :**
`grep [OPTION] CHAÎNE [FICHIER...]`

| OPTION | Utilisation                                                       |
| ------ | ----------------------------------------------------------------- |
| -l     | Donne seulement le nom des fichiers où le critère a été trouvé    |
| -c     | Donne seulement le nombre de lisnes trouvées obéissant au critère |
| -v     | Donne les lignes où le critère n'a pas été trouvé                 |
| -i     | Ne pas tenir compte de la casse                                   |
| -n     | Pour n'affiche que les numéros des lignes trouvées                |
| -w     | Pour imposer que le motif corresponde à un mot entier d'une ligne |                                                           |

## Recherche de fichiers
`man -k CHAINE` = Recherche parmis la chaîne
`locate NOM` = Recherche où se situe un fichier, dont on connaît un partie ou intégralement le nom

# Cours 4 : Espace disque, Quotas, Archivages
## Espace disque
`lsqblk` = Lister périphériques de stockage et partitions
`df -h` = Connaître espace total
`duf` = comme df, mais présentation améliorée
`quota` = Voire quota de la machine + espace utilisé, disponible
`du -h [ENTREE]` = Affichage espace disque d'un répertoire + donne détail des sous-répertoires
`ncdu` = Logiciel amélioré de `du` mais trie répertoires par taille + naviguer dans arborescence des répertoires
`qdirstat .` = Logiciel graphique pour espace occupé (Treemap)

`*~` = Fichiers backup

## Archivage (à faire)
`zip -r9 R1.01.zip R1.01` = Archiver sous format zip
`tar --gzip -cvf R1.01.tar.gz R1.01` = Archive sous format TAR+GZIP 
`tar --bzip2 -cvf R1.01.tar.bz2 R1.01` = Archive sous format TAR+BZIP2
`tar --xz -cvf R1.01.tar.xz R1.01` = Archie sous format TAR+XZ
`tar --zstd -cvf R1.01.tar.zst R1.01` = Archive sous format TAR+ZSTD
`7z a R1.01.7z R1.01`

**Restauration d'un répertoire :**
`unzip ~/R1.01.zip` = Pour zip
Différents formats de TAR :
`tar --gzip -xvf ~/R1.01.tar.gz`
`tar --bzip2 -xvf ~/R1.01.tar.bz2`
`tar --xz -xvf ~/R1.01.tar.xz`
`tar --zstd -xvf ~/R1.01.tar.zst`

7zip : `7z x ~/R1.01.7z`

**Verification de l'intégralité d'une archive** :
`zip -T R1.01.zip`
`gzip -t R1.01.tar.gz`
`bzip2 -t R1.01.tar.bz2`
`xz -t R1.01.tar.xz`
`zstd -t R1.01.tar.zst`
`7z t R1.01.7z`

⇒ `okteta` = Modifier des octets contenus dans un fichier en mode héxadécimale

# Cours 5 : Permissions Unix, Scripts shell, Liens symboliques
## Droits d'accès aux fichiers
`chmod [-R] [QUI] + | - PERM ENTREE` = Changer droit d'accès
⇒ `u`, `g`, `o` pour `QUI` et `r`, `w`, `x` pour `PERM` + `-R` = Récursivité (pour tous les dossiers) et `+|-` pour ajout ou supp permission

## Scripts shell
`PATH` = Variable d'environnement la plus connue
`variable="valeur"` = Association de la valeur à la variable
`#!/bin/bash` = Savoir que c'est un script
`echo "Ca marche !"` = Affiche *Ca marche !*
`$1, $2` ... = Variables passées dans le script par le shell
`./exemple-script variable1 variable 2` = Appel d'un script dans le shell avec en variables `variable1` et `variable 2` pour les variables `$1` et `$2` qui prendront successivement ces valeurs
`export VARIABLE` = Variable d'environnement
`shellcheck` = Vérifier qu'un script est écrit correctement
`ln -s LIEN NOUVELLE_COMMANDE` = Créer un lien symbolique

# Cours 6 : Connexion à distance
## Depuis une machine de l'IUT
### Par SSH
`ssh NOM_DE_LOGIN@pc-dg-xxx-yy` = Connexion à un pc via SSH
Attention, si lancement d'un logiciel Linux sur Windows, ne marchera pas !
`micro FICHIER` = Modifier un fichier directement sur le shell sans logiciel

### Client VNC
1. Télécharger exécutable `vncviewer64-x.y.exe`
2. Lancer client VNC puis taper `pc-dg-xxx-yy` puis bouton Connect
Ensuite, client normal

### X2Go
Lancer client X2Go puis nvlle session avec paramètres :
- HOST : pc-dg-xxx-yy
- Login : VOTRE_NOM_LOGIN
- Session Type : MATE
## Depuis sa machine
### Avec un shell
`ssh NOM_DE_LOGIN@transit.iut2.univ-grenoble-alpes.fr` = Lancer + étapes précédantes de shell pour se connecter

### Avec VNC graphique serveur transit
Installer TigerVNC
`ssh -f -N -L 5900:localhost:5900 NOM_DE_LOGIN@transit.iut2.univ-grenoble-alpes.fr`

<mark style="background: #FF5582A6;">A COMPLETER</mark>
## Linux
