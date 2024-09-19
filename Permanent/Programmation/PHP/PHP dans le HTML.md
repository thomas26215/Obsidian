Il est possible d'écrire du code PHP dans du code HTML. Dans la méthode suivant nous écrirons le code HTML dans un fichier PHP :
```PHP
<?php
	$location = "Montélimar"
	$day = intval(date("d"));
	$date = intval(date("d/m/Y"));
?>

<!DOCTYPE html>
<html lang="fr" dir="ltr">

	<head>
		<meta charset="utf-8">
		<title>Ma home page</title>
	</head>
	<body>
		<h1>Ceci est ma Home page</h1>
		<p>
			Bonjour vous êtes à l'<?= $location ?>.
			Nous sommes un jour <strong>
				<?php if ($day % 2 == 0) { ?>
					pair
				<?php } else { ?>
					impair
				<?php } ?>
			</strong>
		</p>
		<p>
			La date d'aujourd'hui est : <strong><?= $date ?></strong>
		</p>
		<p>
			Le numéro du jour est : <strong><?= $day ?></strong>
		</p>
	</body>
</html>
```
- Tout d'abord, le code PHP est entouré par `<?php ... ?>`, que ce soit pour la déclaration et l'initialisation des variables au tout début du code mais également pour la condition dans le bloc HTML
- Le code HTML s'affiche après le code PHP, de la même manière que si on le déclarait dans un fichier HTML
- Afin d'afficher une variable dans le code HTML, il faut utiliser `<?= $variable ?>`