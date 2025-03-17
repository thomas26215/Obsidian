Il est possible de rendre une vue quand on accède à la [[Définition des routes|route]]. Pour cela, on utilise la méthode `render` :
```php
namespace App\Controller;
use Symfony\Component\\HttpFoundation\Response;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\Routing\Attribute\Route;

class DefaultController extends AbstractController {
	#[Route('/hello/{userName}', name: 'hello_page')]
	public function hello(string $userName) : Response {
		return $this->render("hello.html.twig", ["username" => $userName,]);
	}
}
```

On voit ici que la vue rendue est `hello.html.twig` et qu'on lui  a passé en paramètres `userName`

