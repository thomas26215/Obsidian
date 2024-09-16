---
MOOC: "[[Cours]]"
Ressource: "R3.07 : Réseaux"
Cours: TP 1
Date: 
tags: 
Complete: false
Learned: false
---
# Exercice 3

1. 
	1. **start** ⇒192.168.0.20
	2. **end** ⇒ 192.168.0.254
	3. **option subnet** ⇒ 255.0.0.0
	4. **opt router** ⇒ 192.168.10.0
	5. **opt dns** ⇒ 192.168.10.2 - 192.168.10.10
	6. **option lease** ⇒ 128000
	7. **interface** ⇒ eth0
4. 
	1. Avec la commande `ip a show dev ens3`, nous obtenons l'adresse IP 11.22.33.90/24
	2. C'est le truc par défaut
	3. Il y a marqué default : 11.22.33.1
	4. C'est ce que nous avons rentré dans `nameserver`


# Exercice 4
| Station | Adresse MAC       | Adresse IP  |
| ------- | ----------------- | ----------- |
| PC1     | 00:50:79:66:68:00 | 192.168.0.1 |
| PC2     | 00:50:79:66:68:01 | 192.168.0.2 |
| PC3     | 00:50:79:66:68:02 | 192.168.0.3 |
| PC4     | 00:50:79:66:68:03 | 192.168.0.4 |
| PC5     | 00:50:79:66:68:04 | 192.168.0.5 |
| PC6     | 00:50:79:66:68:05 | 192.168.0.6 |

Switch 1

| Adresse machine   | Port |
| ----------------- | ---- |
| 00:50:79:66:68:00 | 1    |
| 00:50:79:66:68:01 | 2    |
| 00:50:79:66:68:02 | 3    |
| 00:50:79:66:68:03 | 4    |
| 00:50:79:66:68:04 | 4    |
| 00:50:79:66:68:05 | 4    |
Switch 2

| Adresse machine   | Port |
| ----------------- | ---- |
| 00:50:79:66:68:00 | 1    |
| 00:50:79:66:68:01 | 2    |
| 00:50:79:66:68:02 | 3    |
| 00:50:79:66:68:03 | 4    |
| 00:50:79:66:68:04 | 4    |
| 00:50:79:66:68:05 | 4    |

# Exercice 5
- PC1 et PC3 ne peuvent plus communiquer car ils ne sont pas dans le même VLAN
- PC1 et PC4 ne peuvent plus communiquer far ils ne sont pas dans le même VLAN