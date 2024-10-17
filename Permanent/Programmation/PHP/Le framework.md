---
MOOC: "[[Programmation]]"
Langage: PHP
Type: MVC
tags:
---
Le framework MVC sert à simplifier et standardiser la gestion des vues dans une architecture MVC. Cela permet de séparer les responsabilité, de simplifier la gestion de paramètres, une meilleur flexibilité et une meilleure convention de nommage.

>[!info]
>Concrètement, elle ne fait que charger un fichier du répertoire `view` puis arrête le code avec `exit(0);`


<mark style="background: #BBFABBA6;">Exemple</mark> :
```php
<?php 

// Classe minimaliste pour normaliser l'usage d'une vue
// Cette classe est inspiré du moteur et compilateur de template Smarty
class View {
// Paramètres de la vue, dans un tableau associatif
private array $param;
// Chemin vers le fichier de la vue
private string $filePath;

// Constructeur d'une vue
function __construct() {
	// Initialise un tableau vide de paramètres
	$this->param = array();
}

// Ajoute un paramètre à la vue
// Il n'y a aucune contrainte de type pour la valeur
// Cela peut être par exemple un objet du modèle.

function assign(string $varName,$value) {
	$this->param[$varName] = $value;
}

// Affiche la vue : on indique uniquement son nom
function display(string $view) {

	// Ajoute le chemin relatif vers le fichier de la vue
	// ATTENTION: pour éviter de créer une variable locale $filePath qui risque
	// de se collisionner avec les variables de la vue, utilise un attribut de l'objet
	$this->filePath = "view/".$view.'.view.php';
	
	// Tous les paramètres de $this-param sont dupliqués en des variables
	// locales à la fonction display. Cela simplifie l'expression des
	// valeurs de la vue. Il faut simplement utiliser <?= $variable
	
	// Parcourt touts les paramètres de la vue
	foreach ($this->param as $key => $value) {
		// La notation $$ désigne une variable dont le nom est dans une autre variable
		// Cela crée une variable locale dont le nom est dans la variable $key
		$$key = $value;
	}
	
	// Inclusion de la vue
	// Comme cette inclusion est dans la portée de la méthoe display alors
	
	// seules les variables locales à display sont visibles.
	require($this->filePath);
	// Apres cela le PHP est terminé, plus rien ne s'exécute
	exit(0);
	}
}
?>
```

- Les variables : 
	- `private array $param;` = un tableau associatif pour stocker les variables à passer à la vue
	- `private string $filePath;` ⇒ Le chemin vers les fichiers de la vue
- Le constructeur de la vue ⇒ Initialise le tableau de paramètres
- Fonction `assign` ⇒ Permet d'ajouter les variables à la vue, variables qui seront accessibles dans le fichier de vue
- Fonction `display` ⇒ Méthode qui le coeur du système :
	1. Construire le chemin du fichier de vue
	2. Elle crée des variables locales à partir des paramètres assignés.
	3. Elle inclut le fichier de vue.
	4. Elle termine l'exécution du script