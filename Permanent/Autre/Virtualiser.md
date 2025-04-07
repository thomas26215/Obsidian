---
MOOC: "[[Autre]]"
Thème: Réseaux informatiques
Sujet: Virtualisation
tags:
  - définition
Complete: false
Learned: false
---
Virtualiser est le fait de transformer des ressources matérielles en ressources logiques qui sont plus faciles à gérer
**Exemple** :
- Installer un 2e OS dans une machine virtuelle
- Plus simple que d'installer 2 OS sur une machine physique
- Plus simple car l'OS virtualisé est stocké dans une image disque et pas besoin de partitionner le stockage du poste
- Plus pratique car on peut faire tourner les 2 OS simultanéments

Le [[Processeur]] fait déjà de la virtualisation : il est partagé entre les différentes applications (time-sharing, round-robing)
[[Utilisation de la RAM comme cache|RAM]] aussi virtualisée : chaque processus voit un espace mémoire virtuel, plus grand que espace mémoire physique
Lo stockage aussi : il est partagé entre les diffs applications installées et les fichiers peuvent être vus comme une abstraction logique des secteurs physiques du disque [[SGF - Arborescence et système de fichiers|SGF]]