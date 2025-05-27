La méthode la plus courante pour créer des ListView longues est de créer un `ListView.builder`. Elle construit des éléments à la demande (méthode lazy loading) uniquement lorsque ceux-ci entrent dans la zone visible de l'écran.

> [!Example]
> ```dart
>ListView.builder(
>  itemCount: 100, // Nombre d'éléments dans la liste
>  itemBuilder: (context, index) {
>    return ListTile(
>      title: Text('Item $index'),
>    );
>  },
>)
> ```

