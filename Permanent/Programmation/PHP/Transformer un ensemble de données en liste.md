## Les tableaux indexés

### Transformer un élément en liste
Lorsqu'on travaille avec des fonctions qui acceptent des listes (ou tableaux), il est souvent nécessaire de transformer un élément, qu'il s'agisse d'un entier, d'une chaîne de caractères, d'un nombre à virgule flottante, ou d'autres types, en liste. Cela permet de passer ces éléments en tant que paramètres dans des fonctions qui attendent un tableau (`$array`). Voici comment procéder :

#### Exemple avec un entier
Prenons une variable `$entier` que nous souhaitons passer en paramètres dans une fonction. Pour la transformer en liste, nous utilisons la syntaxe suivante :

```php
$liste = [$entier];
```

<mark style="background: #BBFABBA6;">Exemple :</mark>
```php
public function read(int $id) {
    $dao = DAO::get();
    try {
        $liste = [$id]; // Je transforme mon entier en liste
        $result = $dao->query("SELECT * FROM contact WHERE id = ?", $liste);
        return new Contact($result[0]["prenom"], $result[0]["nom"], $result[0]["phone"]);
    } catch (Exception $e) {
	        // Gestion des erreurs
        echo "Erreur : " . $e->getMessage();
    }
}
```

#### Exemple avec une chaîne de caractères
De même, si vous avez une chaîne de caractères que vous souhaitez passer comme liste :

```php
$chaine = "exemple";
$liste = [$chaine]; // Transforme la chaîne en liste
```

#### Exemple avec un nombre à virgule flottante
Pour un nombre à virgule flottante, la transformation est similaire :

```php
$float = 3.14;
$liste = [$float]; // Transforme le float en liste
```

### Transformer un ensemble d'éléments en liste
Il est également possible de transformer un ensemble d'éléments en liste. Par exemple, si vous avez plusieurs entiers, chaînes ou floats que vous souhaitez passer à une fonction, vous pouvez les rassembler dans un tableau. Voici quelques méthodes :

1. **Création manuelle d'un tableau** :
   ```php
   $entier1 = 1;
   $string1 = "test";
   $float1 = 2.5;
   $liste = [$entier1, $string1, $float1]; // Liste contenant différents types
   ```

2. **Utilisation de la fonction `range()`** :
   Pour créer une liste d'entiers consécutifs :
   ```php
   $liste = range(1, 10); // Crée un tableau contenant les entiers de 1 à 10
   ```

3. **Transformation d'un tableau existant** :
   Si vous avez déjà un tableau d'éléments et que vous souhaitez le transformer en liste :
   ```php
   $tableauExistants = [4, "texte", 5.5];
   $liste = array_values($tableauExistants); // Récupère les valeurs du tableau existant
   ```

### Conclusion
Transformer des éléments (qu'ils soient entiers, chaînes de caractères, floats ou autres types) en listes est une opération courante en PHP qui facilite le passage de paramètres dans les fonctions. Cela permet également de travailler plus facilement avec des ensembles de données dans des requêtes SQL ou d'autres opérations nécessitant des tableaux.