# **Cours Complet : Les Formulaires Symfony**

## **1. Introduction aux Formulaires Symfony**

Symfony fournit un composant puissant pour gérer les formulaires HTML. Ce composant permet de créer des formulaires dynamiques, de valider les données saisies par l'utilisateur, et de mapper automatiquement ces données à des entités PHP (souvent liées à Doctrine ORM).

### **Caractéristiques principales :**
- Génération automatique de HTML via Twig.
- Mapping automatique entre les champs du formulaire et l'entité associée.
- Validation des données côté backend grâce aux contraintes définies sur l'entité.
- Réutilisation des formulaires grâce à des classes dédiées.

### **Commande pour générer un formulaire :**
```bash
php bin/console make:form
```

---

## **2. Workflow de Mise en Œuvre des Formulaires**

1. **Créer** un formulaire Symfony (dans un contrôleur ou une classe PHP dédiée).
2. **Transmettre** le formulaire à un template Twig pour affichage et saisie utilisateur.
3. **Traiter** les données soumises par le formulaire.
4. **Persister** ou manipuler les données dans la base de données.

---

## **3. Exemple Pratique : Création d'un Formulaire Symfony**

### **3.1 Définition d'une Entité `Task`**

Les formulaires Symfony sont souvent associés à des entités Doctrine. Voici une entité `Task` qui sera utilisée pour le formulaire :

```php
namespace App\Entity;

use Symfony\Component\Validator\Constraints as Assert;

class Task
{
    #[Assert\NotBlank(message: 'Le champ tâche ne peut pas être vide.')]
    private ?string $task = null;

    #[Assert\NotBlank(message: 'La date ne peut pas être vide.')]
    #[Assert\Type(type: '\DateTime', message: 'La date doit être valide.')]
    private ?\DateTime $dueDate = null;

    public function getTask(): ?string
    {
        return $this->task;
    }

    public function setTask(string $task): void
    {
        $this->task = $task;
    }

    public function getDueDate(): ?\DateTime
    {
        return $this->dueDate;
    }

    public function setDueDate(?\DateTime $dueDate): void
    {
        $this->dueDate = $dueDate;
    }
}
```

---

### **3.2 Création d'un Formulaire dans une Classe PHP**

Pour réutiliser facilement un formulaire, il est recommandé de le définir dans une classe dédiée.

#### Commande pour générer la classe de formulaire :
```bash
php bin/console make:form TaskType
```

#### Exemple de classe `TaskType` :
```php
namespace App\Form\Type;

use App\Entity\Task;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\DateType;
use Symfony\Component\Form\Extension\Core\Type\SubmitType;
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class TaskType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('task', TextType::class, ['label' => 'Tâche'])
            ->add('dueDate', DateType::class, ['label' => 'Date limite'])
            ->add('save', SubmitType::class, ['label' => 'Créer']);
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'data_class' => Task::class,
        ]);
    }
}
```

---

## **4. Utilisation du Formulaire dans le Contrôleur**

### **4.1 Construction et Affichage du Formulaire**

Dans votre contrôleur, vous pouvez construire le formulaire et le transmettre au template Twig.

#### Exemple :
```php
use App\Entity\Task;
use App\Form\Type\TaskType;
use Doctrine\ORM\EntityManagerInterface;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;

class TaskController extends AbstractController
{
    #[Route('/task/new', name: 'task_new')]
    public function new(Request $request, EntityManagerInterface $entityManager): Response
    {
        // Créer une nouvelle instance de l'entité Task
        $task = new Task();

        // Construire le formulaire lié à l'entité Task
        $form = $this->createForm(TaskType::class, $task);

        // Traiter les données soumises par l'utilisateur (si elles existent)
        $form->handleRequest($request);

        if ($form->isSubmitted() && $form->isValid()) {
            // Persister les données en base via EntityManager
            $entityManager->persist($task);
            $entityManager->flush();

            // Rediriger vers une autre page après succès (par exemple, liste des tâches)
            return $this->redirectToRoute('task_list');
        }

        // Afficher le formulaire dans le template Twig
        return $this->render('task/new.html.twig', [
            'form' => $form->createView(),
        ]);
    }
}
```

---

### **4.2 Rendu du Formulaire en Twig**

Dans le fichier Twig (`task/new.html.twig`), utilisez les fonctions Twig pour afficher le formulaire :

```twig
{% extends 'base.html.twig' %}

{% block title %}Créer une nouvelle tâche{% endblock %}

{% block body %}
Créer une nouvelle tâche

{{ form_start(form) }}
    {{ form_row(form.task) }}
    {{ form_row(form.dueDate) }}
    {{ form_row(form.save) }}
{{ form_end(form) }}
{% endblock %}
```

