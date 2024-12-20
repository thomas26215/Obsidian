Il faut s'assurer que l'extension PDO SQlite est activée dans sa configuration PHP :

```php
try {
	$pdo = new PDO('sqlite:' . __DIR__ . '/database.sqlite');
	$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
	$pdo->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC);
} catch(PDOException $e) {
	die("Erreur de connexion : " . $e->getMessage());
}
```