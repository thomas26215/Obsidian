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

