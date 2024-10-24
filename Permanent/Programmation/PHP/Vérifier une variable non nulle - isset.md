En PHP, il est possible de vérifier si une variable est définie ou bien si elle est nulle. pour cela, il faut utiliser la fonction `isset` :
- Retourne `false` si a la valeur `NULL`
- Retourne `true` sinon
```php
if(isset($variable)){
	echo "Voici la variable" . $variable;
else{
	echo "Variable non définie"
}
}
```
Ici il serait possible de retourner une exception

Il est également possible de le faire sur une variable récupéree dans l'URL :
```php
if(isset($_GET['nom'])){
	$nom = $_GET['nom'];
	echo "Bonjour, je m'appelle" . $nom;
}else{
	echo "Aucun nom fournit dans l'URL"
}
```