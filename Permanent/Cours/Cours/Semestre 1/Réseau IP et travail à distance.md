---
MOOC: "[[Cours]]"
Ressource: "R1.04 : Introduction aux systèmes d'exploitation\ret à leur fonctionnement"
Cours: "Cours 6 : Réseau IP et travail à distance"
Date: 2023-10-16
tags: 
Complete: true
Learned: true
---
# Introduction

Dans l'univers des réseaux informatiques, les objectifs et les utilités sont variés, englobant des aspects essentiels pour le fonctionnement des systèmes d'exploitation modernes. Les réseaux jouent un rôle central dans la centralisation et le partage de ressources, notamment le stockage, les sauvegardes, les imprimantes, la puissance de calcul (CPU et RAM) permettant une utilisation à distance, la maintenance et le support technique, entre autres. De plus, ils offrent un accès à Internet, qui englobe des fonctionnalités telles que la messagerie électronique, la navigation sur le Web et la prise en charge d'applications client/serveur, y compris les bases de données.

# Environnement réseau de l'IUT2

Au sein de l'IUT2 (Institut Universitaire de Technologie 2), un environnement réseau spécifique est en place pour répondre aux besoins éducatifs et opérationnels.

# Adresses et ports dans les réseaux IP
Il est nécessaire à un PC de [[L'utilité des adresses IP|détenir une adresse IP]] afin de se connecter à Internet. Les adresse IPv4 étant épuisées, nous sommes passés aux adresses IPv6.
Il est tout à fait possible de créer une [[Les adresses privées]] pour pouvoir bénéficier de plus d'appareils que d'adresses IP publique utilisées. Cependant, il faut un mécanisme de traduction d'adresse pour assurer une connexion à Internet et assurer l'utilisation des application réseaux
Il existe de nombreux moyens pour [[La configuration d'une adresse|configurer une adresse]], notamment le DHCP, uti
§;nw>lisés par la majorité
Enfin, quand on utilise des logiciels serveurs, il est nécessaire de prendre en compte [[La notion de ports réseaux]].

# Travail à distance

Le travail à distance se décline en deux formes principales : l'utilisation de machines distantes et le transfert de fichiers.

Il est important de noter que les serveurs de transit ont une capacité limitée et ne peuvent pas prendre en charge un grand nombre d'étudiants simultanément. De plus, leur disponibilité n'est pas garantie, donc il est recommandé de ne les utiliser que de manière ponctuelle. Les périodes de forte activité, telles que les veilles de rendu de projets, nécessitent une certaine prudence, car il vaut mieux travailler sur sa propre machine dans ces cas.

# Utilisation de machines à distance

L'utilisation de machines à distance repose sur divers protocoles, en fonction du mode d'accès choisi.

## [[Utiliser une machine à distance en mode texte|Mode texte]]


    

## Mode graphique

Dans le mode graphique, plusieurs options sont disponibles, notamment :

- **X11** : X11 est un système graphique client-serveur où un serveur X11 tourne sur la machine locale de l'utilisateur, tandis que les applications clientes s'exécutent sur la machine distante. Cependant, cette fonctionnalité est désactivée par défaut sous Linux en raison de préoccupations de sécurité.
    
- **VNC** : VNC permet à un pseudo-serveur graphique de s'exécuter sur la machine distante, tandis que l'utilisateur utilise un client VNC sur sa machine locale pour interagir avec le bureau distant. Bien que VNC offre moins de latence que X11, il peut utiliser davantage de bande passante.
    
- **X2Go** : X2Go est une alternative plus simple aux protocoles précédents, utilisant une connexion SSH unique et ne nécessitant qu'une seule authentification. Il est compatible avec Linux, macOS, et peut être utilisé aussi bien à l'IUT2 qu'à l'extérieur. Cependant, il peut présenter une légère latence par rapport à VNC et ne prend pas en charge l'exécution de l'environnement Plasma.
    

En conclusion, les réseaux informatiques offrent des fonctionnalités essentielles, des adresses IP aux ports, en passant par des protocoles variés pour le travail à distance. Ces éléments sont cruciaux pour garantir la connectivité, la sécurité et la gestion des ressources à l'échelle mondiale.