En futter, `Expanded` est un widget qui permet à un widget enfant de prendre tout l'espace disponible edans `Row` ou `Column`

**=> Exemple** :

```dart
Row (
	children: [
		Icon(Icons.arow_back),
		Expanded(
			child: Text("Ce titre prendra la place restante dans le Row"),
		),
	],
),
```

=> Dans ce cas-là, ça permet au texte de prendre toute la largeur possible

---


[[Row]]
[[Column]]