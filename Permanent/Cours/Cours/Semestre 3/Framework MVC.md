---
MOOC: "[[Cours]]"
Ressource: R3.01
Cours: 
Date: 
tags: 
Complete: false
Learned: false
---
En séance de TP, nous utilisons un Framework réduit afin de faciliter la gestion du MVC dans les différentes pages. Il agit sur les contrôleurs et les vues

## 1 - Le contrôleur
Grâce à ce framework, l'ajout d'informations à la vue depuis le contrôleur est plus aisée. En effet, il va exister des méthodes préparées afin de passer des variables depuis à le contrôleur à la vue

```php
<php

//Include les fichiers nécessaires
include_once('framework/view.fw.php'); //Le framework
include_once('model/article.class.php'); //Modèle
include_once('model/categorie.class.php'); //Modèle

/* Récupérer les variables nécessaires */

$nombreUtilisateurs = UserBase::getNombreUsers();
$user = UserBase::getUser(13);
$emailUser = UserBase::getEmail($user)

/* Créer la vue */
$view = new View();
$view->assign('nombreUsers', $nombreUtilisateurs);
$view->assign('user', $user);
$view->assign('emailUser', $emailUser);

/* Afficher la vue */
$view->display("Nom vue");
?>
```