`ValueChanged<T>` est un alias de type défini dans Flutter/Dart. C'est une fonction qui prend un argument de type `T` et ne retourne rien (void). Il est souvent utilisé pour représenter des callbacks qui sont appelés lorsque la valeur d'un widget change, comme dans le cas d'un `TextField`, d'un `Checkbox`, ou d'autres widgets interactifs.

```dart
typedef ValueChanged<T> = void Function(T value);
```

> [!Example] Utilisation typique
> ```dart
> final ValueChanged<String> onTextChanged;
> ```
> Le parent passe une fonction qui sera appelée chaque fois que le texte change dans un `TextField`.

---

> [!Example] Example simple et complet
> ```dart
> class monWidget extends StatelessWidget {
>   final ValueChanged<String> onTextChanged;
>   MonWidget({required this.onTextChanged});
>
>   @override
>   Widget build(BuildContext context) {
>     return TextField(
>       onChanged: onTextChanged,
>     );
>   }
> }
> ```
>
> Et dans le parent :
> ```dart
> MonWidget(
>   onTextChanged: (value) {
>     print('Le texte a changé : $value');
>   },
> );
:wa
> ```
