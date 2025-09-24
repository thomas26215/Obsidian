


# Exercice 1

## Question 1

$$A=\begin{pmatrix}-1&2\\1&2\\1&-6\end{pmatrix}x=\begin{pmatrix}x_1\\x_2\end{pmatrix}y=\begin{pmatrix}4\\6\\-6\end{pmatrix}$$

![[Drawing 2025-09-23 10.14.53.excalidraw]]

$c_1\space x_2=\frac{1}{2}x_1+2$
$c_2\space x_2=\space -\frac{1}{2}x_1+3$
$c_3\space x_2=\frac{1}{6}x_1+1$

Et pour savoir si on barre au dessus ou en dessous, on remplace pour chaque équation x par 0 et on regarde si vérifié. Si juste, on barre au dessus, sinon en dessous.

Point d'intersection entre $c_2$ et $c_3$ :
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

- $x_{11}$ = nombre d'autos envoyées de l'usine 1 au concessionnaire 1
- $x_{12}$ = nombre d'autos envoyées de l'usine 1 au concessionnaire 2
- $x_{21}$= nombre d'autos envoyées de l'usine 2 au concessionnaire 1
- $x_{22}$ = nombre d'autos envoyées de l'usine 2 au concessionnaire 2

> Fonction objectif : $min\space z = 20x_{11} + 30x_{12} + 30x_{21} + 50x_{22}$

Contraines d'approvisionnement :
$$\begin{Bmatrix}x_{11}+x_{12}=80\\x_{21}+x_{22}=100\end{Bmatrix}$$

Contraines de demande :
$$\begin{Bmatrix}x_{11}+x_{21}=40\\x_{12}+x_{22}=60\end{Bmatrix}$$

Non-négativité : $x_{ij} \geq 0$

> Nouvelle fonction objectif : $min\space z = 20x_{11}+30(60-x_{22})+30(40-x_{11})+50x_{22}=3000-10x_{11}+20x_{22}$
> $min=3000-10x_{11}+20x_{22}$ si $x_{11}+60-x_{22}<=80$, $x_{22}=20$ => $40-x_{11}+x_{22}<=100$ et $x_{11},x_{22}>=0, x_{11}<=40, x_{22}<=60$

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

Soient $x_1, x_2, x_3$ les quantités produites respectivement des produits de $P_1, P_2, P_3$.
> Fonction objectif : $max\space z=5x_1+3x_2+4x_3$

Contraintes :
$$\begin{Bmatrix}4x_1+2x_2+4x_3<=80\\2x_1+2x_2+3x_3<=50\\x_1+3x_2+2x_3<=40\\x_1,x_2,x_3>=0\end{Bmatrix}$$

