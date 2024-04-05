---
MOOC: "[[Autre]]"
Sujet: Mathématiques
Type: Arithmétique
tags:
---
Définition de l'algorithme d'Euclide
- Étant donné deux entiers a et b tels que 0 < b < a, l'ensemble des diviseurs communs à a et b est le même que l'ensemble des diviseurs communs à b et à a mod b
- Donc, pgcd(a, b) = pgcd(b, a mod b)
- Démonstration 5
**Exemple :**
Supposons que nous voulons calculer le PGCD de 48 et 18.

1. On commence par diviser 48 par 18, ce qui donne un quotient de 2 et un reste de 12 (car 48=18×2+12).
    
2. Ensuite, on réapplique l'algorithme d'Euclide en remplaçant le diviseur (18) par le reste précédent (12) et le diviseur initial (48) par le diviseur (18). Ainsi, on calcule pgcd(18,12)pgcd(18,12).
    
3. On répète ce processus jusqu'à ce que le reste soit égal à zéro. Dans notre exemple :
    
	$pgcd(48,18)=pgcd(18,12)\space car 48\space =18×2+12$
	$pgcd(18,12)=pgcd(12,6)\space car\space 18=12×1+6$
	$pgcd(12,6)=pgcd(6,0)\space car\space 12=6×2$
    
4. Lorsque le reste devient zéro, le dernier diviseur non nul est le PGCD. Dans notre exemple, pgcd(6,0)=6pgcd(6,0)=6.

---
**Links**
[[Le PGCD]]