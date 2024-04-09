# Le niveau transport
**Schéma**

- **USER DIAGRAM PROTOCOL (UDP)** : Service de transport *simple* sans connexion
- **TRANSMISSION CONTROL PROTOCOL (TCP)** : Service de transport avec connexion (fiabilité de connexion)

⇒ **Service de segmentation**

Le but est le transport des datagrammes ou des flots d'octets entre un processus application client et un processus application serveur
**Identification des processus client et serveur :**
- Adresse IP ne suffit pas : plusieurs applis tournent sur la même station
- Numéro de processussystème ne convient pas car PID local et dépend du sys utillisé
- **Numéro de port :** Champs sur 16 bits de l'en-tête TCP et UDP

Un port est un vealeur sur 16 bits identifiant une conenxion avec processus sur une station
⇒ De 0 à 1023 = ports système. Privilège admin pour  utiliser
- 22 : SSH
- 25 : SMTP
- 80 : HTTP
De 1024 à 49151 = ports enregistrés par IANA. Peuvent être utilisés sans privilèges ADMIN :
- 5432 : postgreSQL
- 8080 : port HTTP alternatif ou tomcat
Le reste est alloué dynamiquement pour les processus (jusqu'à 65535)
> [!info]
> On dit que les applications écoutent sur un port

Analogie postale

# UDP
- Comm dite *directe*
- Encapsulation : dans un paquet IP (taille max = celle de IP)
- Pas de fragmentation
- Pas de contrôle d'erreur

→ Transmission ou réception des paquets dans un ordre non contranit → adapté aux application en tps réel où la latence peut être un prblm

Adapté pour :
- ..
- ..

2 propriétés en plus que IP :
1. Numéros de ports pour distinguer diff connexions
2. Somme de contrôle sur un partie de l'entête

Rapide et adapté au broadcast :
- Pas de retransmission
- Pas d'ordonnancement des paquets
Non fiable
- Pas de vérif
- Pas de gestion de duplication ou perte données
- Pas de garantie que tous paquets parvenus à destination

# TPC
C'est une couche logicielle masquant aux applis contraintes du réseau
Service de transport fiable en mode flot d'octet

Notion de connexion TCP associée au couple constitué du processus client et du processus serveur

Réalisation du mode flot :
- Ouverture de connexion, préalable à tout échange de données
- Numérotation des octets de données à émettre
- Emission et réception des octets et blocs de segments, indépendemment des dépôts et retraits faits par les programmes applicatifs → Stockage en mémoire

- Transfert fiable : livraison des segments dans l'ordre et gestion des segments perdus. Utilisation numéros de séquence pour réordonner flux digital

**Contrôle de flux :** TCP fournit un moyen au destinataire de contrôle le débit des données envoyées par la source pour que l'émetteur n'émette pas trop vite par rapport au récepteur
**Contrôle de congestion :**
- Pertes interprétées ..



- App dépose données dans tampon émission : flot d'émission, ordre dans lequel tampon sera celui de la transmission
- TCP envoie ce flot par segment
- TCP émet octets du flot dès qu'il le peut : s'ily a octets non encore émis et si connexion lui permet
MIN(Na, MSS, W)
- Na = Nombre d'octets d'apps à émettre, stockée dans tampon émission
- MSS (Maximum Segment Size) : Dépend de taille max de la tram Maximum Transfert Unit (MTU)
  MSS = MTU - en-têtes IP et TCP
- W = Fenêtre = Volume autorisé par programme TCP réception

> [!tip] Fiabilisation des échanges TCP
> Contrôle d'erreur : numérotation des octets, aquittement des octets reçus ..


