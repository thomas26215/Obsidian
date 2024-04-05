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

# Exo 3
1. Il envoie à tout le monde
2. Il l'envoie à P1 et il ajoute P3
3. Il y a au moins un commutateur derrière
