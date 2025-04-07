---
MOOC: "[[Cours]]"
Ressource: "R4.12 : Algèbre linéaire"
Cours: Algèbre linéaire
Date: 
tags: 
Complete: false
Learned: false
---
[[Permanent/Cours/TD/Semestre 4/Algèbre linéaire|Algèbre linéaire]] => TD


[[Introduction aux Espaces vectoriels]]
[[Combinaison linéaire et Sous-espace engendré]]
[[Indépendance, Générateurs et Bases]]

[[Applications linéaires]] (+ [[Théorème du rang]])

[[Ecrire la matrice d'une application linéaire]]


---
# Matrice d'une application linéaire
Si $E$ et $E'$ sont de dimension $n$ et $p$ respectivement, choisissons une base $\{e_1,e_2, \dots, e_n\}$ de $E$ et une base $\{\epsilon_1,\epsilon_2, \dots, \epsilon_n\}$ de $E'$. Les images par $f$ des vecteurs $e_1, \dots, e_j$ se décomposent sur la base $\{\epsilon_1, \dots, \epsilon_n\}$
=> $f(e_j)=a_{1j}\epsilon_1 + a_{2j}\epsilon_2 + \dots + a_{pj}\epsilon_p, j\in I$

On appelle matrice de $f$ dans les bases $B=\{e_1,e_2,\dots,e_n\}$ de $E$ et $C=\{\epsilon_1,\epsilon_2, \dots, \epsilon_n\}$ de $E'$ la matrice notée $M(f)_{B,C}$ appartenant = $\mathcal{M}_{PN}(K)$ dont les colonnes sont les composantes des vecteurs $f(e_1), \dots, f(e_n)$ dans la base $C$ :
$$M(f)_{B,C}=\begin{pmatrix}a_{11}&a_{12}&\dots&a_{1n}\\a_{21}&a_{22}&\dots&a_{2n}\\.&.&\dots&.\\a_{p1}&a_{p2}&\dots&a_{pn}\end{pmatrix}$$

