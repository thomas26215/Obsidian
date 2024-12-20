Pour récupérer des données après un `SELECT` en utilisant PDO en PHP, voici les différentes méthodes que vous pouvez utiliser, accompagnées d'exemples pratiques.

## Récupération des données avec PDO

Lorsque vous exécutez une requête `SELECT`, vous obtenez un objet `PDOStatement`. Pour extraire les données de cet objet, vous pouvez utiliser plusieurs méthodes telles que `fetch()`, `fetchAll()`, ou d'autres variantes. Voici comment procéder :

### 1. Utilisation de `fetch()`

La méthode `fetch()` permet de récupérer une seule ligne du résultat de la requête. Chaque appel à `fetch()` renvoie la ligne suivante.

**Exemple :**

```php
<?php
try {
    $pdo = new PDO('sqlite:database.sqlite');
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    
    $stmt = $pdo->query("SELECT * FROM utilisateurs");
    
    while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
        echo "Nom : " . $row['nom'] . ", Email : " . $row['email'] . "<br>";
    }
} catch (PDOException $e) {
    echo "Erreur : " . $e->getMessage();
}
?>
```

### 2. Utilisation de `fetchAll()`

Si vous souhaitez récupérer toutes les lignes d'un coup, utilisez la méthode `fetchAll()`. Cela renvoie un tableau contenant toutes les lignes.

**Exemple :**

```php
<?php
try {
    $pdo = new PDO('sqlite:database.sqlite');
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    
    $stmt = $pdo->query("SELECT * FROM utilisateurs");
    $users = $stmt->fetchAll(PDO::FETCH_ASSOC);
    
    foreach ($users as $user) {
        echo "Nom : " . $user['nom'] . ", Email : " . $user['email'] . "<br>";
    }
} catch (PDOException $e) {
    echo "Erreur : " . $e->getMessage();
}
?>
```

### 3. Utilisation de `fetchColumn()`

Si vous avez besoin de récupérer une seule colonne d'une seule ligne, vous pouvez utiliser `fetchColumn()`. Cela est utile lorsque vous savez que votre requête ne renverra qu'une seule valeur.

**Exemple :**

```php
<?php
try {
    $pdo = new PDO('sqlite:database.sqlite');
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    
    $stmt = $pdo->query("SELECT email FROM utilisateurs WHERE nom = 'John Doe'");
    $email = $stmt->fetchColumn();
    
    echo "Email de John Doe : " . $email;
} catch (PDOException $e) {
    echo "Erreur : " . $e->getMessage();
}
?>
```

### 4. Récupérer plusieurs colonnes avec des conditions

Si vous souhaitez récupérer des données basées sur certaines conditions, utilisez une [[PDO - Exécution de requête préparée|requête préparée]] avec des paramètres.

**Exemple :**

```php
<?php
try {
    $pdo = new PDO('sqlite:database.sqlite');
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    
    // Préparation de la requête
    $stmt = $pdo->prepare("SELECT * FROM utilisateurs WHERE nom = :nom");
    // Liaison du paramètre
    $stmt->execute([':nom' => 'John Doe']);
    
    // Récupération des résultats
    while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
        echo "Nom : " . $row['nom'] . ", Email : " . $row['email'] . "<br>";
    }
} catch (PDOException $e) {
    echo "Erreur : " . $e->getMessage();
}
?>
```

## Conclusion

Après avoir exécuté une requête `SELECT`, vous pouvez facilement récupérer les données en utilisant les méthodes appropriées de l'objet `PDOStatement`. Choisissez la méthode qui correspond le mieux à vos besoins en fonction de la quantité et du type de données que vous souhaitez traiter. Les méthodes `fetch()`, `fetchAll()`, et `fetchColumn()` sont les plus courantes pour manipuler les résultats des requêtes SQL en PHP avec PDO.