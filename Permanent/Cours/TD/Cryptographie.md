---
MOOC: "[[Cours]]"
Ressource: "R3.09 : Cryptographie"
Cours: "TD 1 : Cryptographie"
Date: 
tags: 
Complete: false
Learned: false
---
## Exercice 6
### Question 1
**Question a**
> XVPIXG

**Question b**
> Les messages chiffrés et les clés sont des séquences de lettres de longueur k, utilisant l'alphabet {A, B, ..., Z}.Pour déchiffrer un message :
> 
> 1. Soit $c = y_1y_2...y_k$ le message chiffré
> 2. Soit $n = n_1n_2...n_k$ la clé
> 
> Le message déchiffré $m = x_1x_2...x_k$ est obtenu comme suit :Pour chaque position i (de 1 à k) :
> - Localiser la lettre $n_i$ de la clé dans la première colonne du tableau de Vigenère
> - Sur cette ligne, trouver la lettre $y_i$ du message chiffré
> - La lettre $x_i$ du message déchiffré est celle qui apparaît en haut de la colonne contenant $y_i$

>En d'autres termes, pour chaque lettre $y_i$ du message chiffré, on cherche dans le tableau de Vigenère la colonne où $y_i$ apparaît sur la ligne commençant par $n_i$. La lettre $x_i$ du message déchiffré est alors celle qui se trouve en tête de cette colonne.

**Question c**
> Sogris

### Question 2

**Question a**
>Table d'addition modulo 26

**Question b**
> **Message chiffré :** Pour chaque lettre de mon mot clair, je convertis la lettre en chiffre suivant le tableau $(A=0, B=1, ..., Z=25)$, je fais de même pour chaque lettre de ma clé correspondant à la lettre du mot clair, ainsi, ma lettre du mot clair donne m, ma lettre de ma clé donne $k$, et ma lettre chiffrée c s'obtient par $c = (m + k)$ mod 26, que je reconvertis ensuite en lettre.
> 
> **Message déchiffré :** Pour chaque lettre de mon mot chiffré, je convertis la lettre en chiffre suivant le tableau $(A=0, B=1, ..., Z=25)$, je fais de même pour chaque lettre de ma clé correspondant à la position de la lettre chiffrée, ainsi, ma lettre du mot chiffré donne c, ma lettre de ma clé donne $k$, et ma lettre déchiffrée m s'obtient par $m = (c - k + 26)$ mod 26, que je reconvertis ensuite en lettre.

**Question c**


## Exercice 7
### Question 1
> Il est impossible de déchiffrer ce message car si il est bien mis en oeuvre, il est théoriquement impossible de le casse car la clé est aussi longue que le message lui-même, chaque charactère de la clé est choisi de manière aléatoire et la clé n'est utilisée qu'une seule fois, d'uù le nom jetable

### Question 2
#### Avantages
> - **Sécurité théorique absolue** : C'est le seul système de chiffrement prouvé comme étant inconditionnellement sûr
> -**Simplicité** : Le processus de chiffrement et de déchiffrement est relativement simple à comprendre et à mettre en œuvre

#### Inconvénients
>- **Gestion des clés** : La nécessité d'avoir une clé aussi longue que le message et de ne l'utiliser qu'une seule fois pose des problèmes logistiques importants
>- **Distribution sécurisée des clés** : Les deux parties doivent échanger la clé de manière sûre, ce qui peut être difficile dans certains contextes
>- **Génération de clés véritablement aléatoires** : Il est crucial mais difficile de générer des clés parfaitement aléatoires en grande quantité
>- **Utilisation unique** : Chaque clé ne peut être utilisée qu'une seule fois, ce qui limite son utilisation pratique pour des communications fréquentes
>- **Volume de données** : Le système nécessite de stocker et de gérer un volume important de clés, égal au volume des messages à échanger