# Changer le type
La propriété `display` permet de transformer n'importe quel élément d'un type vers un autre (**Exemple : de type `inline` comme pour les liens vers `block`**) :
```css
a{
	display: block;
}
```
Il est aussi possible de masquer des éléments avec la valeur `none` :
```css
.secret{
	display: none;
}
```

# Poitionner ses éléments
La propriété `position` nous permet de repositionner nos éléments. Il y  a plusieurs types de déplacement

## 1. Position relative
`position: relative` permet de positionner l'éléments par rapport à sa position initiale. Prenons l'exemple d'un lien qui se trouve dans une phrase, si on veut le déplacer un peu plus en bas et à droite dans la phrase, on pourrait faire :
```css
a{
	position: relative;
	top: 6px;
	left: 10px;
}
```

## 2. Position absolu
`position: absolute;` nous permet de positionner notre éléments n'importe où dans la page. En fait, à partir du moment où nous mettons la position en absolu, le point d'origine n'est pas l'endroit où il devrait se glisser logiquement mais il va se positionner par rapport au premier éléments qu'il rencontre dans ses parents

## 3. Mettre un éléments au dessus d'un autre
Dans certains cas, on veut qu'un éléments soit au dessus d'un autre pour une meilleure lisibilité. Ainsi, on peut utiliser la propriété `z-index`. L'élément ayant la valeur la plus élevée sera placée au-dessus des autres