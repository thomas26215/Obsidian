---
MOOC: "[[Programmation]]"
Langage: Web
Type: CSS
tags:
---
Pour appliquer une couleur de fond unique à une page Web, il faut utiliser la propriété CSS `background-color`. Cette approche est similaire à la [[Ajouter de la couleur sur un texte CSS|coloration d'un texte]], mais la balise appropriée à cibler est `<body>` pour affecter l'ensemble de la page :

```CSS
body{
	background-color: black; /* Fond noir */ color: white; /* Texte en blanc */
}
```

Ici, nous avons appliqué la couleur de fond à toute la page (sélecteur `body`). Cependant, on pourrait appliquer la couleur de fond uniquement pour les paragraphes :
```CSS
h1{
	color: purple;
}
```