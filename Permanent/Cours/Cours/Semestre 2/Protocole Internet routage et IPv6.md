---
MOOC: "[[Cours]]"
Ressource: "R2.05 : Réseaux"
Cours: "Cours 1 : Protocole Internet : routage et IPv6"
Date: 
tags: 
Complete: false
Learned: false
---
Principe du routage IPv4 : Le routage IPv4 implique le transfert de paquets de données entre différents réseaux via des routeurs. Les décisions de routage sont basées sur une table de routage qui associe les adresses de destination aux interfaces de sortie.

Routeur IP et son rôle : Un routeur IP est un équipement crucial dans la transmission des paquets entre différents réseaux. Il possède des adresses logiques (IP) dans chaque réseau et des adresses physiques (MAC) pour le transfert de données.

Fonctions du routeur : Les principales fonctions d'un routeur incluent la transmission des paquets (datagram forwarding) et la mise à jour des tables de routage à l'aide d'algorithmes spécifiques.

Routage IP : Lorsqu'un paquet IP arrive dans un routeur, il est retransmis soit directement à la station destinataire s'ils sont sur le même réseau, soit vers un autre routeur connecté. Le routage se fait "de proche en proche" en utilisant des tables de routage.

Algorithme de sélection dans la table de routage : Pour chaque paquet à envoyer, l'algorithme de routage teste chaque ligne de la table de routage jusqu'à trouver une correspondance entre l'adresse IP de destination et une adresse réseau dans la table.

Acheminement des paquets : L'acheminement des paquets implique plusieurs étapes telles que l'extraction de l'adresse de destination, la recherche dans la table de routage et la retransmission du paquet vers le prochain routeur.
**Calcul de correspondance :** <mark style="background: #FF5582A6;">Si (adrIP-dest & Genmask) == adrDestination, alors Trouve</mark>

Longest Match Routing Rule : Si un adresse destination peut répondre à plusieurs réseaux connus d'une routeur, alors c'est le plus grans nombre de bits qui est choisi

Le TTL (TIme To Live) : Durée de vie des paquets IP (Champs spécifique dans le paquet). Initialisé avec une certaine valeur, décrémenté pour chaque passage d'un routeur et meurt arrivé à 0.
⇒ **Utilité :** Les paquets perdus

Protocole Internet (IP) : IPv6 : IPv6 est la dernière version du Protocole Internet. Contrairement à IPv4, qui utilise des adresses sur 32 bits, IPv6 utilise des adresses sur 128 bits, offrant ainsi un espace d'adressage beaucoup plus large.

Notation des adresses IPv6 : Les adresses IPv6 sont généralement représentées sous forme de huit groupes de quatre chiffres hexadécimaux, séparés par des deux-points. Les adresses IPv6 sont utilisées pour l'unicast, l'anycast et le multicast.

Types d'adresses IPv6 : Les types d'adresses IPv6 comprennent les adresses unicast (global unicast, unique local unicast, link-local unicast), anycast et multicast, chacune ayant des utilisations spécifiques.

ICMPv6 et Neighbor Discovery Protocol (NDP) : ICMPv6 est intégré à IPv6 et remplace plusieurs protocoles liés à IPv4. Le Neighbor Discovery Protocol (NDP) permet la découverte des voisins sur un réseau IPv6 et remplace des protocoles comme ARP.

Fragmentation des données : Un paquet IP est découpé en plusieurs paquets IP

Avantages d'IPv6 : IPv6 offre un espace d'adressage plus vaste, élimine le besoin de fragmentation des paquets et propose de nouvelles fonctionnalités telles que la qualité de service (QoS).

En conclusion, comprendre les principes du routage IP et les spécificités d'IPv6 est essentiel pour la conception et la gestion des réseaux modernes.

[[cours_3.pdf]]