En Flutter, un `ReorderableListView` est un widget qui permet de créer une liste dont les éléments peuvent être réordonnés par glisser-déposer. C'est particulièrement utile pour les applications où l'utilisateur doit organiser des éléments dans un ordre spécifique.

1. Chaque élément de la liste doit avoir une clé unique pour que Flutter puisse suivre l'élément même s'il change de position
2. Le Widget gère l'affichage du déplacement mais c'est au développeur de gérer la réordonnancement dans la liste des données
3. On doit fournir une fonction `onReorder` qui sera appelée lorsque l'utilisateur déplace un élément

> [!Example] Example simple
> ```dart
> class MaListeReorganisable extends StatefulWidget {
>   @override
>   _MaListeReorganisableState createState() => _MaListeReorganisableState();
> }
>
> class _MaListeReorganisableState extends State<MaListeReorganisable> {
>   List<String> _items = ['Pain', 'Beurre', 'Confiture', 'Fromage'];
>
>   @override
>   Widget build(BuildContext context) {
>     return ReorderableListView(
>       onReorder: (oldIndex, newIndex) {
>         setState(() {
>           if (newIndex > oldIndex) newIndex -= 1; // Ajuste l'index si on déplace vers le bas
>           final item = _items.removeAt(oldIndex);
>           _items.insert(newIndex, item); // Réinsère l'élément à la nouvelle position
>         });
>       },
>       children: [
>           for(int i = 0; i < _items.length; i++)
>             ListTile(
>               key: ValueKey(_items[i]), // Clé unique pour chaque élément
>               title: Text(_items[i]),
>               trailing: Icon(Icons.drag_handle), // Icône pour indiquer que l'élément peut être déplacé
>             ),
>       ],
>     );
>   }
> }


---

> [!Example] Exemple avec un builder
> ```dart
> ReorderableListView.builder(
>   itemCount: _items.length,
>   itemBuilder: (context, index) {
>     return ListTile(
>       key: ValueKey(_items[index]),
>       title: Text(_items[index]),
>     ),
>   },
>   onReorder: (oldIndex, newIndex) {
>     setState(() {
>       if (newIndex > oldIndex) newIndex -= 1; // Ajuste l'index si on déplace vers le bas
>       final item = _items.removeAt(oldIndex);
>       _items.insert(newIndex, item); // Réinsère l'élément à la nouvelle position
>     });
>   },
>);
> ```

