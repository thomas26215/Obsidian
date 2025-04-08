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
Les promesses permettent de gérer des opérations asynchrones. Elles permettent de gérer des tâches prenant du temps à s'exécuter sans pour autant bloquer le reste du code. Une promesse peut être dans l'un des trois états suivants :
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

Il est possible de chaîner plusieurs promesses permettant d'éviter le callback hell

> [!Example]
> ```javascript
> fetch('https:/api.example.com/users')
> 	.then(response => response.json())
> .then(user => fetch(`https:/api.example.com/posts/${user.id}`))
> .then(response => response.json())
> .then(posts => console.log(posts))
> .catch(error => console.error(error));
> ```
> 
> **Explications détaillées** :
> - On récupère les utilisateurs
> - On récupère les posts de l'utilisateur
> - On affiche les posts
> - On gère les erreurs

Il existe une méthode `Promise.all()` qui permet d'exécuter plusieurs promesses en parallèle et de renvoyer un tableau de résultats

> [!Example]
> ```javascript
> Promise.all([promise1, promise2, promise3])
> .then(resultats => {
> 	console.log(resultats);
> })
> .catch(erreur => console.error(erreur));

---

Voici un exemple complet sur l'utilisation des promesse :

```javascript
console.log("Début du chargement du profil");

const chargerProfilUtilisateur = new Promise((resolve, reject) => {
	setTimeout(() => {
		const utilisateur = {
			nom: "John",
			age: 30
		};
		
		if(Math.random() < 0.5) {
			resolve(utilisateur);
		} else {
			reject("Erreur lors du chargement du profil");
		}
	}, 3000);
});

chargerProfilUtilisateur
	.then(utilisateur => {
		console.log(utilisateur);
	})
	.catch(erreur => {
		console.error(erreur);
	})
	.finally(() => {
		console.log("Fin du chargement du profil");
	});

console.log("Chargement du profil en cours ...");
```

Ici, le script JS commence par afficher "Début du chargement du profil" puis crée une promesse `chargerProfilUtilisateur` qui simule un chargement de profil utilisateur. Si le chargement réussit, la promesse est réalisée et affiche le profil de l'utilisateur. Si le chargement échoue, la promesse est rejetée et affiche une erreur. Enfin, le script affiche "Fin du chargement du profil", même si le chargement du profil échoue.


# Ascyn et fetch

## Introduction à l'asynchronisme en JavaScript avec `async` et `await`

L'asynchronisme en JavaScript permet d'exécuter des tâches longues sans bloquer l'exécution du reste du programme. Cela est particulièrement utile pour des opérations telles que les requêtes HTTP, les accès aux fichiers ou les temporisations. Les mots-clés **`async`** et **`await`** simplifient la gestion des promesses et rendent le code asynchrone plus lisible.

---

### **Le mot-clé `async`**

Le mot-clé **`async`** devant une fonction indique que cette fonction est asynchrone. Une fonction asynchrone retourne toujours une promesse.

#### Exemple :
```javascript
async function myFunction() {
  return "Hello";
}

// Equivalent à :
function myFunction() {
  return Promise.resolve("Hello");
}
```

Vous pouvez utiliser `.then()` pour traiter la valeur retournée par une fonction asynchrone :
```javascript
myFunction().then(value => console.log(value)); // Affiche "Hello"
```

---

### **Le mot-clé `await`**

Le mot-clé **`await`** est utilisé uniquement à l'intérieur d'une fonction déclarée avec `async`. Il suspend l'exécution de la fonction jusqu'à ce que la promesse soit résolue ou rejetée.

#### Exemple simple :
```javascript
async function fetchData() {
  const promise = new Promise((resolve) => {
    setTimeout(() => resolve("Données récupérées"), 2000);
  });

  const result = await promise; // Attendre que la promesse soit résolue
  console.log(result); // Affiche "Données récupérées"
}

