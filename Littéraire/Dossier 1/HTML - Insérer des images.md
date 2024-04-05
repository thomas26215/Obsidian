---
MOOC: "[[Medias]]"
Type: Livre, Video
Categorie: Productivite, Programmation
Auteur: 
Lien: 
tags:
---


Afin d'afficher une Image dans notre page web, il est nécessaire d'utiliser la balise orpheline `<img>` qui doit être accompagnée de deux attributs :
- `src` : Elle indique la source de l'image, qu'elle soit dans un de nos dossiers ou qu'elle soit directement présente sur Internet
- `alt` : Quie permet de mettre une description alternative si la page ne s'affiche pas

### Les deux principaux attributs
#### 1 - La source de l'image
L'attribut `src` permet de décrire la source de l'image, de la même manière que pour [[HTML - Les liens hypertext|insérer des liens]] vers d'autres pages, il suffit de préciser le chemin vers l'image, avec les mêmes propriétés pour les dossiers (`dossier/fichier` ou `../fichier`) :
```html
<src="images/logo.png"> <!--Pour afficher l'image se nommant 'logo.png' qui se trouve dans le dossier images-->
<!--Attention à ne pas oublier d'écrire l'extension ! (.png, .jpeg ...)-->

<src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTlmTy2FYEeJ7N2Lj1y14Ih9nxYZaRo1PJHDpMQrLxfew&s"> <!-- Permet d'afficher une image qui est directement présente sur Internet 
```

> Il faut éviter d'utiliser les accents, les majuscules, les espaces pour les noms de fichiers ou de dossiers. En effet, cela peut poser problème. Par exemple, **`Images du site/Image toute bête.jpg`** va poser problème. Il faudrait au contraire écrire : **`images_du_site/image_toute_bete.jpg`**

#### 2 - Une description alternative
L'attribut `alt` permet de donner une discription alternative à l'image. Autrement dit, si l'image ne parvient pas à s'afficher, le texte présent dans cet attribut sera affiché à la place.
Egalement, le texte alternative sera décrit pour les personnes malvoyantes.
**Exemple** :
```html
<src="images/logo.png" alt="Ceci est une image"> <!-- Le fichier se nommant 'logo.png' sera affiché automatiquement. Si l'affichage n'est pas possible, le texte 'Ceci est une image' sera affichée à la place
```

### Le bon format d'image
Afin de faciliter l'affichage des images, il est nécessaire d'utiliser le format adéquat pour chaque type d'image :
- **Une photo** : JPEG
- **Une image avec peu de couleurs (-256)** : PNG 8 bits, GIF éventuellement
- **Une image avec beaucoup de couleurs** : PNG 24 bits
- **Une image animée** : GIF animé
- **Un logo vectoriel** : SVG

### Les infobulles
L'attribut `title` permet d'afficher des informations supplémentaires lorsque l'utilisateur va passer sa souris sur l'image. A noter que cet attribut est facultatif contrairement à l'attribut `alt`
> **A ne pas confondre avec la balise `title` qui sert à afficher un titre**

**Exemple** :
```html
<img src="montagnes.png" title="Alors, envie de vous balader n'est-ce pas ?" alt="Chemin de randonnée au milieu des montagnes">
```

### Les miniatures cliquables
Il est conseillé d'utliliser cette alternative si l'image est trop grosse : Utiliser une image réduite qui sera affichée sur le site web, et une image plus détaillée qui sera affichée uniquement si le visiteur clique sur l'image réduite.
Pour se faire, il faut tout d'abord disposer de deux versions de l'image : l'originale et la réduite. Il faut placer les deux images dans le même dossier, puis afficher l'image réduite et insérer un lien vers l'image originial :
```html
<p>Vous souhaitez voir l'image dans sa taille d'origine ? Cliquez dessus !<br>
    <a href="images/montagne.jpg"><img src="images/montagne_mini.jpg" alt="Chemin de randonnée au milieu des montagnes" title="Cliquez pour agrandir" ></a>
</p>
```
