En Symfony, il est possible de mettre en place un service de traduction. La première étape est d'installer le composant de traduction via Composer :

```shell
composer require symfony/translation
```

Une fois cela fait, il faut configurer le fichier `config/package/translation.yaml` pour définir la langue par défaut de l'application et définir le chemin des fichiers de traduction :

```yaml
framework:
		default_locale: fr # Langue par défaut
		translator:
			default_path: '%kernel.project_dir%/translations' # Chemin des fichiers de traduction
			fallbacks: ['fr'] # Langue de repli
```

Ensuite, il faut définir les langues supportées dans le fichier `config/services.yaml` :

```yaml
parameters:
		locales: ['fr', 'en']
```

Pour un bon service de traduction, il est nécessaire d'ajouter le paramètre `{_locale}` dans les routes pour définir la langue de la page. Par exemple, pour une route `/contact`, il faudra ajouter `{_locale}` :

```php
namespace App\Controller;

class DefaultController extends AbstractController {
	#[Route(
		path: '/{_locale}', //Ajout du paramètre _locale pour chaque route
		name: 'app_default_index',
		requirements: ['_locale' => '%app.supported_locales%'], //Contraindre le paramètres _locale en fonction des langues supportées dans config/service.yaml
		defaults: ['_locale' => 'fr'] //Valeur par défaut pour _locale (A définir uniquement sur la page d'accueil)
	)]

	#[Route(
		path: '/{_locale}/contact',
		name: 'app_default_contact',
		requirements: ['_locale' => '%app.supported_locales%']
	)]
	public function contact() {
		// ...
	}
}
```

Pour les éléments sans routes, il est possible d'utiliser le service translator dans le code PHP:

```php
use SymSymfony\Contracts\Translation\TranslatorInterface;

public function index(TranslatorInterface $translator) {
	$message = $translator->trans('Bonjour');
```

On va ensuite définir les éléments à traduire dans le fichier Twig en utilisant la balise `{% trans %}` :

```twig
<p> {% trans %}Bonjour{% endtrans %} </p>
```

Les traductions sont stockées dans des fichiers `XLIFF` dans le dossier `translations`. Par exemple, pour la traduction en anglais, on va créer un fichier `messages.en.xliff` :

```xml
<?xml version="1.0"? endoding="utf-8"?>>
<xliff version="1.2" xmlns="urn:oasis:names:tc:xliff:document:1.2">
	<file source-language="en" datatype="plaintext" original="file.ext">
		<body>
			 <trans-unit id="1" resname="Bonjour">
				 <source>Bonjour</source>
				 <target>Hello</target>
			</trans-unit>
		</body>
	</file>
</xliff>
```

Il existe une commande pour extraire automatiquement les fichiers à traduire :
```shell
php bin:console translation:extract --force fr
php bin:console translation:extract --force en
```
=> Cela génère un fichier `messages.fr.xliff` et un fichier `messages.en.xliff` dans le dossier `translations` où il ne reste plus qu'à traduire le contenu en complétant les balises `<target>`.

Finalement, pour que l'utilisateur puisse changer sa langue, il faut ajouter un sélecteur de langue dans le fichier Twig `base.html.twig` :

```twig
{% for locale in app.supported_locales %}
	<a href="{{ path(app.request.attribute.get('_route'), app.request.attribute.get('_route_params')|merge({'_locale': locale})) }}">
		{{ locale }}
	</a>
{% endfor %}
```}