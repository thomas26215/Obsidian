---
MOOC: "[[Cours]]"
Ressource: "R2.05 : Réseaux"
Cours: "Cours 6 : VLAN"
Date: 
tags: 
Complete: false
Learned: false
---
Un réseau LAN avec des sous-réseaux est simple à mettre en place, cependant, il y a un manque de sécurité et il y a un traffic important sur toutes les machines
→ Une meilleure isolation en utilisant les sous-réseaux locaux virtuels en utilisant un seul commutateur (VLAN => *virtual local area Network*)

Attention, le nombre de VLAN est limité à 4096 ($2^{12}$). Pour détenir une plus grande taille, il peut être nécessaire d'utililser un [[XVLAN]] (notamment pour les distributeur d'adresses comme Orange, Free).
Le protocole Ethernet utliisé est 802.1Q

# VLAN
Switch 2-3 :
- Séparation des sous-réseaux au nvieau des ports (broadcast et sécurité)
- Un seul matériel est utilisé pour jouer rôle de commutateur ET routeur
- Grande flexibilit"