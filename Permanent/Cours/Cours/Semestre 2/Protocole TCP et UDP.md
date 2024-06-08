---
MOOC: "[[Cours]]"
Ressource: 
Cours: 
Date: 
tags: 
Complete: false
Learned: false
---
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

Un port est une valeur sur 16 bits identifiant une conenxion avec processus sur une station
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
- protocoles basés sur transaction (DHCP, NTP)
- cas où la correction d'erreur en tps réel n'est pas nécessaire (Jeux vidéo, conférence ...)

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

# TCP
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
- Pertes interprétées comme signal de congestion de flux dans le réseaux
- L'émetteur réagit en diminuant le débit de transmission
**Sn** : Sequence number : n° du premier octet contenu dans le champ info (n° dans le lot de données d'émission).
**An** : Acknowledge number : n° du prochain octet attendu dans le lot de données reçues, acquitte les octets de n° inférieurs.
**AW** : Advertised receive Window : fenêtre de réception (notée ici W).
**H.lg : Header Length** : longueur de l'en-tête, en mots de 32 bits (si pas d'option, H.lg=5).
**Control (Flags) :** <0, 0, URG, ACK, PSH, RST, SYN, FIN>
 ▶ SYN : demande d'ouverture de connexion (O).
 ▶ FIN : demande de fermeture de connexion (F).
 ▶ ACK : le paquet acquitte des données ou une demande O/F.
 ▶ PSH : le segment contient des données qui peuvent être délivrées à l'application.
**Checksum** : même calcul que pour l'UDP.

![[Pasted image 20240528013351.png]]


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


**An =** Numéro du prochain octet à recevoir
**Sn =** Prochain numéro d'octet attendu
**W =** Place disponible à la réception, récepteur indique combien d'octets il peut encore recevoir
**Flags**
 → **ACK :** Le paquet acquiette des données
 → **PSH :** Le segment contient des données qui peuvent être délivrées à l'application
 → **SYN :** Mise en place de la connexion
⇒ **Les paquets Sn, An et W** dans chaque segment
# Echange à l'ouverture d'une connexion
**Flag SYN** = Mise en place connexion
**AW** = Window
**MSS** = Maximum Size Segment. Taille maximum à envoyer
Initialisation de An, Sn et AW de chaque côté de la connexion
# Echanges à la fermeture de connexion
Après une demande **Fin**, les tampons sont vidés puis la connexion est arrêtée

# Numéro de séquence
**Sn** → Numéro du premier octet du segment transmis (compris entre 0 et $0^{32})$. Implanté comme un entier non signé
$S_{n+1}=(S_n+len)mod\space2^{32}$ 

<mark style="background: #BBFABBA6;">Exemple</mark> : Un client avec
- Sn=4 294 966 996 (xFFFFFED4)
- Le client envoie envoie 400 octets
- Le esrveur reçoit le segment et renvoie un ack 
→ Quel sera le numéro An ?

$A_n=S_{n+1}=(S_n+len)mod2^{32}$
$A_n=4 294 966 996+400mod2^{32}$
...

## Numéro de séquence intial
Plusieurs connexions TCP ayant les mêmes sources et destinations peuvent co-exister
→ Les numéros de séquence ne doivent pas être les mêmes !
→ Choix pseudo aléatoire du numéro de séquence initial **Initial Sequence Number (ISN)**
*ISN = M + F(localip, localport, remoteip, remoteport, secretkey)*

## Evolution des numéros de séquence à  l'ouverture
Si le drapeau SYN n'est pas présent, l'émétteur devrait recevoir $ACK=(Sn+len)mod2^{32}$
Si le drapeau SYN est présent, l'émetteur devrait recevoir $ACK=(Sn+1)mod2^{32}$

# Contrôle de congestion
La congestion d'un réseau infrmatique est la condition dans laquelle une augmentation du trafic (flux) provoque un ralentissement global de celui-ci
TCP utilise 4 algorithmes : *slow start, congestion avoidance, fast retransmit et fast recovery*

## Fenêtre de congestion et de retransmission
⇒ Indique le nombre N de segments de taille MSS pouvant être envoyés en une seule fois
2 fenêtres dans une connexion TCP (**AW** et **CW**) et le minimum des deux détermine la quantité envoyée
Un ACK peut acquitter plusieurs segments. Si un ACK n'arrive pas au bout d'un certain temps $T_{max}, le segment est retransmis
$T_{max} = $RTO^a$ souvent égal à deux fois le RTT (calculé tout au long de la connexion)

## Slow start and congestion avoidance
Comment calculer **CW** ?
Lors de détextion congestion, connexion redémarre lentement puis la taille N de la fenêtre de congestion croît rapidement