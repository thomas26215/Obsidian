---
MOOC: "[[Mathématiques]]"
Thématique: 
tags:
---
Le **petit théorème de Fermat** est un résultat fondamental en arithmétique modulaire, énoncé pour la première fois par Pierre de Fermat dans une lettre à Frénicle de Bessy en 1640. Ce théorème stipule que si $p$ est un nombre premier et $a$ un entier qui n'est pas divisible par $p$, alors :

$$
a^{p-1} \equiv 1 \mod p
$$

Cela signifie que $a^{p-1} - 1$ est un multiple de $p$. Une formulation équivalente du théorème est que pour tout entier $a$, on a :

$$
a^p \equiv a \mod p
$$

Cela implique que la différence $a^p - a$ est également un multiple de $p$ pour tout entier $a$

## Histoire et Démonstration

Le petit théorème de Fermat a été démontré pour la première fois par le mathématicien suisse **Leonhard Euler** en 1736. Bien que Fermat lui-même n'ait pas fourni de preuve complète, son énoncé a été reconnu comme un des résultats majeurs en théorie des nombres. Euler, dans ses travaux, a formalisé et prouvé ce théorème, contribuant ainsi à son acceptation dans le domaine mathématique

## Applications

Le petit théorème de Fermat possède de nombreuses applications, notamment :

- **Cryptographie** : Il est utilisé dans des algorithmes de chiffrement comme RSA.
- **Théorie des nombres** : Il aide à déterminer la primalité et à analyser les propriétés des entiers.
- **Calculs modulo** : Il simplifie les calculs exponentiels dans le cadre des congruences.

## Exemple

Considérons un exemple simple avec $p = 7$ (un nombre premier) et $a = 3$ (qui n'est pas divisible par 7). Selon le petit théorème de Fermat :

$$
3^{7-1} = 3^6
$$

Calculons $3^6$:

$$
3^6 = 729
$$

Nous devons vérifier si $729 \equiv 1 \mod 7$. En divisant 729 par 7, nous trouvons :

$$
729 \div 7 = 104 \quad (\text{reste } 1)
$$

Donc, effectivement, $3^6 \equiv 1 \mod 7$, confirmant ainsi le petit théorème de Fermat. 

Ce théorème reste l'un des piliers de l'arithmétique moderne et continue d'être enseigné dans les cours de mathématiques avancées.
