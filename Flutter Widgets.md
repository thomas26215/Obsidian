Les widgets sont les éléments de base pour toutes interface utilisateurs Flutter. Ils sont utilisés l'interface de l'application


## Les principaux types de widgets
### StatelessWidgets
Les widgets `StatelessWidget` sont des widgets immuables qui ne peuvent pas être modifiés après leur création. Ils sont utilisés pour afficher des données statiques.
Le `StatelessWidget`est un widget qui ne peut être reconstruit que lorsqu'il est inséré ou retiré de l'arbre des widgets.

**Exemple** :
```dart
class MyWidget extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return Text("Bonjour");
    }
}
```

### StatefulWidgets
Les widgets `StatefulWidget` sont des widgets mutables qui peuvent être modifiés après leur création. Ils sont utilisés pour afficher des données dynamiques.
Voici le **cycle de vie** d'un `StatefulWidget` :
- `createState` : Crée l'état du widget
- `initState` : Initialise l'état du widget
- **build** : Construit le widget
- setState : Met à jour l'état du widget
- `dispose` : Nettoie l'état du widget

**Exemple** :
```dart
class MyWidget extends StatefulWidget {
    @override
    _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
    int _counter = 0;

    void _incrementCounter() {
        setState(() {
            _counter++;
        });
    }

    @override
    Widget build(BuildContext context) {
        return Column(
            children: [
                Text("Nombre de clics : $_counter"),
                ElevatedButton(
                    onPressed: _incrementCounter,
                    child: Text("Cliquez-moi"),
                ),
            ],
        );
    }
}
```


### StatefulWidgets

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

### 3.3 Container
Le widget `Container` est un widget de mise en page qui peut contenir un seul enfant. Il peut être utilisé pour appliquer des décorations, des marges, des rembourrages, etc.

Contenu possible :
- `child` : Widget enfant
- `child` : Widget enfant
- `color` : Couleur de fond
- `itemBuilder` : Fonction pour construire des éléments dynamiquement
- `itemCount` : Nombre d'éléments pour la construction dynamique


## 4. Widget d'affichage
### 4.1 Text

Le widget `Text` affiche du texte à l'écran. Il peut être personnalisé avec des styles

**Contenu possible** :
- `data` : Texte à afficher
- `style` : Style du texte
- `textAlign` : Alignement du texte
- `maxLines` : Nombre maximum de lignes
- `overflow` : Gestion du débordement de texte

***Exemple*** :
```dart
Text(
    "Bonjour",
    style: TextStyle(
        fontSize: 20,
        color: Colors.blue,
        fontWeight: FontWeight.bold,
    ),
)
```

### 4.2 Image

Le widget `Image` affiche une image à l'écran. Il peut être chargé à partir d'une URL, d'un fichier local ou d'une ressource

**Contenu possible** :
- `image` : ImageProvider (AssetImage, NetworkImage, FileImage)
- `width` : Largeur de l'image
- `height` : Hauteur de l'image
- `fit` : Mode de redimensionnement (cover, contain, fill)
- `alignment` : Alignement de l'image

***Exemple*** :
```dart
Image(
    image: AssetImage("assets/image.jpg"),
    width: 100,
    height: 100,
    fit: BoxFit.cover,
)
```

## 5. Widget d'interaction
### 5.1 Button (ElevatedButton, TextButton, OutlinedButton, OutlineButton)

Les widgets `ElevatedButton`, `TextButton` et `OutlinedButton` sont des boutons interactifs qui peuvent être personnalisés avec des styles

**Contenu possible** :
- `onPressed` : Fonction appelée lors du clic
- `child` : Widget enfant (Text, Icon)
- `style` : Style du bouton (couleur, bordure, ombre)

***Exemple*** :
```dart
ElevatedButton(
    onPressed: () {},
    child: Text("Cliquez-moi"),
    style: ButtonStyle(
        backgroundColor: MaterialStateProperty.all(Colors.blue),
        padding: MaterialStateProperty.all(EdgeInsets.all(10)),
    ),
)
```

### 5.2 GestureDetector

Le widget `GestureDetector` permet de détecter les gestes de l'utilisateur, comme les clics, les appuis longs, les balayages, etc.

**Contenu possible** :
- `child` : Widget enfant
- **Diverses fonctions de `Callback`** :
    - `onTap` : Clic simple
    - `onDoubleTap` : Double clic
    - `onLongPress` : Appui long
    - `onPanUpdate` : Balayage
    - `onScaleUpdate` : Zoom
    - `onVerticalDragUpdate` : Glissement vertical
    - `onHorizontalDragUpdate` : Glissement horizontal
    - `onForcePressStart` : Appui fort
    - `onForcePressEnd` : Fin d'appui fort
    - `onForcePressPeak` : Pic d'appui fort
    - `onForcePressUpdate` : Mise à jour d'appui fort
    - `onSecondaryTap` : Clic droit
    - `onSecondaryLongPress` : Appui long droit
    - `onSecondaryPanUpdate` : Balayage droit
    - `onSecondaryScaleUpdate` : Zoom droit
    - `onSecondaryVerticalDragUpdate` : Glissement vertical droit
    - `onSecondaryHorizontalDragUpdate` : Glissement horizontal droit
    - `onSecondaryForcePressStart` : Appui fort droit

***Exemple*** :
```dart
GestureDetector(
    onTap: () {
        print("Clic simple");
    },
    onDoubleTap: () {
        print("Double clic");
    },
    onLongPress: () {
        print("Appui long");
    },
    child: Text("Appuyez-moi"),
)
```
