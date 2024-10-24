---
MOOC: "[[Programmation]]"
Langage: 
Type: 
tags:
---
## 1. Ouvrir un fichier CSV
Pour ouvrir un fichier, il est nécessaire d'utiliser la fonction `fopen` :
Il faut ensuite utiliser la fonction `fgetcsv` afin de lire chacune des lignes. Attention : chaque fois que nous utilisons cette fonction, cela lit la ligne suivante.
```php
$filename = "Chemin vers mon fichier CSV";
$file = fopen($filename, 'r'); // "r" signifie en lecture seule
$row1 = fgetcsv($file); // Lecture de la première ligne
$row2 = fgetcsv($file); // Lecture de la deuxième ligne
$row3 = fgetcsv($file); // Lecture de la troisième ligne
...
```

## 2. Récupérer les différentes données de la ligne
Une fois que nous avons récupéré les différentes informations de la ligne, il faut lire les informations de chaque colonne. Prenons notre ligne : `$row` qui suite de la méthode `fgetcsv($file);`. Il faut faire `$valeur = $row[x]`, $x-1$ le numéro de la colonne


Prenons la ligne : `Thomas Venouil 18 France` :
```php
$row = fgetcsv($file);
$prenom = $row[0];
$nom = $row[1];
$age = $row[2];
$PaysNaissance = $row[3];
```


## 3. Code typique
```php
private function load(string $filename){
	$info1 = array();
	$info2 = array();
	$file = fopen($filename, 'r');
	fgetcsv($file) //Généralement, la première ligne contient infos de ctxt
	while(($row = fgetcsv($file)) !== false){
		$info1[] = $row[0];
		$info2[] = $row[1];
	}
}
```
Utilisation de [[Permanent/Programmation/PHP/Les listes|listes]]
