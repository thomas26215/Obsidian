---
MOOC: "[[Autre]]"
Thème: Informatique
Sujet: Chiffrement - RSA
tags:
---

##### Génération des clés

1. Choisir 2 nombres premiers $p$ et $q$
2. Calculer $n=p*q$
3. Trouver fonction d'Euler $φ(n)=(p-1)(q-1)$. Représente le nombre d'entiers compris en 1 et $n$ qui sont premiers avec $n$
4. Calculer l'exposant de déchiffrement $d$ tel que $de≡1(modϕ(n))$
5. On doit trouver $e$ d'exposant de chiffrement $1<e<φ(n)$ tel que $d*e\equiv 1(\Phi(n))$. Autrement dit, il existe une $e\in\mathbb{Z}/n\mathbb{Z}, pgcd(e, \Phi(n)) = 1$

##### Clé de chiffrement et de déchiffrement

- On a la clé publique composée de $(n, e)$ avec $n$ le module de chiffrement et $e$ l'exposant de chiffrement
- On a la clé privée composée de $(n, d)$ avec $n$ le module de chiffrement et p l'exposant de déchiffrement

##### Chiffrer ou déchiffrer un message

- Nous pouvons crypter un message $m$ tel que $0\le m<n$ avec la formule $c\equiv m^e(mod\space n)$
- Nous pouvons décrypter le message chiffré $c$ grâce à la formule $m\equiv c^d(mod\space n)$

#### Vérification

$$C^d=(M^e)^d=M^{ed}$$ Or, $d$ est l'inverse de $l$ dans $\mathbb{Z}/\Phi(n)\mathbb{Z}$ donc : $$ed\equiv 1, \mathbb{Z}/\Phi(n)\mathbb{Z} ⇔ ed\equiv 1(mod\space \Phi(n)) ⇔ ed\equiv 1+k\Phi(n) ⇔ M^{ed}=M^{1+k\Phi(n)} \equiv1(mod\space n)$$
Or, d'après le [[Théorème d'Euler|protocole d'Euler]], $M^{\Phi(n)}\equiv 1(mod\space n)$ lorsque $pgcd(M, n) = 1$
Donc $M^{ed}M^{k\Phi(n)}\equiv M*(M^{\Phi(n)})^e\equiv M(mod\space n)$ ...
Finalement, $C^d\equiv M(mod\space n)$

