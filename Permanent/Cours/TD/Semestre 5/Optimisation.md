 


# Exercice 1

## Question 1

$$A=\begin{pmatrix}-1&2\\1&2\\1&-6\end{pmatrix}x=\begin{pmatrix}x_1\\x_2\end{pmatrix}y=\begin{pmatrix}4\\6\\-6\end{pmatrix}$$

![[Drawing 2025-09-23 10.14.53.excalidraw]]

$c_1\space x_2=\frac{1}{2}x_1+2$
$c_2\space x_2=\space -\frac{1}{2}x_1+3$
$c_3\space x_2=\frac{1}{6}x_1+1$

Et pour savoir si on barre au dessus ou en dessous, on remplace pour chaque équation x par 0 et on regarde si vérifié. Si juste, on barre au dessus, sinon en dessous.

Point d'intersection entre $c_2$et $c_3$:
$$\begin{Bmatrix}x_1+2x_2=6\\-x_1+6x_2=6\end{Bmatrix} <=> \begin{Bmatrix}x_1+2x_2=6\\-8x_2=12\end{Bmatrix} <=> \begin{Bmatrix}x_1=3\\x_2=\frac{3}{2}\end{Bmatrix}$$
=> $z=12+\frac{9}{2}=\frac{33}{2}$

## Question 2

$x_1^*=0$
$x_2^*=1$
$z^*=3$

# Exercice 2
## Question 1
## Question 1
Maximiser une fonction revient à minimiser son opposé, donc on pose :
$$max\space z'=2x_1+x_2$$
## Question 2
$$A=\begin{pmatrix}1\\1&1\\2&3\end{pmatrix}x=\begin{pmatrix}x_1\\x_2\end{pmatrix}y=\begin{pmatrix}4\\5\\12\end{pmatrix}$$

$c_1\space x_1 >= 4$
$c_2\space x_2=-x_1+5$
$c_3\space x_2=-\frac{2}{3}x_1+4$

![[Drawing 2025-09-23 10.50.39.excalidraw]]


# Exercice 3
## Question 1

## Variables :

- $x_{11}$= nombre d'autos envoyées de l'usine 1 au concessionnaire 1
- $x_{12}$= nombre d'autos envoyées de l'usine 1 au concessionnaire 2
- $x_{21}$= nombre d'autos envoyées de l'usine 2 au concessionnaire 1
- $x_{22}$= nombre d'autos envoyées de l'usine 2 au concessionnaire 2

> Fonction objectif : $min\space z = 20x_{11} + 30x_{12} + 30x_{21} + 50x_{22}$

Contraines d'approvisionnement :
$$\begin{Bmatrix}x_{11}+x_{12}=80\\x_{21}+x_{22}=100\end{Bmatrix}$$

Contraines de demande :
$$\begin{Bmatrix}x_{11}+x_{21}=40\\x_{12}+x_{22}=60\end{Bmatrix}$$

Non-négativité : $x_{ij} \geq 0$

> Nouvelle fonction objectif : $min\space z = 20x_{11}+30(60-x_{22})+30(40-x_{11})+50x_{22}=3000-10x_{11}+20x_{22}$
> $min=3000-10x_{11}+20x_{22}$si $x_{11}+60-x_{22}<=80$, $x_{22}=20$=> $40-x_{11}+x_{22}<=100$et $x_{11},x_{22}>=0, x_{11}<=40, x_{22}<=60$

$$min = 3000+10x_{11}+20x_{22}$$
si
$$\begin{Bmatrix}x_{11}-x_{22}<=20\\-x_{11}+x_{22}<=60\\x_{11},x_{22}>=0\end{Bmatrix}$$

## Question 2

$$A=\begin{pmatrix}1&-1\\-1&1\end{pmatrix}x=\begin{pmatrix}x_{11}\\x_{22}\end{pmatrix}y=\begin{pmatrix}20\\60\end{pmatrix}$$

$c_1\space x_{11}-x_{22}=20 <=> x_2=2=x_{11}-20$
$c_2\space -x_{11}+x_{22}=60 <=> x_2=x_{11}+60$

![[Drawing 2025-09-23 11.29.47.excalidraw]]

