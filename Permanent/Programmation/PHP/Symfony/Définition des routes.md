---
MOOC: "[[Programmation]]"
Langage: PHP - Symfony
Type: Routage
tags:
---
# Syntaxe de Base

La méthode recommandée pour définir des routes dans Symfony est d'utiliser l'attribut `#[Route]`. Cela permet de lier un chemin URL à une méthode de contrôleur. La syntaxe générale est la suivante :

```php
#[Route("chemin", name: "nom_de_la_route")]
```

- **chemin** : Il s'agit de l'URL que l'utilisateur doit visiter pour accéder à cette route.
- **nom_de_la_route** : C'est un identifiant unique pour la route, qui peut être utilisé pour générer des URLs ou rediriger vers cette route dans le code.

# Exemple Pratique
## Exemple 1

Prenons un exemple concret :

```php
#[Route("/", name: "login")]
public function index(): Response {
	return new Response('Page de connexion');
}
```

Dans cet exemple :

- Le chemin est `/`, ce qui signifie que cette route sera accessible à la racine du site (par exemple, `localhost:8000`).
- Le nom de la route est `login`, ce qui permet de référencer cette route facilement dans d'autres parties de l'application.

## Exemple 2

```php
<?php
namespace App\Controller;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Rounting\Annotation\Route;

class Authentification extends AbstractController {
    #[Route('/authentification{page}', name: 'authentification')]

    public function loginAccount(): Response {
        return $this->render('authentification/login.html.twig', [
            'controller_name' => $this->controllerName,
            'login', ...,
            ...
        ]
    }
    public function createAccount(): Response {
        ...
    }
    public function index(): Response {
        $page = $request->query->get('page', 'createAccount');
        if($page == 'login') {
            return createAccount();
        } else {
            return loginAccount();
        }
    }
}



# Fonctionnement

Lorsque le serveur web reçoit une requête pour le chemin spécifié (dans cet exemple, `/`), il redirige vers la méthode correspondante du contrôleur (ici, `index()`). Cette méthode exécute sa logique et retourne une réponse qui sera affichée à l'utilisateur.
