![[TD2Arithmetique.pdf]]

## Exercice 1

Exercice 1

> Les classes de congruence de Z/6Z sont : {0̄, 1̄, 2̄, 3̄, 4̄, 5̄}

Exercice 3

> Diviseurs de zéro : 2̄, 3̄, 4̄
> Éléments inversibles : 1̄, 5̄

Exercice 4

> - 4̄4 × 7̄7 = 2̄ × 5̄ = 4̄
> - 1̄13 + 2̄013 = 5̄ + 1̄ = 0̄

## Exercice 2

| a   | b   | r   | q   | u    | v   |
| --- | --- | --- | --- | ---- | --- |
| 143 | 100 | 43  | 1   | 1    | -1  |
| 100 | 43  | 14  | 2   | -2   | 3   |
| 43  | 14  | 1   | 3   | 7    | -10 |
| 14  | 1   | 0   | 14  | -100 | 143 |

Question 1

> Le pgcd(143, 100) est le dernier reste non nul dans la colonne r, soit 1

Question 2

> On lit directement les valeurs de u et v sur la ligne où r = 1 :  
> u = 7 et v = -10  
> Donc : 143 × 7 + 100 × (-10) = 1

Question 3

> L'inverse de 100 modulo 143 est la valeur de v sur la ligne où r = 1, soit -10. Cependant, nous devons exprimer cette valeur dans Z/143Z, donc : $-10 ≡ 133 (mod 143)$

## Exercice 3

### Calcul du pgcd de 114 et 33

1. **Algorithme d'Euclide :**

    - 114÷33=3114÷33=3 reste 1515
    - 33÷15=233÷15=2 reste 33
    - 15÷3=515÷3=5 reste 00

    Le dernier reste non nul est 3, donc pgcd(114,33)=3pgcd(114,33)=3.

2. **Identité de Bézout :**On remonte les calculs pour trouver un couple (u,v)(u,v) tel que 114u+33v=3114u+33v=3.

    - 3=33−2×153=33−2×15
    - 15=114−3×3315=114−3×33

    En substituant :

    - 3=33−2×(114−3×33)3=33−2×(114−3×33)
    - 3=7×33−2×1143=7×33−2×114

    Donc, un couple possible est u=−2u=−2, v=7v=7.

3. **Inverse de 33 dans Z/114Z :**Comme le pgcd(114, 33) n'est pas égal à 1, l'inverse de 33 dans Z/114Z n'existe pas.

### Calcul du pgcd de 114 et 35

1. **Algorithme d'Euclide :**

    - 114÷35=3114÷35=3 reste 99
    - 35÷9=335÷9=3 reste 88
    - 9÷8=19÷8=1 reste 11
    - 8÷1=88÷1=8 reste 00

    Le dernier reste non nul est 1, donc pgcd(114,35)=1pgcd(114,35)=1.

2. **Identité de Bézout :**On remonte les calculs pour trouver un couple (u,v)(u,v) tel que 114u+35v=1114u+35v=1.

    - 1=9−81=9−8
    - 8=35−3×98=35−3×9
    - Substituer pour obtenir :
        - 1=(9)−(35−3×(9))=4×(9)−(35)1=(9)−(35−3×(9))=4×(9)−(35)
        - Substituer encore :
        - 9=(114−3×(35))9=(114−3×(35))
        - Finalement :
        - 1=(4×(114)−(12×(35)))−(35)1=(4×(114)−(12×(35)))−(35)
        - Simplifier :
        - 1=(4×(114))−(13×(35))1=(4×(114))−(13×(35))

    Donc, un couple possible est u=4u=4, v=−13v=−13.

3. **Inverse de 35 dans Z/114Z :**Puisque le pgcd(114, 35) est égal à 1, l'inverse de 35 dans Z/114Z existe et est donné par la valeur de v modulo n. Ainsi, l'inverse est :−13≡101(mod114)−13≡101(mod114).

L'inverse de 35 dans Z/114Z est donc 101ˉ101ˉ.

## Exercice 4

1. Coder la lettre W :
   W correspond à x = 22
   f(22) = 9 × 22 + 8 = 206
   206 ≡ 24 (mod 26)
   24 correspond à la lettre Y
   Donc, W est codée par Y.

