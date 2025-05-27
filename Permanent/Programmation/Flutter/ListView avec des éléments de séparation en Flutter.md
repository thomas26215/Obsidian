Le Widget `ListView.separated` en Flutter est utilisé pour créer une liste avec des éléments de séparation entre chaque élément. Cela est particulièrement utile pour améliorer la lisibilité et l'esthétique de la liste. La syntaxe est la même que pour [[Builder pour ListView en Flutter|ListView.builder]]. on va simplement ajouter un paramètre `separatorBuilder` pour définir le widget de séparation.

> [!Example]
> ```dart
> ListView.separated(
>   itemCount: 100, // Nombre d'éléments dans la liste
>   itemBuilder: (context, index) => ListTile(title: Text('Item $index')),
>   separatorBuilder: (context, index) => Divider(), // Séparateur entre les éléments
> )
> ```

