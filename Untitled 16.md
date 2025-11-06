```python
fonction estTas(H(1..n))
	pour i  de 1 à n/2 faire
		gauche=2*i
		droit=2*i+1
		si gauche <= n et H[i] < H[gauche] alors
			retourner FAUX
		fin si
		
		si droit  <= n et H[i] < H[droit] alors
			retourner FAUX
		fin si
	fin pour
	retourner VRAI
fin fonction
```

```python
fonction supprimerPetitTas(H[1..n]) :
    // Étape 1 : rechercher le plus petit parmi les feuilles
    indice_petit ← ⌊n/2⌋ + 1
    valeur_petit ← H[indice_petit]

    pour i de ⌊n/2⌋ + 2 à n faire
        si H[i] < valeur_petit alors
            valeur_petit ← H[i]
            indice_petit ← i
        fin si
    fin pour

    // Étape 2 : suppression de cet élément
    H[indice_petit] ← H[n]
    n ← n - 1

    // Étape 3 : rétablir la propriété du tas
    // On "remonte" si l'élément est plus grand que son parent
    i ← indice_petit
    tant que i > 1 et H[i] > H[⌊i/2⌋] faire
        échanger(H[i], H[⌊i/2⌋])
        i ← ⌊i/2⌋
    fin tant que

    retourner n     // nouvelle taille du tas
fin fonction
```