2. Détermination de la fonction de décodage :

    (a) Montrer que pour tous nombres entiers relatifs x et j, on a :
    9x ≡ j (mod 26) ⇔ x ≡ 3j (mod 26)

    Pour cela, nous allons utiliser l'algorithme d'Euclide étendu pour trouver l'inverse de 9 modulo 26 :

    | q   | r   | u   | v   |
    | --- | --- | --- | --- |
    | -   | 26  | 1   | 0   |
    | -   | 9   | 0   | 1   |
    | 2   | 8   | 1   | -2  |
    | 1   | 1   | -1  | 3   |
    | 8   | 0   | 9   | -26 |

    L'inverse de 9 modulo 26 est 3.

    Donc, si 9x ≡ j (mod 26), alors en multipliant les deux côtés par 3 :
    3 \* 9x ≡ 3j (mod 26)
    x ≡ 3j (mod 26)

    Réciproquement, si x ≡ 3j (mod 26), alors en multipliant par 9 :
    9x ≡ 9 \* 3j ≡ j (mod 26)

    Ainsi, l'équivalence est démontrée.

    (b) En déduire la fonction de décodage f⁻¹ :

    Partant de y ≡ 9x + 8 (mod 26)
    y - 8 ≡ 9x (mod 26)
    3(y - 8) ≡ 3 \* 9x ≡ x (mod 26)
    3y - 24 ≡ x (mod 26)
    3y + 2 ≡ x (mod 26) (car -24 ≡ 2 (mod 26))

    Donc f⁻¹(y) = 3y + 2 (mod 26)

    (c) Décoder la lettre L :
    L correspond à y = 11
    f⁻¹(11) = 3 × 11 + 2 = 35
    35 ≡ 9 (mod 26)
    9 correspond à la lettre J

    Donc, L est décodée par J.

## Exercice 5

1. Coder le mot INFINI :

I (8) : f(8) = 11 × 8 + 1 = 89 ≡ 11 (mod 26) → L
N (13) : f(13) = 11 × 13 + 1 = 144 ≡ 14 (mod 26) → O
F (5) : f(5) = 11 × 5 + 1 = 56 ≡ 4 (mod 26) → E
I (8) : f(8) = 11 × 8 + 1 = 89 ≡ 11 (mod 26) → L
N (13) : f(13) = 11 × 13 + 1 = 144 ≡ 14 (mod 26) → O
I (8) : f(8) = 11 × 8 + 1 = 89 ≡ 11 (mod 26) → L

INFINI est codé en LOELOIL

2. Déterminer la fonction de déchiffrage f⁻¹ :

Nous devons trouver l'inverse de 11 modulo 26. Utilisons l'algorithme d'Euclide étendu :

| q   | r   | u   | v   |
| --- | --- | --- | --- |
| -   | 26  | 1   | 0   |
| -   | 11  | 0   | 1   |
| 2   | 4   | 1   | -2  |
| 2   | 3   | -2  | 5   |
| 1   | 1   | 3   | -7  |
| 3   | 0   | -11 | 26  |

L'inverse de 11 modulo 26 est -7, qui est équivalent à 19 modulo 26.

Partant de y ≡ 11x + 1 (mod 26)
y - 1 ≡ 11x (mod 26)
19(y - 1) ≡ 19 × 11x ≡ x (mod 26)
19y - 19 ≡ x (mod 26)
19y + 7 ≡ x (mod 26) (car -19 ≡ 7 (mod 26))

Donc f⁻¹(y) = 19y + 7 (mod 26)

3. Décoder le message XAZXZSBC :

X (23) : f⁻¹(23) = 19 × 23 + 7 = 444 ≡ 2 (mod 26) → C
A (0) : f⁻¹(0) = 19 × 0 + 7 = 7 ≡ 7 (mod 26) → H
Z (25) : f⁻¹(25) = 19 × 25 + 7 = 482 ≡ 14 (mod 26) → O
X (23) : f⁻¹(23) = 19 × 23 + 7 = 444 ≡ 2 (mod 26) → C
Z (25) : f⁻¹(25) = 19 × 25 + 7 = 482 ≡ 14 (mod 26) → O
S (18) : f⁻¹(18) = 19 × 18 + 7 = 349 ≡ 11 (mod 26) → L
B (1) : f⁻¹(1) = 19 × 1 + 7 = 26 ≡ 0 (mod 26) → A
C (2) : f⁻¹(2) = 19 × 2 + 7 = 45 ≡ 19 (mod 26) → T

Le message décodé est CHOCOLAT.

## Exercice 6

1.  Démonstration du système d'équations :

    - Pour E (4) codé par E (4) : f(4) = 4a + b ≡ 4 (mod 26)
    - Pour J (9) codé par N (13) : f(9) = 9a + b ≡ 13 (mod 26)
      Ces équations correspondent directement au système donné.

