---
MOOC: "[[Autre]]"
Thème: Mathématiques
Sujet: Logique
tags:
---

**Prédicat** : Affirmation qui porte sur des symboles représentant des éléments variables ou inconnus d'un ensemble fixé. Cet ensemble est appelé univers
Pereillement aux formules, les prédicats qui portent sur le même univers peuvent être combinés entre eux à l'aide de connecteurs $non, et, ou, ⇒, ⇔$ pour former de nvx prédicts
**Exemple** :

- Considéront l'ensemble des entiers naturels $\N$ et $n$ un élément variable, $(n>=2)ou(v<-1)$ est un prédicat dépendant d'une variable. L'univers de prédicat est $\N$

$\forall n\in \N, n>=0$
$\exists n \in \N, n>=0$ : Il existe $n$ appartenant à $\N$, $n>0$

$\forall n\in N, \exists m\in N;n<m$
⇒ Pour tout entier $n$, il existe une entier $m$ strictement plus grand que $n$. Ici, $m$ peut dépendre de l'entier $n$ puisqu'il est placé après. Cette assertion est vraie : pour tout $n\in N$, le nombre $m=n+1$ appartient à N et vérifie bien $n<m$

$\exists m\in N, \forall n\in N; n<m$
Il existe un entier $m$ tel que pour tout entier $n$ vérifie $n<m$. Cette assertion est fausse

