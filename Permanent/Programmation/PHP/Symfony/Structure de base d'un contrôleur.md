---
MOOC: "[[Programmation]]"
Langage: PHP - Symfony
Type: Contrôleur
tags:
---
## Création d'un Contrôleur de Base dans Symfony

Les contrôleurs sont au cœur du modèle MVC dans Symfony, gérant la logique de l'application et la réponse aux requêtes HTTP. Voici un exemple de base de création d'un contrôleur :

```php
namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;

class MonController extends AbstractController {
    public function index(): Response {
        return new Response('Hello, world!');
    }
}
```

### Points Clés :

1. **Namespace** : Les contrôleurs sont généralement placés dans le namespace `App\Controller`.
2. **Héritage** : La classe étend `AbstractController`, fournissant des méthodes utilitaires et l'accès aux services Symfony.
3. **Méthode d'Action** : `index()` est une méthode d'action simple retournant une réponse HTTP.
4. **Objet Response** : La méthode retourne un objet `Response`, encapsulant la réponse HTTP.
5. **Type de Retour** : L'utilisation de `: Response` spécifie le type de retour, améliorant la lisibilité et la sûreté du code.
L'extension de `AbstractController` est cruciale car elle offre des fonctionnalités essentielles de Symfony, comme le rendu de templates, la gestion des sessions, et l'accès aux services.
