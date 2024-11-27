---
MOOC: "[[Programmation]]"
Langage: PHP - Symfony
Type: Contrôleur
tags:
---
#### 1. Définition
L'objet `Request` dans Symfony représente une requête HTTP. Il encapsule toutes les informations envoyées par le client au serveur, telles que les paramètres de la requête, les données du formulaire, les fichiers téléchargés, et les en-têtes HTTP.

#### 2. Accès aux Données
L'objet `Request` permet d'accéder facilement aux différentes parties de la requête :

- **Paramètres de la requête GET**:
  ```php
  $request->query->get('param', 'valeur_par_defaut');
  ```

- **Données POST**:
  ```php
  $request->request->get('param');
  ```

- **Fichiers téléchargés**:
  ```php
  $request->files->get('nom_du_fichier');
  ```

- **En-têtes HTTP**:
  ```php
  $request->headers->get('Nom-De-L-En-Tete');
  ```

#### 3. Utilisation dans un Contrôleur
Dans un contrôleur Symfony, l'objet `Request` est généralement injecté comme paramètre d'une méthode d'action :

```php
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;

class MonController extends AbstractController {
    #[Route("/", name: "home")]
    public function index(Request $request): Response {
        $name = $request->query->get('name', 'Inconnu');
        return new Response('Bonjour ' . $name);
    }
}
```

#### 4. Méthodes Utiles
Voici quelques méthodes courantes de l'objet `Request` :

- `isMethod($method)`: Vérifie si la requête utilise une méthode HTTP spécifique (GET, POST, etc.).
- `getContent()`: Récupère le contenu brut de la requête.
- `getLocale()`: Récupère la locale de la requête.

#### 5. Importance
L'objet `Request` est essentiel pour construire des applications web interactives et dynamiques en Symfony. Il permet aux développeurs de traiter les données envoyées par les utilisateurs et d'y répondre de manière appropriée.
