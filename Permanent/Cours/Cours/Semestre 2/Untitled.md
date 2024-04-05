---
MOOC: "[[Cours]]"
Ressource: "R2.05 : Réseaux"
Cours: "Cours 1 : Protocole Internet : routage et IPv6"
Date: 
tags: 
Complete: false
Learned: false
---
Quand un routeur reçoit un paquet, le routeur choisi vers quel routeur retransmettre le paquet entrant pour que celui-ci arrive à destination
- En IP (mode commuté) : Le choix est effectué indépendamment pour chaque paquet
- Choix effectué en se servant d'infos contenues dans table de routage
- Entrée d'une table de routage envoyées soit manuellement, soit automatiquement avec un algorithme de routage en se basant sur diffs critères (débit possible, disponibilité sur ligne, taux d'erreurs, nombre de noeurs intermédiaires)
Fonction d'un routeur :
- Transmission des paquets
- Mise à jour tables de routage

**Algorithme de sélection dans la table de routage**
⇒ Pour chaque paquet, chaque ligne est essayée successivement jusqu'à trouver une correspondance entre l'adresse IP destinataire et une adresse réseau de la colonne Destiantion


Classes d'algorithme de routage :
- Algorithme de routage fixe
- Algorithme de routage adaptifs : s'adapte aux modification de la topologie et, plus rarement, à celles du trafic automatiquement