En Flutter, le widget `TextField` est le widget de saisie de base en Flutter, soit avec un clavier physique, soit avec un clavier virtuel

> [!Example]
> ```dart
> TextField(
> 	onChanged: (text) {
> 		print('Le texte a changé : $text');
> 	},
> 	onSubmitted: (text) {
> 		print('Le texte a été soumis: $text');
> 	},
> ),
> ```

- **onChanged** : Cette méthode est appelée chaque fois que l'utilisateur modifie le texte
- **onSubmitted** : Cette méthode est appelée quand l'utilisateur appuie ur *Entrée*

---

Il est possible de modifier l'apparence du TextField en utilisant la propriété [[La décoration d'un TextField - Flutter|Decoration]]
On peut également l'intégrer dans un formulaire ([[Récupérer la valeur d'un  TextField - Flutter]])

=> Récupérer la valeur du champs : 
