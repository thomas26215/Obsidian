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

