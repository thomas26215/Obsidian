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
$(1,\; 0.5,\; 1,\; 0.25,\; 0,\; 0 \;|\; 20)$

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




# Système de phases


Prenons ce problème où la base initiale n'est pas réalisable :

**Maximiser** $Z=x1+x2Z = x_1 + x_2Z=x1+x2$

Sous contraintes :

$x1+x2≥2x1≤3x2≤2x1,x2≥0\begin{cases} x_1 + x_2 \geq 2 \\ x_1 \leq 3 \\ x_2 \leq 2 \\ x_1, x_2 \geq 0 \end{cases}⎩⎨⎧x1+x2≥2x1≤3x2≤2x1,x2≥0$

## 1. Mise sous forme standard

- Pour $≥$ : on soustrait une variable d'écart et **ajoute une variable artificielle**.
    
- Pour $\leq$ : on ajoute une variable d'écart.
    

On obtient :

$x1+x2−x3+a1=2x1+x4=3x2+x5=2x1,x2,x3,x4,x5,a1≥0\begin{cases} x_1 + x_2 - x_3 + a_1 = 2 \\ x_1 + x_4 = 3 \\ x_2 + x_5 = 2 \\ x_1, x_2, x_3, x_4, x_5, a_1 \geq 0 \end{cases}⎩⎨⎧x1+x2−x3+a1=2x1+x4=3x2+x5=2x1,x2,x3,x4,x5,a1≥0$

Variables d'écart : $x3,x4,x5x_3, x_4, x_5x3,x4,x5$
Variable artificielle : $a1a_1a1$ 

## 2. Tableau initial (Phase 1)

On veut **minimiser** a1a_1a1 (fonction objectif auxiliaire : Z1=a1Z_1 = a_1Z1=a1).

|Base|x1|x2|x3|x4|x5|a1|RHS|
|---|---|---|---|---|---|---|---|
|a1|1|1|-1|0|0|1|2|
|x4|1|0|0|1|0|0|3|
|x5|0|1|0|0|1|0|2|
|Z1|0|0|0|0|0|1|0|

## 3. Première itération (Phase 1)

- On cherche à faire sortir a1a_1a1 de la base.
    
- On regarde les coefficients de la ligne Z1Z_1Z1 : ici, tous sont nuls sauf pour a1a_1a1.
    
- On exprime a1a_1a1 en fonction des autres variables (ligne 1) :  
    a1=2−x1−x2+x3a_1 = 2 - x_1 - x_2 + x_3a1=2−x1−x2+x3
    
- Pour faire sortir a1a_1a1, on fait entrer une variable avec un coefficient négatif dans la ligne de a1a_1a1. Ici, x3x_3x3 a un coefficient de −1-1−1.
    

**Variable entrante :** x3x_3x3  
**Variable sortante :** a1a_1a1

On pivote sur la case (ligne 1, colonne x3x_3x3) :

- Normaliser la ligne 1 par −1-1−1 :  
    x3=2−x1−x2+a1x_3 = 2 - x_1 - x_2 + a_1x3=2−x1−x2+a1
    

Nouveau tableau (après pivot) :

|Base|x1|x2|x3|x4|x5|a1|RHS|
|---|---|---|---|---|---|---|---|
|x3|-1|-1|1|0|0|1|2|
|x4|1|0|0|1|0|0|3|
|x5|0|1|0|0|1|0|2|
|Z1|0|0|0|0|0|1|0|

On élimine x3x_3x3 des autres lignes (méthode de Gauss). Ici, seul x3x_3x3 est dans la base, donc pas d'autres modifications immédiates.

## 4. Deuxième itération (Phase 1)

- On continue à faire sortir a1a_1a1 de la base si elle y est encore.
    
- On regarde la ligne Z1Z_1Z1 : si tous les coefficients des variables artificielles sont nuls et Z1=0Z_1 = 0Z1=0, on a fini la phase 1.
    
- Ici, a1a_1a1 n'est plus dans la base, et sa valeur est 0.
    

**On a donc trouvé une base réalisable pour le problème initial.**

## 5. Passage à la phase 2

- On retire la colonne a1a_1a1 du tableau.
    
- On remplace la fonction objectif par celle du problème initial : Z=x1+x2Z = x_1 + x_2Z=x1+x2.
    
- On continue l'algorithme du simplexe classique à partir de cette base.
    

## 6. Résumé des étapes

1. **Mise sous forme standard** : Ajout de variables d'écart et artificielles.
    
2. **Phase 1** : Minimiser la somme des variables artificielles pour obtenir une base réalisable.
    
3. **Phase 2** : Optimiser la fonction objectif d'origine à partir de la base trouvée.
    

---

**À retenir :**

- Les variables artificielles servent uniquement à démarrer l'algorithme quand aucune base réalisable n'est évidente.
    
- Si, à la fin de la phase 1, la valeur minimale de la fonction auxiliaire est strictement positive, le problème n'a pas de solution réalisable.
    
- Sinon, on continue avec la phase 2 pour trouver la solution optimale du problème initial.
    

Veux-tu qu’on fasse ensemble la phase 2 sur cet exemple, ou que je détaille chaque pivot étape par étape ?