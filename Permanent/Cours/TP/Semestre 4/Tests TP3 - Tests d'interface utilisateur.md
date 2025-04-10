L'objectif est de réaliser des tests d'interface utilisateurs en utilisant *Cypress*, de générer automatiquement des tests Cypress ainsi que de maîtriser l'interception de requêtes

# Cypress
C'est un framework de tests fonctionnels s'appuyant sur des librairies d'assertion, en particulier `Chai`

## Installation et exécution
Pour utiliser **Cypress** dans notre projet, il faut commencer par l'installer. Dans le répertoire de notre projet, exécuter la commande `npm install cypress --save-dev`. Cela l'installe comme une dépendance de développement du projet et ajoute une entrée dans le fichier `package.json`. L'option `--save-dev` est importante car cela spécifie que **Cypress** est utilisé pour le développement (tests)

Une fois installer, il faut exécuter la commande `./node_modules/.bin/cypress open` pour pouvoir lancer **Cypress**

> Dans le fichier `scripts.json`, si j'ajoute dans la section `scripts` le code suivant :
> ```Json
> {
> 	"scripts": {
> 		"cypress:open": "cypress open"
> 	}
>}
>```
> Je pourrai ainsi lancer `Cypress` en faisant la commande `npm run cypress:open`

> [!Attention]
> Il faut que le serveur soit lancé : `npm run serve` !
## Test de l'interface du jeu d'échecs
Une fois **Cypress** lancé, il faut cliquer sur le bouton *Open project* pour ouvrir le projet contenant le code source du jeu d'échecs. Nous allons par la suite choisir l'approche *E2E testing*. Il faut finalement lancer une suite de tests (exemple : `simple.cy.js`)
Une fois le navigateur choisit, ce dernier va se lancer sur le tableau de bord Cypress, qui affiche :
- Un ensemble de suites de tests d'intégration dans la partie centrale
- Le navigateur choisit pour lancer les tests
- Les tests passés et ceux qui ne l'ont pas été dans la partie gauche
- Une vue graphique montrant concrètement l'exécution du test à droite
- En haut, un récapitulatif des tests passés, échoués et quelques informations sur le navigateur à droite
<div style="display: flex; justify-content: space-between;">   <img src="Pasted image 20250312135845.png" alt="Image 1" style="width: 48%;">  <img src="Pasted image 20250312135903.png" alt="Image 2" style="width: 48%;"> </div>

Le test qui s’est exécuté est un **test fonctionnel**. Le système est vu comme une boite noire. Après avoir simulé deux interactions sur l’interface, on vérifie de manière globale le comportement de l’application. Ici, nous vérifions qu’une pièce puisse être sélectionnée (la case de l’échiquier devient _active_) puis désélectionnée (la case redevient inactive)

En nous intéressant à la structure du test fonctionnel :
```JS
describe('Move a piece on the chessboard', () => {
  beforeEach(() => {
    cy.visit('http://localhost:8090/web/');
  });

  it('move a white pawn from c7 to c6', function () {
    cy.get('#chessboard .rank:nth-child(2) div:nth-child(3)').click();

    cy.get('#chessboard .rank:nth-child(2) div:nth-child(3)').should(
      'have.class',
      'active'
    );

    cy.get('#chessboard .rank:nth-child(3) div:nth-child(3)').click();

    cy.get('#chessboard .rank:nth-child(2) div:nth-child(3)').should(
      'not.have.class',
      'active'
    );
  });
});
```

Comme dit plus tôt, Cypress s'appuie sur Mocha pour l'écriture de tests fonctionnels. On retrouve les appels de fonctions de `hook` ainsi que la spécification des cas de tests avec la fonction `it()̀
1. La toute première étape est de visiter la page : `cy.visit('http://localhost:8090/web/');` (Le numéro de port peut être édité dans le fichier `package.json`, ligne `"serve": "http-server ./ -p 8090"`)
2. On va ensuite trouver un élément de la page à partir d'un sélecteur CSS : `cy.get()`
3. On peut simuler un click de la sourir : `cy.click()`
4. Finalement, on va effectuer des assertions sur l'état de l'élément : `cy.should()
D'autres fonctions existent :
- `cy.type()` : Simuler une entrée clavier
- `cy.intercept()` : Intercépter les requêtes réseaux et simuler les réponses
- `cy.trigger('blur')` ou `cy.blur()` : Pour simuler la perte de focus sur un élément