fetchData();
```

---

### **Combinaison de `async` et `await`**

Ces deux mots-clés permettent de structurer le code asynchrone de manière linéaire, comme un code synchrone.

#### Exemple avec plusieurs étapes :
```javascript
async function processData() {
  const data = await fetchDataFromAPI(); // Récupération des données
  const processedData = await processDataLocally(data); // Traitement local
  console.log(processedData);
}
```

---

### **Gestion des erreurs avec `try/catch`**

Pour gérer les erreurs dans une fonction asynchrone, utilisez un bloc `try/catch`.

#### Exemple :
```javascript
async function fetchProducts() {
  try {
    const response = await fetch("https://api.example.com/products");
    if (!response.ok) throw new Error(`Erreur HTTP : ${response.status}`);
    
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(`Erreur lors de la récupération des produits : ${error}`);
  }
}

fetchProducts();
```

---

### **Exécution concurrente avec `Promise.all`**

Si vous avez plusieurs promesses à exécuter en parallèle, utilisez **`Promise.all()`** pour attendre qu'elles soient toutes résolues.

#### Exemple :
```javascript
async function fetchMultipleData() {
  const [data1, data2] = await Promise.all([
    fetch("https://api.example.com/data1"),
    fetch("https://api.example.com/data2")
  ]);

  console.log(data1, data2);
}
```

---

### **Différences entre exécution séquentielle et concurrente**

| Type d'exécution       | Description                                                                 | Temps total |
|-------------------------|-----------------------------------------------------------------------------|-------------|
| Séquentielle            | Les promesses sont exécutées une par une (chaque `await` attend l'autre).   | Somme des temps individuels |
| Concurrente             | Les promesses sont exécutées en parallèle (`Promise.all`).                  | Temps du processus le plus long |

#### Exemple comparatif :
```javascript
// Exécution séquentielle
async function sequentialExecution() {
  const result1 = await fetchData1();
  const result2 = await fetchData2();
}

// Exécution concurrente
async function concurrentExecution() {
  const [result1, result2] = await Promise.all([fetchData1(), fetchData2()]);
}
```

---

### **Points importants**

- Une fonction marquée avec `async` retourne toujours une promesse.
- Le mot-clé `await` simplifie la gestion des promesses en rendant leur résolution synchrone.
- Utilisez `try/catch` pour capturer les erreurs dans les fonctions asynchrones.
- Préférez `Promise.all()` pour exécuter plusieurs tâches en parallèle lorsque cela est possible.

Ces concepts sont essentiels pour écrire un code JavaScript efficace et lisible dans les environnements modernes.

---

# Exemple d'un fetch avec async

### **Explication complète de l'utilisation de `.then()` avec `fetch`**

`fetch` est une API JavaScript moderne pour effectuer des requêtes HTTP. Elle retourne une **promesse** qui peut être utilisée avec `.then()` pour gérer les étapes successives de la requête. Voici une explication détaillée pour comprendre comment utiliser `.then()` dans le contexte d'une requête AJAX vers `generation.php`.

---

### **Étapes d'une requête avec `fetch` et `.then()`**

1. **Effectuer une requête HTTP avec `fetch` :**
   - La méthode `fetch()` envoie une requête HTTP et retourne une promesse.
   - Cette promesse est résolue lorsque la réponse est disponible (même si le statut HTTP indique une erreur, comme 404 ou 500).

2. **Vérifier la réponse HTTP :**
   - Une fois la promesse résolue, vous recevez un objet `Response`.
   - Vous devez vérifier si la réponse est correcte en utilisant la propriété `response.ok`. Si cette propriété est `false`, cela signifie qu'il y a eu une erreur côté serveur.

3. **Convertir les données en JSON :**
   - Si la réponse est correcte, vous pouvez utiliser la méthode `.json()` de l'objet `Response` pour convertir les données en un objet JavaScript. Cette méthode retourne également une promesse.

4. **Traiter les données JSON :**
   - Une fois que les données sont converties en JSON, vous pouvez les utiliser dans votre application.

5. **Gérer les erreurs :**
   - Si une erreur survient à n'importe quelle étape (par exemple, problème réseau ou erreur dans le script PHP), vous pouvez capturer cette erreur avec `.catch()`.

---

# **Exemple complet avec explications**

Voici un exemple complet avec des commentaires détaillés :

```javascript
// Requête AJAX vers generation.php
fetch('generation.php') // Étape 1 : Envoi de la requête GET
  .then(response => {
    // Étape 2 : Vérification de la réponse HTTP
    if (!response.ok) {
      // Si le statut HTTP n'est pas OK (exemple : 404, 500), on lève une erreur
      throw new Error(`Erreur HTTP : ${response.status}`);
    }
    // Étape 3 : Conversion des données en JSON (retourne une promesse)
    return response.json();
  })
  .then(data => {
    // Étape 4 : Traitement des données JSON
    console.log(`Mot à deviner : ${data.mot}, Nombre d'essais : ${data.nb_essais}`);
    
    // Exemple d'intégration dans l'interface utilisateur
    updateGameUI(data.mot, data.nb_essais);
  })
  .catch(error => {
    // Étape 5 : Gestion des erreurs
    console.error('Erreur lors de la récupération du mot :', error);
  });

