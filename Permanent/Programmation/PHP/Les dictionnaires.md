---
MOOC: "[[Programmation]]"
Langage: PHP
Type: Listes
tags:
---
Voici comment déclarer et initialiser un dictionnaire :
```PHP
$liste = array('Thomas' => 'Venouil', 'Sophie' => 'Arnaud', 'Brayan' => 'Bils');
```

>[!info] Récupérer une valeur ?
> Pour récupérer une valeur, il faut que je l'appelle pas sa clé (`cle => valeur`)

Ainsi, je peux appeler une valeur de cette manière :
```PHP
$valeur = liste["Thomas"];

// Ce que ça me retournera : "Venouil"
```

# Boucler pour récupérer toutes le valeurs du dictionnaire
De la même manière qu'en Java, il est possible de faire un boucle `foreach` afin de boucler sur toutes les valeurs :
```PHP
$output
$output = "<table>\n"
foreach($liste as $cle => $valeur){
	$output .=  " <tr><th>$cle</th><td>$valeur</td></tr>\n"
}
$output .= "</table>"
```
- Cette boucle parcourt chaque élément du tableau et place pour chaque élément la clé dans la variable `$cle` et la valeur dans la variable `$valeur`
- Il est maintenant possible d'afficher ce tableau qui est un tableau de paire clé-valeur