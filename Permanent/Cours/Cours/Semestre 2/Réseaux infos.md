---
MOOC: "[[Cours]]"
Ressource: "R2.04b : Communication bas niveau"
Cours: "Cours 1 : Les réseaux informatiques"
Date: 
tags: 
Complete: false
Learned: false
---
1 réseau est un ensemble d'équipements reliés entre eux qui s'échangent des informations. On peut distinguer plusieurs types de réseaux : des réseaux routiers, des réseaux postiers ..
Une définition générale est qu'un réseau est une ensemble de composants et de communications interconnectés représenté par des noeuds et des liens

En Informatique on peut distinguer :
- Les noeuds
	- Terminaux (Téléphone, PCs ...)
	- Equipements d'interconnexions (commutateur, routeur)
- Les liens
	- Par câble
	- Par fibre optique
	- Par électromagnétique

Il existe différentes topologies (graphes) :
- Les graphes en étoile
- Les graphes en anneau
- Les graphes en bus

On peut distinguer plusieurs propriétés en réseau :
- **De** = Volume de données/temps (b/s)
- **Tp** = Distance/vitesse de propagation (m/s)
- **QoS** = Qualité de service
- **Facilité d'utilisation**
- **Sécurité**

Quand on échange des informations, que ce soit par vocal ou bien dans notre cas par informatique, il est indispensable  :
- d'identifier l'émetteur et le récepteur. Pour cela, il existe la notion d'adresse des personnes, les applications, les machaines
- de réaliser des échanges de bonne qualité
	- Fiabilité
	- Adaptabilité
	- Equité d'accès aux ressources
	- Parler le même langage

Il existe des protocoles en informatique, de la même manière qu'on ne va pas dire "Hey, salut" au Roi d'Angleterre. Attention, le code Morse n'est pas un protocole mais un codage

---
Pour rendre la communication entre PCs possible, ce problème a ététd divisé en plusieurs sous-problèmes, normalisé sous le termse d'ISO :

| Unité de donnée | Couches          |
| --------------- | ---------------- |
| Données         | 7 - Application  |
| Donnée          | 6 - Présentation |
| Donnée          | 5 - Session      |
| Segment         | 4 - Transport    |
| Paquet          | 3 - Réseau       |
| Tram            | 2 - Liaison      |
| Bit             | 1 - Physique                 |

Couches du modèle TCP/IP :

| Couche | Sous-problème | Implanté dans | Protocoles |
| ---- | ---- | ---- | ---- |
| Application | Communication utilisateur/application | Logiciel | http, ftp ... |
| Transport | Assurer la communication entre deux processus | Système d'exploitation | TCP, UDP |
| Réseau | Trouver les chemin pour chaque paquet de données à envoyer entre deux machines de réseaux locaux différents | Système d'exploitation | IP |
| Liaison de données | Gérer l'accès a médium | Carte réseau | Ethernet, WiFi ... |
| Physique | Taduire l'information binaire en ondes électromagnétiques sur le lien physique | Carte réseau | Ethernet, WiFi ... |

**Adressage dans les réseaux :**
⇒ Adresse au niveau application : identifiants utilisés par les applications : adresse e-mail, URL ...
⇒ Adresse au niveau transport : numéro de port TCP/UDP pour identifier le processus : port 80
⇒ Adresse au niveau réseau : Adresse IP = identifier les équipements d'un réseau indépendamment de la localisation géographique
- Adresse IpV4
- Adresse IpV6
⇒ Adresse au niveau liaison/physique : adresse physique
- Ex : adresse Ethernet MAC


**Définitions sur les équipements informatique** :
- Commutateur = Equipement reliant les équipements entre eux
- Réseau local = Ensemble de machines qui ont chacune une carte réseau connéctées par un commutateur  et dont les adresses IP partagent une partie commune
- Routeur = Une machine reliant 2 LANs
- AREA Network = Une machine reliant un ensemble de LANs

⇒ Les technologies les plus utilisées sont le WiFi, l'Ethernet, le Blutooth et le CPL


Les normes de famille Ethernet
⇒ *Exemple* : 100BASE-T
→ 100 = 100Mb/s
→ BASE = bande de base
→ T = Support de transmission

