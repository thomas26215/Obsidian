Pour exécuter une requête simple :

```php
$sql = "INSERT INTO utilisateurs (nom, email) VALUES ('John Doe', 'john@example.com')";
$dbh->exec($sql);
```