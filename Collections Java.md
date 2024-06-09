- `ArrayList`
- `TreeSet`
- `TreeMap`
- `HashSet`
- `HashMap`


# Itérateur
**Définir un itérateur :** `Iterator<Classe> it = Collection.iterator();`
⇒ **Définit un itérateur sur la Collection `Collection`**

## Accéder au prochain élément
`int p1 = it.next();`
Cela permet de récupérer le prochain élément de l'itérateur
⇒ Retourne l'élément de la classe de l'itérateur (`Iterator<Integer> it = liste.iterator()` renvoie un INT pour la méthode `next();`)

*Exemple :*
```Java
ArrayList<Integer> liste = new ArratList<>(new Arrays.asList(1,2,3,4,5));
Iterator<Integer> it = liste.iterator();
for(int i = 0; i < 3; i++){
	int j = it.next() //Récupérer le prochain
	System.out.println(j); //Afficher l'élément récupéré
}
```
```sortie
1
2
3
```

## Vérifier si présence du prochain élément
`it.hasNext();` ⇒ Renvoie un booléen
⇒ Renvoie `true` Si il y a un prochain élément, `false` sinon.

*Afficher tous les éléments d'un itérateur :*
```Java
TreeSet<Integer> liste = new TreeSet<>(Arrays.asList(1,2,3,4,5));
Iterator<Integer> it = liste.iterator();
while(it.hasNext()){ //Vérifier s'il y a bien un élément suivant
	it.next();       //Passer à l'élément suivant
	System.out.println(it);
}
```

## Supprimer un élément
`it.remove();`
⇒ Permet de retirer de la collection le dernier élément lu
Ne pas mettre deux foit de suite `it.remove();` Car bug

*Exemple :*
```Java
TreeSet<Integer> liste = new TreeSet<>(Arrays.asList(1,2,3,4,5));
Iterator<Integer> it = liste.iterator();
it.next();
it.remove();
```

# HashMap
```Java
HashMap<Integer, String> map = new HashMap<>();
HashMap<Integer, String> mapWithCapacity = new HashMap<>(50);
```

⇒ Définit une structure de données qui stocke des valeurs de paires clé-valeur

Voici les différentes fonctions :
- `map.put(clé, valeur);`
- `map.get(clé);` ⇒ Renvoie la valeur de la clé
- `map.remove(clé)` ⇒ Supprime la clé avec la paire