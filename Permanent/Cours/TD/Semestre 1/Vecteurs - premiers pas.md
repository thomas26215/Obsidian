---
MOOC: "[[Cours]]"
Ressource: "R1.01 : Initiation au développement"
Cours: "TD 5 : Vecteurs - Premiers pas"
Date: 2023-10-09
tags:
---
# Exercice 2
a)
```Java
public static int minimum(ArrayList<Integer> vectEnt){
	int min = vectEnt.get(0);
	for(int i = 1; i < vectEnt.size(); i++){
		if(vectEnt.get(i) < min){
			min = vectEnt.get(i)
		}
	}
	return min;
}
```

b)
```Java
public static int nbInfVal(ArrayList<Integer> vectEnt, int val){
	int nbInf = 0;
	for(int i = 0; i < vectEnt.size(); i++){
		if(vectEnt.get(i) < val){nbInf += 1}
	}return nbInf;
}
```

c)
```Java
public static int indicePremVal(ArrayList<Integer> vectEnt, int val){
	for(int i = 0; i < vectEnt.size(); i++){
		if(vectEnt.get(i) == val){return i}
	}return -1
}
```

# Exercice 3
## a
```Java
public static int nbPointsAbsSupVal(ArrayList<Point> vectPoint, int valeur){
	int nbValeursSup = 0;
	for(int i = 0; i < vectPoint.size()){
		if(vectPoint.get(i).getX() > valeur){
			nbValeursSup += 1;
		}
		return nbValeursSup;
	}
}
```

# b
```Java
public static ArrayList<Point> sym0deVectPoint(ArrayList<Point> vectPoint){
	ArrayList<Point> finale = new ArrayList<>();
		for(int i = 0; i < vectPoint.size(); i++){
		int x = vectPoint.get(i).getX();
		int y = vectPoint.get(i).getY();

		//Créer un point symétrique en inversant les coordonnées
		Point actual_point = new Point(-x, -y);
		finale.add(actual_point);
		
	}
	return finale;
}
```

# c
```Java
public static void repartQuartier(ArrayList<Point> vectPoint){
	int haut_gauche = 0;
	int haut_droit = 0;
	int bas_gauche = 0;
		int bas_droit = 0;
	for(int i = 0; i < vectPoint.size(); i++){
		int x = vectPoint.get(i).getX();
		int y = vectPoint.get(i).getY();
		if(x < 0 && y < 0){
			bas_gauche++;
		}else if(x > 0 && y < 0){
			bas_droit++;
		}else if(x < 0 && y > 0){
			haut_gauche++;
		}else if(x > 0 && y > 0){
			haut_droit++;
		}
	}
	System.out.println("Repartition des points du vecteur par quartier du plan :");
	System.out.println("Nombre de points situés au-dessus de l'axe horizontal :");
	System.out.println("Quartier Haut Gauche : " + haut_gauche);
	System.out.println("Quartier Haut Droit : " + haut_droit);
	System.out.println("Quartier Bas Gauche : " + bas_gauche);
	System.out.println("Quartier Bas Droit : " + bas_droit);
}
```