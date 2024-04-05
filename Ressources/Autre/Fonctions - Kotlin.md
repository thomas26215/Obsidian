---
Type de ressource : programmation
Langage : Kotlin
tags : programmation/Kotlin/concret
---
Voici une fonction toute simple :
```Kotlin
fun main(args: Array<String>){
	println("Hello world")
}
```
Premièrement, nous remarquons qu'une fonction en Kotlin commence par l'attribut `fun`. Il est suivit du nom de la fonction
Ensuite, le type des paramètre du paramètre est indiqué après son nom (`args`). Les deux points servent à la déclaration du type
Une fonction peut être déclarée sans être à l'intérieur d'une classe grâce à l'extension `kt` (voir plus loin)

Observons maintenant ce code :
```Kotlin
private fun minOf(a: Int, b: Int): Int{
		return if (a < b) a else b
}
```
On voit que les paramètres sont séparés d'une virgule. Aussi, pour spécifier ce que ça retourne, nous utilisons les deux points suivit du type retourné
Pour ce qui est retourné, il faut savoir la différence entre une [[Expression - Programmation]] et une [[Instruction]]
Il important de considérer cela car la plupart des structures de contrôle sont considérées comme des [[Expression - Programmation]] et retourneront donc une valeur même si non spécifié.

Pour comprendre à quoi servent les expressions, il faut reprendre notre précedant exemple `minOf`. Le `if` est considéré comme un expression, et cela va nous permettre de réaliser ce genre de chose :
```Kotlin
private fun minOf(a: Int, b: Int): Int = if(a < b) a else b
```
Ou même encore en plus compacte :
```Kotlin
private fun minOf(a: Int, b: Int) = if(a < b) a else b
```
Nous remarquons que c'est très lisible. En effet, cette fonction n'a pas de corps ; elle n'a pas de `{ }` mais une expression à la place
Mais celle-ci ne se limite pas aux fonction retournant une valeur :
```Kotlin
fun sayHello() = println("Hello !")
```
équivaut à 
```Kotlin
fun sayHello(): Unit = println("Hello !")

```
équivaut à
```Kotlin
fun sayHello(): Unit{
	println("Hello !")
}
```

Pour finir, si une fonction possède un corps et que l'on souhaite retourner une valeur, l'inférence de type ne fonctionnera pas dans ce cas-là (Kotlin a fait ce choix pour optimiser les performances de son compilateur)
=> La déduction du type de valeur à retourner peut devenir très gourmande en terme de ressources, surtour si elle fait plusieurs dizaines de lignes
**Exemple** :
```Kotlin
// 😱
fun getUrlApi() { return "https://www.my.api.com" }

// 🙂
fun getUrlApi(): String { return "https://www.my.api.com" }

// 😎
fun getUrlApi() = "https://www.my.api.com"
```
