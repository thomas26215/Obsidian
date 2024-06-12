---
MOOC: "[[Programmation]]"
Langage: Java
Type: Tri d'objets
tags:
---
Tout d'abord, dans la classe où l'on utilise `CompareTo`, il faut implémenter l'interface `Comparable<Classe>`.
Il faut ensuite appeler la fonction `compareTo`, et retourner les bonnes valeurs.
Enfin, quand des éléments de cette classe sont mis dans une liste (`List`, `ArrayList`, `HashSet` ...), il faut utiliser `Collections.sort(Liste)` afin de trier selon le `compareTo`

>[!info] Automatiquement trié ?
>Les éléments implémentant l'interface `Comparable` sont triés à l'insertion dans une collection triée comme `TreeSet`


```java
public class Personne implement Comparable<Personne>{
	private String name,
	private int age;

	public Personne(String name, int age){
		//On définit
	}
	/*
	 * On définit les getters et setters
	 */

	/*
	 * Tri par âge décroissant
	 */
	
	@Override
	public int compareTo(Personne autrePersonne){
		if(this.age < autrePersonne.getAge()){
			return 1;
		}else if(this.age > autrePersonne.getAge()){
			return -1;
		}else{
			return 0;
		}
	}
	
	public static void main(String[] args){
		List<Personnes> personnes = new ArrayList<>();
		personnes.add(new Personne("Alice", 30));
		personnes.add(new Personne("Bob", 25));
		personnes.add(new Personne("Charlie", 42));

		Collections.sort(personnes);

		for(Personne p : personnes){
			System.out.println(p);
		}
	}
}
```