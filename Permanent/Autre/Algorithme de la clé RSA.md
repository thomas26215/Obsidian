---
MOOC: "[[Autre]]"
Sujet: Informatique
Type: Chiffrement - RSA
tags:
---
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