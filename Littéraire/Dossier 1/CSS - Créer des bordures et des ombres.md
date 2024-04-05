La superpropriété `border` nous permet de disposer d'un large éventail de possibilités pour modifier les bordures des éléments. Il existe plusieurs propriétés de base :
- `border-width`
- `border-color`
- `border-style`
Il est possible d'utiliser jusqu'à 3 valeurs associé à la propriété `border`pour modifier :
- **La largeur** : Elle est définie en pixel (**Ex** : 2px)
- **La couleur** : Elle se note soit avec le nom de la couleurs, soit avec la valeur hexadecimale, soit avec la valeur RGB
- **Le type de bordure** : Il existe 4 mots-clés pour désigner le type de bordure :
	- `solid` : Un trait simple
	- `double` Un double trait
	- `dotted` : En pointillés
	- `dashed` : Un trait en tirets

Il est tout à fait possible de mettre une bordure à gauche et non la même à droite. Pour cela, il existe plusieurs propriétés :
- `border-top` : pour modifier la bordure du haut
- `border-bottom` : pour modifier la bordure du bas
- `border-left` : pour modifier la bordure de gauche
- `border-right` : pour modifier la bordure de droite
Voici un exemple :
```html
<p class="element">Élément</p>
```

```css
.element {
    border-top: 3px #EB5353 dotted;
    border-right: 3px #F9D923 double;
    border-bottom: 3px #36AE7C dashed;
    border-left: 3px #187498 solid;
}
```

On pourrait tout à fait n'avoir qu'un bord d'un seul côté :
```css
.element {
    font-size: 25px;
    background-color: skyblue;
    border-left: 5px #187498 solid;
    padding: 100px;
}
```

### Arrondir les angles
La propriété `border-radius` permet de donner des coins arrondis aux bords :
```css
.element {
    font-size: 25px;
    background-color: skyblue;
    border-radius: 10px;
    padding: 100px;
}
```

On peut donner jusqu'à quatre paramètres afin d'arrondir les angles que l'on veut et de quelle valeur spécifique dans l'ordre : en haut à gauche, en haut à droite, en bas à droite, en bas à gauche
```css
.element {
    font-size: 25px;
    background-color: skyblue;
    border-radius: 10px 30px 0px 90px;
    padding: 100px;
}
```

### Comment ajouter une ombre ?
La propriété `box-shadow` permet justement d'ajouter cette ombre et prend en compte quatre paramètres dans l'ordre suivant :
1. Le décalage horizontal de l'ombre
2. Le décalage vertical de l'ombre
3. L'adoucissement du dégradé
4. La couleur du dégradé
⇒ L'adoucissement peut-être :
- faible (valeur inférieure à celle du décalage)
- normal (valeuu égale à celle du décalage)
- forte (valeur supérieure à celle du décalage)

`text-shadow` nous permet de répéter le même processus sur un texte :
```css
h1 {
    font-size: 50px;
    text-shadow: 3px 3px 0px rgba(0,0,0,0.2);
    padding: 100px;
}
```
