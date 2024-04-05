


[[Ajouter de la couleur sur un texte CSS]]


[[Couleur de fond unie]]
### Les images
Pour pouvoir afficher une image en fond, il faut utiliser la propriété CSS `background-image`.  Il est possible de rentrer le lien de l'image de deux manières :
- de manière aboslu (`http://...`)
- De manière relative (`fond.png`)

```CSS
body{
	background-image: url("paysage.jpg")
}
```
### Les comportements de l'image de fond

Si nous décidons de définir une image de fond, alors il y a plusieurs propriétés qui peuvent être appliquées dessus :
- `background-attachment: fixed;` : L'image de fond est fixe quand on déroule la page
- `background-size: cover;` : Redimensionne la page pour qu'elle s'adapte à la taille de la fenêtre
- `background-position: ..;` : Indique où doit se positionner l'image de fond. Associer avec `top`, `right`,  `center`, `left`, `bottom`.

### La superpropriété background
La superpropriété `background` permet de réunir 5 propriétés en 1 :
1. `background-image`
2. `background-repeat`
3. `background-attachment`
4. `background-size`
5. `background-position`

**Exemple :**
```CSS
.banniere{
	background: url("paysage.jpg") cover center;
}
```

### Les dégradés
Afin d'appliquer ce genre d'effets en tant que fond d'écran, il faut utiliser la propriété `background` avec la valeur `linear-gradiant` :
```css
body{
brackground: linear-gradiant(90deg, #8360c3, #2ebf91)
}
```
En français, cela signifie : 
> C'est un gradiant linéaire qui part de 90degrès vers la droite et qui part de la couleur `#8360c3` vers la couleur `#2ebf91`

![[Pasted image 20230720210053.png]]

### Un peu de transparence
La propriété `opacity` indique l'apparence du fond d'écran et des images.
- Une valeur de `0` indique un élément totalement transparent
- Une valeur de `1` indique un élément totalement opaque
