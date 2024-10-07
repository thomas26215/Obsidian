---
MOOC: "[[Mathématiques]]"
Thématique: Intégrale
tags:
---
On sait $(uv)'=u'v+v'u$
Ainsi $uv'=(uv)'-u'v$

Ainsi :
> Soit $uv'=(uv)'-u'v$
> On peut donc en déduire que :
> $$\int uv'\space dx=\int (uv)'-\int u'v ⇔ \int uv'\space dx = uv-\int u'v$$

Il s'agit donc de choisir intelligemment son $u$ et son $v'$ de sorte que que l'on puisse obtenir la primitive de $v'$ facilement

---
<mark style="background: #BBFABBA6;">Exemple 1 :</mark>
> $$\int \stackrel{\tiny\text{u = x u'=1 v=sin(x) v'=cos(x)}}{\boxed{\displaystyle xcox(x)}}dx=xsin(x) - \int sin(x)dx=xsin(x)+cos(x)+C$$


<mark style="background: #BBFABBA6;">Exemple 2 :</mark>

> $u = xcos(x), u'= xsin(x)+cos(x)$ (Reprendre ce qui a été fait à **l'exemple 1**)
> $v = cos(x), v'=-sin(x)$
> 
> $$\begin{equation} \begin{split} \int xcos^2(x)dx& =  [xsin(x)+cos(x)]cos(x)+\int sin(x)[xsin(x)+cos(x)]dx \\ & = [xsin(x)+cos(x)]cos(x)+\int xsin^2(x)dx+\int sin(x)cos(x)dx \\ & =[xsin(x)+cos(x)]cos(x)+\int x(1-cos^2(x))dx + \frac{sin^2(x)}{2} \\ & = [xsin(x)+cos(x)]cos(x) + \frac{sin^2(x)}{2}+\frac{x^2}{x}-\int xcos^2(x) dx   \end{split} \end{equation} $$
> Ainsi : 
> $$2I = xsin(x)cos(x)+cos^2(x)+\frac{sin^2(x)}{2}+\frac{x^2}{2} ⇔ 2I = \frac{xsin(x)cos(x)+cos^2(x)}{2}+\frac{sin^2(x)}{4}+\frac{x^2}{4}$$
> 


