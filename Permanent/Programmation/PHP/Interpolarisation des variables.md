---
MOOC: "[[Programmation]]"
Langage: PHP
Type: Chaînes de charactères
tags: 
Complete: 
Learned:
---
L'interpolation permet d'insérer directement la valeur d'une variable dans une chaîne :

```php
$nom = 'Gwenn'; echo "Bonjour $nom"; // Affiche : Bonjour Gwenn
```

Pour éviter les ambiguïtés, on peut utiliser les accolades :

```php
echo "Bonjour {$nom}_Dupont";
```