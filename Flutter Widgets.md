Les widgets sont les éléments de base pour toutes interface utilisateurs Flutter. Ils sont utilisés l'interface de l'application

## 1. Widget de structure
### 1.1 Scaffold
Le widget `Scaffold` fournit une structure de base pour l'écran de l'utilisateur. Il est utilisé comme widget racine pour la plupart des écrans

**Contenu possible** :
- `appBar` : Un widget AppBar pour la barre supérieure
- `body` : Le contenu principal de l'écran (tout widget)
- `floatingActionButton` : Un bouton d'action flottant
- `drawer` : Un menu latéral (généralement un Drawer)
- `bottomNavigationBar` : Une barre de navigation inférieure
- `persistentFooterButtons` : Des boutons persistants en bas
- `bottomSheet` : Un widget pour afficher du contenu en bas
- `backgroundColor` : Couleur de fond de l'écran

***Exemple*** :
```dart
Scaffold {
	appBar: AppBar(title: text("Mon App")),
	body: Center(child: Text("Contenu principale")),
	floatingActionButton: FloatingActionButton(
		onPressed: () {},
		child: Icon(Icons.add);
	)
}
```


### 1.2 AppBar
Le widget `AppBar` ajoute une barre supérieur à l'application. Elle peut afficher le titre de la page et les actions

**Contenu possible** :
- `leading` : Widget avant le titre (souvent une icône)
- `title` : Titre de la page
- `actions` : Liste de widgets pour les actions
- `flexibleSpace` : Espace flexible pour effets de défilement
- `bottom` : Widget en bas de l'AppBar (souvent TabBar)

***Exemple*** :
```dart
AppBar(
	title: Text("Accueil"),
	actions: [
		IconButton(icon: Icon(Icons.search), onPressed: () {}),
		IconButton(icon: Icon(Icons.settings), onPressed: () {}),
	],
)
```

## 3. Widget de mise en page
### 3.1 Column et row
le widget `Row` d'organiser les widgets horizontalement et le widget `Column` permet d'organiser les widgets verticalement. C'est assez utile pour créer des widgets flexibles

**Contenu possible** :
- `children` : Liste de widgets enfants
- `mainAxisAlignment` : Alignement sur l'axe principal
- `crossAxisAlignment` : Alignement sur l'axe transversal

***Exemple*** :
```dart
Column {
	mainAxisAlignment: MainAxisAlignment.spaceEvenly,
	children: [
		Text("haut"),
		Text("milieu"),
		Text("bas"),
	],
}
```

### 3.2 ListView
Le widget `ListView` créer une liste scrollabe de widgets pour afficher une collection d'éléments défilables

**Contenu possible** :
- `children` : Liste fixe de widgets
- `itemBuilder` : Fonction pour construire des éléments dynamiquement
- `itemCount` : Nombre d'éléments pour la construction dynamique
- `scrollDirection` : Direction de défilement

***Exemple*** :
```dart
ListView.builder {
	ItemCount: 100,
	ItemBuild: (context, index) {
		return ListTile(title: Text("Item $index"));
	}
}
```

***Exemple en récupérant les éléments d'une BDD*** :
```dart
import "package:flutter/material.dart";
import "package:sqflite/sqflite.dart";

class HorizontalListView extends StatefulWidget {
	@override
	_HorizontalListViewState createState() => _HorizontalListViewState();
}

_HozirontaleListViewState extends State<HorizontalLstView> {
	List<Map<String, dynamic>> _items = [];

	@override
	void initState() {
		super.initState();
		_loadItems();
	}

	Future<void> _loadItems() async {
		Database db = await openDatabase("database.db");
		List<Map<String, dynamic>> results = await db.query("table");
		setState(() {
			_items = results;
		});
	}

	@override
	Widget build(BuildContext context) {
		return Container(
			height: 100,
			child: ListView.builder(
				scrollDirection: Axis.horizontal,
				itemCount: _item.length,
				itemBuidler: (context, index) {
					final item = _items[index];
					return Container ()
						width: 100,
						margin: EdgeInsets.symmetric(horizontal: 5),
						color: item['id'] > 5 ? Colors.red : Colors.black,
						child: Center(
							child: Text(
								item["name"],
								style: TextStyle(color: Colors.white),
							),
						),
					);
				},
			),
		);
	}
}
```