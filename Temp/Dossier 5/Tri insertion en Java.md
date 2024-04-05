```Java
private static void triSelection(ArrayList v) 
{
	int i = 0; // v[0..i-1] trié et v[0..i-1] ≤ v[i..v.size()-1) [invariant] 
	while (i < v.size()-1) { // traiter jusqu’à l’avant dernier
	// trouver l'indice du plus petit dans v[i..v.size()-1]
		int indMin = i; // initialisation de indMin au premier de la zone à traiter 
		int j = i + 1; // commencer la recherche au suivant 
		while (j < v.size()) { // chercher jusqu’au dernier indice 
			if (v.get(j) < v.get(indMin)) {
					indMin = j;
				}
				j = j + 1;
			} // si indMin != i permuter 
			if (indMin != i) {
				int temporaire = v.get(i);
				v.set(i, v.get(indMin));
				v.set(indMin, temporaire);
			} // v[0..i] trié et v[0..i] ≤ v[i+1..v.size()-1) // affichage du vecteur courant but pédagogique
			System.out.println("itération n° " + (i + 1) + " : " + v);
			i = i + 1; 1// avancer // v[0..i-1] trié et v[0..i-1] ≤ v[i .. v.size()-1) [invariant]
		}
		// i = v.size()-1
		// v[
```

---
**Links :**
[[Tri par insertion]]