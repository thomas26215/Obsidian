---
MOOC: "[[Programmation]]"
Langage: Java
Type: Tri d'objets
tags:
---
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