---
MOOC: "[[Autre]]"
Sujet: Informatique
Type: Chiffrement - RSA
tags:
---
Actuellement, il est très difficile de cracker la clé publique à partir de la clé privée, en raison des propriétés mathématiques sur lesquelles repose le système RSA
La clé publique comprend le module de chiffrement (n) et l'exosant de chiffrement (e). Cependant, il est très difficile de retrouver l'exposant de déchiffrement (d) et les facteurs premiers utiliséspour générer les clés à partir de la clé publique

Si Charles connaît $(n, e), C$
Les verrous pour Charles sont $p$ et $q$ car ils sont très grands donc il ne peut pas factoriser ([[Algorithme de la clé RSA]])

Par manque de puissance de calcul, il est impossible de cracker une clé. Il faudrait un algorithme bien plus performant ou bien un [[Ordinateur quantique]] ce qui pourrait mettre en danger les communications actuelles