Pour ajouter des paramètres à une requête préparée en utilisant PDO avec SQLite, vous pouvez utiliser la méthode `bindParam()` ou `bindValue()`. Voici comment procéder :

## Utilisation de bindParam()

```php
$stmt = $dbh->prepare("INSERT INTO utilisateurs (nom, email) VALUES (:nom, :email)");
$nom = "Jane Doe";
$email = "jane@example.com";
$stmt->bindParam(':nom', $nom, PDO::PARAM_STR);
$stmt->bindParam(':email', $email, PDO::PARAM_STR);
$stmt->execute();
```

## Utilisation de bindValue()

```php
$stmt = $dbh->prepare("INSERT INTO utilisateurs (nom, email) VALUES (:nom, :email)");
$stmt->bindValue(':nom', "John Doe", PDO::PARAM_STR);
$stmt->bindValue(':email', "john@example.com", PDO::PARAM_STR);
$stmt->execute();
```

Il est important de noter que :

1. `bindParam()` lie une référence à une variable. Si la valeur de la variable change avant l'exécution, la nouvelle valeur sera utilisée.

2. `bindValue()` lie directement une valeur. C'est utile pour lier des valeurs immédiates ou des éléments de tableau.

3. Pour les requêtes LIKE, n'incluez pas les caractères '%' dans la requête préparée. Ajoutez-les à la variable PHP avant de la lier[4].

Exemple avec LIKE :

```php
$keyword = "%".$_GET['keyword']."%";
$stmt = $dbh->prepare("SELECT * FROM utilisateurs WHERE nom LIKE :keyword");
$stmt->bindParam(':keyword', $keyword, PDO::PARAM_STR);
$stmt->execute();
```

Ces méthodes améliorent la sécurité en prévenant les injections SQL et augmentent les performances en permettant la réutilisation des requêtes préparées.