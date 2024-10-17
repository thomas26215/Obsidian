Le fichier `index.php` est le point d'ntrée de notre routeur. C'est cellui qui reçois toutes les requêteset les dirigent vers les contrôleurs appropriés
<mark style="background: #BBFABBA6;">Voici un exemple</mark> :
```PHP
>?php
$ctrl = $_GET['ctrl'] ?? 'main';
const CTRLS = array('main', 'getName', 'getLanguage');
if(!in_array($ctrl, CTRLS)){
	$error = 'Mauvais controleur : "'.$ctrl.'" query string "'.$_SERVER['QUERY_STRING'].'"';
  require_once('view/error.view.php');
  exit(0);
}
$path = 'controler/'.$ctrl.'.ctrl.php';
require_once($path);
?>
```

<mark style="background: #ADCCFFA6;">Explications</mark> :
1. ``$ctrl = $_GET['ctrl'] ?? 'main';`` ⇒ Si un paramètre `ctrl` est présent dans l'URL (`$_GET`), il sera utilisé. SInon, le contrôleur par défaut sera choisit
2. `const CTRLS = array('main', 'getName', 'getLanguage');` ⇒ Liste des contrôleurs autorisés pour empêcher l'exécution de fichier inexistants
3. Vérifier si le contrôleur demandé est dans la liste des contrôleurs disponibles (liste `CTRLS`). Sinon, une page d'erreur s'affiche et le script se termine
4. Chargement du contrôleur