---

# 📌 Contexte : Cypress et `cy.intercept()`

`cy.intercept()` est une commande de **Cypress** qui permet d’**intercepter, espionner, modifier ou simuler** les requêtes réseau (HTTP/HTTPS) faites par ton application. Cela rend les tests plus **rapides, stables et indépendants** du backend.

---

## 🛠️ Syntaxe de base

```js
cy.intercept(method?, url?, routeHandler?)
```

- **`method`** (optionnel) : Méthode HTTP (`GET`, `POST`, `PUT`, etc.)
    
- **`url`** : URL ou motif de l'URL à intercepter (string, RegExp ou glob pattern comme `**/api/users`)
    
- **`routeHandler`** (optionnel) :
    
    - pour espionner : `req => { /* ... */ }`
        
    - pour simuler : un objet (`{ fixture: 'user.json' }`, ou `statusCode`, `body`, etc.)
        

---

## 🔍 Espionner une requête

```js
cy.intercept('GET', '/api/users').as('getUsers');
cy.visit('/dashboard');
cy.wait('@getUsers');
```

👉 Cela permet d’attendre que l’appel `/api/users` ait lieu, et d’en vérifier les détails (statut, corps, etc.).

---

## 🧪 Modifier ou simuler une réponse

```js
cy.intercept('GET', '/api/users', {
  statusCode: 200,
  body: [{ id: 1, name: 'Alice' }],
}).as('mockedUsers');
```

👉 Même si le serveur est indisponible, le test passe car Cypress retourne une **réponse simulée**.

---

## 📁 Utiliser une fixture

```js
cy.intercept('GET', '/api/users', { fixture: 'users.json' }).as('mockUsers');
```

➡️ `users.json` est un fichier dans `cypress/fixtures/`

---

## 🧠 Exemples avancés

### Filtrage avec requêtes dynamiques

```js
cy.intercept('GET', '**/api/users/**', (req) => {
  req.continue((res) => {
    expect(res.statusCode).to.eq(200);
  });
});
```

### Modifier la requête avant l’envoi

```js
cy.intercept('POST', '/api/login', (req) => {
  req.body.username = 'admin';
  req.continue();
});
```

---

## 🔗 Comparaison avec `.route()` (ancienne méthode)

Avant Cypress v6.0 :

```js
cy.server();
cy.route('GET', '/api/users', 'fixture:users.json');
```

➡️ Maintenant remplacé par `cy.intercept()` (plus puissant et flexible).

---

## ⚠️ Attention : Tests Java ≠ Cypress

Cypress est basé sur **JavaScript**, pas Java.  
Si tu fais du **test d’API ou UI en Java**, il existe d'autres outils :

|But|Outil Java équivalent|
|---|---|
|UI testing|Selenium WebDriver|
|API mocking|WireMock|
|Assertion réseau|REST Assured|
|E2E complète|Testcontainers + SpringBootTest|

---

## ✅ Avantages de `cy.intercept`

- Pas besoin de serveur backend pendant les tests
    
- Plus rapide et fiable (moins dépendant du réseau)
    
- Permet de tester des cas d’erreurs difficiles à reproduire
    
- Espionnage des requêtes pour vérification précise
    

---

## 🎯 Cas d’usage typique

Imaginons que tu développes un tableau de bord :

```js
describe('Dashboard', () => {
  it('affiche la liste des utilisateurs', () => {
    cy.intercept('GET', '/api/users', {
      fixture: 'users.json',
    }).as('getUsers');
    
    cy.visit('/dashboard');
    cy.wait('@getUsers');
    cy.get('ul.users li').should('have.length', 3);
  });
});
```


