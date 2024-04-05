---
MOOC: "[[Cours]]"
Ressource: java
Cours: "Cours 9 : Liste chaînée"
Date: 
tags: 
Complete: false
Learned: false
---
# Notion de type abstrait de données
## Qu'est ce qu'une TAD ?
Une TAD est une collection d'objets munies d'opérations sur ces éléments. Cela ne définit pas la façon dont les données sont stockées ni la façon dont les opérations sont implantés. Effectivement, on ne sait pas comment les données sont stockées.
On connaît déjà plusieurs TAD : `ArrayList<E>`, vecteur trié ... ⇒ Collection séquentiellement indexée

## Définition d'une TAD
Une TAD est définie par :
- **Un nom** : Un nom de type abstrait
- **L'utilisation** : Les types abstraits utilisés par celui que l'on définit
- **Les opérations** : Prototype de toutes les opérations que l'on peut faire sur le type abstrait. Parmis celles-ci, on trouve le constructeur, les transformateurs et les observateurs

## Les opérations d'un TAD
Une opération est dotée d'une pré-condition et d'une post-condition
Elle détient également une suite finie d'éléments $l_1, ..., l_n$
On appelle :
- **Tête de liste** : le premier élément de la liste
- **Reste de liste** : La liste $l_2, ..., l_n$
- **Longueur de liste** : Le nombre d'éléments de la liste
- **Liste vide** : Une liste sans éléments
- **Successeur d'un élément** : L'élément suivant de la liste, l'élément $l_{n+1}$

Les différentes opérations :
- **estVide()** boolean
- **getLongeur()**  int
- **getInfoAtPosit(posit)** info
- **InserTete(nouvelleInfo)**
- **supprimeTete()**
- **insereAtPosit(position, nouvelleInfo)** bool
- **supprimeAtPosit(position)** bool
- **setInfoAtPosit(position, nouvelleInfo)** bool
- **vide()**

## La description d'un TAD
Un TAD sera décrit par une interface qui définira uniquement les opérations. La classe ListeChainee implentera une liste implantant une interface et définira la structure de données utilisée pour représenter la liste et implantera les opérations décrites dans l'interface.

# Définition d'une interface
Une interface définit un ensemble de méthodes abstraites et éventuellement des constantes de classe
**Exemple en Java :**
```Java
public interface Mon_Interface{
	//déclaration des constantes
	type nomDeConstante = valeur;
	//signature de méthodes publiques abstraites
	type maMethode(type et nom des paramègtres formels);
}
```
Il faut savoir que n'importe quelle classe Java peut implanter une interface en utilisant en implantant toutes les méthodes que l'interface propose `public class Ma_Classe implements Une_Interface{...}`
Une classe peut aussi implanter plusieurs interfaces

# Les listes chaînées
## La classe cellule d'une liste chaînée
Il faut savoir qu'une cellule a deux attributs : Un attribut info et un attribut CelluleSuivante. Voici une classe modèle d'une cellule :
```Java
public class Cellule<TypeInfo>{
	private TypeInfo info;
	private Cellule<TypeInfo> celluleSuivante;

	public Cellule(TypeInfo info){
		this.info = info;
		this.celluleSuivante = null;
	}

	public Cellule(TypeInfo info, Cellule<TypeInfo> CelluleSuivante){
		this.info = info;
		this.CelluleSuivante = CelluleSuivante;
	}

	/*Getters et setters de info et CelluleSuivante*/
}
```

# Classe ListeChainee
On implémente le TAD liste au moyen d'une liste chaînée de `Cellule`
- **Tete** = pointeur sur la première cellule
- **nbCellules** = Nombre de Cellules de la liste


# Les exceptions
Il est possible qu'un programme rencontre une erreur ou un évènement anormal. Cela peut être dût à une erreur technique ou bien à une erreur métier. Dans ce cas-là, il faut prévoir un traitement d'erreur sur les instructions suscptibles de les provoquer.

## Le traitement d'exceptions en Java
En Java, une exception est créée par la JVM ou par une levée d'exception par le programmeur. Il y a deux solutions possibles : attraêr l'exception immédiatement pour la traiter ou bien relancer l'exception à la méthode qui a déclenché le traitement erroné
Voici la synthaxe :
```Java
try{
	
}catch (MonException e){

}[catch (AutreException e){....}]
```
---
**Questions :**
1. De quoi est composée une TAD ? Cela définit quelque chose ?
2. Donner des exemple de TAD déja connues
3. Par quoi est définit une TAD ?
5. Comment décrire une TAD ?
6. Comment définir une interface ? Quelles classes Java peut en utiliser une ?
7. De quoi est composée une cellule ?
8. Quelles sont les variables appartenant à la classe ListeChainee ?
9. Qu'est ce que les exceptions ? Comment les traiter en Java ?