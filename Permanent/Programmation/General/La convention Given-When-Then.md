---
MOOC: "[[Programmation]]"
Langage: General
Type: Tests Unitaires
tags:
---
Pour écrire un test unitaire, une convention est ***Given-When-Then*** :
- **Given :** Construction de l'état du monde
- **When :** Exécution du code testé
- **Then** : Vérification du résultat obtenu (assetion, prédiction de l'oracle)

>[!Example] Exemple (Code écrit en JavaScript)
>
>```javascript
import assert from 'node:assert';
>import Money from '../src/money.js';
>
>describe('Money', function() {
>	describe('#add()', function() {
>		it('should correctly add two moneys with the same currency', function() {
>			let m1 = new Money(10.0, 'EUR'), //Given
>				m2 = new Money(20.0, 'EUR'); //Given
>			m1.add(m2); //When
>			assert.equals(m1.amount, 30.0); //Then
>		});
>	});
>})
>```