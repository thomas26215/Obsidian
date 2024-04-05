---
MOOC: "[[Cours]]"
Ressource: "R2.04b : Communication bas niveau"
Cours: "Cours 2 : Protocole Internet - adressage"
Date: 
tags: 
Complete: false
Learned: false
---
Internet : Interconnexion des réseaux *Inter Net* ou inter-réseau.
Architecture = Architecture TCP/IP et pour objectif le déploiement d'applications sur un inter-réseau indépendamment des technologies physiques de ces réseaux

L'Interface assure l'accès aux réseaux physiques

**Le protocole IP** a pour fonction assure acheminement des donées d'une machine à une autre.
- Aucun contrôle d'erreurs
- Service de base type BE
- Service de fragmentation de données
Deux versions :
- IPv4 - 32 bits
- IPv6 - 128 bits

Le but d'IP est la communication entre machines de LANS différentes
Un besoin d'abstraction :
- Myriade de protocoles utilisés
- Adresses MAC non organisées par réseau
- Adresse MAC non uniques
- Tables des commutateurs = capacité limitée
IP est globale inter-réseau
- Adresse IP représente l'@ machine et l'@ réseau
	- Partie réseau
	- partie machine
- Adresse IP = logique ; Ne dépend pas du matériel. Peut être reconfigurée

Adressage hiérarchique de base
- Identification du réseau → Poids forts de l'adresse IP
- Identification de chaque machine dans le réseau → Poids faibles de l'adresse IP
Le routeur a une adresse IP dans chacun des 2 réseaux, donc avec un préfixe réseau X et une avec le préfixe réseau Y. Ses adresses IP sont par exemple X7 et Y6

**Format d'adresse** IPv4 :
- Suite de 32 = n + m bits
- n bits pour identifer réseau
- m bits pour identifier machine sur réseau
**Plage d'adresse** :
→ Un réseau  IP, identifié par ses n bits de poids forts, possède $2^m$ valeurs qui définissent une plage d'adresse, réparties en  :
- Une adresse IP du réseau : les m bits sont tous à 0
- Les adrsses machines : au maximum $2^m-2$ machines
- Une adresse de diffusion : les m bits sont sout à 1

**Masque de réseau :**
- Permet de séparer la partie réseau de la partie machine par le calcul (ET bit-à-bit)
- Masque = tous les n-bits sont à 1 et tous les m-bits sont à 1

**Notation CIDR** : Adresse IP / nombre de bits du préfixe réseau 
- 192.18.131.0/24
  → 24 bits de préfixe réseau, reste 8 bits  pour la partie adresse machine. Adresse de diffusion dans ce réseau : 192.18.131.255 

**Réseau privés** : 192.168.0.0/16, 172.16.0.0/12, 10.0.0.0/8
**Loopback** : 127.0.0.0/8


**Limites d'IPv4 :**
- Adressage sur 32 bits → $2^{32}$ bits 
- Depuis février 2011, plus de lots d'adresses disponibles
- → Nécessité de passer à IPv4 : déploiement par opérateurs ...

- Possibilité de répartir adresses d'un réseau IP pour créer réseaux IP plus petits
- Un sous-réseau IP est un réseau IP
- Découpage en déplaçant vers la droite la limite de séparation partie machine et partie réseau

**Routage IP :** Lorsqu'un paquet arrive dans un routeur, celui-ci transmet le paquet soit directement à la station destinataire si celle-ci est connectée au routeur ou  vers un autre routeur auquel il est directement connecté. Routage de proche en proche

Dans l'inter-réseau Internet, la sélection d'un chemin partant de la source vers la destinataire est appelé le routage. Un chemin passe par 3 types de stations : la source, un nombre invariable de routeurs et la destination

Un routeur IP, c'est un équipement connecté à plusieurs réseaux IP qui permet l'acheminement des paquets d'une réseau à l'autr. Il possède une adresse logique pour chacun des routeurs auquel il est connecté et une adresse physique dans chacun des réseaux auquel il est connecté


