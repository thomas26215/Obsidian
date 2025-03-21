Ce cours couvre l'utilisation de SQLite dans une application flutter. On va se concentrer ici sur la création d'une structure d'une BDD, la gestion des tables et les opérations CRUD

Il faut savoir que SQLite est une BDD légère, rapide et autonome et parfaitement adaptée aux applications Flutter. Nous utilisons en Flutter le package `sqflite` pour l'interaction avec SQLite

---

La classe `DabaseHelper` gère la connexion à la base de données SQLite et fournit des méthodes CRUD génériques, tandis que les modèles de données (comme User) intègrent ces opérations en implémentant des méthodes `toMap()` et `fromMap()` pour faciliter la conversion entre les objets Dart et les enregistrements de la base de données

# Mise en place du modèle
Tout d'abord, il faut créer une classe pour l'objet que l'on souhaite manipuler
>[!Example]
>```dart
>class Profil {
>	final int? id;
>	final int userId
>	...
>	
>	Profil({this.id, required this.nom, ...})
>}

Et nous allons y implémenter des méthodes de base :
- Une méthode `toMap()` qui va nous retourner un objet sous la forme `{nomAttribut : variable}`
- Une méthode `fromMap()` créant un objet à partir d'une map

>[!Example]
>```dart
>Map<String, dynamic> toMap() {
>	return {
>		'id': id,
>		'user_id': userId,
>		'nom': nom,
>		...
>	}
>}
>
>factory Profil.fromMap(Map<String, dynamic> map) {
>	return Profil(
>		id: map['id'],
>		userId: map['usr_id],
>		nom: map['nom'],
>		...
>	)
>}
>```

Ces deux méthodes son essentielles pour les conversions entre les objets Dart et les enregistrements de la BDD. Elles permettent de :
- Faciliter l'insertion et la màj des données dans la BDD en convertissant l'objet en un format compatible avec SQLite
- Simplifier la création d'objets à partir des résultats de requêtes de la BDD

# Méthodes sur la BDD
## Mise en place du Singleton
La mise en place du Singleton pour `DatabaseHelper` est une technique cruciale pour assurer une gestion efficace et cohérente de la base de données dans une application Flutter. Cette approche garantit qu'une seule instance de `DatabaseHelper` est créée et utilisée tout au long de l'exécution de l'application.
Pour implémenter ce pattern, nous utilisons trois éléments clés :
1. Une variable statique `instance` qui contient l'unique instance de `DatabaseHelper`.
2. Un constructeur privé `_init()` qui empêche la création directe d'instances de la classe.
3. Un constructeur factory qui retourne toujours l'instance unique.

>[!Important] Mise en place
>```dart
>class DatabaseHelper {
>	static final DatabaseHelper instance = DatabaseHelper.init();
>	DatabaseHelper._init();
>	factory DatabaseHelper() {
>	}
>}
>```

## Liaison avec SQLite
La liaison avec SQLite dans le contexte du Singleton `DatabaseHelper` est un concept fondamental pour une gestion efficace de la base de données dans une application Flutter.

Le Singleton assure qu'une seule instance de `DatabaseHelper` existe, ce qui signifie qu'une seule connexion à la base de données SQLite est maintenue tout au long de l'exécution de l'application. Cette approche présente plusieurs avantages importants.

Premièrement, elle garantit la cohérence des opérations sur la base de données. Toutes les parties de l'application interagissent avec la même instance de `DatabaseHelper`, évitant ainsi les conflits potentiels qui pourraient survenir avec des connexions multiples.

Deuxièmement, cette méthode optimise l'utilisation des ressources. La connexion à la base de données n'est établie qu'une seule fois, puis réutilisée, ce qui est plus efficace que d'ouvrir et fermer constamment de nouvelles connexions.

Enfin, l'utilisation d'un Singleton simplifie considérablement la gestion de la base de données dans l'ensemble de l'application. Les développeurs peuvent facilement accéder aux fonctionnalités de la base de données à partir de n'importe quel point de l'application, sans se soucier de la gestion de multiples instances ou connexions.

En résumé, le pattern Singleton pour `DatabaseHelper` offre une solution élégante et efficace pour gérer les interactions avec SQLite, assurant performance, cohérence et facilité d'utilisation dans le développement d'applications Flutter.

```dart
static Database? _database;
Future<Database> get database async {
	if (_database != null) return _database!;
	_database = await _initDB('database.db');
	return _database!;
}
```

Il est important de noter que cette implémentation utilise la classe `Database` fournie par le package sqflite. Cette classe offre de nombreuses méthodes pour interagir avec la base de données SQLite, telles que `execute()` pour exécuter des requêtes SQL, `insert()` pour ajouter des données, `query()` pour récupérer des informations, `update()` pour modifier des enregistrements existants, et `delete()` pour supprimer des données[](https://dev.to/arslanyousaf12/sqlite-in-flutter-the-complete-guide-11nj). Ces méthodes permettent aux développeurs de réaliser toutes les opérations CRUD (Create, Read, Update, Delete) nécessaires pour une gestion complète de la base de données dans leur application Flutter.

Il faut savoir que dans la majorité des méthodes du modèle, on passe la `DatabaseHelper` sur laquelle on va pouvoir effectuer les méthodes  de `Database`.
> [!Example]
> ```dart
> 



