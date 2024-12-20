Les requêtes préparées offrent une meilleure sécurité et performance que les [[PDO - Exécution de requête simple|requête simple]] :

```php
$stmt = $dbh->prepare("INSERT INTO utilisateurs (nom, email) VALUES (:nom, :email)");
$stmt->bindParam(':nom', $nom);
$stmt->bindParam(':email', $email);

$nom = "Jane Doe";
$email = "jane@example.com";
$stmt->execute();
```