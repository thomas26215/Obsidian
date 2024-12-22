---
MOOC: "[[Autre]]"
Thème: Informatique
Sujet: Chiffrement - RSA
tags:
---

La cryptographie RSA a été inventé par les 3 chercheurs Rivest, Shamir et Adleman
L'algorithme est connu de tous ; la difficulté réside dans la difficulté de factoriser de grands nombres entiers en produits de facteurs premiers

### Fonctionnement - Principe

1. Clé publique + clé privée crées par la même personne (qu'on nomm Alice)
2. Alice va donner à Bob sa clé publique
3. Bob chiffre son message grâce à la clé publique qu'Alice lui a envoyé.
   **Remarque** : Il ne peut plus lui-même déchiffrer son message
4. Alice déchiffre le message grâce à se clé privée

La spécificité est que la clé publique et la clé privée sont fabriquée simultanément ; il n'est pas possible de trouver la clé privée en ayant la clé publique : il faut déterminer les deux premiers nombre premier pour créer une de ces clés, et cela est très difficile car c'est mathématiquement très difficile de factoriser un grand nombre en produits d'entiers premiers

![[Algorithme de la clé RSA]]

![[Craquer une clé RSA]]