// Fonction pour mettre à jour l'interface utilisateur
function updateGameUI(mot, nbEssais) {
  document.getElementById("word").textContent = "_ ".repeat(mot.length); // Affiche des tirets pour chaque lettre
  document.getElementById("attempts").textContent = `Nombre d'essais restants : ${nbEssais}`;
}
```

---

### **Explications des étapes**

#### **Étape 1 : Envoi de la requête GET**
```javascript
fetch('generation.php')
```
- La méthode `fetch()` envoie une requête HTTP GET à l'URL spécifiée (`generation.php`).
- Elle retourne immédiatement une promesse qui sera résolue lorsque le serveur répondra.

#### **Étape 2 : Vérification de la réponse HTTP**
```javascript
.then(response => {
  if (!response.ok) {
    throw new Error(`Erreur HTTP : ${response.status}`);
  }
  return response.json();
})
```
- L'objet `response` contient les métadonnées de la réponse (statut HTTP, en-têtes, etc.).
- La propriété `response.ok` est `true` si le statut HTTP est compris entre 200 et 299.
- Si le statut n'est pas correct, on lève une erreur avec `throw new Error(...)`.
- Si tout va bien, on appelle `response.json()` pour convertir les données en JSON.

#### **Étape 3 : Conversion des données en JSON**
```javascript
return response.json();
```
- La méthode `.json()` lit le corps de la réponse et le convertit en un objet JavaScript.
- Cette méthode retourne également une promesse qui sera résolue avec les données JSON.

#### **Étape 4 : Traitement des données JSON**
```javascript
.then(data => {
  console.log(`Mot à deviner : ${data.mot}, Nombre d'essais : ${data.nb_essais}`);
})
```
- Les données JSON sont disponibles sous forme d'un objet JavaScript.
- Dans cet exemple, on suppose que l'objet JSON a cette structure :
  ```json
  {
    "mot": "ELEPHANT",
    "nb_essais": 6
  }
  ```
- Vous pouvez ensuite utiliser ces données dans votre application (par exemple, mettre à jour l'interface utilisateur).

#### **Étape 5 : Gestion des erreurs**
```javascript
.catch(error => {
  console.error('Erreur lors de la récupération du mot :', error);
});
```
- Si une erreur survient à n'importe quelle étape (problème réseau, erreur dans le script PHP, etc.), elle sera capturée ici.
- Vous pouvez afficher un message d'erreur ou prendre d'autres mesures.

---

### **Avantages et inconvénients de `.then()`**

#### Avantages :
1. Facile à comprendre pour les débutants.
2. Permet de chaîner plusieurs opérations asynchrones.
3. Compatible avec tout environnement moderne supportant les promesses.

#### Inconvénients :
1. Peut devenir difficile à lire si plusieurs étapes sont chaînées (effet "callback hell").
2. Moins lisible que l'approche avec `async/await` lorsque le code devient complexe.

---

### **Comparaison avec `async/await`**

Voici comment le même code pourrait être écrit avec `async/await` :

```javascript
async function fetchWord() {
  try {
    const response = await fetch('generation.php'); // Envoi de la requête GET

    if (!response.ok) {
      throw new Error(`Erreur HTTP : ${response.status}`);
    }

    const data = await response.json(); // Conversion en JSON
    console.log(`Mot à deviner : ${data.mot}, Nombre d'essais : ${data.nb_essais}`);
    
    updateGameUI(data.mot, data.nb_essais); // Exemple d'intégration dans l'UI

  } catch (error) {
    console.error('Erreur lors de la récupération du mot :', error);
  }
}