$x_{11}^*=40$
$x_{22}^*=20$
$x_{1}^*=0$
$x_{12}^*=40$
$z^*=3000$

# Exercice 4
## Question 1

Soient $x_1, x_2, x_3$les quantités produites respectivement des produits de $P_1, P_2, P_3$.
> Fonction objectif : $max\space z=5x_1+3x_2+4x_3$

Contraintes :
$$\begin{Bmatrix}4x_1+2x_2+4x_3<=80\\2x_1+2x_2+3x_3<=50\\x_1+3x_2+2x_3<=40\\x_1,x_2,x_3>=0\end{Bmatrix}$$



# Exercice 5

$x_1$ = Nombres d'unités produites avec la technique 1
$x_2$ = Nombre d'unités produites avec la technique 2
$x_3$ = Nombre d'unités produites avec la technique 3

Maximiser la marge totale :
$$Z=3x_1+4x_2+5x_3$$

Contraintes :
- $0,5x_1+1,5x_2+2x_3\leq12$ 
- $2x_1+1,5x_2+0,5x_3\leq15$
- $x_1, x_2, x_3\geq0$ 


On ajoute les variables d'écarts :
- $0,5x_1+1,5x_2+2x_3+x_4=12$ 
- $2x_1+1,5x_2+0,5x_3+x_4=15$

Tableau initial :

| Base  | $x_1$ | $x_2$ | $x_3$ | $x_4$ | $x_5$ | RHS  |
| ----- | ----- | ----- | ----- | ----- | ----- | ---- |
| $x_4$ | $0,5$ | $1,5$ | $2$   | $1$   | $0$   | $12$ |
| $x_5$ | $2$   | $1,5$ | $0,5$ | $0$   | $1$   | $15$ |
| $Z$   | $3$   | $4$   | $5$   | $0$   | $0$   | $0$  |

## 1e itération
**Variable entrante** : $x_3$
**Test du rapport** :
- Ligne $x_4$ : $12/2=6$
- Ligne $x_5$ : $15/0,5=30$

Le plus petit rapport est $6$ donc $x_4$ sort

**Pivot** : élément $a_{13}=2$


Normaliser la ligne $x_4$ : diviser par $2$ :
- $0.25x_1+0.75x_2+1x_3+0.5x_4=6$
Eliminer $x_4$ des autres lignes (méthode de Gauss)


| Base  | $x_1$   | $x_2$   | $x_3$ | $x_4$   | $x_5$ | RHS  |
| ----- | ------- | ------- | ----- | ------- | ----- | ---- |
| $x_3$ | $0,25$  | $0,75$  | $1$   | $0,5$   | $0$   | $6$  |
| $x_5$ | $1,875$ | $1,125$ | $0$   | $-0,25$ | $1$   | $12$ |
| $Z$   | $1,75$  | $0,25$  | $0$   | $-2,5$  | $0$   | $30$ |

## 2e itération

**Variable entrante** : $x_1$
**Test du rapport** :
- Ligne $x_3$ : $6/0,25=24$
- Ligne $x_5=12/1,875 = 6,4$

Le plus petit rapport est $6,4$ donc $x_5$ sort
**Pivot** : élément $a_21=1,875$


| Base  | $x_1$ | $x_2$  | $x_3$ | $x_4$    | $x_5$     | RHS    |
| ----- | ----- | ------ | ----- | -------- | --------- | ------ |
| $x_3$ | $0$   | $0,6$  | $1$   | $0,533$  | $0,133$   | $4,4$  |
| $x_1$ | $1$   | $0,6$  | $0$   | $-0,133$ | $0,533$   | $6,4$  |
| $Z$   | $0$   | $-0,8$ | $0$   | $-2,267$ | $0-0,933$ | $18,8$ |
|       |       |        |       |          |           |        |

## 3e itération

**Variable entrante** : x2x2 (coefficient négatif dans Z, donc on arrête ici car on maximise et tous les coefficients sont négatifs ou nuls).

## Lecture de la solution optimale

Variables de base :

- $x_1=6.4x_1=6.4$
- $x_3=4.4x_3=4.4$
- $x_2=0x_2=0$

**Valeur optimale :**

$$Z^*=3×6.4+4×0+5×4.4=19.2+0+22=41.2$$

