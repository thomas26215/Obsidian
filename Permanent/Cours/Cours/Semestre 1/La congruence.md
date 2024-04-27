---
MOOC: "[[Cours]]"
Ressource: "R2.09 : Mathématiques"
Cours: 
Date: 
tags: 
Complete: false
Learned: false
---
# Le principe de congruence
## La base
$a\equiv b(mod\space n)$ ⇔ $a=b+nk, k\in\Z$ et $q$ quelconque
$a\equiv b(mod\space n)$ se lit a congrue à b module n
$a\equiv b(mod\space n)$ ⇔ $n|(a-b)$

Il y a quelques astuces pour trouver plus facilement la congruence :
1. Vérifier que le nombre peut être simplifié indépendamment
   ($47*10\equiv 2*0\equiv0(mod\space5)$)
2. Vérifier si la puissance peut être divisée en plusieurs puissances
   ($2^{k+1}\equiv2^k*2$)
3. Vérifier si la décomposition de la puissance peut aider
   ($2^{40}\equiv2^{2*20}\equiv(2^2)^{20}\equiv1^{20}\equiv1(mod\space5)$)

## Propriétés
Si $a\equiv b(mod\space n) ⇔ \exists k\in \Z, a=b+kn$ 

On suppose $a\equiv b(mod\space n)$ et $c\equiv d(mod\space n)$. Alors :
- $ax+cy\equiv bx+dy(mod\space n)$
	$a\equiv b(mod\space n) ⇔ \exists k\in \Z, a=b+kn$
	$c\equiv d(mod\space n) ⇔ \exists k\in \Z, =b+kn$
	Donc $a+c\equiv b+d(mod\space n)$ 
- $ac\equiv bd(mod\space n)$
	Exemple : Calculons $171*37(mod\space 17)$
	$171*37\equiv 1*3(mod\space 17)$

Pour tout $m\in\N$ si $a\equiv b(mod\space n)$ alors $a^m\equiv b^m(mod\space n)$

$ac\equiv bc(mod\space n) ⇔ a\equiv b(mod\space n/ \delta)$ où $\delta=pgcd(c,n)$ 

Soient $n_1 et n_2\in\N*$ alors $\begin{Bmatrix}a\equiv b(mod n_1) \\ a\equiv b(mod n_2) \end{Bmatrix}$ Compléter

Comment montrer $10^6-1$ multiple de $7$ ?
	C'est équivalent à dire $10^6-1\equiv 0(mod\space 7) ⇔ 10^6\equiv 1(mod\space 7)$
	$10^6\equiv 3(mod\space 7)$ donc $10^6\equiv3^6\equiv3^{2*3}\equiv(3^2)^3\equiv2^3\equiv8\equiv1(mod\space7)$ 

# Les équations et le théorème des restes chinois
## Le tableau

Si $q\equiv b(mod\space n)$, $q$ une équation, il faut faire un tableau avec en première ligne les entiers $a$ de $0$ à $(n-1)$. La ligne suivante comporte en première colonne l'équation et les autre colonnes les $b$ où $q(a)\equiv b(mod\space n)$.
Il faut enfin trouver la ou les solutions où $b$ est solution de $q\equiv0(mod\space n)$

| x    | 0   | 1   | 2   |
| ---- | --- | --- | --- |
| 2x+1 | 1   | 0   | 2

1 est solution de $2x+1\equiv 0(mod 3)$
Donc $1+3k$ est également solution
$2(1+3k)+1\equiv 2*1+1+6k\equiv0+0\equiv0(mod\space3)$ 
$S={1+3k,k\in\Z}$

## L'équation
Si $\begin{Bmatrix}x\equiv a_1(mod\space n_1) \\ x\equiv a_2(mod\space n_2)\end{Bmatrix}$ avec $pgcd(n_1, n_2)=1$ ($n_1$ et $n_2$ premiers entre eux), alors il faut trouver deux nombres $k_1$ et $k_2$ de telle sorte que $n_1*k_2+n_2*k_1=1$.
Enfin, il faut calculer $d=n_1*a_2*k_2+n_2*a_1*k_1$ et trouver $x=d(mod\space n_1n_2)$

# Petit théorème de Fermat
## Le théorème de Fermant
$a^p\equiv a(mod\space p)$ Si $p$ nombre premier
$a^{p-1}\equiv1(mod\space p)$ si en plus $\neg(p|a)$
**Exemple 1 :**
	Calculer $27^{134}(mod11)\equiv5^{134}(mod11)$
	On sait $11$ premier ($p$). De plus, $\neg(11|5)$
	Ainsi, $5^{11-1}\equiv1(mod11) ⇔ 5^{10}\equiv1(mod11)$ ($a^{p-1}\equiv1(mod\space p)$)
	⇒ $5^{134}\equiv5^{10*13+4}\equiv(5^{10})^{13}*5^4\equiv1^{13}*5^4\equiv5^4\equiv(5^2)^2\equiv25^2\equiv3^2\equiv9(mod11)$ 

## La fonction d'Euler
La fonction d'Euler ($\Phi(n)$) est le nombre d'entiers inférieurs et premiers à $n$
**Exemple 1** :
	$\Phi(8)=card({1,3,5,7})=4$
**Exemple 2** :
	$\Phi(55)=\Phi(11*5)=10*4=40$

---


Il faut aussi savoir que :
- Si $p$ premier, $\Phi|(p)=p-1$. Cela explique l'exemple précédant où $\Phi(11*5)=10*4$ 
- Si $p$ premier, $\Phi(p^2)=(p-1)p^{k-1}$

Si $pgcd(m,n)=1$, $\Phi(m<n)=\Phi(m)*\Phi(n)$ 
Soit $n=\Pi_{i=1}P_i$ la décomposition en produits de facteurs premiers de $n-\Phi(n)=\Pi^n_{i=1}\Phi(P_i^{d_i})$ 
	Donc ...
	$75=15*5=3*5$ donc $\Phi(75)=(3-1)3^{1-1}*(5-1)5^{2-1}=2*4*5=40$ 

Soit un entier $n$ non nul et $a$ un entier tel que $pgcd(a,n)=1$ alors $a^{\Phi(n)}\equiv1(mod\space n)$
	Calculer $3^{49}(mod\space35)$
	$pgcd(3,35)=1$ on peut donc appliquer le théorème d'Euler
	$\Phi(35)=\Phi(5*7)=4*6=24$ et $3^{24}\equiv1(mod\space35)$
	$3^{49}\equiv3^{24*2+1}\equiv(3^{24})^2*3\equiv3(mod\space35)$ 