Nous avons vu dans [[Rendre une vue Twig dans une route|cette note]] qu'il est possible de passer des variables depuis le contrôlleur vers la vue Twig. Il est donc possible de les utiliser dans le [[Les templates Twig|template Twig]] :

> [!Example]
> ```php
> $this->render('fichierTwig', ["userName" => $userName, "age", => $age, "email" => $email])
> ```
> 
> Fichier Twig `fichierTwig` :
> ```twig
> {# templates/Default/fichierTwig.html.twig}
> <html>
> <!DOCTYPE html>
> 	<body>
> 		{% if age > 18%}
> 			{{ userName }} a plus de 18 ans
> 		{% else %}
> 			{{ userName }} a moins de 18 ans
> 	</body>
> </html>
> ```