# Chiffrement Affine

## Définition
Le **chiffrement affine** est un chiffrement par substitution mono-alphabétique, où chaque lettre d'origine est remplacée par une unique autre lettre. C'est un code simple à comprendre, mais l'un des plus faciles à casser.

## Fonction de Chiffrement
La fonction de chiffrement affine est définie par les paramètres $a$ et $k$ et va de l'ensemble $\mathbb{Z}/26\mathbb{Z}$ dans lui-même :

$$
C_{a,k} : \mathbb{Z}/26\mathbb{Z} \to \mathbb{Z}/26\mathbb{Z} \\
x \mapsto ax + k
$$

Pour tout $x \in \mathbb{Z}/26\mathbb{Z}$, $y = C_{a,k}(x)$ est le chiffré de $x$.

### Exemple
Pour les paramètres $a = 3$ et $k = 1$ :
- ${3,1}(0) = 1$
- $C_{3,1}(1) = 4$
- ...

---

# Déchiffrement

## Fonction Inverse
Pour déchiffrer, il faut exprimer $x$ en fonction de $y$ dans $\mathbb{Z}/26\mathbb{Z}$ :

$$
y = C_{a,k}(x) \Rightarrow y = ax + k \Rightarrow ax = y - k
$$

### Condition pour Déchiffrer
Il doit exister un entier $a'$ tel que :

$$
a' a \equiv 1 \pmod{26}
$$

Cela signifie que si l'inverse de $a$ existe, on peut déchiffrer :

$$
x = a' (y - k)
$$

où $a' = a^{-1}$ est l'inverse de $a$ dans $\mathbb{Z}/26\mathbb{Z}$.

## Fonction de Déchiffrement
La fonction de déchiffrement affine est donnée par :

$$
D_{a,k} : \mathbb{Z}/26\mathbb{Z} \to \mathbb{Z}/26\mathbb{Z} \\
x \mapsto a^{-1} x - a^{-1} k
$$

Si l'inverse de $a$ existe, alors la fonction de déchiffrement est la bijection réciproque de la fonction de chiffrement, ce qui implique que :

$$
D_{a,k}(C_{a,k}(x)) = x
$$
