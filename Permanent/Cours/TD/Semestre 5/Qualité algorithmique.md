**Cours** : [[Permanent/Cours/Cours/Semestre 5/Qualité algorithmique|Qualité algorithmique]]

# 1. Relations asymptotiques

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



# 2. Simplification asymptotique
## a) $f(n) = 3n + 10$

Le terme dominant est $3n$, donc :

**Réponse :** $\Theta(n)$

---

## b) $f(n) = an + b$  avec $a > 0$

Le terme dominant est $an$, donc :

**Réponse :** $\Theta(n)$

---

## c) $f(n) = 3n^2 + 4n + 1$

Le terme dominant est $3n^2$, donc :

**Réponse :** $\Theta(n^2)$

---

## d) $f(n) = an^2 + bn + c$ avec $a > 0$

Le terme dominant est $an^2$, donc :

**Réponse :** $\Theta(n^2)$

---

## e) $f(n)$ est un polynôme positif de degré $d$ (coefficient de $n^d$ positif)

Le terme dominant est de degré $d$, donc :

**Réponse :** $\Theta(n^d)$

---

## f) $f(n, m) = 3n + 10m$

Les deux termes sont linéaires, donc on garde le maximum :

**Réponse :** $\Theta(n + m)$

---

## g) $f(n, m) = anm + bn + cm + d$ avec $a, b, c > 0$

Le terme dominant est $anm$ (produit croisé), donc :

**Réponse :** $\Theta(nm)$

---

## h) $f(n, m) = \dfrac{3n^2 + 4n + 1}{n + m + nm}$

### Analyse asymptotique :

- Numérateur : $3n^2 + 4n + 1 = \Theta(n^2)$
- Dénominateur : $n + m + nm = \Theta(nm)$ (car $nm$ domine)

Donc : $f(n, m) = \dfrac{\Theta(n^2)}{\Theta(nm)} = \Theta\left(\dfrac{n}{m}\right)$

**Réponse :** $\Theta\left(\dfrac{n}{m}\right)$


# 3) Changer la taille des données
## a) $f(n) = \log_2 n$

On utilise la propriété des logarithmes :  
$\log_2(4n) = \log_2 4 + \log_2 n = 2 + \log_2 n$

**Conclusion :** $f(4n) = f(n) + 2 \quad \Rightarrow \quad f(4n) = \Theta(f(n))$

---

## b) $f(n) = \sqrt{n}$

$\sqrt{4n} = \sqrt{4} \cdot \sqrt{n} = 2\sqrt{n}$

**Conclusion :** $f(4n) = 2f(n)$

---

## c) $f(n) = n$

$f(4n) = 4n = 4f(n)$

**Conclusion :** $f(4n) = 4f(n)$

---

## d) $f(n) = n^2$

$f(4n) = (4n)^2 = 16n^2 = 16f(n)$

**Conclusion :** $f(4n) = 16f(n)$

---

## e) $f(n) = n^3$

$f(4n) = (4n)^3 = 64n^3 = 64f(n)$

**Conclusion :** $f(4n) = 64f(n)$

---

## f) $f(n) = 2^n$

$f(4n) = 2^{4n} = (2^n)^4 = f(n)^4$

**Conclusion :** $f(4n) = f(n)^4$ (croissance exponentielle très rapide)

# 7) Petites et grandes boucles

## a) Boucle simple de 0 à $n$
- La boucle s'excute N fois

=> Ordre de temps : $O(N)$

## b) Boucle de $N$ à $0$ par pas de 2
- Nombre d'itérations environ $\frac{N}{2}$ fois

=> Ordre de temps : $O(N)$

## c) Boucles imbriquées
- Boucle extérieure fait $N$ itérations, boucle intérieure aussi
- Total : $N*N=N^2$

Ordre de temps : $O(N^2)$

## d) 
- Pour $I=1$ à $N$ : La boucle intérieure fait $I$ itérations
- Total : $1+2+3+...+N=\frac{N(N+1)}{2}$

=> Ordre de temps : $O(N^2)$

## e)
- Valeurs de $I$ : $1, 2, 4, 8, ..., \leq N$
- Nombre d'itérations : $log_2N$

=> Ordre de temps : $O(log\space N)$

## f)
- Valeurs de $I$ : $N, \frac{N}{2}, \frac{N}{4}, ..., 1$
- Nombre d'itérations : $log_2N$

=> Ordre de temps : $O(log\space N)$

## g)
- Pour chaque $I$, la boucle intérieure fait environ $log_2I$ itérations
- Total : $\sum_{I=1}^Nlog\space I = NlogN$

=> Ordre de temps : $O(NlogN)$

## h)
- Limite extérieure : $log_2N$ itérations (car $I$ multiplié par 2)
- Pour $I=1, 2, 4, ..., N$, la boucle effectue  $I$ incréments
- Total : $1+2+4+...+N=2N-1=O(N)$

=> Ordre de temps  : $O(N)$