- **Technique 1** : 6.4 unités
- **Technique 2** : 0 unité
- **Technique 3** : 4.4 unités
- **Marge maximale** : 41.2 €

# Exercise 6

$$c_1\;x_2=-2x_1+2$$
$$c_1\;x_2=-\frac{1}{3}x_1+1$$

## Méthode du simplexe — Exemple complet et commenté

### Énoncé du problème

On cherche à **maximiser** la fonction objectif :

$Z = x_1 + x_2$

sous les contraintes (avant ajout des variables d'écart) :

$2x_1 + x_2 \le 2$ 
$x_1 + 3x_2 \le 3$ 
$x_1, x_2 \ge 0$

---

### 1) Mise sous forme standard (ajout des variables d'écart)

Pour transformer les inégalités en égalités on ajoute des variables d'écart $x_3$et $x_4$:

$2x_1 + x_2 + x_3 = 2$ 
$x_1 + 3x_2 + x_4 = 3$ 

Les variables de base initiales sont $x_3$et $x_4$(elles correspondent aux variables d'écart).

---

### 2) Tableau initial du simplexe

Nous utilisons la **convention classique** où la ligne $Z$contient les coefficients $-c_j$(donc des valeurs négatives pour une maximisation) :

| Base  | $x_1$| $x_2$| $x_3$| $x_4$| RHS |
| ----- | -----:| -----:| -----:| -----:| ----:|
| $x_3$| 2     | 1     | 1     | 0     | 2    |
| $x_4$| 1     | 3     | 0     | 1     | 3    |
| **Z** | -1    | -1    | 0     | 0     | 0    |

**Explication :** la ligne $Z$contient $-c_j$(ici $-1$et $-1$). Pour améliorer $Z$on choisira la colonne qui a le coefficient le plus **négatif**.

---

### 3) Choix de la variable entrante

Dans la ligne $Z$, les coefficients pour $x_1,x_2$sont $-1$et $-1$. On a un **ex æquo** (même valeur négative). Par convention on peut choisir l'une des deux ; ici on choisit :

$\Rightarrow $**$x_1$ est la variable entrante.**

**Remarque :** choisir $x_2$donnerait une autre suite d'itérations mais la même solution optimale finale.

---

### 4) Test du rapport (choix de la variable sortante)

Pour chaque ligne on calcule :

$\displaystyle \text{Rapport} = \frac{\text{RHS}}{\text{coefficient de la colonne entrante}}$

- Ligne $x_3$: $\dfrac{2}{2} = 1$ 
- Ligne $x_4$: $\dfrac{3}{1} = 3$

Le plus petit rapport positif est $1$→ **$x_3$sort**.  
Pivot = $a_{11} = 2$(intersection colonne $x_1$/ ligne $x_3$).

**Explication :** le test du rapport choisit la contrainte la plus limitante pour l'augmentation de la variable entrante, afin de rester dans la région réalisable.

---

### 5) Première opération de pivot (entrer $x_1$, sortir $x_3$)

#### 5.1 Normalisation de la ligne pivot
Diviser la ligne pivot (ligne $x_3$) par $2$:

Nouvelle ligne $x_1$(la base devient $x_1$) :

$x_1 : \; (1,\; 0.5,\; 0.5,\; 0 \;|\; 1)$

(qui correspond à $x_1 + 0.5x_2 + 0.5x_3 = 1$).

#### 5.2 Élimination de la colonne $x_1$dans les autres lignes
- Ligne $x_4 \leftarrow$ligne $x_4 - 1\times$nouvelle ligne $x_1$:

$(1,\;3,\;0,\;1\;|\;3) - (1,\;0.5,\;0.5,\;0\;|\;1) = (0,\;2.5,\;-0.5,\;1\;|\;2)$.

- Ligne $Z \leftarrow$ligne $Z + 1\times$nouvelle ligne $x_1$(on ajoute car $Z$avait $-1$) :

$(-1,\;-1,\;0,\;0\;|\;0) + (1,\;0.5,\;0.5,\;0\;|\;1) = (0,\;-0.5,\;0.5,\;0\;|\;1)$.

#### Tableau après la 1ʳᵉ itération

| Base | $x_1$| $x_2$| $x_3$| $x_4$| RHS |
|------|------:|------:|------:|------:|-----:|
| $x_1$| 1     | 0.5   | 0.5   | 0     | 1    |
| $x_4$| 0     | 2.5   | -0.5  | 1     | 2    |
| **Z**| 0     | -0.5  | 0.5   | 0     | 1    |

**Interprétation :** $x_1$est désormais variable de base et vaut $1$si toutes les variables non basiques sont posées à $0$. La valeur courante de l'objectif (RHS de la ligne $Z$) est $1$.

---

### 6) Deuxième itération — choix de la variable entrante

On regarde la ligne $Z$(coefficients des non-basiques) :  
- $x_2$a coefficient $-0.5$(négatif), $x_3$a $0.5$(positif).  
Donc la seule colonne avec coefficient négatif est $x_2$→ **$x_2$entre**.

**Explication :** un coefficient négatif dans $Z$indique que l’on peut augmenter la valeur de $Z$en entrant cette variable.

---

### 7) Test du rapport (pour $x_2$)

Calcul des rapports pour les lignes où le coefficient de $x_2$est strictement positif :

- Ligne $x_1$: $\dfrac{1}{0.5} = 2$ 
- Ligne $x_4$: $\dfrac{2}{2.5} = 0.8$

Le plus petit rapport est $0.8$→ **la ligne pivot est $x_4$**, donc **$x_4$sort**.  
Pivot = $a_{42} = 2.5$.

---

### 8) Deuxième opération de pivot (entrer $x_2$, sortir $x_4$)

#### 8.1 Normalisation de la ligne pivot
Diviser la ligne $x_4$par $2.5$pour obtenir la nouvelle ligne de base $x_2$:

$x_2 : \; (0,\;1,\;-0.2,\;0.4 \;|\; 0.8)$

(= $x_2 -0.2x_3 + 0.4x_4 = 0.8$).

#### 8.2 Élimination de la colonne $x_2$dans les autres lignes
- Mise à jour de la ligne $x_1$:

$\text{ligne } x_1 \leftarrow \text{ligne } x_1 - 0.5\times\text{ligne } x_2$

$(1,\;0.5,\;0.5,\;0\;|\;1) - 0.5\times(0,\;1,-0.2,\;0.4\;|\;0.8)$ 
$= (1,\;0,\;0.5 + 0.1,\; 0 - 0.2\;|\;1 - 0.4)$ 
$= (1,\;0,\;0.6,\;-0.2\;|\;0.6)$.

- Mise à jour de la ligne $Z$:

$\text{ligne } Z \leftarrow \text{ligne } Z + 0.5\times\text{ligne } x_2$ 
(car $Z$contenait $-0.5$pour $x_2$)

$(0,\;-0.5,\;0.5,\;0\;|\;1) + 0.5\times(0,\;1,-0.2,\;0.4\;|\;0.8)$ 
$= (0,\;0,\;0.5 -0.1,\; 0 + 0.2\;|\;1 + 0.4)$ 
$= (0,\;0,\;0.4,\;0.2\;|\;1.4)$.

#### Tableau final après la 2ᵉ itération

| Base | $x_1$| $x_2$| $x_3$| $x_4$| RHS  |
|------|------:|------:|------:|------:|-----:|
| $x_1$| 1     | 0     | 0.6   | -0.2  | 0.6  |
| $x_2$| 0     | 1     | -0.2  | 0.4   | 0.8  |
| **Z**| 0     | 0     | 0.4   | 0.2   | 1.4  |

**Explication :** la ligne $Z$n'a plus de coefficient **négatif** pour une variable non basique : tous les coefficients sont $\ge 0$. D'après la règle du simplexe (pour une maximisation avec la convention $-c_j$), la solution est donc **optimale**.

---

### 9) Lecture de la solution finale

On lit la solution en posant toutes les variables non basiques à $0$(ici $x_3 = 0$et $x_4 = 0$) :

- $x_1 = 0.6 = \dfrac{3}{5}$ 
- $x_2 = 0.8 = \dfrac{4}{5}$ 
- $x_3 = 0$ 
- $x_4 = 0$

Valeur optimale de l'objectif :

$Z^* = x_1 + x_2 = 0.6 + 0.8 = 1.4 = \dfrac{7}{5}$


## 