## 1. Code propre
Il faut savoir que différencier le code sale du propre ne signifie pas bien coder. Il faut non seulement l'identifier, mais également réussir à employer des stratégies pour transformer du code sale en code propre. Celui qui ne connaît pas cette sensibilité saura reconnaître qu'un code est sale, mais ne saura pas comment le transformer en code propre.
<mark style="background: #BBFABBA6;">Exemple</mark> : On sait si un tableau est beau ou pas, mais on ne sait pas faire un beau tableau

### Définition d'un code propre selon de grands programmeurs
- **Bjarne Stroustrup** : La logique doit être simple pour les bogues aient du mal à se cacher
- **Grady Booch** : Un code propre ne cache jamais les intention du concepteur, mais est au contraire constitué d'abstraction nettes et de lignes de contrôles franches
- **Dave Thomas** : Un code propre peut être lu et développé par un développeur autre que le développeur d'origine. Il dispose de tests unitaires et de recettes. Il fournit une API claire et minimale. *Selon lui, un code sans tests ne peut pas être propre*
- **Michaël Feathers** : Un code propre semble toujours avoir été par quelqu'un de soigné. Tout a déjà été imaginé par l'auteur et si vous imaginez des améliorations, vous revenez toujours au point de départ, en apréciant le code que l'on vous a laissé
- **Ron Jeffries** : Par ordre de prioriété, un code simple doit passer tous les tests, n'est pas redondant et minimise le nb d'entités, comme les classes, les méthodes, les fonctions et assimilées. *Il fait référence ici à la redondance : on ne foit pas retrouver plusieurs fois le même code*

### Nous sommes des auteurs
Quand on écrit une ligne de code, il ne faut pas oublier que nous sommes des auteurs qui écrit pour des lecteurs qui vont juger notre travail

Lorsque nous rejouons une session d'édition, on se rend compte que le rapport passé à lire et le temps passé à écrire est bien supérieur à 10:1 => Il est impossible d'écrire du code sans le lire, ainsi, en rendant un code plus facile à lire, on le rend plus facile à écrire

## 2. Noms significatifs
### Choisir des noms révélateurs
Il faut choisir des noms révélateurs. Les variables doivent répondre à un certains nombres de règles:
- La raison de son existence
- Son rôle
- Son utilisation
Le code suivant est du mauvais code :
```java
int d; //Temps écoulé en jours
```
=> Si une variable nécessite un commentaire, elle n'est pas assez descriptives
```java
int elapsedTimeInDays;
int daysSinceCreation;
int fileAgeInDays;
```
Les noms donnés sont bien plus descriptifs

**Exemple :**

Ce code :
```java
public List<int[]> getThem() {
	List<int[]> list1 = new ArrayList<int[]>
	for(int[] x : theList) 
		if(x[0] == 4)
			list1.add(x);
	return list1;
}
```
Est bien moins expressif que :
```java
public List<int[]> getFlaggedCells() {
	List<int[]> flaggedCells = new ArrayList<int[]>
	for(int[] cell : gameBoard) 
		if(cell[STATUS_VALUE] == FLAGGED)
			flaggedCells.add(cell);
	return flaggedCells;
}
```
En effet, le premier code nous fais nous poser plein d'interrogations, alors que le second pose un nom sur des concepts, améliorant considérablement la qualité du code. La simplicité du code n'a pas changé, mais ce dernier est devenu beaucoup plus explicite