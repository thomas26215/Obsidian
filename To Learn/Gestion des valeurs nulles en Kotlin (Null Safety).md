---
MOOC: "[[Programmation]]"
Langage: Kotlin
Type: 
tags: []
---
Kotlin, un langage moderne basé sur la [[JVM]], propose une approche plus sûre pour la [[Gestion des valeurs nulles (Null Safety)|gestion des valeurs nulles]]. Par défaut, les variables en Kotlin ne peuvent pas contenir de valeurs `null`, réduisant ainsi considérablement le risque de `NullPointerExceptions`. Pour indiquer explicitement qu'une variable peut être nulle, il suffit d'ajouter un point d'interrogation (`?`) après le type de données :
```Kotlin
var name = "Thomas"
name = null //Cela ne marche pas car on a pas spécifié la possibilité de nullité lors de la déclaration de l'erreur
//Cela causera une erreur

var message: String? = "Mon message peut être null"
message = null //Ca marchera car on a spécifié lors de la déclaration de la variable que celle-ci peut prendre la valeur nulle
```
Cette indication incite les développeurs à prendre des précautions lors de la manipulation de la variable. De plus, Kotlin offre des mécanismes tels que l'opérateur `?.` (safe call) et les vérifications conditionnelles pour gérer efficacement les variables potentiellement nulles :
```Kotlin
//1e manière
var nom: String? = "Thomas"
message?.toUpperCase()

//2e manière
var nom: String? = "Thomas"
if(message != null) message.toUpperCase()
```

---
**Links :**
[[Gestion des valeurs nulles (Null Safety)]]