# 🧪 Exemple typique : Interception de reCAPTCHA v2 (invisible ou visible)

### 🔍 Cas concret

Ton application utilise reCAPTCHA v2, qui envoie une requête réseau du type :

```http
POST https://www.google.com/recaptcha/api2/reload
```

ou parfois

```http
POST https://www.google.com/recaptcha/api/siteverify
```

---

### ✅ Solution Cypress : interception + simulation de réponse

```js
describe('Login avec reCAPTCHA', () => {
  it('simule la validation du CAPTCHA', () => {
    // Intercepte l’appel au service Google reCAPTCHA et renvoie une réponse "succès"
    cy.intercept('POST', 'https://www.google.com/recaptcha/**', {
      statusCode: 200,
      body: { success: true, challenge_ts: Date.now(), hostname: 'localhost' }
    }).as('captcha');

    cy.visit('/login');

    cy.get('input[name="email"]').type('user@example.com');
    cy.get('input[name="password"]').type('password123');

    cy.get('form').submit();

    // Optionnel : attendre que la requête CAPTCHA ait été "mockée"
    cy.wait('@captcha');

    // Vérifie la redirection ou l’affichage d’un message
    cy.url().should('include', '/dashboard');
  });
});
```

---

### ⚠️ Attention

- Certaines implémentations ne font **pas d'appel AJAX** vers reCAPTCHA, mais intègrent un **script frontend** qui bloque ou interagit avec le DOM.
    
- Dans ce cas, il faut soit :
    
    - **mock le script** via `cy.intercept('GET', 'https://www.google.com/recaptcha/**')`
        
    - **désactiver reCAPTCHA côté frontend** si l’environnement de test est détecté (ex. `if (Cypress.env('test')) disableCaptcha()`)
        

---

## ✅ Bonus : Stratégie de contournement "propre"

Une pratique fréquente en entreprise est de **désactiver ou simuler le captcha côté serveur si on est en test** :

```js
// Dans ton backend
if (process.env.NODE_ENV === 'test') {
  // bypass captcha check
  return res.json({ success: true });
}
```

Ensuite dans Cypress, tu ne te préoccupes même plus de l’interception.

---

Tu veux que je t’aide à gérer un captcha dans un projet **Java + Spring Boot** ? Ou tu veux aussi voir un exemple avec hCaptcha ou un autre type de captcha ?


# Exemple avec envoi mail
## 🧾 **Consigne simplifiée**

> Quand l’utilisateur tape l’e-mail **[abc@provider.com](mailto:abc@provider.com)** et quitte le champ :
> 
> - Intercepte l’appel `GET /email?email=...` et renvoie une réponse disant que l’e-mail est déjà utilisé.
>     
> - Vérifie que le champ est invalide.
>     
> - Vérifie que le message d’erreur s’affiche avec le bon texte : **"This email has already been used"**.
>     

---

## ✅ **Code Cypress correspondant**

```js
describe('TF7 - Email déjà utilisé', () => {
  it('affiche une erreur si l’e-mail est déjà dans la base', () => {
    // Interception de la requête AJAX de vérification d’email
    cy.intercept('GET', '/email?email=*', {
      statusCode: 200,
      body: {
        presentInDatabase: true,
        msg: 'This email has already been used'
      }
    }).as('checkEmail');

    cy.visit('/inscription'); // adapte selon ton URL réelle

    // Saisie de l’e-mail
    cy.get('input[name="email"]').type('abc@provider.com').blur(); // blur = perte de focus

    // Attend la requête interceptée
    cy.wait('@checkEmail');

    // Vérifie que le champ est invalide
    cy.get('input[name="email"]').should('have.class', 'is-invalid'); // adapte la classe selon ton HTML

    // Vérifie le message d’erreur
    cy.get('.email-error') // adapte le sélecteur à ton code
      .should('be.visible')
      .and('contain', 'This email has already been used');
  });
});
```

---

Souhaite-tu que je t’adapte le test à ta structure HTML précise (ex: classes Bootstrap, messages d’erreur, etc.) ?