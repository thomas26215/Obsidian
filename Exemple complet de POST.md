```php
<?php
// Initialisation des variables
$nom = $prenom = $email = $age = $sexe = "";
$pizzas = [];
$errors = [];

// Vérification si le formulaire a été soumis
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Vérification si le bouton "Valider" a été cliqué
    if (isset($_POST['valider'])) {
        // Récupération et validation des données
        if (empty($_POST['nom'])) {
            $errors['nom'] = "Le nom est requis.";
        } else {
            $nom = htmlspecialchars(trim($_POST['nom']));
        }

        if (empty($_POST['prenom'])) {
            $errors['prenom'] = "Le prénom est requis.";
        } else {
            $prenom = htmlspecialchars(trim($_POST['prenom']));
        }

        if (empty($_POST['email'])) {
            $errors['email'] = "L'email est requis.";
        } elseif (!filter_var($_POST['email'], FILTER_VALIDATE_EMAIL)) {
            $errors['email'] = "Format d'email invalide.";
        } else {
            $email = htmlspecialchars(trim($_POST['email']));
        }

        if (empty($_POST['age'])) {
            $errors['age'] = "L'âge est requis.";
        } elseif (!is_numeric($_POST['age'])) {
            $errors['age'] = "L'âge doit être un nombre.";
        } else {
            $age = intval(trim($_POST['age']));
        }

        if (empty($_POST['sexe'])) {
            $errors['sexe'] = "Veuillez sélectionner votre sexe.";
        } else {
            $sexe = $_POST['sexe'];
        }

        if (isset($_POST['pizzas'])) {
            $pizzas = $_POST['pizzas'];
        }

        // Si aucune erreur, afficher les résultats
        if (empty($errors)) {
            echo "<h2>Résultats :</h2>";
            echo "Nom : " . $nom . "<br>";
            echo "Prénom : " . $prenom . "<br>";
            echo "Email : " . $email . "<br>";
            echo "Âge : " . $age . "<br>";
            echo "Sexe : " . ($sexe == 'm' ? 'Masculin' : 'Féminin') . "<br>";
            echo "Pizzas sélectionnées : " . implode(", ", $pizzas) . "<br>";
        }
    }
}
?>

<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulaire PHP</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        form { border: 1px solid #ccc; padding: 20px; border-radius: 5px; }
        label { display: block; margin-bottom: 5px; }
        input[type="text"], input[type="email"], input[type="number"], select { width: 100%; padding: 8px; margin-bottom: 10px; }
        input[type="submit"], input[type="reset"] { padding: 10px 15px; margin-right: 10px; }
        .error { color: red; font-size: 0.9em; }
    </style>
</head>
<body>

<h1>Formulaire d'inscription</h1>

<form action="" method="post">
    
    <fieldset>
        <legend>Informations Personnelles</legend>

        <label for="nom">Nom :</label>
        <input type="text" name="nom" id="nom" value="<?php echo htmlspecialchars($nom); ?>" required>
        <?php if (isset($errors['nom'])) echo "<div class='error'>".$errors['nom']."</div>"; ?>

        <label for="prenom">Prénom :</label>
        <input type="text" name="prenom" id="prenom" value="<?php echo htmlspecialchars($prenom); ?>" required>
        <?php if (isset($errors['prenom'])) echo "<div class='error'>".$errors['prenom']."</div>"; ?>

        <label for="email">Email :</label>
        <input type="email" name="email" id="email" value="<?php echo htmlspecialchars($email); ?>" required>
        <?php if (isset($errors['email'])) echo "<div class='error'>".$errors['email']."</div>"; ?>

        <label for="age">Âge :</label>
        <input type="number" name="age" id="age" value="<?php echo htmlspecialchars($age); ?>" required min="1">
        <?php if (isset($errors['age'])) echo "<div class='error'>".$errors['age']."</div>"; ?>

        <label>Sexe :</label>
        <input type="radio" name="sexe" value="m" <?php if ($sexe == 'm') echo 'checked'; ?>> Masculin
        <input type="radio" name="sexe" value="f" <?php if ($sexe == 'f') echo 'checked'; ?>> Féminin
        <?php if (isset($errors['sexe'])) echo "<div class='error'>".$errors['sexe']."</div>"; ?>
        
    </fieldset>

    <fieldset>
        <legend>Choix de Pizzas</legend>

        <label for="pizzas">Sélectionnez vos pizzas préférées :</label><br>
        <select name="pizzas[]" id="pizzas" multiple size="3">
            <option value="margherita" <?php if (in_array('margherita', $pizzas)) echo 'selected'; ?>>Margherita</option>
            <option value="pepperoni" <?php if (in_array('pepperoni', $pizzas)) echo 'selected'; ?>>Pepperoni</option>
            <option value="vegetarienne" <?php if (in_array('vegetarienne', $pizzas)) echo 'selected'; ?>>Végétarienne</option>
            <option value="quattro_stagioni" <?php if (in_array('quattro_stagioni', $pizzas)) echo 'selected'; ?>>Quattro Stagioni</option>
            <option value="bbq_chicken" <?php if (in_array('bbq_chicken', $pizzas)) echo 'selected'; ?>>BBQ Chicken</option>
        </select><br>

    </fieldset>

    <!-- Boutons de soumission -->
    <input type="submit" name="valider" value="Valider">
    <input type="reset" value="Réinitialiser">
</form>

</body>
</html>

```