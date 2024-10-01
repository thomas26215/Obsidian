
# Univers
## Exemple du jeu de Tarot

⇒ J'ai un bout dans mon jeu. Quelle est la probabilité qu'il y en ait 1 dans le chien ?

Soit $\Omega$ l'ensemble de toutes les paires composées d'une combinaison de 18 cartes parmis 78 pour former la main et d'une combinaison de 6 cartes parmis les 60 restantes pour former le chien
>[!info] Comment trouver $\Omega$ ?
>Il suffit de prendre uniquement ce qui nous intéresse : Dans notre cas, nous nous interessons uniquement à ce qui se trouve dans le chien et dans une main. Ainsi, nous allons nous intéresser à ce qui se passe dans ma main (18 cartes composent une main) et à ce qui se passe dans le chien (-18 cartes car on a déjà mon jeu)

({Main : 18 cartes parmis 78}, {Chien : 6 cartes parmis 78-18=58})
La taille de l'Univers est $C^{18}_{78}*C^6_{60}$

Soit $A$ le sous-ensemble contenant toutes les paires ({1 main avec un bout + 17 cartes parmis 75}, {Chien 6 cartes parmis 60})
Le nombre de couples dans A est $3*C^{17}_{75}*C^6_{60}$
⇒ Car pour former une main avec exactement un bout, on a 3 possibilités pour choisir le bout et pour chacune de ces possibilités, il reste à former toutes les mains possibles de 17 cartes prises parmis 75 cartes car on veut exactement un bout

Dans le sous-ensemble $A$, on considère le sous-ensemble $B$ contenant toutes les paires ({1 main avec un bout + 17 autres cartes parmis 75}, {Chien contient 1 autre bout + 5 autres cartes parmis 59})
Le nombre de paires dans B est $3*C^{17}{75}*2*C{6}_{59}$

## Exemple des deux dés

Soit $\Omega$ l'ensemble de tous les couples $(a, b)$ composés d'une arrangement à répétitions de 2 dés de six faces
({6 faces}, {6 faces})
La taille de l'Univers est 6x6 = 36

⇒ La variable aléatoire X représente le plus grand nombre des deux nombres sortis. Les valeurs possibles de X sont les entiers de 1 à 6

⇒ Pour chaque valeur de X, nous devons compter combien de couples $(, b)$ donnent cette valeur :
- X=1 : $(1, 1)$ ⇒ 1 cas
- X=2 : $(2, 1), (1, 2), (2, 2)$ ⇒ 3 cas
- X=3 : $(3, 1),(3,1),(3,2),(2,3),(3,3)$ ⇒ 5 cas
- X=4 ⇒ 7 cas
- X=5 ⇒ 9 cas
- X=6 ⇒ 11 cas
La loi de la probabilité de X est donc $\frac{nombre de cas favorables pour X=x}{36}$


| Terme mathématique | Ordre important ? | Répétitions possibles ? | Dénombrement                 | Exemple           |
| ------------------ | ----------------- | ----------------------- | ---------------------------- | ----------------- |
| Permutation        | Oui               | Non                     | n!                           | Melange de cartes |
| Combinaison        | Non               | Non                     | $(^n_k)=\frac{n!}{k!(n-k)!}$ | Bridge            |
| P-uplet            | Oui               | Oui                     | $n^p$                        | MasterMind        |
| Arrangement        | Oui               | Non                     | $\frac{n!}{(n-k)!}$          | Tiercé            |

---



<mark style="background: #ADCCFFA6;">Les différentes lois</mark>
![[Loi de Bernouilli]]

![[Loi binomiale]]

![[Loi géométrique]]

---


Loi d'une variable aléatoire
Expérience et variance
Loi de Bernouilli, binomiale, géométrique
