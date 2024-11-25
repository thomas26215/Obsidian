---
MOOC: "[[Programmation]]"
Langage: PHP
Type: Les bases
tags: 
Complete: true
Learned: true
---
En PHP, la déclaration se fait de la manière suivante :
```PHP
$variable = 10;
$variable2 = "Thomas";
```
Et oui, les variables en déclarées n'ont pas besoin d'être déclarées. Elles savent directement leurs types quand on rentre le contenu.

L'utilisation peut être faite de la manière suivante :
```PHP
echo $variable;
```

Nous avons ici utilisé la balise `echo` afin d'afficher la variable

Il existe plusieurs types de données :
- Les entiers
- Les booléens
- Les flottants
- Les chaînes de caractères

Nous définissons les constantes avec `define()` ou `const`
**Exemple :**
```php
define("pi", 3.14159);
const TAUX = 6.55957;
```

