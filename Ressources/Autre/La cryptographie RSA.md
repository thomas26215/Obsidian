La cryptographie RSA a été inventé par les 3 chercheurs Rivest, Shamir et Adleman
L'algorithme est connu de tous ; la difficulté réside dans la difficulté de factoriser de grands nombres entiers en produits de facteurs premiers

### Fonctionnement - Principe
1. Clé publique + clé privée crées par la même personne (qu'on nomm Alice)
2. Alice va donner à Bob sa clé publique
3. Bob chiffre son message grâce à la clé publique qu'Alice lui a envoyé.
   **Remarque** : Il ne peut plus lui-même déchiffrer son message
4. Alice déchiffre le message grâce à se clé privée

La spécificité est que la clé publique et la clé privée sont fabriquée simultanément ; il n'est pas possible de trouver la clé privée en ayant la clé publique : il faut déterminer les deux premiers nombre premier pour créer une de ces clés, et cela est très difficile car c'est mathématiquement très difficile de factoriser un grand nombre en produits d'entiers premiers
### L'alogrithme
##### Génération des clés
1. Choisir 2 nombres premiers $p$ et $q$
2. Calculer $n=p*q$
3. Trouver fonction d'Euler $φ(n)=(p-1)(q-1)$. Représente le nombre d'entiers compris en 1 et $n$ qui sont premiers avec $n$
4. On doit trouver $e$ d'exposant de chiffrement $1<e<φ(n)$ tel que $d*e\equiv 1(φ(n))$
##### Clé de chiffrement et de déchiffrement
- On a la clé publique composée de $(n, e)$ avec $n$ le module de chiffrement et $e$ l'exposant de chiffrement
- On a la clé publique composée de $(n, p)$ avec $n$  le module de chiffrement et p l'exposant de déchiffrement
##### Chiffrer ou déchiffrer un message
- Nous pouvons crypter un message $m$ tel que $0\le m<n$ avec la formule $m^e\equiv c(n)$
- Nous pouvons décrypter le message chiffré $c$ grâce à la formule $c^d\equiv m(n)$

### Méthode pour craquer une clé
Actuellement, il est très difficile de cracker la clé publique à partir de la clé privée, en raison des propriétés mathématiques sur lesquelles repose le système RSA
La clé publique comprend le module de chiffrement (n) et l'exosant de chiffrement (e). Cependant, il est très difficile de retrouver l'exposant de déchiffrement (d) et les facteurs premiers utiliséspour générer les clés à partir de la clé publique
Par manque de puissance de calcul, il est impossible de cracker une clé. Il faudrait un algorithme bien plus performant ou bien un [[Ordinateur quantique]] ce qui pourrait mettre en danger les communications actuelles