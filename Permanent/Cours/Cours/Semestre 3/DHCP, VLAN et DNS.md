---
MOOC: "[[Cours]]"
Ressource: "R3.07 : Réseaux"
Cours: DHCP, VLAN et DNS
Date: 
tags: 
Complete: false
Learned: false
---
**Internet** = Interconnected Network
⇒ Choix d'1 chemibn en fonction de l'IP destination. Table de routage màj. Il existe différents algorithmes et différents protocoles. Protocole de proche en proche par communication de paquets

Table avec physique, liaison de données, réseau, transport et application => [[Réseaux infos]]


Couches :
- 2 : Liaison
	- Ethernet
	- Wifi
	- ATM
- 3 : Réseaux ⇒ IP (ICMP ou ARP)
- 4 : Transport
	- [[Protocole TCP et UDP]]
- Application
	- TCP
		- HTTP
		- SMTP
		- SSH
	- UDP
		- DNS
		- DHCP
		- RTP

**Identifiants dans l'architecture TCP/IP :** 
- L'adresse physique du niveau interface dépend du réseau physique (MAC)
- L'adresse du niveau réseau
	- Adresse IP = adresse logique
	- Une ou plusieurs par interface
- Identification des processus au niveau transport = adresse IP + num port
- Identification des utilisateurs/ressources dans les apps : addresse mail, URL

**Le protocole IP :** Acheminement des unités de données dans l'inter-réseau
- Sans contrôle d'erreur ni contrôle de flux de bout en bout
- Service de base de type BE
  Service de fragmentation des données si réseaux travesrés ont MTU de valeurs diffs

>[!rappel]
>**IPv4** = adresse sur 32 bits
**IPv6** = adresse sur 128 bits

Protocole ARP pour trouver qui correspond à une adresse via boradcast

DHCP permet de configurer dynamiquement une station au sein d'un réseau

DHCP suit un modèle client-serveur. Ils allouent des adresses réseaux et fournissent des paramètres de configuration aux clients configurés dynamiquement
Il est composé de deux éléments :
- Un procotol applicatif pour déliver paramètres de configuration spécifiques à un hôte
- Un mécanisme d'allocation d'adresses réseau aux hôtes

# La nécessité d'un VLAN
- LAN (Local area Network)
	- Simple
	- Manque de sécurité
	- Trafic important → broadcast arrivant sur toutes les machines
- On pourrait implanter un sous réseau
	- Isolation de sous-réseaux
	- Mais un coût important
- En isolant les ports à l'intérieur
	- Séparation des sous-réseaux au niveau des ports
	- Un seul commutateur utilisé

Il faut des VLANs (un LAN de 50 station sera plus encombré que 10 VLANs de 50 stations) pour améliorer la bande passante, améliorer la sécurité et facilité la gestion

Les VLANS sont souvent répartits sur plusieurs équipements

Champs TPID = identifier le mode tagged trame du protocole 802.1Q. Egalement différencier trames Ethernet simples qui ont juste le champs Type
Une trame 802.1Q a une taille maximale de 1522 octets au lieu de ... pour  trame Ethernet


# DNS
Pour transporter HTTP, IP doit obtenir une adresse IP source et destination
Il faudrait donc connaître l'ensemble des adresses IP des serveurs auxquels on souhait accéder. Mais une adresse IP est difficile à retenir. C'est pour cela que l'on utilise des noms de domaine.
Le DNS associe un nom à une machine. On retrouve donc l'adresse IP à partir du nom. Cela repose sur une table de correspondance <Nom, adresse IP>

Un serveur centralisé facilite la maintenance mais ne passe pas à l'échelle la taille de la table, la charge et le temps de réponse et la panne