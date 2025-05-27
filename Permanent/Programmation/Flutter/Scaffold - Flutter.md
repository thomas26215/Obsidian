Le **Scaffold** est un widget fondamental en Flutter.. Il est utilisé pour construire la base d'une interface utilisateur. Il fournit une structure de mise en page standard qui inclut des éléments tels que :
- **AppBar** : une barre d'application en haut de l'écran.
- **Drawer** : un menu latéral qui peut être ouvert pour naviguer dans l'application.
- **BottomNavigationBar** : une barre de navigation en bas de l'écran.
- **FloatingActionButton** : un bouton d'action flottant pour des actions principales.
- **Body** : la zone principale de contenu de l'écran.
- **SnackBar** : pour afficher des messages temporaires en bas de l'écran.
- **BottomSheet** : pour afficher des contenus supplémentaires en bas de l'écran.

Le `Scaffold` sert de conteneur principal et facilite l'intégration de ces éléments sans avoir à les gérer séparément
```dart
Scaffold(
	appBar: AppBar(
		title: Text('Titre de l\'AppBar'),
	),
	body: Center(
		child: Text('Contenu principal de l\'écran'),
	),
	floatingActionButton: FloatingActionButton(
		onPressed: () {
			// Action à effectuer lorsque le bouton est pressé
		},
		child: Icon(Icons.add),
	),
)