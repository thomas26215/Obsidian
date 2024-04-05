---
Type de ressource : Programmation
Langage : Kotlin
tags : programmation/Kotlin/concret
---
### Les bases
Contrairement à Java (voir [[Kotlin]]), il est très long et très répétitif de créer le [[Constructeur - Programmation|constructeur]]. En effet, le constructeur qui ne sert qu'à initialiser les attributs s'écrirait de cette manière en Java :
```Kotlin
public class User{
	private String email;
	private String password;
	public int age;
	
//Getters + setters

..

// Fonctions

..
}
```
Au contraire, en Kotlin, le code est beaucoup + simple :
```Kotlin
class User(var email: String, var password: String, var age: Int)

//Code référence
```
En effet, nous remarquons que le code est beaucoup plus concis. Analysons le code en détail : Nous remarquons -  de la même manière que Java - que nous utilisons le mot-clé `class` suivit du nom de la classe afin de déclarer la classe. Aussi, tous les attributs de la classe sont directement renseignés entre les parenthèses. Il n'est pas néssaire de créer une fonction supplémentaire à l'intérieure de la classe (contrairement à Java !)

Au niveau des modificateurs de visibilité, ils sont au nombre de 4 :
- `private` : Uniquement accessible dans la classe
- `protected` : Visible dans classe + sous-classes ([[Héritage]])
- `internal` : Visible par tous ceux d'un même [[Module]]
- `public` : Visible partout

Pour utiliser la classe en tant qu'objet, cela est également différent qu'en Java :
**En Java** : `User user = new User("hello@gmail.com", "azerty", 27);` 
**En Kotlin** : `User user = User("hello@gmail.com", "azerty", 27)`
Et oui ! Il n'y a pas besoin de `new` ici. Cela contribue encore à la compaticité du code
> Même si l'objet de la classe est de type immuable, les propriétéde celui-ci pourra tout-de-même être modifié

Pour les getters et setters :
- `val` : Immuables => Uniquement [[Les classes|assesseur]]
- `var` : Muables => [[Les classes|Assesseur]] + [[Les classes|mutateurs]]
Aussi, par défaut, la visibilité sera `public`

Occupons-nous maintenant des `getters` et `setters` :
```Kotlin
val user = User("hello@gmail.com", "azerty", 27)
user.email //Getter
user.email = "new_email@gmail.com" //Setter
```
Plus besoin des `get` et `set` comme en Java ! Il faut juste appeler la propriété par son nom ! Cependant, comment vérifier la modification de l'email ?
```Kotlin
class User(val email: String, var password: String, var age: Int)
```
Et oui ! `val` immuable donc pas de `setter` !

### Modifier getter et setter
Maintenant, si l'on souhaite ajouter une action quand on met on récupère la valeur d'un attribut. En Java, il aurait juste fallut modifier la fonction `getter` ou `setter`. Cependant, en Kotlin, c'est légèrement différent :
```Kotlin
class User(email: String, var password: String, var age: Int){
	var email: String = email
		get(){
			println("User is getting  their email")
			return field
		}
		set(value){
			println("User is setting their email")
			field = value
		}
}
```
Retirer `val` devant le nom de la propriété `email` pour pouvoir avoir accès au `getter` et `setter` : cela permet de le considérer comme une paramètre et non comme une propriété
Ensuite, nous l'avons déclarée dans le corps de la classe + initialisée celle-ci grâce au paramètre située dans le constucteur. Puis utilisation `set()` et `get()`pour modifier son comportement dans le getter et setter
Enfin, le mot clé `field`fait référence à la propriété en elle-même

### Décalarer un attribut en privé
Nous savons que sans aucune modification, l'attribut est en `public`