# Relations asymptotiques

## a) $f_1(n) = n^2$, $f_2(n) = n^2 + 1$

La fonction $f_2(n) = n^2 + 1$ est équivalente à $f_1(n) = n^2$ pour des grandes valeurs de $n$, car le terme constant $+1$ devient négligeable. On a donc :

- Relation asymptotique : $f_1(n) = \Theta(f_2(n))$

**Conclusion :** $f_1(n) = \Theta(f_2(n))$

---

## b) $f_1(n) = n^2$, $f_2(n) = n^2 + n$

Dans ce cas, $f_2(n) = n^2 + n$ est dominé par $n^2$ pour des grandes valeurs de $n$. Le terme $n$ devient négligeable par rapport à $n^2$. On a donc :

- Relation asymptotique : $f_1(n) = \Theta(f_2(n))$

**Conclusion :** $f_1(n) = \Theta(f_2(n))$

$$lim_{n->+\infty}\frac{f1(n)}{f2(n)}=lim=\frac{n^2}{n^2+n}\frac{1}{1+\frac{1}{n}} = 1$$

---

## c) $f_1(n) = n^2$$f_2(n) = 3n^2 + 4n + 1$

Ici, $f_2(n)$ est une fonction quadratique avec des termes supplémentaires $4n$ et $1$. Toutefois, pour des grandes valeurs de $n$, le terme dominant est $3n^2$. On a donc :

- Relation asymptotique : $f_1(n) = \Theta(f_2(n))$

**Conclusion :** $f_1(n) = \Theta(f_2(n))$

$$lim_{n->+\infty}=\frac{f1(n)}{f2(n)}=lim=\frac{n^2}{3n^2+4n+1}=\frac{1}{3+\frac{4}{n}+\frac{1}{n}}=\frac{1}{3}$$

---

## d) $f_1(n) = 10n^2$, $f_2(n) = n^3$

Dans ce cas, $f_2(n) = n^3$ croît plus vite que $f_1(n) = 10n^2$ à mesure que $n$ devient grand. On a donc :

- Relation asymptotique : $f_1(n) = O(f_2(n))$ et $f_2(n) = \Omega(f_1(n))$

**Conclusion :** $f_1(n) = O(f_2(n))$, $f_2(n) = \Omega(f_1(n))$

$$lim_{n->+\infty}=\frac{f1(n)}{f2(n)}=lim=\frac{10n^2}{n^3}=\frac{10}{n}$$

---

## e) $f_1(n)$ et $f_2(n)$ sont des polynômes positifs de degré $d$ (coefficient de $n^d$ positif)

Si $f_1(n)$ et $f_2(n)$ sont des polynômes de même degré $d$, la relation entre les deux fonctions est déterminée par les coefficients des termes de plus haut degré. Comme les termes dominants sont de même ordre, on a :

- Relation asymptotique : $f_1(n) = \Theta(f_2(n))$

**Conclusion :** $f_1(n) = \Theta(f_2(n))$

---

## f) $f_1(n)$ est un polynôme de degré $d_1$ et $f_2(n)$ est un polynôme de degré $d_2$

Si $f_1(n)$ est un polynôme de degré $d_1$ et $f_2(n)$ est un polynôme de degré $d_2$, la relation entre les deux fonctions dépend des degrés. Si $d_1 = d_2$, la relation est $\Theta$, mais si $d_1 < d_2$, on a $f_1(n) = O(f_2(n))$, et si $d_1 > d_2$, on a $f_2(n) = O(f_1(n))$.

- Si $d_1 = d_2$, alors $f_1(n) = \Theta(f_2(n))$
- Si $d_1 < d_2$, alors $f_1(n) = O(f_2(n))$
- Si $d_1 > d_2$, alors $f_2(n) = O(f_1(n))$

**Conclusion :** La relation dépend des degrés $d_1$ et $d_2$.

