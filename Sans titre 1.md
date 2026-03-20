
```dart
void _changerAvis() {
  setState(() {
    _isAvisOui = !_isAvisOui;
  });
}
```


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

## Exercice 3 — `AvisNotifier` avec `StateNotifier`

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

class AvisNotifier extends StateNotifier<bool> {
  
  // Constructeur : initialisation de l'état à true
  AvisNotifier() : super(true);

  // Méthode pour changer l'avis
  void changerAvis() {
    state = !state;
  }
}

// Instanciation du provider
final avisProvider = StateNotifierProvider<AvisNotifier, bool>(
  (ref) => AvisNotifier(),
);
```

---

## Exercice 4 — `Exercice1Page` consommatrice du provider

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

class Exercice1Page extends ConsumerWidget {
  const Exercice1Page({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    
    // On s'abonne à l'état booléen du provider
    final bool isAvisOui = ref.watch(avisProvider);

    return Scaffold(
      body: Center(
        child: Center(
          child: Text(isAvisOui ? 'OUI' : 'NON'),
        ),
      ),
      floatingActionButton: ChangerAvisButton(
        () => ref.watch(avisProvider.notifier).changerAvis(),
      ),
    );
  }
}
```

---

## `main.dart` — Point d'entrée

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

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
    return const MaterialApp(
      home: Exercice1Page(),
    );
  }
}
```

---

## Résumé final

|Exercice|Classe|Rôle|
|---|---|---|
|Ex. 1|`_Exercice1PageState`|`setState()` pour état local|
|Ex. 2|`ChangerAvisButton`|`StatelessWidget` + `VoidCallback`|
|Ex. 3|`AvisNotifier`|`StateNotifier<bool>` + `StateNotifierProvider`|
|Ex. 4|`Exercice1Page`|`ConsumerWidget` + `ref.watch()`|

### Les 3 règles du cours à retenir :

- **`StateNotifier<T>`** → gère l'état, initialisation dans `super()`
- **`StateNotifierProvider`** → expose le notifier aux widgets
- **`ConsumerWidget`** → widget qui consomme un provider via `ref`