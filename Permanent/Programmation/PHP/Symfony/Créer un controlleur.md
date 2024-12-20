---
MOOC: "[[Programmation]]"
Langage: PHP - Symfony
Type: Contrôleur
tags:
---
### Commande de Création

Pour créer un nouveau contrôleur dans Symfony, il faut utiliser la commande :

```shell
php bin/console make:controller NomDuController
```

La commande `make:controller` va automatiquement :

1. Créer un fichier de contrôleur dans `src/Controller`
2. Générer une méthode `index()` par défaut
3. Ajouter [[Définition des routes|une route]] de base
4. Créer un template Twig correspondant

### Exemple de Contrôleur Généré

```php
<?php
namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;

class NomDuController extends AbstractController
{
    #[Route('/route', name: 'app_nom_du')]
    public function index(): Response
    {
        return $this->render('nom_du/index.html.twig', [
            'controller_name' => 'NomDuController',
        ]);
    }
}
```

### Points Importants

- Utilisez le **PascalCase** pour nommer votre contrôleur
- Le suffixe `Controller` est une convention recommandée
- Le contrôleur étend toujours `AbstractController`

![[Pasted image 20241210162638.png]]