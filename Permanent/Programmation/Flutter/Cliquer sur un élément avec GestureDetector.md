Le `GestureDetector` est un Widget qui détecte les gestes de l'utilisateur. On peut y retrouver plusieurs actions :
- `onTap` : Déclenché lors d'un tap.
- `onDoubleTap` : Déclenché lors d'un double tap.
- `onLongPress` : Déclenché lors d'une pression longue.
- `onVerticalDragStart` : Déclenché au début d'un glissement vertical.
- `onHorizontalDragStart` : Déclenché au début d'un glissement horizontal.
- `onPanUpdate` : Déclenché lors du déplacement du doigt sur l'écran.

Voici un exemple de code pour utiliser le `GestureDetector` :
```dart
GestureDetector(
    onTap: () => print("Tap!");
    child: Icon(Icons.arrow_back),
)


---

[[Navigator]]
