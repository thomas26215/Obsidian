## 1 - Couleurs et thèmes
En flutter, il est possible de personnaliser l'apparence globale de l'application via `ThemeData`. Cela permet de définir des couleurs, des polices, des formes, des ombres, etc. qui seront utilisées par les widgets de l'application.

Voici les différentes propriétés de `ThemeData` :
- `primaryColor` : Couleur principale de l'application
- `accentColor` : Couleur d'accentuation
- `scaffoldBackgroundColor` : Couleur de fond par défaut des écrans
- `textTheme` : Styles de texte pour les différents éléments de l'interface
- `buttonTheme` : Styles des boutons
- `inputDecorationTheme` : Styles des champs de saisie
- `iconTheme` : Styles des icônes
- `textTheme` : Styles de texte
- `textTheme.headline1` à `headline6` : Styles de texte pour les différents niveaux de titre
- `textTheme.bodyText1` et `bodyText2` : Styles de texte pour le corps du texte
- `textTheme.caption` : Style de texte pour les légendes
- `textTheme.button` : Style de texte pour les boutons
- `textTheme.overline` : Style de texte pour les surtitres
- `textTheme.subtitle1` et `subtitle2` : Styles de texte pour les sous-titres

Voici un exemple d'utilisation de `ThemeData` dans une application Flutter :

```dart
MaterialApp(
    theme: ThemeData(
        primaryColor: Colors.blue,
        accentColor: Colors.red,
        scaffoldBackgroundColor: Colors.white,
        textTheme: TextTheme(
            headline1: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            headline6: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            bodyText1: TextStyle(fontSize: 16),
            bodyText2: TextStyle(fontSize: 14),
            caption: TextStyle(fontSize: 12),
            button: TextStyle(fontSize: 16),
            overline: TextStyle(fontSize: 10),
            subtitle1: TextStyle(fontSize: 18),
            subtitle2: TextStyle(fontSize: 16),
        ),
    ),
)
```