On peut remarquer que les câbles sont constités de 4 paires torsadées. Seulement, pour du 100BASE-T, seulement 2 câbles sont utilisés alors que les 4 sont utilisés pour du 1000BASE-T

Au niveau du réseau Ethernet, le **commutateur** est une noeud d'interconnexion qui redirige les trames en fonction des destinataires
La **Carte interférance réseau** code et décode les trames en signaux, ce qui va détecter les erreurs et assurer la synchronisation
→ Les trames sont transformés en signaux eléctriques ou optiques
→ Transmission en full-duplex (dan s les deux sens en même temps)
→ Les trames sont émises à la demande avec un délai entre chacun appelé *silence inter-trame*
- Pour éviter génération d'erreurs
- Equivalente à la durée d'emission de 96 bits

Chaque CIR est identifié par une adresse MAC allouée par le fabriquant de la carte CIR :
- Elle est de longueur 6 octets
- On la note par groupe de deux chiffres hexa-decimales séparés par *:*
- Les 3 premiers identifient le fabriquant
Le CIR d'une station émet  et reçoit des trames
- En mode Unicast : 1 émetteur et 1 destinataire
- En mode Broadcast : 1 vers toutes les stations
Pour accédes à toutes les machines réseau : `FF:FF:FF:FF:FF:FF`

Le CSMA est la technique de contrôle d'accès au support physique des réseaux internet
- **Emission** : Chaque station écoute en permanence si le bus est occupé
- **Emission** : Si le support est libre la station A peut transmettre. La station destinatrice saura que la trame lui est destinée grâce à l'adresse MAC de destination contenue dans la trame
- **Collision** : Chaque station peut détecter une collision
- **Brouillage** : La station qui détecte une collision émet un signal de brouilage pour avertir toues les autres stations
- **Réémission** : Chaque station attend un délai aléatoire pour réémettre

1. Ethernet initial en bus (câble coaxial)
	1. **Organisation physique** : bus
	2. **Organisation logique** : bus
	   ⇒ Un seul domaine de collision
2. Ethernet moderne avec commutateur
	1. **Organisation physique** : étoile
	2. **Organisation logique** : bus
	   ⇒ Plusieurs domaines de collision

Pour la transmission sans fil, on utilise comme support les ondes électromagnétiques ondulées modulées. On différencies les réseaux sans fil par :
- Leur type (Internet, téléphonique cellulaire)
- Leur distance de transmission (Très courte, locale, Réseau d'accès ...)
- Les données transportées : données et/ou voix

La transmissions WiFi est la transmission d'une onde eléctromagnétiquede haute fréquence à courte ou moyenne distance et à faible puissance. Plus la distance est éloignée, plus le réseau est faible et le taux d'erreur est plus important que par filaire

**Transmission et accès au support :**

Le partage du support se fait par compétition : il y a une écoute avant d'émettre, et une émission si le canal est libre. Il y aura cependant une collision de signal si deux station détectent en même temps que le canal est libre

Filaire != WiFi → ¨Pas possible les collisions sur le support. Le récepteur envoie donc un acquittement pour deux trames reçues

Pour l'émission d'une trame :
1. Ecoute jusqu'à ce que le canal soit libre
2. Attente DIFS et back-off
3. Emission de la trame  d'information
4. A la fin du dernier bit émis, attente d'un délai SIFS (plus court que le DIFS)
5. Réception de l’acquittement au bout du délai SIFS : si l’acquittement n’arrive pas, la station détecte qu’il y a eu collision

--- 
**Questions :**
1. Qu'est-ce qu'un réseau ?
2. Quels sont les différents types de réseaux ?
3. Définir un noeud, un câble
4. Quels sont les différents types de taupologies
5. Donner les différentes propriétés en réseau
6. Que faut-il quand on échange des informations ?
7. Les protocoles ?
8. Qu'est ce que la normalisation ISO ?
9. Donner les couches TCP/IP
10. Les adressages dans les réseaux
11. Qu'est ce qu'un commutateur ? Un réseau local ? Un routeur ? Un AREA Network ?
12. Donner les normes de famille Ethernet