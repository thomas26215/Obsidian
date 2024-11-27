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

Soit $P$ premier et $g$ un [[Générateur]] de $\mathbb{Z}/p\mathbb{Z}$
- Alice génère aléatoirement un élément $x_A$ qui appartient à $(\mathbb{Z}/p\mathbb{Z})^X$
- Bob génère aléatoirement un élément $X_B$ qui appartient à $(\mathbb{Z}/p\mathbb{Z})^X$
- Alice calcule $k_A=g^{x_A}(mod\space p)$ 
- Bob calcule $k_B=g^{x_B}(mod\space p)$ 
- Ils envoient $k_A$ et $k_B$
- Alice reçoit $k_B$ et calcul $k_B^{x_A}=k_{AB}$
- Bob reçoit $k_A$ et calcul $k_A^{xB}=k_{BA}$

$k_{AB}=k_B^{x_A}=g^{x_Bx_A}=g^{x_Ax_B}=k_A^{^{x_B}}=k_{AB}$

Charles connaît $p, g, k_A, k_B$ 
Pour connaître $k_AB$, il faut qu'à partir de $(p, g, k_A, k_B)$, il puisse construire $k_{AB}$ 
Charles est confronté au problème de log discret