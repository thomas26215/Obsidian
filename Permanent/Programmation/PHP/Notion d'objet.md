---
MOOC: "[[Programmation]]"
Langage: PHP
Type: Notion d'objet
tags: 
Complete: true
Learned:
---
Un objet en PHP est une entité logicielle qui possède :
- Des attributs (son "savoir")
- Des méthodes (son "savoir-faire")
Les objets sont créés à partir de classes, qui servent de modèles pour définir leur structure et leur comportement.
## Création et manipulation d'objets
## Déclaration de classe

```php
class Voiture {
	private string $marque;    
	private string $modele;     
	public function __construct(string $ma, string $mo) {        
		$this->marque = $ma;        
		$this->modele = $mo;    
	}
}
```

## Instanciation d'un objet

```php
$v = new Voiture('Renault', 'Kangoo');
```

## Accès aux attributs et méthodes

En PHP, on utilise la notation flèche (->) pour accéder aux attributs et méthodes d'un objet :
```php
$v->couleur = 'rouge'; $v->demarrer();
```

## Caractéristiques du modèle objet PHP
## Dynamicité

PHP permet d'ajouter ou de supprimer des attributs publics de manière dynamique :
```php
$v->nouveauAttribut = 'valeur';
```

## Référence aux objets

Les variables contenant des objets stockent en réalité une référence à l'objet. Lors d'une affectation ou d'un passage en paramètre, c'est cette référence qui est copiée.

## Visibilité des attributs et méthodes

PHP supporte trois niveaux de visibilité :

- `public` : accessible de partout
- `private` : accessible uniquement au sein de la classe
- `protected` : accessible dans la classe et ses sous-classes

## Constructeur et destructeur

Le constructeur est défini par la méthode `__construct()`. Il n'y a pas de surcharge de constructeur en PHP.

```php
function __construct(string $ma, string $mo) 
{
	$this->marque = $ma;    
	$this->modele = $mo;
}
```

Le destructeur, rarement utilisé, est défini par `__destruct()`.

## Getters et Setters

Pour contrôler l'accès aux attributs privés, on utilise des getters et setters :

```php
public function getMarque()
{     
	return $this->marque; 
}
public function setModele(string $value)
{     
	$this->modele = $value;
}
```

PHP offre également des méthodes magiques `__get()` et `__set()` pour un contrôle global des accès