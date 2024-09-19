Certaines fois, l'URL se compose de la façon suivante :
`URL?var1=val1&var2=val2`

Je peux récupérer directement les données de la query string codée dans l'URL. Je peux les récupérer de cette manière
```PHP
$nom = $_GET['nom'];
$age = $_GET['age'];
```

>[!warning] Vérifier qu'ils sont présents
>**Attention !** Il faut que je vérifie que les variables soient présentes dans l'URL sous peine d'une erreur en cas de non présence !


Pour vérifier si une variable est présente dans l'URL, je peux faire ceci :
```PHP
if(isset($_GET['nom'])){ //Verification
	$nom = $_GET['nom']; 
}else{
	$nom = 'inconnu'
}
```