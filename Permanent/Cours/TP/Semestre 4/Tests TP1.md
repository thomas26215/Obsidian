[[Test unitaire]]
[[Test unitaire fonctionnel]]
[[Test unitaire structurel]]

[[La convention Given-When-Then]]

---

[[La librairie assert NodeJS]]




Il est possible de réaliser des tests unitaires avec la libraire par défaut de `Node.JS` en utilisant la librairie d'insertion `assert`. Il faut pour cela l'importer dans notre code de test unitaires : `import assert from 'node:assert'` Voici à quoi pourrait ressembler un test :

```javascript
import assert from 'node:assert';
import Money from '../src/money.js';

describe('Money', function () {
  describe('#add()', function () {
    it('should correctly add two moneys with the same currency', function () {
      // Given: two instances of money with the EUR currency
      let m1 = new Money(10.0, 'EUR'),
        m2 = new Money(20.0, 'EUR');

      // When: we add the amount of m2 to m1
      m1.add(m2);

      // Then: the new amount of m1 should be 30
      assert.equal(m1.amount, 30.0);
    });

    it('should correctly add two moneys with different currencies', function () {
      // Given: two instances of money with the EUR and USD currency
      let m1 = new Money(10.0, 'EUR'),
        m2 = new Money(20.0, 'USD');

      // When: we add the amount of m2 to m1
      m1.add(m2);

      // Then: the new amount of m1 should be 30
      assert.equal(m1.amount, 20.0);
    });

    it('should throw an exception when the currency is neither EUR nor USD', function () {
      // Given: two instances of money with the EUR currency
      let m1 = new Money(10.0, 'EUR'),
        m2 = new Money(20.0, 'BZR'); // BZR : Réal brésilien

      // When: we add the amount of m2 to m1
      m1.add(m2);

      // Then: it should throw an exception
      assert.throws(function () {
        // On capture l'exception
        m1.add(m2);
      });
    });
  });
});
```

Comment est structuré le code :
1. La totalité du code est englobé dans la fonction `describe`. Cela permet de donner une idée du type de code que nous testions (par exemple, sur de l'argent) :
```js
describe('Money', function() {
	...
});
```
2. Nous reproduisons le même schéma :
```js
describe('Money', function()) { //Code présenté précédemment
	describe('Add', function() {
		...
	});
}
```
3. Un test peut être réalisé grâce à `it` :
```js
it('should correctly add two moneys with the same currency', function () {
	...
});
```
4. Dans la fonction `it`, on peut vérifier une assertion grâce à `assert.equal(actual, expected)` :
```js
it('should correctly add two moneys with the same currency', function () {
	let m1 = new Money(10.0, 'EUR'),
		m2 = new Money(20.0, 'EUR');
	m1.add(m2);
	assert.equal(m1.amount, 30.0); //Utilisation ici de assert pour vérifier deux valeurs
});
```


En observant le code fournit, nous observons que la variable `m1` est initialisée à chaque test. Il est possible de factoriser cela en utilisant des hooks

**Le cycle de vie d'un test** : Setup -> Trigger -> Verify -> Teardown
- **Initialisation (Setup) :** Définir le contexte et l'environnement du test
- **Exercise (Trigger) :** Appel de l'unité à tester
- **Vérification (Verify) :** Vérification du résultat ou état produit
- **Désactivation (TearDown) :** Nettoyage, remettre le système dans son état initial

Dans Mocha, Les fictures (setup et teardown) peuvent être initialisées de ma nière globale ou locale. On peut identifier 4 fonction :
- **before()** : Exécutée une seule fois avant tous les tests d’un bloc `describe()`.
- **beforeEach()** : Exécutée avant chaque test (`it()`).
- **after()** : Exécutée une seule fois après tous les tests d’un bloc `describe()`.
- **afterEach()** : Exécutée après chaque test (`it()`).
**Exemple :**
```js
const assert = require('assert');

describe('Tests avec Mocha', function () {
    let m1;

    beforeEach(function () {
        // Réinitialisation avant chaque test
        m1 = { valeur: 0 };
    });

    it('Test 1 - Modification de m1', function () {
        m1.valeur = 10;
        assert.strictEqual(m1.valeur, 10);
    });

    it('Test 2 - m1 doit être réinitialisé', function () {
        assert.strictEqual(m1.valeur, 0);
    });
});

```

---

Dans NodeJS, il existe des librairies d'insertion. L'une des plus connues est la librairies `Chai` qui vient avec 3 style différents : `should()`, `expect̀` et `assert`. Cette librairies est très similaire à celle de la librairie pas défaut de JS

=> La méthode `assert` fonctionne exactement de la même manière que pour la librairie de tests de base de JS. Ainsi, si uniquement des fonction `asserts` sont présentes, il est uniquement nécessaire de changer l'importation de la librairie

**Exemple :**
```js
import Money from '../src/Money';
import { expect } from 'chai';

describe ("Money", function()) {
	describe (#add(), function() {
		it("should correctly add two moneys with the same currency", function() {
			let m1 = new Money (10.0, "EUR"),
			- m2 = new Money (20.0, "EUR");
			m1.add(m2);
	
			expect(m1.amount).to.equal(30.0);
		});
	});
});
```

> [!info] Installation de Chai
> L'installation de Chai se fait avec la commande `npm -i --save-dev chai`

---

