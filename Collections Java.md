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

⇒ Définit une structure de données qui stocke des valeurs de paires clé-valeur. C'est un implémentation de l'interface `Map`

Voici les différentes fonctions :
- `map.put(clé, valeur);`
- `map.get(clé);` ⇒ Renvoie la valeur de la clé
- `map.remove(clé)` ⇒ Supprime la clé avec la paire
- `map.containsKey(cle)` ⇒ Vérification de la présence d'une clé
- `map.containsValue(value)` ⇒ Vérification de la présence d'une valeur

Il est possible de parcourir la HashMap :

```java
/*
 * Solution 1 : par les clés
 */
for (String key : map.keySet()) {
	System.out.println("Key: " + key + ", Value: " + map.get(key));
}
/*
 * Solution 2 : par les valeurs
 */
for (Integer value : map.values()) {
    System.out.println("Value: " + value);
}
/*
 * Solution 3 : Par les entrées (clé-valeur)
 */
for (Map.Entry<String, Integer> entry : map.entrySet()) {
	System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
}
```


D'autres méthodes courantes :
- `.size();` ⇒ Récupérer la taille du `HashMap`
- `.isEmpty();` ⇒ Vérifie si champs vide
- `.clear();` ⇒ Supprime toutes les entrées
- `.putAll(Map<? extends K, ? extends V> m);`


# TreeSet
Un TreeSet est une structure de données permettant de stocker des éléments uniques dans un ordre trié.

## Création d'un TreeSet
Pour créer un TreeSet, on peut utiliser le constructeur par défaut ou bien spécifier un comparateur pour un ordre personnalisé :
```Java
public class Main {
	public static void main(String[] args) {
	// Création d'un TreeSet avec ordre naturel
	TreeSet<String> set = new TreeSet<>();
	// Avec un comparateur personnalisé
	TreeSet<String> setWithComparator = new TreeSet<>((s1, s2) -> s2.compareTo(s1)); // Ordre décroissant
	}
}
```

Pour redéfinir l'ordre naturel, il faut utiliser l'[[Interface Comparable]] et si l'on souhaite définir un ordre différent de l'ordre naturel, utiliser l'[[L'interface Comparator]]

Voici les différentes méthodes  :
- `add` ⇒ Ajouter un élément
- `remove` ⇒ Supprimer un élément


Parcourir les éléments du TreeSet
```java
public class Main {
	public static void main(String[] args)
		{ TreeSet<String> set = new TreeSet<>();
		set.add("apple");
		set.add("banana");
		set.add("cherry"); // Parcours avec une boucle for-each
		for (String fruit : set){
			System.out.println("Fruit: " + fruit);
		} // Parcours avec un itérateur
		Iterator<String> iterator = set.iterator();
		while (iterator.hasNext()){
			System.out.println("Fruit: " + iterator.next());
		}
	}
}
```