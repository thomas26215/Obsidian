---
MOOC: "[[Cours]]"
Ressource: "R2.09 : Mathématiques"
Cours: 
Date: 
tags: 
Complete: false
Learned: false
$:
---
# Exos et exemples associés
Tous les exemples concernant les thèmes seront basé sur ces sujets :
- **Sujet 1 :** ![[Suites et récurrences Info 1.pdf]]
# Les différents types de suite
## Suite arithmétique
- **Formule par récurrence :** $U_{n+1=}U_n+r$
- **Formule explicite :**
  → $U_n=U_0+nr$
  → $U_n = U_p +(n-p)r$
- **Montrer qu'elle est arithmétique :** $U_{n+1}-U_n=r$
- $U_0+U_1+…+U_n=(n+1)\frac{U_0+U_n}{2}$
- $1+2+…+n=\frac{n(n+1)}{2}$
## Suite géométrique
- **Formule par récurrence :** $U_{n+1}=U_n*q$
- **Formule explicite :**
  → $U_n=U_0*q^n$
  → $U_n = U_p*q^{(n-p)}$
- **Montrer qu'elle est géométrique :** $U_{n+1}=q*U_n$
- $U_0*U_1*…*U_n=U_0\frac{1-q^{n+1}}{1-q}$
# Variations d'une suite
- **Croissante** : $U_{n+1} >= U_n$
- **Décroissante :** $U_{n+1} <=U_n$
- **Stationnaire :** $U_{n+1} = U_n$
- **Monotone** si croissante et décroissante

> [!tip] Les manières de montrer
> 1. **Définition + principe de récurrence :**
>    $U_n < U_{n+1} ⇒ U_{n+1} ≤ U_{n+2}​$
> 2. **Soustraction :** $U_{n+1}-U_n$
> 3. **Fraction :** $\frac{U_{n+1}}{U_n}$

# Bornage d'une suite
- **Minorée :** Il existe une réel $m$ tel que $U_n≥m$
- **Majorée** : Il existe un réel $M$ tel que $U_n ≤ M$
- **Bornée** : Entre $m$ et $M$
> [!info] Si majorée et croissante, la suite est convergente

# Opérations sur les suites
On considère deux suites $(U_n)$ et $(V_n)$ et $\lambda$ un réel
- **Addition :** On définit la suite $(U_n)+(V_n)$ comme $(U_n+V_n)$ en additionnant les termes des deux suites
- **Soustraction :** On définit la suite $(U_n)*(V_n)$ comme $(U_n+V_n)$ en multipliant les termes des deux suites
- 
# Limites
**Convergente** : Tend vers une limite finie
**Divergente** : Qui n'a pas de limite finie ⇒ Tend vers + ou - l'infinie

# Opérations sur les limites
- **Théorème des gendarmes :** Si $U_n ≤ V_n ≤ W_n$ et que $^{lim\space U_n = L}_{n→ +\infty}$ et $^{lim\space W_n = L}_{n→ +\infty}$, alors $^{lim\space V_n = L}_{n→ +\infty}$
- **Théorème de comparaison des suites :** Si $U_n ≤ V_n$ et que $^{lim\space U_n = +\infty}_{n→ +\infty}$, alors $^{lim\space U_n = +\infty}_{n→ +\infty}$

# Démonstration par récurrence
> [!tip] Condition initiale
> Montrer que $P(n_0)$ vraie

> [!tip] Condition d'héréditée
> 1. On suppose $P(n)$ vraie pour un entier naturel $n>=0$ (**Hypothèse de récurrence**)
> 2. On montre vrai pour $P_{n+1}$
> ⇒ Alors pour tout entier naturel $n>=n_0$, $P_n$ est vrai

