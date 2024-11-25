---
MOOC: "[[Programmation]]"
Langage: PHP
Type: Tests Unitaires avec MOCK pour BDD
tags:
---
([[MOCK sur une BDD]])
```php
parent::setUp(){
	$this->dbMock = $this->createMock(PDO::class);
	
	$this->userBase = new UserBase();
	$this->setPrivateProperty($this->userBase, 'db', $this->dbMock);
}

private function setPrivateProperty($object, $propertyName, $value){
	$reflection = new ReflectionClass($object);
	$property = $reflection->getProperty($propertyName);
	$property->setAccessible(true);
	$property->setValue($object, $value);
}
```

^eea6a6

1. Tout d'abord, un objet [[MOCK]] de PDO va être crée pour simuler une connexion à la 
⇒ `$this->dbMock = $this->createMock(PDO::class);`
2. Ce [[MOCK]] va être injecté dans la classe `UserBase` à tester, ce qui va remplacer la vraie connexion PDO
   ⇒ `$this->setPrivateProperty($this->userBase, 'db', $this->dbMock);`

>[!warning] Point essentiel !! ^important
>Il est primordiale de comprendre que la fonction `setPrivateProperty(...){...}` est utliisée pour injecter un mock de PDO dans l'objet `userBase`, ce qui permet d'assurer que les opérations effectuées lors des tests n'interagissent pas avec la vraie BDD
>
>Autrement dit, cette fonction va remplacer la connexion réelle à la BDD dans l'objet `UserBase` par un mock de PDO, ce qui signifiera que toutes les opérations de BDD dans `UserBase` utiliseront ce mock au lieu d'une vraie connexion