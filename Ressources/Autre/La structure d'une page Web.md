Une page web a une structure assez spéciale :
![[mise en page d'une page web.png|400]]
Ce n'est pourtant pas très difficile à comprendre :

### L'en-tête
La balise `<header>` permet de gérer l'en-tête d'une page. La plus-part des pages en possède un. C'est la petite bande qui se trouve tout en haut de la page.
```html
<header>
<!-- Placer le code ici -->
</header>
```
Idéalement, il ne faut pas trop surcharger l'en-tête : on préfère que cela reste clair et lisible
> **Attention à ne pas confondre la balise `<header>` qui permet de structurer une partie de la page Web et la balise `<head>` qui est là pour donner des infos générales sur la page comme son titre, des liens vers les polices, vers une feuille de style ...**


### Le pied de page
Au contraire du `<header>`, le `<footer>` se trouve tout en bas de la page. On peut y retrouver des infos tels que des liens de contacts, des mentions légales, la politique de confidentialité ...

### Le menu de navigation
Les principaux liens du site se retrouvent dans la balise `<nav>`. Comme indiquer, il s'y retrouve les principaux liens pour se diriger dans le site Web. On peut y trouver le menu principale du site, le menu généralement réalisé sous forme de liste

### Le contenu principale de la page Web
La partie la plus importantes du site, celle qui regroupe les informations essentielles, se retrouvent dans la balise `<main>` . La balise ne soit être présente qu'une fois par page

### Las balises section
Il est possible de regrouper les éléments d'une page se trouvant dans le `<main>` par *thématiques*. Pour cela, il suffit d'utiliser des balises `<section>` :
```html
<main>

<section>
<!-- Code -->
</section>

<section>
<!-- Code -->
</section>

</main>
```

### Mettre du contenu supplémentaire
Généralement, les informations qui sont placées sur le côté (gauche ou droit) de la balise `<main>`  sont des informations supplémentaires qui ne rentreraient pas dans les catégories précédantes. Cette balise se nomme `<aside>`

## Des balises servant seulement à structurer la page
En effet, il est tout à fait d'obtenir le même résultat avec ou sans balises. Ces balises servent juste à obtenir une meilleure lisibilité du code pour s'y repérer dans le futur. En effet, le placement des élement se fera avec le CSS