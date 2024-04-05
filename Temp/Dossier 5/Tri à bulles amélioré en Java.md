```Java
private static void triBulles(ArrayList v) {
	int j; // pour faire descendre la bulle
	int i = 0; // v[0..i-1] trié et v[0..i-1] ≤ v[i..v.size()-1)[invariant]
	boolean  onAPermute = true,
	while (onAPermute) {
		j = v.size()-1; // indice du dernier élément départ descente de bulles
		onAPermute = false;
		while (j > i) { // faire descendre la bulle jusqu’à i
		// si le suivant est strictement plus petit que le précédent permuter
			if (v.get(j) < v.get(j-1)) {
				int temporaire = v.get(j);
				v.set(j, v.get(j-1));
				v.set(j-1, temporaire);
				onAPermute = true;
			}
			// reculer j
			j = j - 1; 
		} 
		// v[0..i] trié et v[0..i] ≤ v[i+1..v.size()-1)
		// affichage du vecteur courant but pédagogique
		System.out.println("itération n° " + (i+1) + " : " + v); // avancer i i = i + 1; // v[0..i-1] trié et v[0..i-1] ≤ v[i .. v.size()-1) [invariant]
	}
	// i = v.size()-1
	// v[0..v.size()-2] trié et v[0..v.size()-2] ≤ v[v.size()-1..v.size()-1) => v trié }
}
```

---
**Links :**
[[Tri à bulle]]