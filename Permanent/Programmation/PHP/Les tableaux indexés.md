---
MOOC: "[[Programmation]]"
Langage: PHP
Type: Listes
tags: 
Complete: true
Learned: true
---
Un tableau indexé se définit de cette manière :
```php
$fruits = array('pomme', 'poire', 'pêche');
```

Pour récupérer une valeur, il faut faire :
```php
$valeur = $fruits[index];
```

Il existe certaines opérations sur les tableaux, qui sont également disponibles pour les [[Les dictionnaires - Tableaux associatifs]]
- Ajout d'éléments : `$tableau[] = 'nouvelle valeur';`
- Taille d'un tableau : `count($tableau)` ou `sizeof($tableau)`
- Affichage : `print_r($tableau)` ou `var_dump($tableau)`
- Conversion chaîne/tableau : `explode()` et `implode()`