2.  (a) Soustrayons la première équation de la seconde :
    5a ≡ 9 (mod 26)
    Multiplions les deux côtés par 21 (inverse de 5 mod 26) :
    a ≡ 21 \* 9 ≡ 7 (mod 26)

    (b) Substituons a = 7 dans 4a + b ≡ 4 (mod 26) :
    28 + b ≡ 4 (mod 26)
    b ≡ 2 (mod 26)
    Donc f(x) = 7x + 2

    (c) Pour démontrer 7x ≡ z (mod 26) ⇔ x ≡ 15z (mod 26) :
    Multiplions les deux côtés par 15 (inverse de 7 mod 26) :
    15 \* 7x ≡ 15z (mod 26)
    x ≡ 15z (mod 26)
    La réciproque se démontre de la même manière.

    (d) Pour trouver f⁻¹(y) :
    y ≡ 7x + 2 (mod 26)
    y - 2 ≡ 7x (mod 26)
    15(y - 2) ≡ x (mod 26)
    15y - 30 ≡ x (mod 26)
    15y + 22 ≡ x (mod 26)
    Donc f⁻¹(y) = 15y + 22

    (e) Décodage du message JW P N W M RCF W M Y :
    J (9) → B (1)
    W (22) → O (14)
    P (15) → N (13)
    N (13) → J (9)
    W (22) → O (14)
    M (12) → U (20)
    R (17) → R (17)
    C (2) → A (0)
    F (5) → T (19)
    W (22) → O (14)
    M (12) → U (20)
    Y (24) → S (18)

        Le message décodé est : BON JOUR A TOUS

## Exercice 7

## Exercice 8

1. $77 = 7 × 11$ (décomposition en facteurs premiers)
2. $φ(77) = φ(7) × φ(11) = 6 × 10 = 60$
3. Théorème d'Euler pour $a = 9$ et $n = 77$ :
   $$9^{60} \equiv 1 \pmod{77}$$

4. Division euclidienne de $125$ par $φ(77) = 60$ :
   $125 = 2 × 60 + 5$

5. Calcul de $9^{125} (mod 77)$ :
   $$9^{125} \equiv 9^{2×60+5} \equiv (9^{60})^2 × 9^5 \equiv 1^2 × 9^5 \equiv 9^5 \pmod{77}$$
   $$9^5 = 59049 \equiv 67 \pmod{77}$$

Donc, $$9^{125} \equiv 67 \pmod{77}$$

## Exercice 9

• $100^{193} (mod 291)$:
$φ(291) = φ(3) × φ(97) = 2 × 96 = 192$
$193 = 1 × 192 + 1$
$$100^{193} \equiv 100^{192+1} \equiv 100^{192} × 100 \equiv 1 × 100 \equiv 100 \pmod{291}$$

• $11^{300} (mod 119)$:
$φ(119) = φ(7) × φ(17) = 6 × 16 = 96$
$300 = 3 × 96 + 12$
$$11^{300} \equiv 11^{3×96+12} \equiv (11^{96})^3 × 11^{12} \equiv 1^3 × 11^{12} \equiv 11^{12} \pmod{119}$$
$$11^{12} \equiv 64 \pmod{119}$$

• $190^{3205} (mod 187)$:
$φ(187) = φ(11) × φ(17) = 10 × 16 = 160$
$3205 = 20 × 160 + 5$
$$190^{3205} \equiv 3^{20×160+5} \equiv (3^{160})^{20} × 3^5 \equiv 1^{20} × 3^5 \equiv 3^5 \pmod{187}$$
$$3^5 \equiv 56 \pmod{187}$$

## Exercice 10

Pour $a = 9$ et $n = 85$:
$φ(85) = φ(5) × φ(17) = 4 × 16 = 64$
L'inverse de $e = 5$ dans $Z/64Z$ est $d = 13$ car $5 × 13 ≡ 1 (mod 64)$
Calculons $a^(e×d)$ et $(a^e)^d$ dans $Z/85Z$:

$$9^{(5×13)} \equiv 9^{65} \equiv 9 \pmod{85}$$
$$(9^5)^{13} \equiv 9^{65} \equiv 9 \pmod{85}$$

## Exercice 11

1. Dans le protocole RSA, l'inverse d de e dans $Z/φ(n)Z$ existe toujours et peut être calculé pour les raisons suivantes :

