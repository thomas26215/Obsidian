---
MOOC: "[[Programmation]]"
Langage: PHP
Type: 
tags: 
Complete: true
Learned: true
---
PHP inclut une variété d'opérateurs:

- Arithmétiques: `+`, `-`, `*`, `/`, `%`
- Comparaison: == , `!=`, `<`, `<=`, `>`, `>=`, = = = , `!==`
- Logiques: `AND`, `&&`, `OR`, `||`, `XOR`

## Structures de contrôle

PHP offre les structures de contrôle classiques:
```php
if ($condition)
{
	// code
} elseif ($autre_condition)
{
	// code
} else {
	// code
}
for ($i = 0; $i < 10; $i++) {
	// code
} while ($condition) {
	// code
}
switch ($variable)
{
	case 'valeur1':
		// code
		break;
	default:
		// code
}
```