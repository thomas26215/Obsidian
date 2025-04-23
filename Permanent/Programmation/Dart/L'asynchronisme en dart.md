# Programmation asynchrone en Flutter avec `Future<type>`, `async`, `await` et `Completer`
## 1. Introduction
En Flutter (et Dart), la programmation asynchrone est essentielle pour effectuer des opérations longues (comme les appels réseau, l’accès à une base de données, ou la lecture de fichiers) sans bloquer l’interface utilisateur. Pour cela, Dart propose des outils puissants : `Future<type>`, les mots-clés `async` et `await`, ainsi que le concept de `Completer`.
## 2. Qu’est-ce qu’un `Future<type>` ?

## Définition
Un `Future<T>` est un objet qui représente une valeur qui sera disponible dans le futur, après la fin d’une opération asynchrone.
- Le type générique `<T>` indique le type de la valeur qui sera retournée (par exemple, `Future<String>`, `Future<int>`, `Future<Map<String, dynamic>>`, etc.).

## États d’un Future
Un `Future` peut être dans deux états principaux :
- **Incomplet** : l’opération n’est pas terminée, la valeur n’est pas encore disponible.
- **Complété** : l’opération est terminée, le `Future` fournit soit :
    - Une valeur (succès)
    - Une erreur/exception (échec)
## Pourquoi préciser le type `<T>` ?

- Garantit la cohérence des données.
- Permet à l’éditeur de détecter les erreurs de type à la compilation.
- Améliore la lisibilité et la maintenabilité du code.
- Utile pour les widgets comme `FutureBuilder` qui attendent un type précis.

## 3. Les mots-clés `async` et `await`

## `async`

- Permet de marquer une fonction comme asynchrone.
- Une fonction `async` retourne toujours un `Future`.
- À l’intérieur, on peut utiliser le mot-clé `await`.

## `await`

- S’utilise uniquement dans une fonction marquée `async`.
- Permet de "mettre en pause" l’exécution de la fonction jusqu’à la fin de l’opération asynchrone.
- Récupère directement la valeur retournée par le `Future`.
    

## 4. Exemples d’utilisation

## Exemple simple avec `Future<String>`, `async` et `await`

```dart
Future<String> fetchData() async {
  await Future.delayed(Duration(seconds: 2)); // Simule une attente
  return "Données reçues après 2 secondes";
}

void main() async {
  print("Début");
  String result = await fetchData();
  print(result); // Affiche "Données reçues après 2 secondes"
  print("Fin");
}
```
## Utilisation avec `then()` et `catchError()`

```dart
fetchData().then((value) {
  print(value);
}).catchError((error) {
  print("Erreur : $error");
});
```

## 5. Utilisation dans Flutter avec `FutureBuilder`

`FutureBuilder` est un widget Flutter qui permet d’afficher dynamiquement des données asynchrones dans l’interface.

```dart
Future<String> fetchData() async {
  await Future.delayed(Duration(seconds: 2));
  return "Données asynchrones";
}

@override
Widget build(BuildContext context) {
  return FutureBuilder<String>(
    future: fetchData(),
    builder: (context, snapshot) {
      if (snapshot.connectionState == ConnectionState.waiting) {
        return CircularProgressIndicator();
      } else if (snapshot.hasError) {
        return Text('Erreur : ${snapshot.error}');
      } else {
        return Text('Résultat : ${snapshot.data}');
      }
    },
  );
}
```

## 6. Utilisation avancée : le `Completer`

Un `Completer` permet de contrôler manuellement la complétion d’un `Future`.  
C’est utile pour intégrer des callbacks ou gérer des scénarios complexes comme les timeouts.

## Exemple


```dart
Future<String> fetchWithCompleter() {
  final completer = Completer<String>();

  // Simule une opération asynchrone
  Future.delayed(Duration(seconds: 2), () {
    completer.complete("Résultat avec Completer");
    // Pour signaler une erreur : completer.completeError("Une erreur");
  });

  return completer.future;
}

```
## 7. Bonnes pratiques

- **Toujours typer explicitement vos `Future`** pour éviter les erreurs et améliorer la lisibilité.
- **Gérer les erreurs** avec `try/catch` ou `catchError`.
- **Ne pas bloquer l’UI** : toutes les opérations longues doivent être asynchrones.
- **Utiliser `FutureBuilder`** pour afficher les résultats asynchrones dans l’interface Flutter.

## 8. Résumé

- Un `Future<T>` représente une valeur qui sera disponible plus tard, après une opération asynchrone.
- Le mot-clé `async` permet d’écrire des fonctions asynchrones, et `await` attend la fin d’un `Future`.
- Préciser le type `<T>` du `Future` est essentiel pour la sécurité et la clarté du code.
- Le `Completer` offre un contrôle avancé sur la complétion des `Future`.
- Ces outils sont indispensables pour écrire des applications Flutter réactives, performantes et maintenables.
