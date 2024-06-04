---
MOOC: "[[Cours]]"
Ressource: "R2.04b : Communication bas niveau"
Cours: "Exercice 1 : Ethernet et WiFi"
Date: 2024-02-13
tags: 
Complete: false
Learned: false
---
# Exo 1
## Partie 1
1. L'expression du temps de propagation est Tp = distance/vitesse de propagation
   ⇒ Ainsi, on a, avec nos valeurs, $T_p=\frac{L}{V_p}$
2. $T_p=\frac{100}{10^{-6}}=0.5m/s$ 
## Partie 2
1. $D_e=\frac{N}{T_e} ⇔ T_e*D_e=N ⇔ T_e=\frac{N}{D_e}$
2. Le débit maximale $D^{max}_{e}$ de ce réseau est 1000 MegaBits (**1000**BASE-T)
3. $T^{max}_e=\frac{N^{max}}{D^{max}}=\frac{1526*8}{1000*10^6}=12microsecondes$ 
   ($8+6+6+1+1500+4 = 1526 octets*8bits=12208bits$ et $D_{max}=10^9$ donc $T_{max}=\frac{12208}{10^{-9}}=12208*10^{-9}=13208bs$)
## Partie 3
1. Silence inter-trame = temps d'émissions de $96bits$
2. Silence inter-trame = $\frac{96}{10^9}=96ns$ $1000BASE-T$ 
## Partie 4
4. $T_{transmission}=2*Te+T_p+T_e+T_e+T_p+T_s{silence}$ 
   $2*T_e=12microsecondes$
   $T_p=0.5nanosecondes$ 

# Exo 3
## Partie 1
1. $1100 0000.0110 0100.0011 1000.0000 0000$
   Soit $192.100.56.1$ à $192.100.56.254$ (Première et dernière machine)
2. Masque : $11111111.11111111.11111111.00000000$
3. Adresse de diffusion : $1100 0000.0110 0100.0011 1000.11111111$
4. On peut connecter au maximum 253 machine
## Partie 1 en remplaçant 24 par 25
1. $11000000.01100100.00111000.00000000$
   Soit $192.100.56.1$ $192.100.56.127$
2. Masque : $11111111.1111111.11111111.10000000$
3. Broadcast : $11000000.01100100.00111000.01111111$
## Partie 2 suite
1. $192.1.131.0/24$ → eth0
   $192.168.16.0/23$ → wlan0
   Les deux interfaces sont actives car le UP est actif
## Partie 3
### Exercice 1
1. Il faut au minimum 10 bits ($2^{10}$) pour la partie machine
2. Masque de réseau : $11111111.11111111.11111100.00000000$
   Egalement $256.256.253.0$
3. $202.0.64.1$ à $202.0.67.254$
4. $202.0.96.0/22$

### Exercice 2
1. On peut y adresse $2^9-2$ machines - $11000000.10000001.00100000.00000000$
2. L'adresse de diffusion est $11000000.10000001.00100001.11111111$ ($194.129.33.255$)

3. $2^9$ = 256 et $\frac{256}{4}=64$

| Numéro du sous-réseau | Adresse réseau (CIDR) | Masque          | Adresse diffusion | Nombre max de stations |
| --------------------- | --------------------- | --------------- | ----------------- | ---------------------- |
| 1                     | 194.129.32.0/25       | 255.255.255.128 | 194.129.32.127    | 126                    |
| 2                     | 194.129.32.128/25     | 194.129.33.0    | 194.129.32.255    | 126                    |
| 3                     | 194.129.33.0/25       |                 | 194.129.33.127    | 126                    |
| 4                     | 194.129.33.128/25     |                 | 194.129.33.255    | 126                    |
4. Réseau 4
$194.129.33.188 = 0010000110111100$ et $255.255.255.128=1111111110000000$
bit a bit : $0010000110000000 = 33.128$ 

### Exercice 4

|                                            | Réseau  IP 1                        | Réseau IP 2                          |
| ------------------------------------------ | ----------------------------------- | ------------------------------------ |
| Adresse réseau en CIDR                     | 192.168.2.128/26                    | 192.168.2.128/25                     |
| Adresse de réseau                          | 192.168.2.128                       | 92.168.2.128                         |
| Masque de réseau                           | 255.255.255.192                     | 255.255.255.128                      |
| Adresse de diffusion                       | 192.168.2.191                       | 92.168.2.255                         |
| Nombre de stations possible dans le réseau | 62 stations possibles sur le réseau | 126 stations possibles sur le réseau |
| 192.168.2.193 dans le réseau ?             |                                     | Oui car 128 <= 193 <= 255            |



