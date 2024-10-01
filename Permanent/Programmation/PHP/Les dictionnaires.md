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

# Boucler pour récupérer toutes  les valeurs du dictionnaire
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

# Vérifier la présence d'un élément
Il est possible de vérifier si un clé existe dans un dictionnaire :
```PHP
$liste = array('Thomas' => 'Venouil', ...);

function checkKeyInArray(string  $cle):String{
	global $liste
	if(array_key_exists($element, $cle)){
		//Code
	}
}
```

- Nous avons notre liste `$liste`
- Nous créons une [[Les fonctions|fonction]] qui prend en paramètres un string `$element`
- Nous faisons `$global $liste` pour récupérer la liste qui n'est pas dans la fonction
- Nous vérifions si une clé est présent dans la liste par la fonction `array_key_exists`

>[!Warning] Eviter les erreurs
>Généralement, nous vérifions si  la clé existe dans la liste pour éviter de faire une recherche d'élément avec une clé qui n'existe pas. **C'est donc une condition préalable pour éviter de faire des erreurs**