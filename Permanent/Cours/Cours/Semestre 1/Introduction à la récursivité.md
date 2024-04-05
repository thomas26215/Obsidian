---
MOOC: "[[Cours]]"
Ressource: "R1.01 : Initiation au développement"
Cours: "Cours 8 : Introduction à la récursivité"
Date: 2023-11-21
tags: 
Complete: false
Learned: false
---
La récursivité est le fait qu'une fonction s'appelle elle-même. Il est nécessaire d'une condition d'arrêt pour que la fonction ne s'appelle pas indéfiniment. Il faut également être sûr que la condition d'arrêt sera atteinte.

**Recherche dichotomique par récursivité :**
```Java
private static int principale(ArrayList<Integer> v, int valeur){
	return worker(v, valeur, 0, v.size()-1)
}
private static int worker(ArrayList<Integer> v, int valeur, int min, int max){
	if(min == max){min==max?min:-min}
	else{
		m = (min+max)/2
		if(valeur <= v.get(m)){return worker(v, valeur, min, m);}else{return worker(v, valeur, m+1, max);}
	}
}
```

**Recherche dichotomique par itérations**

**Tri fusion :**
```Java
public static void triFusion(ArrayList<Integer> vInt, int inf, int sup){
	if(inf < sup){
		int m = (inf+sup)/2
		triFusion(vInt, inf, m);
		triFusion(vInt, m+1, sup);
		fusionTabG_TabD(vInt, inf, m, sup);
	}
}
public static void fusionTabG_TabD(ArrayList<Integer> vInt, int inf, int m, int sup){
	ArrayList<Integer> temp = new ArrayList<>();

	int i = inf;
	int j = m;

	while(i <= m && j <= sup){
		if(vInt.get(i) < vInt.get(j)){
			temp.add(vInt.get(i));
			i++;
		}else{
			temp.add(vInt.get(j));
			j++;
		}
	}

	while(i <= m){
		temp.add(vInt.get(i));
		i++;
	}
	while(j <= sup){
		temp.add(vInt.get(j));
		j++;
	}

	for(int k = 0; k <= vTemp.size(); k++){
		vInt.set(inf+k, vTemp.get(k));
	}

}
```

La première fonction va diviser successivement la liste en deux parties, jusqu'à ce qu'il ne reste plus qu'un seul élément par liste. La deuxième fonction sera appelée afin de rassembler la liste. Il n'y aura certes rien à faire pour les éléments seuls, mais il faudra rassembler les listes d'éléments seuls en listes de deux éléments triés, puis ces dernières en listes de quatre éléments triées ..
La deuxième fonction s'occupe donc de ca. Dans la première partie, elle va s'occuper de retrier les éléments, dans la deuxième elle va ajouter pour les éléments de la liste qui n'ont pas été triées et finalement, elle va remplacer la partie de liste originale par la liste triée