- e est choisi de manière à être premier avec φ(n). Cela signifie que $PGCD(e, φ(n)) = 1$.
- Lorsque deux nombres sont premiers entre eux, il existe toujours un inverse modulaire.
- Pour calculer d, on utilise l'algorithme d'Euclide étendu. Cet algorithme permet de trouver deux entiers m et n tels que :

    $e × d + m × φ(n) = 1$

    Cela équivaut à dire que : $e × d ≡ 1 (mod φ(n))$

    Ainsi, d est l'inverse modulaire de e modulo $φ(n)$.

2. Pour montrer que $x^d (mod n)$ permet de retrouver $m$, utilisons le théorème fondamental du RSA :

Soit m le message original,$x = m^e (mod n)$ le message chiffré, et $d$ l'exposant de déchiffrement.

$x^d ≡ (m^e)^d ≡ m^{ed} (mod n)$

Or, par construction de $d$, nous avons :
$ed ≡ 1 (mod φ(n))$

Cela signifie qu'il existe un entier $k$ tel que :
$ed = 1 + k × φ(n)$

Donc :
$x^d ≡ m^(1 + k × φ(n)) ≡ m × (m^{φ(n)})^k (mod n)$

D'après le théorème d'Euler, pour tout m premier avec $n$ :
$m^φ(n) ≡ 1 (mod n)$

Ainsi :
$x^d ≡ m × 1^k ≡ m (mod n)$

## Exercice 12 (Chiffrement/Déchiffrement RSA)

1. Pour chiffrer $M = 100$ avec la clé publique $(319, 11)$, on calcule :
   $$ C ≡ M^e (mod n)≡ 100^{11} (mod 319)≡ 263 (mod 319)$$

2. Pour calculer $d$, nous devons trouver $φ(n)$. Comme $$319 = \Phi(11) × \Phi(29), \Phi(319) = 10 × 28 = 280.$$
   Nous cherchons $d$ tel que $ed ≡ 1 (mod φ(n))$, soit $11d ≡ 1 (mod 280)$.
   On trouve $$d = 51 car 11 × 51 = 561 ≡ 1 (mod 280)$$

3. Pour déchiffrer C = 133 avec d = 51 :

    $$
    M ≡ C^d (mod n)
       M ≡ 133^51 (mod 319)
       M ≡ 12 (mod 319)
    $$

4. Le message codé $625$ ne peut pas résulter d'un codage avec la clé publique ou privée car $625 > 319$. Tous les messages chiffrés doivent être inférieurs à $n$.

## Exercice 13 (Cryptographie RSA et authentification)

## Calcul des clés privées

Pour déterminer les clés privées du professeur et du secrétariat, nous devons d'abord calculer les valeurs de $n$ et $\phi(n)$ pour chaque clé publique.

### Clé publique du professeur : (55, 3)

1. **Calcul de $\phi(n)$** :

    - $n = 55$ peut être factorisé en $p = 5$ et $q = 11$.
    - Donc, $\phi(55) = (5-1)(11-1) = 4 \times 10 = 40$.

2. **Calcul de la clé privée $d$** :
    - Nous devons trouver $d $tel que $d \cdot e \equiv 1 \mod \phi(n)$, c'est-à-dire $d \cdot 3 \equiv 1 \mod 40$.
    - En utilisant l'algorithme d'Euclide étendu, nous trouvons que $d = 27$.

Ainsi, la clé privée du professeur est **(27, 55)**.

### Clé publique du secrétariat : (33, 3)

1. **Calcul de \phi(n)$** :

    - $n = 33 $peut être factorisé en $p = 3$ et $q = 11$.
    - Donc, $\phi(33) = (3-1)(11-1) = 2 \times 10 = 20$.

2. **Calcul de la clé privée $d$** :
    - Nous devons trouver $d$ tel que $d \cdot e \equiv 1 \mod \phi(n)$, c'est-à-dire $d \cdot 3 \equiv 1 \mod 20$.
    - En utilisant l'algorithme d'Euclide étendu, nous trouvons que $d = 7$.

Ainsi, la clé privée du secrétariat est **(7, 33)**.

## Chiffrement de la note

Pour chiffrer la note avec la clé RSA du secrétariat :

- **Message clair** : 12
- **Clé publique du secrétariat** : (33, 3)

Le message chiffré $C$ est calculé par :

$$
C = M^e \mod n
$$

Donc :

$$
C = 12^3 \mod 33
$$

Calculons cela :

$$
12^3 = 1728
$$

$$
1728 \mod 33 = 12
$$

Le message chiffré correspondant à la note **12** est donc **12**.

## Authentification du message

Pour signer la note avec sa clé privée et chiffrer le résultat avec la clé RSA du secrétariat :

