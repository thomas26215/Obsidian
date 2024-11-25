---
MOOC: "[[Programmation]]"
Langage: PHP
Type: BDD
tags:
---
## Introduction à PDO et SQLite

PDO (PHP Data Objects) est une interface d'abstraction pour accéder aux bases de données en PHP. Elle offre une approche orientée objet et un socle commun pour se connecter à différents systèmes de gestion de bases de données (SGBD).SQLite est un SGBD léger intégré directement à PHP, qui stocke toute la base de données dans un seul fichier.

## Connexion à la base de données

Pour se connecter à une base de données SQLite avec PDO :

```php
try {
	$dbh = new PDO('sqlite:chemin/vers/fichier.db');
	$dbh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e){
	 die("Erreur de connexion : " . $e->getMessage());
}
```

Le Data Source Name (DSN) pour SQLite est simplement le chemin vers le fichier de la base de données.

## Exécution de requêtes simples

Pour exécuter une requête simple :

```php
$sql = "INSERT INTO utilisateurs (nom, email) VALUES ('John Doe', 'john@example.com')";
$dbh->exec($sql);
```

## Requêtes préparées

Les requêtes préparées offrent une meilleure sécurité et performance :

```php
$stmt = $dbh->prepare("INSERT INTO utilisateurs (nom, email) VALUES (:nom, :email)");
$stmt->bindParam(':nom', $nom);
$stmt->bindParam(':email', $email);

$nom = "Jane Doe";
$email = "jane@example.com";
$stmt->execute();
```

## Récupération de données

Pour récupérer des données :

```php
$stmt = $dbh->query("SELECT * FROM utilisateurs");
while ($row = $stmt->fetch(PDO::FETCH_ASSOC))
{
	echo $row['nom'] . " - " . $row['email'] . "<br>";
}
```

## Gestion des transactions

PDO permet de gérer facilement les transactions :

```php
try {
	$dbh->beginTransaction();
	// Exécuter plusieurs requêtes ici
	$dbh->commit();
} catch (Exception $e)
{
	$dbh->rollBack();
	echo "Erreur : " . $e->getMessage();
}
```

## Fermeture de la connexion

La connexion se ferme automatiquement à la fin du script, mais on peut la fermer explicitement :

`$dbh = null;`