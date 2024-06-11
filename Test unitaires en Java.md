---
MOOC: "[[Programmation]]"
Langage: Java
Type: Tests Unitaires
tags:
---
Les tests unitaires sont des tests automatisés vérifiant les plus petites parties testables d'une application (les méthodes d'une classe)

## Tests unitaires avec JUnit5
## Structure du code JUnit5
Dans ma classe de Test (`PersonneTest` par exemple), je peux créer autant de fonction que je souhaite faire de tests. Voici la construction :
- La méthode est annotée de `@test`
- La méthode contenant le test
- A l'intérieur de la méthode
	- Le code que je souhaite vérifier
	- Une assertion ou une vérification pour vérifier si le code testé est valable (`asserEquals`, `assertTrue`)

```java
public class PersonneTest{
	@Test
	void ageInferieurA100(){
		//Code
		Personne personne = new Personne("Sophie", 19);
		//Vérification pour savoir si l'âge est inférieur à 100
		assertTrue(personne.getAge()<100);
	}
}
```