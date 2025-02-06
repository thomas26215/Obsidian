# Contexte

Enseignements précédants concernant la virtualisation
- SAE S1.03
- SAE S2.03
- SAE S3.03


# Introduction
Virtualiser = Transformer ressources matérielles en ressources logiques plus faciles à gérer
**Exemple** :
- Installer un 2e OS dans une machine virtuelle
- Plus simple que d'installer 2 OS sur une machine physique
- Plus simple car l'OS virtualisé est stocké dans une image disque et pas besoin de partitionner le stockage du poste
- Plus pratique car on peut faire tourner les 2 OS simultanéments

Le CPU fait déjà de la virtualisation : il est partagé entre les différentes applications (time-sharing, round-robing)
[[Utilisation de la RAM comme cache|RAM]] aussi virtualisée : chaque processus voit un espace mémoire virtuel, plus grand que espace mémoire physique
Lo stockage aussi : il est partagé entre les diffs applications installées et les fichiers peuvent être vus comme une abstraction logique des secteurs physiques du disque [[SGF - Arborescence et système de fichiers|SGF]]

Machines virtuelles tournent grâce à superviseur
- Virtualisation de serveur
- Virtualisation de poste de travail

## Virtualisation de stockage
Diffs types de stockage :
- DAS (Direct Attached Storage) : disque dur interne (SATA, NVMe, ...)
- SAN (Storage Area Network) : réseau de stockage. Mis à disposition sous forme de blocs (iSCSI, Fibre Channel)
- NAS (Network Attached Storage) : stockage en réseau. Mis à disposition sous forme de fichiers (NFS, SMB)

Virtualisation de stockage dans un OS classique
- Exemple 1 : Linux et LVM2. Volumes physiques (DAS) sont regroupés en groupes de volumes, puis en volumes logiques. Ces volumes logiques sont ensuite partitionnés et formatés
- Exemple 2 : Windows et *Storage Spaces*

Exemples de virtualisation avec NAS :
- Machine sans stockage (*diskless*) qui boote par réseau sur un SGF NFS (*Network File System*)

Exemple de virtualisation avec SAN
- Réseau de  stockage sur infrastructure de type Fibre Channel, Ethernet ou Infiniband
- Protocole d'accès iSCSI sur IP et est le précurseur de SAS
- Ce stockage distant est mis à disposition d'un cluster de serveur physiques ou d'hyperviseurs

## Virtualisation de réseau
VPN : Virtual Private Network
- Masque l'adresse IP réelle de l'utilisateur (privacy, contournement de restriction d'accès)
- Travail à distance
- Liaison sécurisée entre 2 sites distants

[[VLAN]] : Virtual Local Area Network
- Nombre de VLAN limité à 4096 ($2^{12}$)
- Protocole Ethernet 802.1Q

VXLAN : Virtual Extensible LAN
- Utilisé dans les très grands cloud
- Nombre de VLAN limité à 16 millions
- Techniquement : Ethernet encapsulé dans UDP

SDN : Software Defined Network
- Commutateurs virtuels
- Routeurs virtuels
- Pare-feu virtuels
- Exemple de protocole : OpenFlow






# 1. Machines virtuelles et conteneurs
OS hôte : OS sur lequel tourne l'hyperviseur
OS invité : OS qui tourne dans la machine virtuelle

Les points communs entre les machines virtuelles et les conteneurs :
- L'architecture doit être la même
- Les VM/conteneurs sont isolés entre eux et l'OS hôte est isolé des VM/conteneurs
- Ces propriétés sont des promesse en principe, mais il y a des failles de sécurité. Egalement, les VM/conteneurs ne sont pas isolés de l'OS hôte

Différences entre les machines virtuelles et les conteneurs :
- Les conteneurs n'utilisent pas d'OS invité et ne contiennent que les librairies et les fichiers nécessaires à l'exécution de l'application
- Les contenurs sont plus légers que les VM : ils ont moins de couches logicielles, moins de consommation de ressources et moins de temps de démarrage
- Les conteneurs sont moins isolés que les VM : ils partagent le même noyau que l'OS hôte

Il existe 2 types d'hyêrviseurs :
- Pas d'OS tournant sur la machine physique, l'hyperviseur est directement sur le matériel
- Un OS classique tourne sur la machine physique, l'hyperviseur est une application de cet OS


# 2. Intérêts de la virtualisation

Certains serveurs ont de gros besoins en ressources et stockage. Le dimensionnement des serveurs phsyiques est donc assez complexe.
Cependant, avec des serveurs virtuels, on peut le faire à la demande. On va dans un premier temps insataller des serveurs avec le minimum de ressources, puis on va augmenter les ressources en fonction des besoins. Il est en effet plus simple d'upgrader un serveur physique qu'un serveur virtuel.

Egalement, n serveurs virtuels ont besion de moins de matériel que n serveurs physiques, ce qui fait des économies de matériel et d'énergie.


Il y a également un haute disponibilité car une VM peut être transférée d'un serveur à un autre sans interruption de service. Cela permet de faire de la maintenance sans interruption de service.
Il y a cependant quelques inconvénients comme la complexité de la mise en place et la perte de performance.


# 3. Principaux hyperviseurs existants

On choisit un superviseur en fonction de l'architecture de l'hyperviseur, de sa sécurité, du fait de si c'est une licence libre ou propriétaire, de sa faciliité d'utilisation, de sa maintenance ...

# Qemu/KVM
A l'origine, Qemu/KVM était un projet de virtualisation de processeur. Qemu est un émulateur de processeur et KVM est un module du noyau Linux qui permet de faire de la virtualisation matérielle. Qemu/KVM est donc une solution de virtualisation matérielle.
KVM = Kernel-based Virtual Machine. Attention à ne pas le confondre avec les autres KVM !

