---
Complete: false
Learned: false
---
# Résolution linéaire
## Résolution graphique

$max\space f(x)$
si $Ax <= b$
  $x>=0$

## Algorithme du symplexe
Le symplexe est une méthode itérative permettant de résoudre des problèmes d'optimisation linéaire sous la forme : 
$$\begin{aligned}a_{11}x_1 + a_{12}x_2 + ... + a_{1n}x_n <= b_1\\\vdots\\a_{m1}x_1 + a_{m2}x_2 + ... + a_{mn}x_n <= b_m\end{aligned}$$



# Algorithme du simplexe — Résolution complète avec explications

## 1. Mise sous forme standard

Nous voulons **maximiser** :

*Exemple* : Maximiser $5x_1+3x_2+4x_3$ sous les contraintes :
$$\begin{Bmatrix}4x_1+2x_2+4x_3<=80\\2x_1+2x_2+3x_3<=50\\x_1+3x_2+2x_3<=40\\x_1,x_2,x_3>=0\end{Bmatrix}$$

👉 Pour transformer les inégalités en égalités, on ajoute des **variables d’écart** $x_4, x_5, x_6$ :

$4x_1 + 2x_2 + 4x_3 + x_4 = 80$  
$2x_1 + 2x_2 + 3x_3 + x_5 = 50$  
$1x_1 + 3x_2 + 2x_3 + x_6 = 40$

Les variables de base initiales sont donc $x_4, x_5, x_6$.

---

## 2. Tableau initial

| Base | x1 | x2 | x3 | x4 | x5 | x6 | RHS |
|------|----:|----:|----:|----:|----:|----:|----:|
| x4   | 4   | 2   | 4   | 1   | 0   | 0   | 80  |
| x5   | 2   | 2   | 3   | 0   | 1   | 0   | 50  |
| x6   | 1   | 3   | 2   | 0   | 0   | 1   | 40  |
| **Z**| 5   | 3   | 4   | 0   | 0   | 0   | 0   |

👉 La ligne $Z$ contient les **coefficients de la fonction objectif**.  
Pour une maximisation, la variable entrante est celle avec le **plus grand coefficient positif**.

---

## 3. Choix de la variable entrante et sortante

- Dans $Z$, les coefficients sont :  
  - $x_1 = 5$, $x_2 = 3$, $x_3 = 4$.  
- Le plus grand est **5** → donc $x_1$ entre.

Ensuite, on applique le **test du rapport** :  

$\text{Rapport} = \dfrac{\text{RHS}}{\text{Coefficient de la colonne entrante}}$

- Ligne $x_4$ : $80 / 4 = 20$  
- Ligne $x_5$ : $50 / 2 = 25$  
- Ligne $x_6$ : $40 / 1 = 40$

👉 Le plus petit rapport est **20** → $x_4$ sort.  
Le **pivot** est donc $a_{11} = 4$.

---

## 4. Opération de pivot

1. **Normaliser la ligne pivot** (diviser par 4) :  

Nouvelle ligne $x_4$ :  
$ (1,\; 0.5,\; 1,\; 0.25,\; 0,\; 0 \;|\; 20) $

2. **Éliminer la colonne $x_1$** dans les autres lignes (méthode de Gauss).  

Résultat :

| Base | x1 | x2 | x3 | x4   | x5 | x6   | RHS |
|------|----:|----:|----:|-----:|----:|-----:|----:|
| x1   | 1   | 0.5 | 1   | 0.25 | 0   | 0    | 20  |
| x5   | 0   | 1   | 1   | -0.5 | 1   | 0    | 10  |
| x6   | 0   | 2.5 | 1   | -0.25| 0   | 1    | 20  |
| **Z**| 0   | 0.5 | -1  | -1.25| 0   | 0    | 100 |

👉 Interprétation : après cette étape, $x_1$ est devenu variable de base avec valeur $20$.

---

## 5. Deuxième itération

Dans $Z$ :  
- $x_2 = 0.5$  
- $x_3 = -1$  

👉 Le plus grand positif est $0.5$ → $x_2$ entre.

### Test des rapports pour $x_2$

- Ligne $x1$ : $20 / 0.5 = 40$  
- Ligne $x5$ : $10 / 1 = 10$  
- Ligne $x6$ : $20 / 2.5 = 8$  

👉 Plus petit rapport = **8** → $x_6$ sort.  
Pivot = $2.5$.

---

## 6. Opération de pivot (sur $x_6$)

1. Normalisation :  
Nouvelle ligne $x_6$ :  
$(0,\; 1,\; 0.4,\; -0.1,\; 0,\; 0.4 \;|\; 8)$

2. Élimination de la colonne $x_2$ dans les autres lignes.  

Résultat :

| Base | x1 | x2 | x3  | x4    | x5 | x6    | RHS |
|------|----:|----:|-----:|------:|----:|------:|----:|
| x1   | 1   | 0   | 0.8 | 0.3  | 0   | -0.2 | 16  |
| x5   | 0   | 0   | 0.6 | -0.4 | 1   | -0.4 | 2   |
| x2   | 0   | 1   | 0.4 | -0.1 | 0   | 0.4  | 8   |
| **Z**| 0   | 0   | -1.2| -1.2 | 0   | -0.2 | 104 |

👉 $x_2$ est maintenant dans la base avec valeur $8$.

---

## 7. Test d’optimalité

Dans $Z$ :  
- $x_1 = 0$, $x_2 = 0$, $x_3 = -1.2$.  

👉 Aucun coefficient positif → la solution est **optimale**.

---

## 8. Lecture de la solution finale

Variables de base :  
- $x_1 = 16$  
- $x_2 = 8$  
- $x_3 = 0$  

Variables d’écart :  
- $x_4 = 0$, $x_5 = 2$, $x_6 = 0$

Valeur optimale :  

$Z^* = 5 \times 16 + 3 \times 8 + 4 \times 0 = 104$

---

## ✅ Résultat final

- $x_1^* = 16$  
- $x_2^* = 8$  
- $x_3^* = 0$  
- $Z^* = 104$

