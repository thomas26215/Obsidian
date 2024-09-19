---
MOOC: "[[Programmation]]"
Langage: PHP
Type: Fonctions
tags:
---
Il est possible de faire appel à une fonction en PHP. Voici comment faire :
```PHP
$abbreviation = array(''=>'', ...);
function maFonction(string $name, int $age) : string{
	global $abbrevation;
	...
	return $name;
	
}
```

- Il faut tout d'abord que j'inclue les variables extérieures dans ma fonction (`global $abbreviation`)
- Je déclare ma fonction par `function`
- Je rentre en paramètres ce que je veux
- Enfin j'indique le type de retour par `: type`

Maintenant, il est possible d'appeler ce code PHP pour afficher quelque chose dans mon code HTML. Ici, nous imaginons que [[PHP dans le HTML|le code HTML se situe directement dans notre fichier PHP]] :
```PHP
<?php
$full_name = array('Thomas' => 'Venouil', 'Sophie' => 'Arnaud', ...);
function Surname(String first_name) : string{
	global $abbreviation;
	if(array_key_exists($first_name, $liste)){
		return "<bold>{$liste[$first_name]}</bold";
	}
	return first_name;
}
?>


/*
Structure HTML
*/
	<p>Mon prénom est Thomas et mon nom de famille est <?= Surname('Thomas') ?></p>
/*
Fin structure HTML
*/

```

- Le code php est évidement dans la structure `<?php ... ?>`, que ce soit la fonction ou bien la liste
- La fonction PHP vérifie si le prénom est dans la liste et renvoie le nom de famille si présente
	1. <mark style="background: #BBFABBA6;">Appeler la liste à l'intérieur de la fonction</mark> : `global $abbreviation`
	2. <mark style="background: #BBFABBA6;">Vérifier que la clé existe</mark> : `array_key_exists` ([[Les dictionnaires#Vérifier la présence d'un élément|Vérification d'un élément]])
	3. <mark style="background: #BBFABBA6;">Récupérer le nom de famille depuis le prénom</mark> : ([[Les dictionnaires]])
	4. Il faut retourner une string qui sera le code HTML à mettre
- On voit que comme pour le variables, il faut appeler la fonction la fonction par la synthaxe : `<?= fonction() ?>`

>[!info] Résumé
>**Créer la fonction :** `function name(string prenom, int age) : typeRetour{...}`
>**Appel de fonction dans HTML :** `<?= name("Thomas", 18) ?>`