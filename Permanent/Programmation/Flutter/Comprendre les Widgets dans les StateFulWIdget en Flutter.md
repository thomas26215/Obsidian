Prérequis : [[StateFulWidget en Flutter]]

On utilise `widget` dans le `State` car les données ne sont pas directement accessibles depuis la classe `State`. Ainsi, Flutter fournit une variable spéciale `widget` qui permet d'accéder aux propriétés du widget parent.

> [!Example]
> ```dart
> class _MyStatefulWidgetState extends State<MyStatefulWidget> {
>   final String nom;
>
>   const ProfilWidget({Key? key, required this.nom}) : super(key: key);
>
>   @override
>   _ProfilWidgetState createState() => _ProfilWidgetState();
> }
> class _ProfilWidgetState extends State<ProfilWidget> {
>   @override
>   Widget build(BuildContext context) {
>     return Text(widget.nom); // Accès à la propriété 'nom' du widget parent
>   }
> }
> ```

