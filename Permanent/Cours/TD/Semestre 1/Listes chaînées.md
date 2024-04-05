---
MOOC: "[[Cours]]"
Ressource: "R1.01 : Initiation au développement"
Cours: "TD 9 : listes chaînées"
Date: 2023-12-05
tags: 
Complete: false
Learned: false
---
## Exercice 1
## a
```Java
public void insereTete(TypeInfo uneInfo) {
	this.tete = insereTeteWorker(this.tete, uneInfo); 
} 
private Cellule<TypeInfo> insereTeteWorker(Cellule<TypeInfo> cellCour, TypeInfo uneInfo){
	cellule<TypeInfo> nouvelleCell = new Cellule(uneInfo, cellCour);
	nbCellules++;
	return nouvelleCell;
}

public void insereTeteIt(TypeInfo uneInfo){
	Cellule<TypeInfo> nouvelleTete = new Cellule(uneInfo, this.tete);
	this.tete = nouvelleTete;
	nbCellules ++;
}
```

```Java
@Override
public void supprimeTete(){
	this.tete = supprimeteteWorker(this.tet, uneInfo);
}
private Cellule<TypeInfo> supprimeTeteWorker(Cellule<TypeInfo> cellCour){
	nbCellules--;
	return cellCour.getCelluleSuivante();
}
```

```Java
@Override
public boolean insereAtPosit(int position){
	if(nbCellule >= position && position >= 1){
		this.tete = insertAtPosWorker(tete, position, uneInfo)
	}else{
		return false;
	}
}
private Cellule<TypeInfo> insereAtPositWorker(Cellule<TypeInfo>cellCour, int position){
	if(position == 1){
		Cellule<TypeInfo> newC = insertTeteWorker(cellCour, uneInfo);
		return newC;
	}else{
		Cellule<TypeInfo> cellNew = insertAtPosit(CellCour.getCelluleSuivante, position-1, uneInfo);
	}
	return cellNew
}
```