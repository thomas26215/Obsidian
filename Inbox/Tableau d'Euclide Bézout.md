
Le tableau de Bézout est utile pour calculer le $pgcd$ de deux nombres. Il faut savoir :
- $a$ La premier nombre du $pgcd$ Pour chaque ligne suivante, on récupère le b précédant
- $b$ Le deuxième nombre du $pgcd$. Pour chaque ligne suivante, on récupère le reste précédant
- $r$ désigne le reste
- $q$ désigne le quotient

Il permet également de trouver deux entiers relatifs $u$ et $v$ où $au+bv=pgcd(a,b)$

| etape i | a    | b   | r   | q   | u   | v   |
| ------- | ---- | --- | --- | --- | --- | --- |
| -1      |      |     |     |     | 1   | 0   |
| 0       |      |     |     |     | 0   | 1   |
| 1       | 1236 | 96  | 84  | 12  | 1   | -12 |
| 2       | 96   | 84  | 12  | 1   | -1  | 13  |
| 3       | 84   | 12  | 0   | 7   |     |     |
Ici, on a $u=-1$ et $v=13$ donc $1236*(-1)+13*96=12$

---
**Question :**
1. Faire le tableau de Bézout à partir de $pgcd(1236, 96)$
2. En déduire les deux entiers relatifs où $ab+uv=pgcd(a,b)$ et vérifier 