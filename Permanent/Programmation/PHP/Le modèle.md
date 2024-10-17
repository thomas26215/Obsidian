---
MOOC: "[[Programmation]]"
Langage: PHP
Type: MVC
tags:
---
Le modèle représente la logique métier de l'application. Exemple :
```PHP
<?php
class Greeting{
	private string $name;
	const LANGUAGES = array{
		'anglais' => 'hello', ...
	};
	function __construct(string $name){...}
	function sayHelloIn(string $language) : string{...}
	public static function getAllLanguages():array{...}
}
?>
```