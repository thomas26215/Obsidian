MOOC : [[Programmation]]
Status : #status_writing
Type de note : #note_inbox

Il est possible de créer un lien vers une autre page grâce à la balise `<a>` (*anchor*). Il faut par la suite rajouter l'attribut `href=""`. Entre les guillemets est le lien vers la page (Interne ou externe). Il faut ensuite refermer la balise.
⇒ Entre les deux balises entrantes et fermantes, il faut écrire le texte affiché quand l'utilisateur cliquera sur le lien:
**Exemple** :
```html
<a href="Nouvelle page.html">Lien vers la nouvelle page</a>
```
![[Lien hypertext.png]]

### Créer un lien vers une page Internet
Afin de réaliser cela, il faut tout d'abord copier le lien et le mettre entre les guillemets :
```html
<a href="https://www.figma.com/file/CxvRp7cluaH5lpwZ7Zs8SX/Application-fitness?type=design&node-id=0-1&mode=design">Lien vers ma maquette d'application mobile</a>
```
### Créer un lien vers une page interne
Pour créer un lien vers une page qui se situe sur son ordinateur, il faut remplacer le lien par le nom de sa page :
```html
<a href="Nouvelle page.html">Lien vers la nouvelle page</a>
```
Attention, il est possible de faire de cette manière uniquement si la page enfant se trouve dans le même dossier que la page enfant.

Si le fichier *Nouvelle page* se trouve dans un autre dossier, il faut préciser le nom du dossier suivit d'un `/` suivit du nom fichier :
```html
<a href="contenu/Nouvelle page.html">Lien vers la nouvelle page</a>
```
A noter qu'il faut réitérer pour le nombre de sous-dossiers présent :
```html
<a href="contenu/contenu1/contenu2/contenu3/.../Nouvelle page.html">Lien vers la nouvelle page</a>
```
Enfin, si le fichier est *plus haut* dans l'arborescence, il faut utilise `..` :
```html
<a href="../Nouvelle page.html">Lien vers la nouvelle page</a>
```

### Les ancres
Les ancres servent à se diriger rapidement dans une page. Prenons l'exemple d'un contenu qui se trouve au milieu de la page ; Il est possible de s'y diriger rapidement en cliquant sur un texte. Cependant, cela ne s'implémente pas automatiquement

#### 1 - Créer une ancre
Ca sert à indiquer où on doit se diriger quand on clique sur le lien hypertext de lancre correspondant. Il suffit simplement de rajouter l'attribut `id` à un `<p>`, `<h1>` ... :
```html
<h2 id="velos"> Section des vélos</h2>
```

#### 2 - Indiquer où se situe l'ancre
C'est la lien hypertext qui nous permettra de nous rendre à la section de la page voulue

##### 2.1 - L'ancre se trouve sur la même page
Il suffit de mettre l'attribut `#href` suivit du nom de l'ancre (`#nom de l'ancre`)
```html
<a href ="#velos"> Voir la section des velos</a>
```
##### 2.2 - L'ancre se trouve dans une page externe
Dans ce cas là, c'est le même principe que si l'ancre se trouvait sur la même page, mais là, il faut précéder l'ancre par le nom de la page (Le même que si on créait un lien vers une autre page normale) :
```html
<a href ="page externe.html
   #velos"> Voir la section des velos</a>

```

### Cas particuliers
```html
<p>Bonjour. Souhaitez-vous apprendre sur <a href="https://openclassrooms.com" target="_blank">OpenClassrooms</a> ?</p> <!--Ouvre le lien dans un nouvel onglet-->

<a href="mailto:NOMDUMAIL@MAIL.COM">Envoyer moi un mail !</a> <!--Permet d'envoyer un mail-->

<a href="mon_application.java">Testez mon application !</a> <!--Créer un lien hypertext afin de laisser l'utilisateur télécharger un fichier placé au préalable dans le dossier-->
```