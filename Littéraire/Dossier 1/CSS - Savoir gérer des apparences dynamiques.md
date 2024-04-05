Grâce aux pseudo-classes, i lest tout à fait possible de faire varier les éléments de styles une fois que la page a été chargée. Il suffit de faire : `balise:peudoClasse`

**Exemple** :
```css
a:hover{
//Code
}
```

### Modification au survol de la souris
Prenons l'exemple d'un lien hypertexte (cliquable) où l'on voudrait qu'il se passe une action quand le visiteur passe sa souris dessus : Il est possible d'utiliser la peudo-classe `:hover`
**Exemple** :
```css
a:hover{
 color: white;
}
```

### Modification lors du clic sur l'élément
De la même manière que lorsque l'on passe sa souris sur un élément, il est possible de modifier l'élément lorsque le visiteur clique dessus, et ceux, grâce à la pseudo-classe `:active`
**Exemple** :
```css
a:active{
 color: red;
}
```

### Modification lors de la sélection par l'utilisateur
C'est un peu le même principe que pour les sous-classes `:hover` ou `:active`, sauf qu'ici, c'est quand l'élément est sélectionné. C'est utile quand le visiteur visite le site avec sa touche **tab** ou  dans les formulaires
**Exemple** :
```css
a:focus{
	background-color: yellow;
}
```

### Modification lorsqu'un élément a déja été cliqué par le passé
Prenons l'exemple d'un bouton qui a été un fois cliqué par l'utilisateur. Cependant, l'utilisateur revient sur site 3 mois plus tards ; Et on veut que l'élément sur lequel il a cliqué trois mois auparavent se retrouve modifié dès lors qu'il arrive sur le site. Pour cela, il faut utiliser la pseudo-classe `:visited`
> Si l'on ne souhaite pas qu'un lien change de couleur une fois cliqué (de bleu à violet de base), il faut soit-même appliquer la couleur de base du lien hypertexte

**Exemple** :
```css
a:visited{
	color: black;
}
```