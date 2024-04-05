---
MOOC: "[[Cours]]"
Ressource: "R1.04 : Introduction aux systèmes d'exploitation\ret à leur fonctionnement"
Cours: SAE 1.03
Date: 
tags: 
Complete: false
Learned: false
---
**Logiciels libres** : Concept introduit par Richards Stallman au début des années 1980
4 libertés fondamentales : Liberté d'exécuter le logiciel, pour tous usages, liberté d'étudier (code source), liberté de redistribuer le logiciel (+ le vendre) et liberté d'améliorer le logiciel et de publier ses améliorations.
Libre != gratuit
Libre s'oppose à propriétaire et à logiciel privateur

# Installer Linux
**Pdt la SAE :**
- Sur machine virtuelle
- Distribution Debian

**Sur machine personnelle :**
- Distribution Ubuntu conseillée
- Installation Linux utile pour mieux apprendre à utiliser Linux

On peut changer d'OS sur une machine
On apprend beaucoup de choses en installant un OS :
- sur matériel informatique
- sur fonctionnement OS
- ...
On maîtrise ce qui se passe sur sa machine quand on utilise Linux
On a accès à de très nombreux logiciels faciles à utiliser


**Utilisation sudo** : 
- `sudo COMMANDE_AVEC_PRIVILEGES_ROOT`
**Pour suite de commande** :
- lancer un shell `root` : `sudo -i`
- Tous privilèges lancés depuis ce shell auront privilèges `root`
>**Ma commande ne fonctionne pas : ne pas taper `sudo`**, souvent erreur d'utilisateur

 **Mise à jour de sécurité :**
- Sur page principale du site Web `debian.org`
- Sur liste de messagerie `debian-security-announce`
**Peuvent se faire :**
- Automatiuement
- Par trois commandes :
	- `#apt update`
	- `#apt upgrade`
	- `#apt clean`
**Découverte + installation package :**
- Site Debian ou Ubuntu
- `apt search`
- `apt-cache search`
- Commande d'installation : `#apt install NOM-PACKAGE`
- **Exemple :**
  `$ psql`
  ⇒ `not found, but can be installed with ...`
  
# Installation d'outils de développement

## Méthodes de distribution des logiciels
- Magasain dintégré à une distribution linux
- Site web des dév ou de l'éditeur
- Magasin Snap
- Magasin flatpak

Sous forme de code source (archive ou dépot git)  ou sous forme de code exécutable (ou binaire) ⇒ Installateur (attention aux scripts qui *en mettent partout*), archive, package Debian/Ubuntu à installer à la main, ou installation et maj automatique dans avec `apt` si dans un dépot de package, ou enfin en format AppImage

2 magasins : `snap` ou `flatpak`. Fonctionnent sur toutes distributions Linux. Application embarquant leurs propre dépendance. Tournent souvent sur `sandbox` (sécurité +). Occupent cependant + d'espace disque

Emplacement : (`bin` ou `lib` pour la plupart (installés avec **Debian**), `local` pour **Admin**) ⇒ Tout dans dossier `usr`, `snap` ou `flatpak` présents dans `lib`

# Installation à partir d'un archive
ZIP, TAR, 7ZIP + extraction avec gestionnaire de fichiers (Dolphin), unzip et tar (cf [[Espace disque, archivage]])
Emplcaement d'installation : `usr/local/logiciel-x.i` 
Archives contiennent un script de lancement. Lancer en tapant chemin absolu ou on peut créer un lien symbolique (cf [[Droits d'accès, liens symboliques, scripts, compléments de shell]])
Pour installer un nvlle version : Autre répertoire à côté du premier + autre lien symbolique de lancement (changer numéro de version)
Pour désinstaller, supprimer répertoire + lien symbolique

# Snap et flatpak
Une distribution linux n'inclue pas tous logiciels existants. Aussi, un package X ne peut pas être installé sur une distribution Y
Prblms de compatibilité d'un logiciel avec plusieurs distributions
- Langage comme Java, Python : pas trop de prblms
- Langage comme C, C++ : pblms compatibilité binaire avec biblios système
- Démonstrations avec `ldd :ls, cp, evince`
Un éditeur qui veut diffuser un logiciel pour Linux doit le faire pour plusieurs distributions, pour chaque vesion et inclure biblios utilisées dans 

