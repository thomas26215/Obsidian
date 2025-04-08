## Qu'est-ce que Doctrine ORM ?

Doctrine ORM est une couche d'abstraction qui facilite la gestion des bases de données relationnelles en adoptant une approche orientée objet. En utilisant Doctrine, vous pouvez manipuler des objets PHP sans avoir à écrire directement des requêtes SQL. Cela simplifie les opérations CRUD (Create, Read, Update, Delete) et améliore la maintenabilité du code.

### Avantages de Doctrine ORM
- Permet de travailler avec des objets PHP au lieu de tables SQL.
- Simplifie les relations entre les entités (OneToOne, ManyToOne, etc.).
- Offre des fonctionnalités avancées comme la persistance en cascade et la gestion des événements.

---

## Installer Doctrine ORM

Pour intégrer Doctrine dans un projet Symfony, exécutez les commandes suivantes :

```bash
composer require symfony/orm-pack
composer require --dev symfony/maker-bundle
```

Ces commandes installent Doctrine ORM ainsi que l'outil MakerBundle pour générer facilement des entités et autres composants.

---

## Configurer la connexion à la base de données

Dans le fichier `.env`, configurez les informations de connexion à votre base de données :

```env
DATABASE_URL="mysql://username:password@127.0.0.1:3306/nom_de_la_base?serverVersion=mariadb-10.4.14"
```

Remplacez `username`, `password`, et `nom_de_la_base` par vos propres paramètres.

---

## Créer une entité

Une entité représente une table dans la base de données sous forme de classe PHP. Pour générer une entité, utilisez la commande suivante :

```bash
php bin/console make:entity
```

Vous serez invité à :
- Donner un nom à l'entité.
- Définir ses attributs (colonnes).
- Spécifier leurs types (string, integer, etc.).

### Exemple d'entité `Product`

```php
namespace App\Entity;

use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity]
class Product
{
    #[ORM\Id]
    #[ORM\GeneratedValue]
    #[ORM\Column(type: 'integer')]
    private int $id;

    #[ORM\Column(type: 'string', length: 255)]
    private string $name;

    #[ORM\Column(type: 'decimal', scale: 2)]
    private float $price;
}
```

---

## Générer et exécuter les migrations

Les migrations permettent de synchroniser la structure de votre base de données avec vos entités.

1. **Générer une migration** :
   ```bash
   php bin/console make:migration
   ```

2. **Exécuter la migration** :
   ```bash
   php bin/console doctrine:migrations:migrate
   ```

---

## Persister une entité dans un contrôleur

Pour enregistrer une entité en base de données, utilisez l'EntityManager fourni par Doctrine :

### Exemple : Créer un produit

```php
use App\Entity\Product;
use Symfony\Component\HttpFoundation\Response;
use Doctrine\ORM\EntityManagerInterface;

public function createProduct(EntityManagerInterface $entityManager): Response
{
    $product = new Product();
    $product->setName('Keyboard');
    $product->setPrice(1999);

    $entityManager->persist($product);
    $entityManager->flush();

    return new Response('Produit créé avec succès !');
}
```

---

## Récupérer des données depuis la base

Doctrine offre plusieurs méthodes pour récupérer des données via le Repository associé à chaque entité.

### Exemple : Récupérer un produit

```php
$product = $doctrine->getRepository(Product::class)->find($id);
$products = $doctrine->getRepository(Product::class)->findAll();
$product = $doctrine->getRepository(Product::class)->findOneBy(['name' => 'Keyboard']);
```

---

## Mettre à jour et supprimer une entité

### Mettre à jour un produit

```php
$product = $doctrine->getRepository(Product::class)->find($id);
if ($product) {
    $product->setPrice(2499);
    $entityManager->flush();
}
```

### Supprimer un produit

```php
$product = $doctrine->getRepository(Product::class)->find($id);
if ($product) {
    $entityManager->remove($product);
    $entityManager->flush();
}
```

---

## Relations entre entités

Doctrine permet de définir des relations entre les entités pour gérer les associations entre tables.

### Exemple : Relation OneToMany entre `Category` et `Product`

```php
class Category
{
    #[ORM\OneToMany(mappedBy: 'category', targetEntity: Product::class)]
    private Collection $products;
}

class Product
{
    #[ORM\ManyToOne(targetEntity: Category::class, inversedBy: 'products')]
    #[ORM\JoinColumn(nullable: false)]
    private Category $category;
}
```

---

## Validation avant persistance

Symfony Validator s'intègre parfaitement avec Doctrine pour valider les données avant leur persistance.

### Exemple : Validation d'une entité `User`

```php
namespace App\Entity;

use Symfony\Component\Validator\Constraints as Assert;

class User
{
    #[Assert\NotBlank]
    private string $name;

    #[Assert\Email]
    private string $email;
}
```

---

## Optimisation de la persistance

Pour insérer ou mettre à jour un grand nombre d'entités efficacement, utilisez le traitement par lots :

```php
$batchSize = 20;
for ($i = 1; $i setName('User ' . $i);

    $entityManager->persist($user);

    if (($i % $batchSize) === 0) {
        $entityManager->flush();
        $entityManager->clear();
    }
}
$entityManager->flush();
```

