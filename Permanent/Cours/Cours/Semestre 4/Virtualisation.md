# Contexte

Enseignements précédants concernant la virtualisation
- SAE S1.03
- SAE S2.03
- SAE S3.03


# Introduction
[[Virtualiser]]
[[Les VM et les conteneurs]]


## Virtualisation de stockage
[[Les différents types de fichiers]]
[[Comment virtualiser]]

## Virtualisation de réseau
[[VPN]]

[[VLAN]] : Virtual Local Area Network
[[XVLAN]] : Extensible [[VLAN]]


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

La virtualisation complète permet de faire tourner n'importe quel OS et l'OS invité tourne sans modifications tandis que lors de la para-virtualisation, l'OS invité est modifié pour être compatible avec l'hyperviseur. Cela permet cependant d'améliorer les perforamnces. Dans le cas de Linux, le même noyeau de Linux peut être utilisé pour de la para-virtualisation

# 2. Intérêts de la virtualisation

Certains serveurs ont de gros besoins en ressources et stockage. Le dimensionnement des serveurs phsyiques est donc assez complexe.
Cependant, avec des serveurs virtuels, on peut le faire à la demande. On va dans un premier temps insataller des serveurs avec le minimum de ressources, puis on va augmenter les ressources en fonction des besoins. Il est en effet plus simple d'upgrader un serveur virtuel qu'un serveur physique.

Egalement, n serveurs virtuels ont besion de moins de matériel que n serveurs physiques, ce qui fait des économies de matériel et d'énergie.

Il est possible d'utiliser moins de ressources avec une VM qu'avec un serveur physique. En effet, il est par exemple possible de créer un serveur physique avec 1 seul coeur, alors qu'il est impossible de le faire pour du métériel physique.


Il y a également un haute disponibilité car une VM peut être transférée d'un serveur à un autre sans interruption de service. Cela permet de faire de la maintenance sans interruption de service.
Il y a cependant quelques inconvénients comme la complexité de la mise en place et la perte de performance.


# 3. Principaux hyperviseurs existants

On choisit un superviseur en fonction de l'architecture de l'hyperviseur, de sa sécurité, du fait de si c'est une licence libre ou propriétaire, de sa faciliité d'utilisation, de sa maintenance ...
Il existe des superviseurs assez connus comme Qemu ou bien VirtualBox

# 4. Qemu/KVM
A l'origine, Qemu/KVM était un projet de virtualisation de processeur. Qemu est un émulateur de processeur et KVM est un module du noyau Linux qui permet de faire de la virtualisation matérielle. Qemu/KVM est donc une solution de virtualisation matérielle.

KVM = Kernel-based Virtual Machine. Attention à ne pas le confondre avec les autres KVM !
Il a un lien avec Qemu et fait partit du noyeau Linux (Exemple : modules *kvm* sur le disque et modules *kvm* chargés dans le noyeau Linux)
