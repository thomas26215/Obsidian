---
MOOC: "[[Mathématiques]]"
Thématique: Arithmétique modulaire
tags:
---
Le **calcul modulaire** est une opération mathématique qui consiste à déterminer le reste d'une division euclidienne. C'est un concept fondamental en [[L'arithmétique modulaire|arithmétique modulaire]], qui est largement utilisé dans divers domaines des mathématiques, notamment la théorie des nombres et la cryptographie.

## Définition

Pour deux entiers $a$ et $b$ (où $b \neq 0$), le calcul modulaire s'écrit :

$$
a \mod b = r
$$

où $ r $ est le reste de la division de $a$ par $b$. On peut également exprimer cela en termes de congruence :

$$
a \equiv r \mod b
$$

Cela signifie que $a$ et $r$ laissent le même reste lorsqu'ils sont divisés par $b$.

## Méthodes de Calcul

### Méthode 1 : Division Euclidienne

Pour calculer $a \mod b$, on effectue la division euclidienne :

1. Divisez $a$ par $b$.
2. Le reste de cette division est le résultat du calcul modulaire.

**Exemple :** Pour calculer $123 \mod 10$:
- $123 \div 10 = 12$ (quotient)
- Reste : $123 - (12 \times 10) = 3$
- Donc, $123 \equiv 3 \mod 10$.

### Méthode 2 : Utilisation d'Horloges

Le calcul modulaire peut être illustré par l'exemple d'une horloge. Par exemple, si il est 23 heures et que vous ajoutez 8 heures :

$$
(23 + 8) \mod 24 = 7
$$

Ici, on utilise le modulo 24 pour les heures.

## Propriétés des Opérations Modulo

L'arithmétique modulaire permet d'effectuer des opérations telles que l'addition, la soustraction et la multiplication tout en restant dans le cadre du modulo :

- **Addition :**
  
$$
(A + B) \mod C = ((A \mod C) + (B \mod C)) \mod C
$$

- **Soustraction :**

$$
(A - B) \mod C = ((A \mod C) - (B \mod C)) \mod C
$$

- **Multiplication :**

$$
(A \times B) \mod C = ((A \mod C) \times (B \mod C)) \mod C
$$

## Applications

Le calcul modulaire est utilisé dans plusieurs domaines :

- **Cryptographie** : Les algorithmes comme RSA utilisent des opérations modulaires pour sécuriser les communications.
- **Théorie des nombres** : Il aide à résoudre des problèmes liés à la primalité et aux congruences.
- **Informatique** : Les opérations modulo sont couramment utilisées dans les algorithmes, notamment pour gérer les cycles dans les structures de données.

En résumé, le calcul modulaire est un outil puissant qui simplifie de nombreux problèmes mathématiques et informatiques en se concentrant sur les restes de divisions.

