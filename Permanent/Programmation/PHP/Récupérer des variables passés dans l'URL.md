Certaines fois, l'URL se compose de la façon suivante :
`URL?nom=val1&age=val2`

Je peux récupérer directement  les données de  la query string codée dans l'URL. Je peux  les récupérer de cette manière
```PHP
$nom = $_GET['nom'];
$age = $_GET['age'];
```

>[!warning] Vérifier qu'ils sont présents
>**Attention !** Il faut que je vérifie que les variables soient présentes dans  l'URL sous peine d'une erreur en cas de non présence !


Je peux utliiser la méthode [[Vérifier une variable non nulle - isset|isset]] pour vérifier que les paramètres passés dans l'URL ne sont pas nuls
```PHP
if(isset($_GET['nom'])){ //Verification
	$nom = $_GET['nom']; 
}else{
	$nom = 'inconnu'
}
```