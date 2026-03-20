# Correction Complète — Contrôle Flutter R6.05 (Riverpod)

---

## Exercice 1 — `_changerAvis()` (StatefulWidget, inchangé)

```dart
void _changerAvis() {
  setState(() {
    _isAvisOui = !_isAvisOui;
  });
}
```

> L'exercice 1 reste avec `StatefulWidget`, pas de Riverpod ici.

---

## Exercice 2 — Classe `ChangerAvisButton`

```dart
class ChangerAvisButton extends StatelessWidget {
  final VoidCallback _changerAvis;

  const ChangerAvisButton(this._changerAvis, {Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return FloatingActionButton(
      onPressed: _changerAvis,
      child: const Text("Changer d'Avis"),
    );
  }
}
```

---

## Exercice 3 — `AvisNotifier` avec Riverpod

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

// La classe AvisNotifier
class AvisNotifier extends Notifier<bool> {
  
  // Constructeur : initialisation de l'état
  @override
  bool build() {
    return true;
  }

  // Méthode pour changer l'avis
  void changerAvis() {
    state = !state;
  }
}

// Instanciation du provider
final avisProvider = NotifierProvider<AvisNotifier, bool>(
  () => AvisNotifier(),
);
```

---

## Exercice 4 — `Exercice1Page` consommatrice du provider

```dart
class Exercice1Page extends ConsumerWidget {
  const Exercice1Page({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // On écoute l'état du provider
    final isAvisOui = ref.watch(avisProvider);

    return Scaffold(
      body: Center(
        child: Center(
          child: Text(isAvisOui ? 'OUI' : 'NON'),
        ),
      ),
      floatingActionButton: ChangerAvisButton(
        () => ref.read(avisProvider.notifier).changerAvis(),
      ),
    );
  }
}
```

---

## Point d'entrée — `main.dart`

```dart
void main() {
  runApp(
    const ProviderScope( // obligatoire avec Riverpod
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: const Exercice1Page(),
    );
  }
}
```

---

## Résumé Riverpod

|Exercice|Élément|Riverpod|
|---|---|---|
|Ex. 1|État local|`setState()`|
|Ex. 2|Widget réutilisable|`StatelessWidget` + `VoidCallback`|
|Ex. 3|État global|`Notifier<bool>` + `NotifierProvider`|
|Ex. 4|Consommer le provider|`ConsumerWidget` + `ref.watch()`|

### Les 3 règles Riverpod à retenir :

- **`ref.watch()`** → lit l'état et **reconstruit** le widget si ça change
- **`ref.read()`** → lit l'état **sans** reconstruire (pour les actions)
- **`ProviderScope`** → obligatoire à la racine de l'app