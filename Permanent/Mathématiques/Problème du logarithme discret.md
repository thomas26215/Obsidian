---
MOOC: "[[Mathématiques]]"
Thématique: 
tags:
---
## Définition
Soit $p$ un entier premier et $g$ un générateur de $(\mathbb{Z}/p\mathbb{Z})^\times$. Le calcul de :

$$ 
a = g^\alpha \mod p 
$$ 

est "facile" par l'algorithme d'exponentiation dichotomique. 

### Difficulté Inverse
À l'inverse, connaître $a$ et $g$ rend difficile la détermination de l'exposant $\alpha$ tel que :

$$ 
a = g^\alpha 
$$ 

C'est ce qu'on appelle le **problème du logarithme discret**. En théorie, on sait que l'application :

$$ 
(\mathbb{Z}/p\mathbb{Z})^\times \to (\mathbb{Z}/p\mathbb{Z})^\times : \alpha \mapsto g^\alpha 
$$ 

est bijective, mais en pratique, le calcul de l'application réciproque est d'une complexité exponentielle.