# Exo 4
## Partie 2
1. Port source = 12345
   Port destination = 8888
   Sn = 0
   An = 0
   Header len = 24 octets
   Drapeau = Syn
   Fenêtre = 4000
2. MSS = Maximum segmentation size. C'est la taille maximale d'un octet TCP que la machine peut recevoir
3. Mes trois grandes phases sont :
	1. SYN, SYN-ACK, ACK
	2. Echange de données
	3. Fermeture de connexion : Fin, ACK, FIN, ACK
4. **Début =** SYN
   **FIN =** FIN

## Partie 3
1. **Principe d'envoi de données**
	1. An = 1010
	2. Aucune donnée n'est contenue dans le champs de données de l'acquittement
2. **Principe du segmentation de données**
	1. Non car la taille maximale d'un segment est limité par la valeur du MSS. Si la taille du segment à envoyer dépasse le MSS, alors le segment sera découpé en plusieurs segments
	2. Il faudrait envoyer 3 segments TCP successifs, car chaque segment aurait une taille maximale de 1000 octets
3. **Principe de fonctionnement du contrôle de flux**
	1. Aw indique la quantité d'octets que le récepteur est prêt à recevoir sans encombrer son tampon de réception
	2. Si Aw, ça signifie que le récepteur n'est pas prêt à recevoir de nouveaux octetset que l'émetteur' doit suspendre l'envoi de données
	3. L'émetteur détermine le nombre maximum d'octets de données qu'il peut envoyer dans un segment TCP en prenant le minimum entre le MSS et la valeur de AW. Cela garantit que les données envoyées peuvent être toutes reçues par le récepteur sans dépasser sa capacité de réception.
	5. L'envoie des 1000 derniers octets ne peut pas être effectué immédiatement, car le récepteur a atteint sa capacité maximale de réception et a un AW de 0. L'émetteur doit attendre que le récepteur libère de l'espace dans son tampon de réception en consommant des données avant de pouvoir envoyer ces 1000 octets.
	6. Cette situation évoluera lorsque l'application côté serveur commencera à consommer des données du tampon de réception. Cela augmentera la valeur de AW, permettant à l'émetteur d'envoyer les données en attente dans son tampon d'émission. Une fois que le récepteur aura consommé suffisamment de données pour libérer de l'espace dans son tampon de réception, il enverra des ACK avec un AW approprié pour permettre à l'émetteur de continuer à envoyer des données.

## Partie 4
1. Port source = 12345
   Port destination = 8765
   Sn = 0
   An = 0
   Header len = 24 octets
   Drapeau = Syn
   Fenêtre = 50ko
   ...
3. Le délai RTT est le temps qu'il faut pour qu'un segment TCP soit envoyé du client au serveur et que l'accusé réception correspondant revienne au client. Ce délai sera mis à jour grâce à l'estimation du RTT par le client et le serveur, ce qui permettra d'ajuster le délai de temporisation pour les retransmissions de segments en cas de perte
4. 1460 octets
## Partie 5
# Exo 6
1. Les² stations E et F recevront la trame (fait partie du même VLAN)
2. 

| Destination  | Gateway      | GenMask         | Iface |
| ------------ | ------------ | --------------- | ----- |
| 194.199.20.0 | 0.0.0.0      | 255.255.255.128 | eth0  |
| 0.0.0.0      | 194.199.20.1 | 0.0.0.0         | eth0  |

3. 

| Destionation | GateWay | GenMask         | Iface |
| ------------ | ------- | --------------- | ----- |
| 192.168.1.14 | 0.0.0.0 | 255.255.255.128 | VLAN1 |
| 192.168.1.21 | 0.0.0.0 | 255.255.255.128 | VLAN2 |
| 192.168.1.11 | 0.0.0.0 | 255.255.255.168 | VLAN3 |
|              |         |                 |       |
4. .

| Adresse MAC | Port |
| ----------- | ---- |
| @A          | P1   |
| @X          | P2   |
| @Y          | P3   |
| @Z          | P3   |
| @B          | P4   |
| @A          | P4   |
| a0:..:cf    | P7   |
5. .
	1. La station envoie le paquet au comm COM_1 qui contient 

6. .
	1. Ne peut pas envoyer directement donc envoie tram au routeur . Adresse MAC destination contenant tram est adresse MAC du comm et donc comm agit comme routeur






---
---

---


