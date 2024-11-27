Une **classe de congruence modulo $n$** est un sous-ensemble des entiers $\mathbb{Z}$ qui peut être exprimé sous la forme :

$$
a + n\mathbb{Z} = \{ a + nk \; | \; k \in \mathbb{Z} \}
$$

où $a$ est un entier. Cela signifie que tous les entiers de cette classe sont congrus à $a$ modulo $n$.

### Exemples

- La classe $4 + 12\mathbb{Z}$ inclut les entiers de la forme :

$$
\{ 4 + 12k \; | \; k \in \mathbb{Z} \} = \{ ..., -8, 4, 16, 28, ... \}
$$

- La classe $16 + 12\mathbb{Z}$ est identique à la classe $4 + 12\mathbb{Z}$, car $16 - 4 = 12$, qui est un multiple de $12$.
  
- En revanche, la classe $3 + 12\mathbb{Z}$ est distincte de la classe $4 + 12\mathbb{Z}$.

### Représentants des Classes

Un entier $b$ est appelé **représentant** de la classe $a + n\mathbb{Z}$ si :

$$
b \equiv a \mod n
$$

Cela signifie que la différence $a - b$ est un multiple de $n$. Par exemple :

- L'entier $4$ est un représentant de la classe $4 + 12\mathbb{Z}$.
- L'entier $-7$ est également un représentant, car :

$$
4 - (-7) = 11, \quad et \quad 11 \equiv 0 \mod 12
$$

Cependant, l'entier $2$ n'est pas un représentant de cette classe, car :

$$
4 - 2 = 2, \quad et \quad 2 \neq 0 \mod 12
$$

### Choix des Représentants

Il est courant de choisir le représentant $b$ d'une classe $a + n\mathbb{Z}$ tel que :

$$
0 \leq b < n
$$

Cela est toujours possible en utilisant le reste de la division euclidienne de $a$ par $n$. Si on note $r$ le reste, alors :

$$
r = a - nq
$$

où $q$ est le quotient. Ainsi, on peut écrire :

$$
a - r = nq
$$

ce qui implique que :

$$
r \equiv a (mod n)
$$

### Ensemble des Classes de Congruence

Il existe exactement **$n$** classes de congruence modulo $n$, qui sont représentées par les entiers :

$$
0, 1, ..., n-1
$$

L'ensemble des classes de congruence modulo $n$ est noté :

$$
\mathbb{Z}/n\mathbb{Z} = [0, 1, ..., n-1]
$$

### Exemple pour Modulo 5

Pour illustrer, voici les classes de congruence modulo 5 :

- **Classe** $0 = {..., -10, -5, 0, 5, ...}$
- **Classe** $1 = {..., -9, -4, 1, 6, ...}$
- **Classe** $2 = {..., -8, -3, 2, 7, ...}$
- **Classe** $3 = {..., -7, -2, 3, 8, ...}$
- **Classe** $4 = {..., -6, -1, 4, 9, ...}$

Chaque classe contient tous les entiers qui ont le même reste lorsqu'ils sont divisés par $n = 5$. Par exemple :

- La classe contenant le nombre **2** inclut également **7** et **-3**, car ils ont tous le même reste lorsqu'ils sont divisés par **5**.

### Conclusion

Les classes de congruence modulo $n$ permettent d'organiser les entiers en groupes basés sur leurs restes lors de la division par un entier fixe. Cette structure est essentielle dans l'arithmétique modulaire et trouve des applications dans divers domaines mathématiques et informatiques.
