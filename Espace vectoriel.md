---
MOOC: "[[Autre]]"
Thème: Algèbre linéaire
Sujet: Fondements mathématiques
tags: 
Complete: false
Learned: false
---
Un espace vectoriel sur un corps $\mathbb{K}$ (souvent $\mathbb{K} = \mathbb{R}$ ou $\mathbb{K} = \mathbb{C}$) est un ensemble non vide $E$ muni de deux opérations :

1. Une **loi de composition interne** : $E \times E \to E$, $(u,v) \mapsto u + v$
2. Une **loi de composition externe** : $\mathbb{K} \times E \to E$, $(\lambda,u) \mapsto \lambda u$

Ces opérations doivent satisfaire les propriétés suivantes :

- **Associativité** : $(u + v) + w = u + (v + w)$ pour tous $u, v, w \in E$
- **Commutativité** : $u + v = v + u$ pour tous $u, v \in E$
- **Élément neutre** : Il existe un vecteur nul $\vec{0} \in E$ tel que $u + \vec{0} = u$ pour tout $u \in E$
- **Opposé** : Pour tout $u \in E$, il existe $-u$ tel que $u + (-u) = \vec{0}$
- **Distributivité** :
  - $\lambda(u + v) = \lambda u + \lambda v$, pour tous $\lambda \in \mathbb{K}$, $u, v \in E$
  - $(\lambda + \mu)u = \lambda u + \mu u$, pour tous $\lambda, \mu \in \mathbb{K}$, $u \in E$
  - $(\lambda\mu)u = \lambda(\mu u)$ pour tous $\lambda, \mu \in \mathbb{K}$, $u \in E$
- **Élément neutre de la multiplication scalaire** : $1u = u$ pour tout $u \in E$, où $1$ est l'élément neutre dans $\mathbb{K}$