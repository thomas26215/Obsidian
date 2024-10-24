---
MOOC: "[[Mathématiques]]"
Thématique: Fonctions
tags:
---
Une fonction réciproque est l'inverse d'une fonction. Si $g=f(x), x=f^{-1}(y)$
Définition :
> Soit $f$ une fonction bijective d'un ensemble A vers un ensemble B. La fonctin réciproque de $f$, notée $f^{(-1)}$, est la fonction de B vers A telle que :
> - Pour tout $x$ dans A : $f^{(-1)}(f(x)) = x$
> - Pour tout $y$ dans B : $f(f^{(-1)})(y)) = y$

**Exemples :**
> Sur $\mathbb{R}_+=[0;+\infty] → \mathbb{R}_+$
> La fonction réciproque de $x → x^2$
>                    est   $x → \sqrt{x}$
> $Df=[1;+\infty]$ car x³ - 1 doit être ≥ 0
> $f(x)=\sqrt{x^3-1}$ $f(1)=0, lim_{x->+\infty} f(x)=+\infty$   
> $(u^a)'=a*u^{a-1}*u'$ 
> $\forall x\in]1;+\infty[=\frac{3x^2}{2\sqrt{x^3-1}}>0$
> $f : [+1;+\infty[ →  [0;+\infty[$
> $x → \sqrt{x^3-1}$
> fonction strictement continue


> $f(x)=tan(x)$
> $I=]-\frac{\pi}{2}[ → J=\mathbb{R}$
> Sens de variation ?
> $f'(x) = \frac{1}{cos^2x} = 1+tan^2(x)>0$
> donc $f(x)$ est croissante sur $I$
> 
> $arctan(x) : \mathbb{R} → ]-\frac{\pi}{2};\frac{\pi}{2}[$
> $x=tan(y) → y$
> $[arctan(x)]'$          $(fof^{-1})(x)$
> $tan(arctan(x)) = f(f^{-1}(x))=x$ 
> 
> $[tan(arctan(x))]'=(x)'=1$
> $arctan'(x)*[1+tan^2(arctan(x))]=1$
> $arctan'(x)[1+x^2]=1$
> $arctan'(x)=\frac{1}{1+x^2}$ 


> $sin : \mathbb{R} → [-1; +1]$
> $arcsin : [-1;+1] → [-\frac{\pi}{2};+\frac{\pi}{2}]$
> $\forall x\in[-1, +1]$, $sin(arcsin(x)) = x$
>  $\forall x\in[-\frac{\pi}{2};+\frac{\pi}{2}]$, $arcsin(sin(x)) = x$
>  
>  $cos^2(x)+sin^2(x)=1$
>  $cos^2(x)=1-sin^2(x)$
>  $cos(x)=\sqrt{1-sin^2(x)}$
>  
>  $[sin(arcsin(x))]' = arcsin'(x)*cos(arcsin(x))=1$
>  $arcsin'(x)=\frac{1}{cos(arcsin(x))}=\frac{1}{\sqrt{1-sin^2(arcsin(x))}}=\frac{1}{\sqrt{1-x^2}}$  