// Appel de la fonction au chargement de la page
document.addEventListener('DOMContentLoaded', fetchWord);
```

#### Différences :
- Avec `.then()`, vous gérez chaque étape dans un bloc séparé.
- Avec `async/await`, le code semble plus linéaire et ressemble davantage à du code synchrone.

---

### Conclusion

L'utilisation de `.then()` ou `async/await` dépend principalement des préférences personnelles et du contexte du projet. Les deux approches permettent de gérer efficacement les appels asynchrones comme ceux effectués avec `fetch`.

# Exemple 1

Voici un exemple de code complet répondant à votre demande pour implémenter la méthode `getNewWordObject()` et son utilisation dans le contrôleur.

---

### **1. Méthode asynchrone `getNewWordObject()` dans le modèle**
Cette méthode effectue une requête AJAX de type GET vers `generation.php` et retourne un objet JavaScript contenant le mot et le nombre d'essais.

```javascript
// Modèle : model.js
async function getNewWordObject() {
  try {
    const response = await fetch("generation.php"); // Appel AJAX GET
    if (!response.ok) {
      throw new Error(`Erreur HTTP : ${response.status}`);
    }
    const data = await response.json(); // Conversion en objet JS
    return data; // Exemple : { mot: "ELEPHANT", nb_essais: 6 }
  } catch (error) {
    console.error("Erreur lors de la récupération du mot :", error);
    throw error; // Propagation de l'erreur pour gestion ultérieure
  }
}
```

---

### **2. Appel de `getNewWordObject()` dans le contrôleur**
Le contrôleur utilise la méthode asynchrone pour récupérer les données et les intégrer au jeu.

```javascript
// Contrôleur : main.js
async function initGame() {
  try {
    const wordObject = await getNewWordObject(); // Appel de la méthode asynchrone
    console.log(`Mot à deviner : ${wordObject.mot}, Nombre d'essais : ${wordObject.nb_essais}`);

    // Exemple d'intégration dans le jeu
    updateGameUI(wordObject.mot, wordObject.nb_essais);
  } catch (error) {
    console.error("Impossible d'initialiser le jeu :", error);
  }
}

// Fonction pour mettre à jour l'interface utilisateur (exemple)
function updateGameUI(mot, nbEssais) {
  document.getElementById("word").textContent = "_ ".repeat(mot.length); // Affiche des tirets pour chaque lettre
  document.getElementById("attempts").textContent = `Nombre d'essais restants : ${nbEssais}`;
}

// Initialisation du jeu au chargement de la page
document.addEventListener("DOMContentLoaded", () => {
  initGame();
});
```

---

### **3. Exemple de script PHP (`generation.php`)**
Ce script génère un mot aléatoire parmi une liste et retourne un JSON structuré.

```php
 5,
    "ELEPHANT" => 6,
    "TIGRE" => 4,
    "GIRAFE" => 5,
];

$randomWord = array_rand($words); // Sélection aléatoire d'un mot
$response = [
    "mot" => $randomWord,
    "nb_essais" => $words[$randomWord],
];

// Retourne le JSON
header('Content-Type: application/json');
echo json_encode($response);
?>
```

-

---

### **Résumé du fonctionnement**
1. La méthode `getNewWordObject()` envoie une requête AJAX à `generation.php` pour récupérer un mot aléatoire et le nombre d'essais disponibles.
2. Le contrôleur (`main.js`) utilise cette méthode pour initialiser le jeu.
3. L'interface utilisateur est mise à jour dynamiquement avec les données reçues.
4. Le script PHP génère les données nécessaires sous forme de JSON.
