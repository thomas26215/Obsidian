## Les fonctions
En JS, les fonctions se définissent de cette manière :
```js
function nomFonction(parameters){
	//
	return ..;
}
```

>[!important]
>=> Pas besoin de spécifier le type des variables passées en paramètres !

## Récupérer les éléments HTML
Récupérer un élément par son id :
```js
const element = document.getElementById("id");
```

Récupérer un élément selon sa classe CSS :
```js
const element = document.getElementByClassName("className");
```

Récupérer un élément selon son tag :
```js
const element = document.getElementByTagName("p");
```

Récupérer le premier enfant correspondant :
```js
const element = document.querySelector(".maClasse");
```

Récupérer tous les enfants
```js
const element = document.querySelectorAll("p.maClasse");
```




## Les formulaires
- **Récupérer un formulaire :** `const form = document.getElementById('monForm')`
- **Evènement d'écoute sur le forumlaire :**
	- **Gérer la soumission du formulaire :** `form.addEventListener('submit', function(event){...})`
	- **Gérer la réaction aux changements de valeur :** `input.addEventListener('change', function(event){...})`
	- **Réagir quand l'élément reçoit le focus :** `input.addEventListener('focus', function(event){...)}`
- **Empêcher le rechargement de la page lors la soumission :** `event.preventDefault();

**Exemple complet :**
```js

//Fonction randomInteger
//Récupérer les éléments HTML



form.addEventListener('submit', function(e)) {
	e.preventDefault();
	const userGuess  = parseInt(input.value);
	if(userGuess == mysteryNumber) {
		result.textContent = "Bravo !";
		result.style.color = 'green';
	} else if(userGuess < mysteryNumber) {
		result.textContant = "Plus grand !"
		result.style.color = 'red';
	} else {
		result.textContent = 'Plus petit !';
		result.style.color = 'red';
	}
}

```