---

### **4.3 Récupération des Données Soumises**

Une fois que l'utilisateur soumet le formulaire :
1. La méthode `handleRequest()` récupère automatiquement les données envoyées via POST ou GET.
2. La méthode `isSubmitted()` vérifie si le formulaire a été soumis.
3. La méthode `isValid()` valide les données selon les contraintes définies sur l'entité.

#### Accéder aux données du formulaire :
Les données soumises sont automatiquement mappées à l'objet `$task` associé au formulaire.

```php
$taskName = $task->getTask();
$dueDate = $task->getDueDate();
```

Si vous souhaitez accéder directement aux valeurs des champs du formulaire :
```php
$data = $form->getData();
echo $data['task'];
echo $data['dueDate'];
```

---

## **5. Validation des Formulaires**

### **5.1 Définition des Contraintes**
Les contraintes sont définies directement sur l'entité via les annotations ou attributs PHP :

```php
namespace App\Entity;

use Symfony\Component\Validator\Constraints as Assert;

class Task
{
    #[Assert\NotBlank(message: 'Le champ tâche ne peut pas être vide.')]
    private ?string $task = null;

    #[Assert\NotBlank(message: 'La date ne peut pas être vide.')]
    #[Assert\Type(type: '\DateTime', message: 'La date doit être valide.')]
    private ?\DateTime $dueDate = null;

   // Getters et setters...
}
```

---

### **5.2 Validation sans Formulaire**
Vous pouvez valider une entité indépendamment du formulaire avec le service `ValidatorInterface` :

```php
use Symfony\Component\Validator\Validator\ValidatorInterface;

public function validateTask(ValidatorInterface $validator): void
{
    $task = new Task();
    
    // Validation des contraintes définies sur l'entité Task
    $errors = $validator->validate($task);

    if (count($errors) > 0) {
        foreach ($errors as $error) {
            echo $error->getMessage();
        }
    }
}
```

---
# Exemple ajouter un commentaire sur un produit
Nous avons deux entités :
- **Comment**
- **Product**
Il faut maintenant créer le formulaire : `php bin/console make:form CommentType`. Voici le fichier généré :

```php
namespace App\Form;

use App\Entity\Comment;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\IntegerType;
use Symfony\Component\Form\Extension\Core\Type\TextareaType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class CommentType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options): void
    {
        $builder
            ->add('text', TextareaType::class, [
                'label' => 'Votre commentaire',
                'required' => true,
            ])
            ->add('rating', IntegerType::class, [
                'label' => 'Votre note',
                'required' => true,
                'attr' => ['min' => 0, 'max' => 5],
            ]);
    }

    public function configureOptions(OptionsResolver $resolver): void
    {
        $resolver->setDefaults([
            'data_class' => Comment::class,
        ]);
    }
}
```

Le controlleur :
```php

#[Route('/product/{id}/add-comment', name: 'add_comment')]
public function addComment(Product $product, Request $request, EntityManagerInterface $em): Response
{
	if (!$this->getUser()) {
			throw $this->createAccessDeniedException('Vous devez être connecté pour ajouter un commentaire.');
	}
	
	$comment = new Comment();
	$form = $this->createForm(CommentType::class, $comment);
	
	$form->handleRequest($request);
	if ($form->isSubmitted() && $form->isValid()) {
			// Associer le commentaire à l'utilisateur et au produit :
			$comment->setAuthor($this->getUser());
			$comment->setProduct($product);
	
			// Sauvegarder en base de données :
			$em->persist($comment);
			$em->flush();
	
			return $this->redirectToRoute('product_detail', ['id' => $product->getId()]);
	}
	
	return $this->render('product/add_comment.html.twig', [
			'form' => $form->createView(),
			'product' => $product,
	]);
}
```

Finalement, le fichier Twig :

```twig
{% extends 'base.html.twig' %}

{% block title %}
Détail du produit - {{ product.name }}
{% endblock %}

{% block body %}
<h1>{{ product.name }}</h1>
<img src="{{ product.image }}" alt="Image de {{ product.name }}">
<p>{{ product.description }}</p>
<p>Prix : {{ product.price }} €</p>

{% if averageRating is not null %}
<p>Note moyenne : {{ averageRating }}/5</p>
{% else %}
<p>Ce produit n'a pas encore été évalué.</p>
{% endif %}

<h2>Commentaires :</h2>
<ul>
{% for comment in comments %}
<li>
<strong>{{ comment.author.username }}</strong> - Note : {{ comment.rating }}/5<br>
{{ comment.text }}
</li>
{% endfor %}
</ul>

<a href="{{ path('add_comment', { id: product.id }) }}" class="btn btn-primary">Ajouter un commentaire</a>
{% endblock %}
```