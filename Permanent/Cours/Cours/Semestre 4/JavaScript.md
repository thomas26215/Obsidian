# La déclaration des variables en JavaScript
Au début de Javascript, il était possible d'utiliser le mot clé `var` pour déclarer une variable. Cependant, avec l'évolution du langage, il est possible d'utiliser `let` et `const` pour déclarer des variables.
Le mot clé `var` qui a une portée globale et est automatiquement rattaché à l'objet `window` si définit en dehors d'une fonction et a un portée locale si définit à l'intérieur de la fonction

>[!INFO]
>Contrairement aux autres langages, la portée n'est pas définit aux blocs mais bien à la fonction et on peut redéfinit plusieurs fois une même variable sans avoir d'erreur.


```javascript
"use strict";
var test = 1;
if(true) {
	var test = 99;
}
console.log(test); // 99
console.log(window.test); // 99
```

```javascript
var globalScope = "Global";
function maFonction() {
	var localScope = "Local";
	console.log(globalScope); // Global
	console.log(localScope); // Local
}
console.log(globalScope); // Global
console.log(localScope); // ReferenceError: localScope is not defined
```

---

`let` sert à déclarer une variable tandis que `const` sert à déclarer une constante. Ces deux mots clés ont une portée de bloc contrairement à `var`. Une fois une constante définie, il n'est pas possible de la redéfinir. Cependant, si la constante est une référence vers un objet, elle reste modifiable

# Les types primitifs
Il existe 7 types primitifs en JavaScript :
- Number
- String
- Boolean
- Null
- Undefined
- Symbol
- BigInt
Il faut savoir qu'une variable de type primitif stocke la valeur directement dans la variable et elle n'a pas de propriétés ou méthodes mais quand on appelle une méthode sur une chaine `string`, JavaScript va automatiquement utiliser un wrapper d'objet pour que cela fonctionne

Une variable qui a un type objet stocker une référence vers l'objet et dans le cas où on définit un objet en énumérant directement dans le code de l'objet, on parle d'objet littéral


> [!Example] Title
> ```javascript
> let maVoiture = {
> 	marque: "Toyota",
> 	modele: "Yaris"
> 	getNom: function() {
> 		return this.marque + " " + this.modele;
> 	}
> };

En JS, unn objet est un considéré comme un objet exécutable


> [!Example] Title
> ```javascript
> function maFonction() {
> 	console.log("Hello World");
> }
> //On aurait aussi pût écrire let maFonction = function() { console.log("Hello World"); }
> 
> if(maFonction instanceof Object) {
> 	console.log("maFonction est un objet");
> 	//Une fonction est un objet !
> }


# Le JSON
Le JSON est un format de données qui a été spécialement conçu pour l'échange de données entre client et serveur.
En Javascript, nous disposons de nombreuses méthodes pour manipuler le JSON :
- `JSON.stringify()` : Permet de convertir un objet en JSON
- `JSON.parse()` : Permet de convertir un JSON en objet

> [!Example]
> ```javascript
> let obj = {liste: [1,2,3,4,5], valeur: 42};
> console.log(JSON.stringify(obj)); // {"liste":[1,2,3,4,5],"valeur":42}
> 
> obj = {maPropriete: "valeur", maFonction: function() { console.log("Hello World")};
> console.log(JSON.stringify(obj)); // {"maPropriete":"valeur"}
> 
> obj = {propDefinie: 123, propNonDefinie: undefined};
> console.log(JSON.stringify(obj)); // {"propDefinie":123}
> ```
> 
> ---
> 
> ```javascript
> let text = '{ "employees" : [' +
>	'{ "firstName":"John" , "lastName":"Doe" },' +
>	'{ "firstName":"Anna" , "lastName":"Smith" },' +
>	'{ "firstName":"Peter" , "lastName":"Jones" } ]}';
>	
>//On transforme le JSON en objet
>let obj = JSON.parse(text); //Attention ! si chaîne vide, cela renvoie une erreur
>
>console.log(obj.employees[1].firstName); // Anna
>```
>
>---
>
>```javascript
>Json.parse(""); //SyntaxError: Unexpected end of JSON input
>Json.parse("{}"); // {}
>Json.parse("[]"); // []
>Json.parse("{valeur: 42}"); //SyntaxError: Unexpected token v in JSON at position 1})
>Json.parse('{"valeur": 42}'); // {valeur: 42}
>Json.parse("['val1', 'val2']"); //SyntaxError: Unexpected token v in JSON at position 1])
>Json.parse('["val1", "val2"]'); // ["val1", "val2"]


# LocalStorage
En Javascript, la propriété `localStorage` permet de stocker des données de manière persistante dans le navigateur. Il est possible de stocker des données sous forme de clé/valeur et les données sont stockées sous forme de chaîne de caractères. Il faut savoir que les données persistent même après la fermeture du navigateur, le redémarrage de l'ordinateur ou la fermeture de l'onglet. Pour supprimer les données du `localStorage`, il faut le faire explicitement

Nous disposons de plusieurs méthodes :
- `setItem()` : Permet de stocker une paire clé/valeur
- `getItem()` : Permet de récupérer la valeur d'une clé
- `removeItem()` : Permet de supprimer une clé
- `clear()` : Permet de supprimer toutes les données
- `key()` : Permet de récupérer la clé à un index donné
- `length` : Permet de récupérer le nombre de clés

> [!Example]
> ```javascript
> localStorage.setItem("nom", "John");
> console.log(localStorage.getItem("nom")); // John
> localStorage.removeItem("nom");
> localStorage.clear();


## Stocker des tableaux
Dans le localStorage, il n'est possible de stocker que des chaînes de caractères. Pour stocker un tableau, il faut le transformer en JSON

> [!Example]
> ```javascript
> let monTableau = [1,2,3,4,5];
> localStorage.setItem("tableau", JSON.stringify(monTableau)); // Stocker le tableau dans le localStorage
> let tableau = JSON.parse(localStorage.getItem("tableau")); // Récupérer le tableau

---

# Les promesses en JS
Les promesses permettent de gérer des opérations asynchrones. Une promesse peut être dans l'un des trois états suivants :
- `pending` : En attente
- `fulfilled` : Réalisée
- `rejected` : Rejetée
Une promesse est créée avec le constructeur `Promise` et prend en paramètre une fonction qui prend deux arguments : `resolve` et `reject`. `resolve` est appelé lorsque la promesse est réalisée et `reject` lorsqu'elle est rejetée

> [!Example]
> ```javascript
> let maPromesse = new Promise((resolve, reject) => {
> 	if(/* Opération réussie */) {
> 		resolve("Opération réussie");
> 	} else {
> 		reject("Opération échouée");
> 	}
> });

Il est possible de chaîner les promesses avec les méthodes `then` et `catch`. `then` est appelé lorsque la promesse est réalisée et `catch` lorsqu'elle est rejetée

> [!Example]
> ```javascript
> maPromesse.then((message) => {
> 	.then((message) => {
> 		console.log(message);
> 	})
> 	.catch(erreur => {
> 		console.log(erreur);
> 	});