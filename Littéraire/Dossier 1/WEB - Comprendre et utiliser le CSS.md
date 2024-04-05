### Lier le fichier CSS au fichier HTML
Déja, la première chose à faire est de créer un fichier CSS en y aplliquant l'extension `.css`. Une fois cela fait, il faut lier les deux fichiers en utilisant la balise orpheline `<link>`. Et hop ! Le travail est fait !
**Voici un exemple** : 
```html
<head>
    <meta charset="utf-8">
    <title>Ma page</title>
    <link href="style.css" rel="stylesheet"> <!--Permet de lier les deux fichiers-->
</head>
```

### Appliquer une propriété CCS à une balise HTML
Voici un syntaxe CSS :
```CSS
h1{
	color: blue;
}
```
On peut remarquer ici 3 éléments :
1. **Le sélecteur** qui permet de cibler la balise précise à modifier. Il suffit simplement d'écrire la balise (ici `h1`)
2. **Les propriétés CSS** qui permet de modifier les éléments. La propriété utilisée ici permet de modifier la couleur du texte
3. **Les valeurs** qui indique quelle valeur on doit appliquer à la propriété. Ici, la propriété est `color`, la valeur est `blue`, ca permet donc naturellement de modifier la couleur du texte et de le mettre en bleu

- Le sélecteur est suivit de deux accolades. Entre celles-ci sont spécifiées les propriétés  et valeurs CSS :
```css
selecteurs{
	Proprietes et valeurs
}
```
- Chaque propriété est suivit des deux points et de la valeur :
```css
propriete: valeur
```
- Et enfin, chaque ligne se termine par un `;` :
```css
propriete: valeur;
```

### Ajouter une propriété CSS à plusieurs balises HTML
l est vrai qu'il peut être redondant de devoir écrire plusieurs fois la même choses afin d'appliquer la même propriété à plusieurs balises HTML. Examinez :
```css
h1 {
    color: blue;
}

p {
    color: blue;
}
```
Et bien il est tout à fait possible de combiner les déclarations en regroupant les titres des balises en les séparants par une virgule :
```css
h1, p{
	color: blue;
}
```

### Les commentaires
Comme en HTML, il est possible d'écrire un commentaire en CSS. Pour cela, il faut faire `/* commentaire */` 
**Exemple** :
```css
p{
	/*Il est carrément possible
	d'écrire un commentaire
	sur plusieurs lignes */
	color: blue
}
```


### Les classes
Le problème, c'est que si j'applique ce code :
```css
p{
	color: blue;
}
```
Tous les paragraphes de la page web, sans exception, seront écrits en bleu. Il existe cependant des possibilités afin de sélectionner les textes à afficher en bleu

#### 1 - La partie HTML
La première étape est d'implémenter l'attribut `class` sur notre balise HTML. On peut appliquer cet attribut sur à peu près n'importe quel balise HTML :
```html
<h1 class="voici"></h1>
<p class="des"></p>
<img class="classes"></img>
```

#### 2 - La partie CSS
Une fois la classe implémentée, il faut l'appeler avec un `.` dans le fichier CSS. Il faut l'appeler de la manière `.classe` :
```css
.classe{
	color: blue
}
```
Ainsi, tous les paragraphes, titres ... qui on la classe `classe` auront le texte qui s'affichera en bleu