![[TD2Arithmetique.pdf]]
<<<<<<< HEAD
## Exercice 16
=======
## Exercice 1
Exercice 1
> Les classes de congruence de Z/6Z sont : {0̄, 1̄, 2̄, 3̄, 4̄, 5̄}

Exercice 3
> Diviseurs de zéro : 2̄, 3̄, 4̄
> Éléments inversibles : 1̄, 5̄

Exercice 4
>- 4̄4 × 7̄7 = 2̄ × 5̄ = 4̄
>- 1̄13 + 2̄013 = 5̄ + 1̄ = 0̄

## Exercice 2
| a   | b   | r   | q   | u    | v   |
| --- | --- | --- | --- | ---- | --- |
| 143 | 100 | 43  | 1   | 1    | -1  |
| 100 | 43  | 14  | 2   | -2   | 3   |
| 43  | 14  | 1   | 3   | 7    | -10 |
| 14  | 1   | 0   | 14  | -100 | 143 |

Question 1
> Le pgcd(143, 100) est le dernier reste non nul dans la colonne r, soit 1

Question 2
> On lit directement les valeurs de u et v sur la ligne où r = 1 :  
> u = 7 et v = -10  
> Donc : 143 × 7 + 100 × (-10) = 1

Question 3
> L'inverse de 100 modulo 143 est la valeur de v sur la ligne où r = 1, soit -10. Cependant, nous devons exprimer cette valeur dans Z/143Z, donc :  $-10 ≡ 133 (mod 143)$

## Exercice 3
### Calcul du pgcd de 114 et 33

1. **Algorithme d'Euclide :**
    
    - 114÷33=3114÷33=3 reste 1515
    - 33÷15=233÷15=2 reste 33
    - 15÷3=515÷3=5 reste 00
    
    Le dernier reste non nul est 3, donc pgcd(114,33)=3pgcd(114,33)=3.
2. **Identité de Bézout :**On remonte les calculs pour trouver un couple (u,v)(u,v) tel que 114u+33v=3114u+33v=3.
    
    - 3=33−2×153=33−2×15
    - 15=114−3×3315=114−3×33
    
    En substituant :
    
    - 3=33−2×(114−3×33)3=33−2×(114−3×33)
    - 3=7×33−2×1143=7×33−2×114
    
    Donc, un couple possible est u=−2u=−2, v=7v=7.
3. **Inverse de 33 dans Z/114Z :**Comme le pgcd(114, 33) n'est pas égal à 1, l'inverse de 33 dans Z/114Z n'existe pas.

### Calcul du pgcd de 114 et 35

1. **Algorithme d'Euclide :**
    
    - 114÷35=3114÷35=3 reste 99
    - 35÷9=335÷9=3 reste 88
    - 9÷8=19÷8=1 reste 11
    - 8÷1=88÷1=8 reste 00
    
    Le dernier reste non nul est 1, donc pgcd(114,35)=1pgcd(114,35)=1.
2. **Identité de Bézout :**On remonte les calculs pour trouver un couple (u,v)(u,v) tel que 114u+35v=1114u+35v=1.
    
    - 1=9−81=9−8
    - 8=35−3×98=35−3×9
    - Substituer pour obtenir :
        
        - 1=(9)−(35−3×(9))=4×(9)−(35)1=(9)−(35−3×(9))=4×(9)−(35)
        - Substituer encore :
        - 9=(114−3×(35))9=(114−3×(35))
        - Finalement :
        - 1=(4×(114)−(12×(35)))−(35)1=(4×(114)−(12×(35)))−(35)
        - Simplifier :
        - 1=(4×(114))−(13×(35))1=(4×(114))−(13×(35))
        
    
    Donc, un couple possible est u=4u=4, v=−13v=−13.
3. **Inverse de 35 dans Z/114Z :**Puisque le pgcd(114, 35) est égal à 1, l'inverse de 35 dans Z/114Z existe et est donné par la valeur de v modulo n. Ainsi, l'inverse est :−13≡101(mod114)−13≡101(mod114).

L'inverse de 35 dans Z/114Z est donc 101ˉ101ˉ.

## Exercice 4


## Exercice 18
>>>>>>> 9a07ef5 (.)

Exercice 1
> Les éléments inversibles de taille $\Phi(7)=6$ sont $\{\bar{1}, \bar{2}, \bar{3}, \bar{4}, \bar{5}, \bar{6}\}$

Exercice 2
> $<2>=\{\bar{1}, \bar{2}, \bar{4}\}$
> $<3>=\{\bar{1}, \bar{3}, \bar{2}, \bar{6}, \bar{4}, \bar{5}\}$
> $\#<2> != \Phi(7)$
> $\#<3> != \Phi(7)$

Exercice 3
> $(\mathbb{Z}/9\mathbb{Z})= \{\bar{1}, \bar{2}, \bar{4}, \bar{5}, \bar{7}, \bar{8}\}$ sont les éléments inversibles de taille $\Phi(9)=\Phi(3^2)=(3-1)3=6$
> $<2>=\{\bar{1}, \bar{2}, \bar{4}, \bar{8}, \bar{7}, \bar{5}\}$
> $<4>=\{\bar{1}, \bar{4}, \bar{7}\}$
> $<7>=\{\bar{1}, \bar{7}, \bar{4}\} = <4>$
> 
> $<2>$ est un générateur de $(\mathbb{Z}/9\mathbb{Z})= \{\bar{1}, \bar{2}, \bar{4}, \bar{5}, \bar{7}, \bar{8}\}$

## Exercice 17
Exercice 2
> $<3>= \{1, 3, 9, 7\}$
> $<7>= \{1, 7, 9, 3\}$
> $<9>= \{1, 9\}$
> $<11>= \{1, 11\}$
> $<13>= \{1, 13, 9, 17\}$
> $<17>= \{1, 17, 9,13\}$
> $<19>= \{1, 19\}$

Exercice c
> Il n'y a pas de générateur donc le groupe n'est pas cyclique

## Exercice 18
1. Alice : $x_A=7$
2. Bob : $x_B=4$
3. Alice : $k_A=g^