1. **Signature avec la clé privée du professeur** :
    - Utilisons sa clé privée (27, 55).
    - Le message à signer est donc :

$$
S = M^d \mod n
$$

Pour le message clair de **12** :

$$
S = 12^{27} \mod 55
$$

Calculons cela. Pour simplifier le calcul, nous pouvons réduire les puissances modulo à chaque étape.

2. **Chiffrement de la signature** avec la clé publique du secrétariat (33, 3):

Nous devons maintenant chiffrer cette signature avec :

$$
C' = S^{e'} \mod n'
$$

où $e' = 3$et $n' = 33$$.

### Note correspondante

Le secrétariat reçoit le message chiffré correspondant à la signature. Pour retrouver le message clair correspondant à ce chiffre reçu (23), nous devons déchiffrer ce chiffre avec la clé privée du secrétariat.

Utilisons sa clé privée (7, 33):

$$
M' = C'^{d'} mod n'
$$

Calculons cela pour retrouver le message clair.

En résumé :

- La clé privée du professeur est **(27, 55)**.
- La clé privée du secrétariat est **(7, 33)**.
- Le message chiffré correspondant à la note **12** est également **12**.
- Pour déchiffrer le chiffre reçu (23), on appliquera les calculs ci-dessus pour retrouver le message original.


## Exercice 14 (Connaître p et q c'est connaître φ(n))

1. $φ(n) = (p-1)(q-1) = pq - p - q + 1 = n - (p + q) + 1$

2. $pq = n$
   $p + q = n - φ(n) + 1$
   On peut résoudre ce système d'équations du second degré pour trouver p et q.



$$\begin{align*} q = \frac{n}{p} \\ p=\frac{n}{q}=n-\Phi(n)+1 \\ p^2-(n-\Phi(n)+1)p+n=0 \end{align*} $$


3. Pour $n = 17063$ et $φ(n) = 16800$ :
   $p + q = 17063 - 16800 + 1 = 264$
   $pq = 17063$
   On résout : $p^2 - 264p + 17063 = 0$
   $p = 131 ou p = 133$
   Donc ${p, q} = {131, 133}$

## Exercice 15 (Attaque RSA par module commun)

Comme eA et eB sont premiers entre eux, il existe u et v tels que :
ueA + veB = 1 (théorème de Bézout)

On a :
$cA^u × cB^v ≡ (m^eA)^u × (m^eB)^v ≡ m^(ueA + veB) ≡ m^1 ≡ m (mod n)$

Ainsi, Oscar peut calculer m en trouvant u et v (par l'algorithme d'Euclide étendu) et en calculant $cA^u × cB^v mod n$.

## Exercice 16

Exercice 1

> Les éléments inversibles de taille $\Phi(7)=6$ sont $\{\bar{1}, \bar{2}, \bar{3}, \bar{4}, \bar{5}, \bar{6}\}$

Exercice 2

> $<2>=\{\bar{1}, \bar{2}, \bar{4}\}$ > $<3>=\{\bar{1}, \bar{3}, \bar{2}, \bar{6}, \bar{4}, \bar{5}\}$ > $\#<2> != \Phi(7)$ > $\#<3> != \Phi(7)$

Exercice 3

> $(\mathbb{Z}/9\mathbb{Z})= \{\bar{1}, \bar{2}, \bar{4}, \bar{5}, \bar{7}, \bar{8}\}$ sont les éléments inversibles de taille $\Phi(9)=\Phi(3^2)=(3-1)3=6$ > $<2>=\{\bar{1}, \bar{2}, \bar{4}, \bar{8}, \bar{7}, \bar{5}\}$ > $<4>=\{\bar{1}, \bar{4}, \bar{7}\}$ > $<7>=\{\bar{1}, \bar{7}, \bar{4}\} = <4>$
>
> $<2>$ est un générateur de $(\mathbb{Z}/9\mathbb{Z})= \{\bar{1}, \bar{2}, \bar{4}, \bar{5}, \bar{7}, \bar{8}\}$

## Exercice 17

Exercice 2

> $<3>= \{1, 3, 9, 7\}$ > $<7>= \{1, 7, 9, 3\}$ > $<9>= \{1, 9\}$ > $<11>= \{1, 11\}$ > $<13>= \{1, 13, 9, 17\}$ > $<17>= \{1, 17, 9,13\}$ > $<19>= \{1, 19\}$

Exercice c

> Il n'y a pas de générateur donc le groupe n'est pas cyclique

## Exercice 18

1. Alice : $x_A=7$
2. Bob : $x_B=4$
3. Alice : $k_A=g^
