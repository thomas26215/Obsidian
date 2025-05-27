Quand on implémente un `TextField` en Flutter, on peut souhaiter récupérer la valeur que l'utilisateur a rentré. Pour cela, nous pouvons utiliser un `TextEditingController`. Grâce à celui-ci, il est possible :
- d'afficher un texte initial dans le `TextField`
- d'accéder au texte : ***`_controller.text`***

> [!Attention]
> Il faut appeler la méthode `_controller.dispose()` quand on a plus besoin du contrôleur (par exemple dans la méthode `dispose()` d'un [[Flutter - Statefull Widget#3.5 Suppression de l’état (`dispose`)|Statefull Widget]] )

> [!Example]
> ```dart
> final TextEditingController _controller = TextEditingController(text: "Texte initial");
> 
> TextField(
> 	controller: _controller
> 	...
> 	...
> )
> ```

	