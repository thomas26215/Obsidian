- Paquet 1 : $(1, 3, 2, 1)$ et $C^1=15$
- Paquet 2 : $(1, 2, 1, -1)$ et $C^2=7$ 
- Paquet 3 : $(-1, -1, -3, 4)$et $C^3=11$
- Paquet 4 : $(3, 6, 6, -4)$ et $C^4=20$

⇒ **Sous forme de système linéaire :**
$\begin{Bmatrix}1B^1+3B^2+2B^3+1B^4=15\\B^1+2B^2+B^3-B^4=7\\-B^1-B^2+-3B^3+4B^4=11\\3B^1+6B^2+6B^3-4B^4=20\end{Bmatrix}$

(Pour chaque ligne, on mets sous un seul grand système et on rajoute aux coeffs les inconnues $B^1, B^2...$)

⇒ **Sous forme de matrice :**
$\begin{pmatrix}1&3&2&1\\1&2&1&-1\\-1&-1&-3&4\\3&6&6&-4\end{pmatrix}*\begin{pmatrix}B^1\\B^2\\B^3\\B^4\end{pmatrix}=\begin{pmatrix}15\\7\\11\\20\end{pmatrix}$ 

⇒ **Forme échelonnée**
(On a déja sous système linéaire)

$⇔ \begin{Bmatrix}B^1&+3B^2&+2B^3&+B^4&=15\\0&-B^2&-B^3&-2B^4&=-8&L^2 ← L^2-L^1\\0&+2B^2&-B3&+5B^4&=26&L^3 ← L^3+L^1\\0&-3B^2&+0&-7B^4&=-25&L^4 ← L^4-3L^1\end{Bmatrix}$

$⇔ \begin{Bmatrix}B^1&+3B^2&+2B^3&+B^4&=15\\0&-B^2&-B^3&-2B^4&=-8\\0&+0&-3B^3&+B^4&=10&L^3 ← L^3+2L^2\\0&+0&+3B^3&-B^4&=-1&L^4 ← L^4-3L^2\end{Bmatrix}$ 

$⇔ \begin{Bmatrix}B^1&+3B^2&+2B^3&+B^4&=15\\0&-B^2&-B^3&-2B^4&=-8\\0&+0&-3B^3&+B^4&=10\\0&+0&+0&+0&=9&L^4 ← L^4+L^3\end{Bmatrix}$ 

→ **Solution unique :** On peut trouver une solution unique pour toutes les variables
→ **Infinités de solutions** : Certaines variables sont dépendantes à d'autres variables
→ **Aucune solution** : Si on aboutit à une contradiction

---
Si on prend :
- $B_1=(2, 3, -1, 2)$
- $B_2=(3, 1, 2, 0)$
- $B_3=(1, -2, 3, 1)$
- $B_4=(2, 3, 3, -1)$
- $B_5=(2, 0, 7, 1)$

⇒ **Si on prend $g_1=-1$, $g_2=1$, $g_3=2$, $g_4=1$, et $g_5=3$** :
Le code C vaut :
→ $-1\begin{pmatrix}2\\3\\-1\\2\end{pmatrix}+\begin{pmatrix}3\\1\\2\\0\end{pmatrix}+2\begin{pmatrix}1\\-2\\3\\-1\end{pmatrix}+\begin{pmatrix}2\\3\\3\\-1\end{pmatrix}+3\begin{pmatrix}2\\0\\7\\1\end{pmatrix}=\begin{pmatrix}11\\-3\\33\\2\end{pmatrix}$ 

---
- Paquet 1 : $(1,1,1,0)$ et $C_1=(1,-1,0)$
- Paquet 2 : $(1,-2,6,1)$ et $C_1=(3,2,-4)$
- Paquet 3 : $(2,4,2,-1)$ et $C_1=(-2,0,3)$
- Paquet 4 : $(2,0,3,1)$ et $C_1=(0,1,-2)$

→ Il y a 4 blocs car 4 valeurs dans $g$
→ Les blocs sont de taille 3 car les codes sont de taille 3

⇒ **On peut écrire le premier code comme combinaison linéaire des différents blocs $B_1$, $B_2$, ...** :
$B_1+B_2+B_3+0*B_4=\begin{pmatrix}1\\-1\\0\end{pmatrix}$ 
>**Une combinaison linéaire se traduit pas $c_1a_1+c_2a_2+c_3a_3..$
>Où $c_1, c_2$ ... réels
>Et $a_1,a_2$ coefficients** 

⇒ **Ecrire la combinaison linéaire coordonnée par coordonnée en utilisant la notation $B_1=(b_{11}, b_{12}...)$**
$\begin{Bmatrix}b_{11}&+b_{21}&+b_{31}&=1\\b_{12}&+b_{22}&+b_{32}&=-1\\b_{13}&+b_{23}&+b_{33}&=1\end{Bmatrix}$ 