Dans Flutter, quand on utilise des widget et type layout, il essentiel de gérer l'alignement des enfants à l'intérieur pour créer des interfaces soignées et responsives. Nous retrouvons deux propriétés fondamentales :
- `mainAxisAlignment` : C'est la direction dans laquelle les éléments sont organisés
- `crossAxisAlignment` : C'est la direction perpendiculaire à l'axe principal

## `mainAxisAlignment`

Plusieurs valeurs sont disponibles pour `mainAxisAlignment` :
- `MainAxisAlignment.start` : Aligne les enfants au début de l'axe principal.
- `MainAxisAlignment.end` : Aligne les enfants à la fin de l'axe principal.
- `MainAxisAlignment.center` : Centre les enfants sur l'axe principal.
- `MainAxisAlignment.spaceBetween` : Distribue les enfants avec un espace égal entre eux.
- `MainAxisAlignment.spaceAround` : Distribue les enfants avec un espace égal autour d'eux.
- `MainAxisAlignment.spaceEvenly` : Distribue les enfants avec un espace égal entre eux et aux extrémités.

## `crossAxisAlignment`
Plusieurs valeurs sont disponibles pour `crossAxisAlignment` :
- `CrossAxisAlignment.start` : Aligne les enfants au début de l'axe secondaire.
- `CrossAxisAlignment.end` : Aligne les enfants à la fin de l'axe secondaire.
- `CrossAxisAlignment.center` : Centre les enfants sur l'axe secondaire.
- `CrossAxisAlignment.stretch` : Étire les enfants pour remplir l'axe secondaire.
- `CrossAxisAlignment.baseline` : Aligne les enfants sur la ligne de base du texte.



