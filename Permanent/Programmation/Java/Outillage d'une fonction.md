---
MOOC: "[[Programmation]]"
Langage: Java
Type: Outillage
tags:
---
Afin d'outiller une fonction (autrement dit faire le nombre de comparaisons), il est nécessaire d'utiliser une classe générique. En effet, il n'existe aucun moyen connu de renvoyer deux valeurs à la fois dans une fonction, autre le fait de renvoyer avec une fonction. La première étape consiste donc à créer une classe générique immuable, que l'on va nommer `PaireResultatCompteur<R>`, Avec `R` un paramètre de généricité de type classe. Il y aura donc deux attributs, `resultat`, qui sera donc de type `R` et le `compteur` qui sera de type `int` :
```Java
public class PaireResultatCompteur<R>{
	private final resultat R;
	private final resultat compteur;

	public PaireResultatCompteur(R resultat, int compteur){
		this.resultat = resultat;
		this.compteur = compteur;
	}
	public R getResultat(){
		return resultat;
	}
	public int getCompteur(){
		return compteur;
	}
}
```

Une fois cela fait, dans la fonction, nous aurait juste à renvoyer les deux variables en faisant appel à la fonction, ici avec une valeur de base `String` :
```Java
public static PaireResultatCompteur<int> maFonctionQuiRenvoieString{
	String valeur;
	int compteur = 0;

	...
	...

	return new PaireResultatCompteur<>(valeur, compteur);
}
```