# Exo 5
## Partie 1
1. **Analyse d'une trame**
	1. 0000 <mark style="background: #FF5582A6;">08 00 4e 33 5b 00</mark> <mark style="background: #FFB86CA6;">08 00 20 87 b0 44</mark> <mark style="background: #BBFABBA6;">08 00</mark> <mark style="background: #D2B3FFA6;">45 00</mark>
	   0010 <mark style="background: #D2B3FFA6;">00 7f 1c dd 40 00 40 06 34 11 c1 37 33 83 c1 37</mark>
	   0020 <mark style="background: #D2B3FFA6;">33 99</mark> <mark style="background: #CACFD9A6;">c6 fa 00 50 cc 5e 19 88 d6 da 37 a5 50 18</mark>
	   0030 <mark style="background: #CACFD9A6;">c5 f8 0f b4 00 00</mark> 47 45 54 20 2f 69 6e 64 65 78
	   <mark style="background: #FF5582A6;">Destination</mark>
	   <mark style="background: #FFB86CA6;">source</mark>
	   <mark style="background: #BBFABBA6;">EtherType</mark>
	   <mark style="background: #D2B3FFA6;">IP</mark>
	   <mark style="background: #CACFD9A6;">TCP</mark>
	2. **Identification des champs**
		1. Niveau liaison
			1. <mark style="background: #FFB86CA6;">08 00 20 87 b0 44</mark>
			2. <mark style="background: #FF5582A6;">08 00 4e 33 5b 00</mark>
			3. <mark style="background: #BBFABBA6;">08 00</mark>
		2. Niveau réseau
			1. L'adresse IP du serveur (en hexadécimal et en notation décimale pointée) est: `C1:37:33:83` (hexadécimal) / `193.55.51.131` (notation décimale pointée).
			2. L'adresse IP du navigateur (en hexadécimal et en notation décimale pointée) est: `C1:37:33:99` (hexadécimal) / `193.55.51.153` (notation décimale pointée).
		3. Niveau transport
			1. 0xC6FA
			2. 0x0050
## Partie 2
1. C'est adresse MAC serveur qu'on veut
   IP = 192.168.0.17
   Port = 55062
2. **Cours**
3. Ouverture = 43 56 57
   Echange = 58 59 60 61
   Terminaison = 62 63 64 65
4. Taille de message trame 60 : 944 - 66 = 878. Sinon, on regarde la diff de taille WIndow

# Exo 6
## Partie 1
1. Toutes les stations dans le même VLAN recevront la trame de diffusion. Z appartient au réseau 192.168.1.0/24 donc les stations qui vont recevoir la trame sont 
	- F (192.168.1.14)
	- E(192.168.1.21)
2. 

| Destination  | Gateway      | Genmask         | Iface |
| ------------ | ------------ | --------------- | ----- |
| 194.199.20.0 | 0.0.0.0      | 255.255.255.128 | eth0  |
| 0.0.0.0      | 194.199.20.1 | 0.0.0.0         | eth0  |
3. 

| Destination  | Gateway | Genmask         | Iface |
| ------------ | ------- | --------------- | ----- |
| 194.199.20.0 | 0.0.0.0 | 255.255.255.128 | WLAN2 |
| 192.168.0.0  | 0.0.0.0 | 255.255.255.0   | WLAN1 |
| 192.168.1.0  | 0.0.0.0 | 255.255.255.0   | WLAN3 |
4. 

| Adresse MAC | Port |
| ----------- | ---- |
| @A          | P1   |
| @X          | P2   |
| @Y          | P2   |
| @Z          | P3   |
| @B          | P4   |
| @C          | P4   |
5. Ne peut pas envoyer directement donc route par défaut donc trame ethernet vers le routeur qui renvoie une trame vers la destination, ici B

## Partie 2
1. **Intérêt**
	1. Simplification de la gestion, réduction des coûts, amélioration des performances
	   On peut aussi changer les ports plus facilement et + de sécurité
	2. [[Drawing 2024-06-05 00.32.10.excalidraw]]
	3. Il y a deux inter-réseaux car 2 VLANS
	   - Réseau Ethernet connecté à COM/ROUT via les ports P1, P2, P3, et P4 (anciennement COM_1).
	   - Réseau Ethernet connecté à COM/ROUT via les ports P11, P12, P13, P14, et P15 (anciennement COM_2).
	4. Trois réseaux IP distincts
2. .
	1. x

| Destination | Gateway    | Genmask       | Iface |
| ----------- | ---------- | ------------- | ----- |
| 144.19.2.0  | 0.0.0.0    | 255.255.255.0 | eth0  |
| 0.0.0.0     | 144.19.2.1 | 0.0.0.0       | eth0  |
Facile pour reste

3. **Etude du fonctionnement de COM/ROUT (uniquement pour petit 1)**
	1. C'est la première ligne car A et Y sont dans le même VLAN
	2. L'adresse MAC destination de la trame envoyée par A sera a0:..:cc
	3. La commutation car A et Y sont dans le même VLAN
	4. 1 seule trame est nécessaire 