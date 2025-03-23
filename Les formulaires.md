## 1. Introduction aux Formulaires Symfony

Symfony intègre un composant de construction de formulaires ("Form Builder") qui permet de créer et manipuler des formulaires HTML via des objets PHP. Les formulaires Symfony sont toujours associés à une entité PHP (généralement une entité Doctrine).

### Fonctionnalités principales :

- Génération automatique de HTML via Twig
- Mapping automatique entre champs du formulaire et l'entité associée
- Validation des données en backend via annotations sur l'entité
- Deux manières de créer un formulaire :
    - Dynamiquement dans un contrôleur
    - Dans une classe PHP dédiée (réutilisable)

## 2. Workflow de Mise en Œuvre des Formulaires

1. **Construire** un formulaire Symfony (dans un contrôleur ou une classe PHP dédiée).
2. **Transmettre et afficher** le formulaire dans un template pour saisie utilisateur.
3. **Traiter les données** soumises et les persister en base de données.

L'affichage et le traitement du formulaire peuvent être réalisés dans un seul contrôleur ou dans deux contrôleurs distincts.

## 3. Exemple de Formulaire Symfony

### 3.1 Définition d'une Entité `Task`

```php
namespace App\Entity;
class Task {
    protected $task;
    protected $dueDate;

    public function getTask(): string {
        return $this->task;
    }
    public function setTask($task): void {
        $this->task = $task;
    }
    public function getDueDate(): ?\DateTime {
        return $this->dueDate;
    }
    public function setDueDate(?\DateTime $dueDate): void {
        $this->dueDate = $dueDate;
    }
}
```

### 3.2 Création d'un Formulaire dans un Contrôleur

```php
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\Form\Extension\Core\Type\DateType;
use Symfony\Component\Form\Extension\Core\Type\SubmitType;
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\HttpFoundation\Request;

class TaskController extends AbstractController {
    public function new(Request $request) {
        $task = new Task();
        $form = $this->createFormBuilder($task)
            ->add('task', TextType::class)
            ->add('dueDate', DateType::class)
            ->add('save', SubmitType::class, ['label' => 'Create Task'])
            ->getForm();
    }
}
```

### 3.3 Décrire un Formulaire dans une Classe PHP

```php
namespace App\Form\Type;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\DateType;
use Symfony\Component\Form\Extension\Core\Type\SubmitType;
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class TaskType extends AbstractType {
    public function buildForm(FormBuilderInterface $builder, array $options) {
        $builder
            ->add('task', TextType::class)
            ->add('dueDate', DateType::class)
            ->add('save', SubmitType::class);
    }
    public function configureOptions(OptionsResolver $resolver) {
        $resolver->setDefaults([
            'data_class' => Task::class,
        ]);
    }
}
```

## 4. Affichage et Traitement d'un Formulaire

### 4.1 Transmission du Formulaire au Template

```php
public function new(Request $request) {
    $task = new Task();
    $form = $this->createForm(TaskType::class, $task);
    return $this->render('task/new.html.twig', ['myForm' => $form->createView()]);
}
```

### 4.2 Rendu du Formulaire en Twig

```twig
{{ form_start(myForm) }}
    {{ form_row(myForm.task) }}
    {{ form_row(myForm.dueDate) }}
    {{ form_row(myForm.save) }}
{{ form_end(myForm) }}
```

## 5. Validation des Formulaires

### 5.1 Définition des Contraintes

```php
use Symfony\Component\Validator\Constraints as Assert;
class Task {
    #[Assert\NotBlank]
    public $task;
    #[Assert\NotBlank]
    #[Assert\Type("\DateTime")]
    protected $dueDate;
}
```

### 5.2 Validation sans Formulaire

```php
use Symfony\Component\Validator\Validator\ValidatorInterface;
public function validateTask(ValidatorInterface $validator) {
    $task = new Task();
    $errors = $validator->validate($task);
}
```

## 6. CRUD avec Symfony

### 6.1 Génération de l'Interface CRUD

Symfony offre un outil de scaffolding pour générer une interface CRUD automatiquement :

```sh
php bin/console make:crud
```

Cette commande génère un ensemble de fichiers pour la gestion CRUD d'une entité (formulaires, vues, routes, et contrôleurs).

### 6.2 Actions CRUD

- **Create** : Ajout d'une nouvelle entité
- **Retrieve** : Affichage d'une liste ou d'un détail d'entité
- **Update** : Modification d'une entité existante
- **Delete** : Suppression d'une entité