---
MOOC: "[[Programmation]]"
Langage: Java
Type: Tri d'objets
tags:
---
Les interfaces `Comparator` et `Comparable` sont utilisés pour définir l'ordre de tri des objets. Cela permet de les trier de manière spécifiques

# Interface Comparable
Elle est utilisée pour définir l'ordre naturel des objets d'une classe. Elle impose un ordre de tri par défaut pour tous les objets en implémentant la méthode `compareTo`

## Que doit retourner la méthode compareTo ?
Cette méthode doit être implémentée pour déterminer (ou plutôt redéfinir) l'ordre naturel des objets. Elle retourne :
- Un entier négatif (-1) si l'objet courant est inférieur à l'objet spécifié
- 0 si l'objet courant est égal à l'objet spécifié
- Un entier positif (+1) si l'objet courant est supérieur à l'objet spécifié

## Utilisation de CompareTo
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


# L'interface d'un Comparator

>[!Warning]
>Impératif de savoir utiliser `Comparable`

Il se peut que l'utilisation de l'interface Comparable ne suffise pas. En effet, cette interface ne trie que d'une seule manière, mais il se peut que l'on souhaite trier selon certains critères.
L'interface Comparator pemet de créer des objets *comparateur* `monComparateur` et les passer en arguments à certaines méthodes (`Collection.sort(maCollection, monComparateur);`) ou à certains constructeurs (`TreeSet<>(monComparateur);`)

## Solution 1
```java
public class Personne implements Comparable{
	/*
	 * Attributs
	 * Constructeur
	 * Getters et Setters
	 */

	@Override
	public int compareTo(Personne autrePersonne){
		/*
		 * Trier naturellement par ordre décroissant
		 */
	}


	/*
	 * Des fois, je souhaite trier selon le prénom. Nouvelle classe à l'intérieur de ma classe
	 */
	public class MaClasseCompTriParAttrXY implements Comparator<Personne>{
		@override
		public int compare(Personne o1, Personne o2){
			...
			return -1; // o1 inférieur à o2 pour les attributs X, Y
			...
			return 0; // o1 égal à o2 pour les attributs X, Y
			...
			return 1; // o1 supérieur à o2 pour les attributs X, Y
		}
	}
}
public class Main(String[] args){
	//
	Collections.sort(personnes, new MaClasseCompTriParAttrXY());
}
```


## Solution 2
```java
public class Personne implements Comparable{
	/*
	 * Attributs
	 * Constructeur
	 * Getters et Setters
	 */

	@Override
	public int compareTo(Personne autrePersonne){
		/*
		 * Trier naturellement par ordre décroissant
		 */
	}


	/*
	 * Des fois, je souhaite trier selon le prénom. Nouvelle classe à l'intérieur de ma classe
	 */
	public static final Comparator CompMaClasseTriParAttrXY = new Comparator() {
		@override
		public int compare(MaClasse o1, MaClasse o2){
			...
			return -1; // o1 inférieur à o2 pour les attributs X, Y
			... return 0;
			// o1 égal à o2 pour les attributs X, Y
			...
			return 1; // o1 supérieur à o2 pour les attributs X, Y
		}
	};
}
public class Main(String[] args){
	//
	Collections.sort(personnes, new MaClasseCompTriParAttrXY());
}
```


