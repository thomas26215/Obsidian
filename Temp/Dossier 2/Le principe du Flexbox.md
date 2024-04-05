En CSS, on pourrait comparer le flexbox au fait de ranger des cartons : ⇒ Dans un page Web, il peut y avoir plusieurs conteneurs (= cartons) et dans chacuns de ceux-ci peuvent y être placés plusieurs éléments
Tout d'abord, un conteneur est une balise qui peut renfermer d'autres balises. Les conteneurs les plus connus sont les balises `<div>` et `<span>` :

```html
<div class="container">
	<div class="element 1">Element 1</div>
	<div class="element 2">Element 2</div>
	<div class="element 3">Element 3</div>
</div>
```
A noter que ce sont des blocs, donc ils sont censés être placés les uns au dessus des autres. Cependant, il existe une propriété CSS qui nous permet de les aligner sur la même ligne : le `flex` :
```CSS
.container{
	display: flex;
}
```
Ainsi, les éléments sont non plus placés verticalement mais horizontalement.
Il existe d'autres propriétés qui nous permet d'agencer cet arrangement, comme le fait de [[Retour à la ligne de nos éléments flexbox|faire revenir les éléments à la ligne si la place est manquante]], de [[Comprendre les deux types d'axes avec Flexbox|modifier l'alignement principale et secondaire]], ou bien encore de [[Donner une direction à ses éléments avec flexbox|donner une direction aux éléments]]. Mais il faut savoir que pour faire toutes ces modification, la propriété `flex` est indispensable. En effet, sans celle-ce, les nouvelles propriétés énoncées n'auront aucun effet.

---
**Links :**
[[Retour à la ligne de nos éléments flexbox]]
[[Donner une direction à ses éléments avec flexbox]]
[[Comprendre les deux types d'axes avec Flexbox]]