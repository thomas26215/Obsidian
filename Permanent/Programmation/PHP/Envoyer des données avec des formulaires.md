Il faut tout d'abord reprendre les cours HTML sur [[Les formulaires HTML]]
Voici un exemple de formulaire en PHP pour envoyer des données :
```PHP
<?php
<form action="traiter.php" method="get">
	<input type="text" name="nom">
	<input type="text" name="prenom">
	<input type="number" name="age">
	<button type="submit"> Envoyer </button>
</form>
?>
```

Il faut tout d'abord savoir que dans un formulaire (`<form></form>`), un bouton de type `submit` va envoyer les données du formulaires soit par la [[Méthode POST]], soit par la [[Méthode GET]] (paramètres `methode` du form)