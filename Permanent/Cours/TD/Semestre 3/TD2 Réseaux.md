---
MOOC: "[[Cours]]"
Ressource: 
Cours: 
Date: 
tags: 
Complete: false
Learned: false
---
# Exercice 1
## Question 1.1
**Question 1**
>Il y a 8 pages

**Question 2**
> C'est la fragmentation interne


## Question 1.2
**Question 1**
> $40k0 ⇒ 40ko * 10 = 400ko$

**Question 2**
> Adresse logique = 0x1d5a
> Adresse physique = 0x5d5a

**Question 3**

## Question 1.3
**Question 2**

| num page | num case |
| -------- | -------- |
| 3        | 0        |
| 0        | 4        |
| 8        | 1        |
**Question 3**
5 accès à la RAM

# Exercice 2
**Question 1**
> Il n'y a pas encore eu besoin de la place pas encore eu le besoin de déplacer

**Question 2**
> La page 2 n'a pas été swappée car il n'y a pas le bit de présence mais elle n'est pas présente dans le TLB
> La page 9 a pas été swappée car il n'y pas le bit de présence et elle est présente dans le TLB


**Question 3**

| Num de la page lue | Swap utilisé | Défaut de page | Explication |
| ------------------ | ------------ | -------------- | ----------- |
| 1                  | Non          | Non            |             |
| 2                  | Non          | Min            |             |
| 9                  | Oui          | Maj            |             |

# Exercice 3
**Pour le programme 1 :**  
ω = (A0, B0, A0, A1, B1, A1, ..., A4095, B4095, A4095) ⇒ $(AB)^{4096}$ 
**Pour le programme 2 :**  
ω = (A0, B0, A4095, A1, B1, A4094, ..., A4095, B4095, A0)
Dans les deux cas, la chaîne de référence se répète 4096 fois, correspondant aux itérations de la boucle.