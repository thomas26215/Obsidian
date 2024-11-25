## Créer un controller

Pour créer un contrôleur avec Synfony, il faut se rendre dans le répertoire du projet et exécuter la commande suivant :
``` bash
php bin/console make:controller NomController
```
Cela va créer deux fichiers : Un ficher `src/Controller/NomController.php` et un fichier `templates/NomController/index.html.twig`

Pour le moment, nous allons nous interesser au premier fichier crée.
Un fichier controller simple ressemble à ceci :
```php
namespace App\Controller;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;
class HomeController extends AbstractController {
	#[Route('/', name: 'home')]
	public function index(): Response {
		return new Response('Hello World');
	}
}
```

---
### Définition des Routes avec `#[Route]`

#### Syntaxe de Base

La méthode recommandée pour définir des routes dans Symfony est d'utiliser l'attribut `#[Route]`. Cela permet de lier un chemin URL à une méthode de contrôleur. La syntaxe générale est la suivante :
```php
#[Route("chemin", name: "nom_de_la_route")]
```

- **chemin** : Il s'agit de l'URL que l'utilisateur doit visiter pour accéder à cette route.
- **nom_de_la_route** : C'est un identifiant unique pour la route, qui peut être utilisé pour générer des URLs ou rediriger vers cette route dans le code.

#### Exemple Pratique

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
#### Fonctionnement
Lorsque le serveur web reçoit une requête pour le chemin spécifié (dans cet exemple, `/`), il redirige vers la méthode correspondante du contrôleur (ici, `index()`). Cette méthode exécute sa logique et retourne une réponse qui sera affichée à l'utilisateur.

### Récupérer des paramètres
En utilisant classiquement PHP, j'aurai tendance à récupérer les paramètres de l'URL avec la [[Méthode GET]] avec la variable globale `GET` Cependant, il existe une fonction symfony tout prête pour cela. Il faut pour cela faire :
`#Route('/Recette/{slug}-{id}', name:recipe.show')`. Cela permet ainside récupérer dans l'URL les paramètres `slug` et `id`


---

Pour récupérer les paramètres d'URL dans Symfony, vous pouvez utiliser le système de routing intégré qui simplifie la gestion des requêtes par rapport à l'utilisation classique de PHP avec la superglobale `$_GET`. Voici une explication détaillée de cette approche.

## Récupération des Paramètres d'URL avec Symfony

### 1. Définition de la Route

Pour commencer, vous devez définir une route dans votre contrôleur. Utilisez l'attribut `#[Route]` pour spécifier le chemin et les paramètres que vous souhaitez récupérer. Par exemple :

```php
#[Route('/recette/{slug}-{id}', name: 'recipe.show')]
public function show(string $slug, int $id): Response
{
    // Logique pour afficher la recette
}
```

Dans cet exemple :
- **`/recette/{slug}-{id}`** est le chemin de la route.
- **`{slug}`** et **`{id}`** sont des paramètres dynamiques qui seront extraits de l'URL.
- **`name: 'recipe.show'`** donne un nom à cette route, ce qui facilite sa référence ultérieure.

### 2. Accès aux Paramètres dans le Contrôleur

Une fois que vous avez défini la route, Symfony se charge automatiquement de passer les paramètres extraits de l'URL à la méthode du contrôleur. Dans l'exemple ci-dessus, les paramètres `slug` et `id` sont directement accessibles comme arguments de la méthode `show`.

Voici comment vous pouvez utiliser ces paramètres :

```php
public function show(string $slug, int $id): Response
{
    return new Response("Recette: $slug, ID: $id");
}
```

### 3. Utilisation de l'Objet Request

Si vous avez besoin d'accéder à tous les paramètres de la requête (y compris ceux qui ne sont pas définis dans la route), vous pouvez injecter l'objet `Request` dans votre méthode :

```php
use Symfony\Component\HttpFoundation\Request;

public function show(Request $request, string $slug, int $id): Response
{
    // Accéder aux paramètres de la route
    $routeParams = $request->attributes->get('_route_params');

    // Logique pour afficher la recette
    return new Response("Recette: $slug, ID: $id");
}
```

### 4. Récupération des Paramètres dans Twig

Si vous souhaitez afficher ou utiliser ces paramètres dans un template Twig, vous pouvez passer les variables depuis le contrôleur :

```php
public function show(string $slug, int $id): Response
{
    return $this->render('recipe/show.html.twig', [
        'slug' => $slug,
        'id' => $id,
    ]);
}
```

Dans votre template Twig, vous pouvez ensuite accéder à ces variables comme suit :

```twig
<h1>Détails de la recette : {{ slug }}</h1>
<p>ID de la recette : {{ id }}</p>
```

### 5. Bonnes Pratiques

- **Utilisez des noms explicites pour vos routes** afin qu'ils soient facilement compréhensibles.
- **Définissez des contraintes sur vos paramètres** si nécessaire (par exemple, pour s'assurer que `id` est un nombre) en utilisant le paramètre `requirements`.

```php
#[Route('/recette/{slug}-{id}', name: 'recipe.show', requirements: ['id' => '\d+'])]
```

Cela garantit que seules les requêtes avec un `id` numérique atteindront cette route.

## Conclusion

Avec Symfony, récupérer les paramètres d'URL est simple et efficace grâce à son système de routing intégré. En utilisant des attributs pour définir vos routes et en injectant l'objet `Request`, vous pouvez facilement gérer les données passées via l'URL tout en maintenant un code propre et structuré. Cette approche est plus moderne et maintient une séparation claire entre la logique métier et le traitement des requêtes HTTP.
