```Java
public static int nbCartesDeEns(ArrayList<Cartes> vCartes, String uneEnseigne){
	return nbCartesDeEnsWork(vCartes, uneEnseigne, 0);
}
public statuc int nbCartesDeEnsWork(ArrayList<Cartes> vCartes, String uneEnseigne, int indice){
	if(indice == vCartes.size()){
		return 0;
	}else if(vCartes.get(indice) == uneEnseigne){
		return 1 + nbCartesDeEnsWork(nbCartesDeEnsWork(vCartes, uneEnseigne, indice + 1)
	}else if(vCartes.get(indice) != uneEnseigne){
		return 0 + nbCartesDeEnsWork(nbCartesDeEnsWork(vCartes, uneEnseigne, indice + 1)
	}
}
```

```Java
public static int rechCarteDichoRec(ArrayList<Cartes> vCartes, Carte uneCarte){
	return rechDichoRecWorker(vCartes, uneCarte, 0, vCartes.size()-1);
}
public static int rechDichoRecWorker(ArrayList<Cartes> vCartes, Carte uneCarte, int inf, int sup){
	if(min == sup){
		if(v.get(inf).compareTo(uneCarte) == 0){return inf;}
		else{return -1;}
	}else{
		int m = (int+sup)/2;
		if(v.get(m).compareTo(uneCarte) >= 0){return rechDichoRecWorker(vCartes, uneCarte, inf, m);}
		else{return rechDichoRecWorker(vCartes, uneCarte, m+1, sup);}
	}
	
}
```