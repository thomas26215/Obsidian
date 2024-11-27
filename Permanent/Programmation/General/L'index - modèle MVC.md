Dans le cadre du [[Le modèle MVC en PHP]], il se peut qu'il puisse exister un index qui fait office de routeur. Il va être chargé de rediriger l'utilisateur vers les différents les [[Le contrôleur - MVC|contrôleurs]] en recevant les différentes informations. Par exemple, si l'utilisateur clique sur un bouton qui doit rediriger vers la page de `login`, l'informations sera redirigée vers l'index et celui-ci va permettre de rediriger vers la page de `login`

**Par exemple, en PHP :**
```php
<?php

$ctrl $_GET['ctrl'] ?? 'login'; //Par défaut, page login affichée

const CTRLS = ['login', 'register', 'dashboard'];

if(!in_array($ctrl, CTRLS)){
	$require_once('view/error.view.php');
	exit(0);
}

//On appelle le contrôleur
$path = 'controler/' . $ctrl . '.ctrl.php'; //Le chemin du contrôleur
require_once($path);
```