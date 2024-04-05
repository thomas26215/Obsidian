### Changer la taille de son texte
Il faut pour cela utiliser la propriété `font-size` et il est possible de lui indiquer deux types de taille :
- une **taille absolue**
- une **taille relative**

#### 1 - La taille absolue
Il faut indiquer cette taille en `px` (pixels). Si on veut un texte de 16 pixels, il faut indiquer :
```css
p{
font-size: 16px;
}
```
Le problème est que cette taille est fixe, et donc, si la taille d'écran change, la taille du texte reste la même. Ainsi, une texte lisible sur un téléphone le sera moins sur l'écran d'un ordinateur. C'est pourquoi il est possible d'indiquer une taille relative

#### 2 - La taille relative
Il faut indiquer cette taille en `em`. Ainsi, un texte d'un certaine taille sur un téléphone sera agrandit pour être lu sur un ordinateur :
- `1pm` : Une taille normale
- `1.3pm` : Une taille agrandie
- `0.7pm` : Une taille réduite
**Exemple** :
```html
<p class="elem1">Élément 1 : 1em</p>
<p class="elem2">Élément 2 : 1.3em</p>
<p class="elem3">Élément 3 : 2em</p>
```

```css
.elem1 {
font-size: 1em;
}

.elem2 {
font-size: 1.3em;
}

.elem3 {
font-size: 2em;
}
```

### Changer la police
Afin de changer la police d'un texte CSS, il faut utiliser la propriété `font-family` :
```css
balise{
font-family: nom-police;
}
```
Il existe des polices qui fonctionnent sur tous les ordinateurs :
- Arial Black
- Futura
- Helvetica
- Impact
- Trebuchet MS
- Verdena

#### Mettre du texte en italique
Pour réaliser ce procédé, il faut utiliser la propriété CSS `font-size` et lui appliquer la propriété `italic` si l'on souhaite mettre le texte en italique ou `normal` si on souhaite laisser le texte sans modification visuelles (Utiles pour les balises `<em>`)

#### Mettre du texte en gras
Il faut pour cela utiliser la propriété `font-weight` avec la valeur suivante au choix :
- `bold` : mets le texte en gras
- `normal` : laisse le texte normal
- `thin` : le texte est plus fin

#### Souligner du texte
La propriété `text-decoration` permet de faire beaucoup de choses :
- `underline` : souligner le texte correspondant
- `line-throught` : barrer le texte demandé
- `none` : Laisser le texte par défaut

### Aligner du texte
Afin de positionner correctement son texte à l'écran, il est important d'utiliser la propriété `text-align` en associant une des valeurs :
- `left` : positionne le texte à gauche
- `right` : positionne le texte à droite
- `centre` : centre le texte au milieu de la page
- `justify` : permet de justifier le texte
