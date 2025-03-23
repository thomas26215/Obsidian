# Doctrine ORM : Introduction et Utilisation

## Qu'est-ce que Doctrine ORM ?

Doctrine ORM est une couche d'abstraction permettant de manipuler une **base de données relationnelle** en adoptant une approche orientée objet. Il permet d'éviter l'écriture de requêtes SQL complexes en offrant un système de gestion des entités en PHP.

Doctrine ORM résout plusieurs problèmes liés à la **persistance des données**, notamment :

- Récupérer les données (lecture)
- Ajouter de nouvelles entrées
- Mettre à jour les données existantes
- Supprimer des éléments

## Installer Doctrine ORM

Pour installer Doctrine ORM avec Symfony, utiliser la commande suivante :

```shell
composer require symfony/orm-pack
composer require --dev symfony/maker-bundle
```

## Configurer la connexion à la base de données

Modifier le fichier `.env` pour définir les informations de connexion :

```env
DATABASE_URL="mysql://username:password@127.0.0.1:3306/nom_de_la_base?serverVersion=mariadb-10.4.14"
```

## Créer une entité

Une entité est une représentation d'une table de la base de données sous forme de classe PHP. Pour générer une entité, utiliser la commande suivante :

```shell
php bin/console make:entity
```

Cette commande demandera :

- Le nom de l'entité
- Les attributs (colonnes de la table correspondante)
- Les types de données de ces attributs
- Les relations éventuelles avec d'autres entités

Exemple d'entité `Product` :

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

## Générer et exécuter les migrations

Une fois les entités créées ou modifiées, il est nécessaire de mettre à jour la structure de la base de données avec des migrations.

1. Générer une migration :
    
    ```shell
    php bin/console make:migration
    ```
    
2. Exécuter la migration :
    
    ```shell
    php bin/console doctrine:migrations:migrate
    ```
    

## Persister une entité dans un contrôleur

Une entité peut être enregistrée en base de données via un contrôleur en utilisant le **ManagerRegistry**.

Exemple :

```php
use App\Entity\Product;
use Symfony\Component\HttpFoundation\Response;
use Doctrine\Persistence\ManagerRegistry;

public function createProduct(ManagerRegistry $doctrine): Response
{
    $product = new Product();
    $product->setName('Keyboard');
    $product->setPrice(1999);

    $em = $doctrine->getManager();
    $em->persist($product);
    $em->flush();

    return new Response('Produit créé avec succès !');
}
```

## Récupérer des données depuis la base

Doctrine fournit plusieurs méthodes pour récupérer des données via le Repository d'une entité.

Exemple :

```php
$product = $doctrine->getRepository(Product::class)->find($id);
$products = $doctrine->getRepository(Product::class)->findAll();
$product = $doctrine->getRepository(Product::class)->findOneBy(['name' => 'Keyboard']);
```

## Mettre à jour et supprimer une entité

### Mettre à jour un produit

```php
$product = $doctrine->getRepository(Product::class)->find($id);
if ($product) {
    $product->setPrice(2499);
    $em = $doctrine->getManager();
    $em->flush();
}
```

### Supprimer un produit

```php
$product = $doctrine->getRepository(Product::class)->find($id);
if ($product) {
    $em = $doctrine->getManager();
    $em->remove($product);
    $em->flush();
}
```

## Relations entre entités

Doctrine permet de définir des relations entre entités :

- `OneToOne`
- `OneToMany`
- `ManyToOne`
- `ManyToMany`

Exemple d'une relation `OneToMany` entre `Category` et `Product` :

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

## Conclusion

Doctrine ORM est un outil puissant qui facilite la gestion des bases de données en PHP. Il permet de travailler avec une approche orientée objet, de générer automatiquement des migrations et de manipuler les entités de manière intuitive. Il est essentiel de bien comprendre son fonctionnement pour éviter les erreurs et optimiser la gestion des données.