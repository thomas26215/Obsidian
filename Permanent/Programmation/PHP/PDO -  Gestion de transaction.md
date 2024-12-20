Pour gérer les transactions en utilisant PDO avec SQLite, voici un guide détaillé qui explique les étapes nécessaires, accompagné d'exemples de code.

## Gestion des Transactions avec PDO

Les transactions permettent de regrouper plusieurs opérations SQL en une seule unité de travail. Cela garantit que toutes les modifications sont appliquées ou aucune d'entre elles ne l'est, ce qui est essentiel pour maintenir l'intégrité des données.

### 1. Concepts de Base

Les transactions reposent sur quatre propriétés fondamentales connues sous l'acronyme ACID :
- **Atomicité** : Toutes les opérations dans la transaction réussissent ou aucune ne réussit.
- **Consistance** : La base de données passe d'un état valide à un autre état valide.
- **Isolation** : Les transactions concurrentes ne se perturbent pas mutuellement.
- **Durabilité** : Une fois qu'une transaction est validée, elle persiste même en cas de panne.

### 2. Étapes pour Gérer une Transaction

Voici les étapes à suivre pour gérer une transaction avec PDO :

#### a. Démarrer une transaction

Utilisez la méthode `beginTransaction()` pour commencer une nouvelle transaction.

#### b. Exécuter les requêtes

Préparez et exécutez vos requêtes SQL.

#### c. Valider la transaction

Si toutes les opérations réussissent, utilisez `commit()` pour valider la transaction.

#### d. Annuler la transaction

Si une erreur se produit, utilisez `rollBack()` pour annuler toutes les modifications effectuées dans le cadre de cette transaction.

### 3. Exemple de Code

Voici un exemple complet illustrant comment gérer une transaction :

```php
<?php
try {
    // Connexion à la base de données SQLite
    $pdo = new PDO('sqlite:database.sqlite');
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    // Démarrer la transaction
    $pdo->beginTransaction();

    // Préparation des requêtes
    $stmt1 = $pdo->prepare("UPDATE comptes SET solde = solde - :montant WHERE nom = :nom");
    $stmt2 = $pdo->prepare("UPDATE comptes SET solde = solde + :montant WHERE nom = :nom");

    // Définition des paramètres
    $montant = 50;
    
    // Retrait du Compte1
    $cpte1 = 'Compte1';
    $stmt1->bindParam(':nom', $cpte1);
    $stmt1->bindParam(':montant', $montant);
    
    // Exécution de la première requête
    if (!$stmt1->execute()) {
        throw new Exception("Erreur lors du retrait du compte.");
    }

    // Crédit du Compte2
    $cpte2 = 'Compte2';
    $stmt2->bindParam(':nom', $cpte2);
    $stmt2->bindParam(':montant', $montant);
    
    // Exécution de la deuxième requête
    if (!$stmt2->execute()) {
        throw new Exception("Erreur lors du crédit du compte.");
    }

    // Valider la transaction
    $pdo->commit();
    echo "Transaction réussie !";

} catch (Exception $e) {
    // Annuler la transaction en cas d'erreur
    if ($pdo->inTransaction()) {
        $pdo->rollBack();
        echo "Transaction annulée : " . $e->getMessage();
    }
}
?>
```

### 4. Explications du Code

- **Connexion** : On établit une connexion à une base de données SQLite.
- **beginTransaction()** : Démarre une nouvelle transaction.
- **Préparation et exécution des requêtes** : On prépare deux requêtes pour débiter un compte et créditer un autre.
- **Validation ou annulation** :
  - Si toutes les opérations réussissent, `commit()` est appelé pour valider les changements.
  - Si une erreur se produit, `rollBack()` est appelé dans le bloc `catch` pour annuler toutes les modifications.

### 5. Conclusion

La gestion des transactions avec PDO est essentielle pour garantir l'intégrité des données dans votre application. En utilisant `beginTransaction()`, `commit()`, et `rollBack()`, vous pouvez vous assurer que vos opérations sur la base de données sont atomiques et cohérentes.