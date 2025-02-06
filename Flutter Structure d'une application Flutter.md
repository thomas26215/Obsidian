Une application Flutter a une structure bien définir avec plusieurs fichiers et répertoires :
- **lib/** : Contient le code source de l'application
- **assets** : Contient les ressources de l'application (images, polices, ...)
- **pubspec.yaml** : Fichier de configuration de l'application

Le fichier `main.dart` est le point d'entrée de l'application. Il contient le code pour lancer l'application et définir le widget racine.

```dart
import 'package:flutter/material.dart';

void main() {
    runApp(MyApp());
}

class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            home: HomePage(),
        );
    }
}
```
