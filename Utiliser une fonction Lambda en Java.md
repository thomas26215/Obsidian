---
MOOC: "[[Programmation]]"
Langage: Java
Type: Fonctions Lambdas
tags:
---
En Java, les fonctions lambdas sont souvent définies par `(parameters) → expression`. Elles peuvent être utilisées pour instancier des interfaces fonctionnelles (Interface ne contenant qu'une seule méthode abstraite). Par exemple :
```Java
interface MathOperation{
	int operation(int a, int b);
}
public class LambdaAddition{
	public static void main(String[] args){
		//On définit l'opération d'addition
		MathOperation addition = (a,b) -> a + b;
		
		//On utilise l'opération d'addition
		int result = addition.operation(5,3);
	}
}
```

Il existe également des intefaces fonctionnelles fournies par le JDK en important le package `java.util.function` :
- `Function<T, R>` ⇒ Représente une fonction prenant un argument de type **T** et retournant un résultat de type **R**
- `Predicate<T>` ⇒ Prend un argument de type **T** et retourne un **boolean**
- `Consumer<T>` ⇒ Prend un argument de type **T** et ne retourne rien
- `Supplier<T>` ⇒ Ne prend aucun argument et retourne un argument de type **T**

Voici un exemple utilisant `Function` :
```Java
import java.util.function.Function;
public class Example{
	public void main(String[] args){
		Function<String, Integer> stringLength = s -> s.length();
		int length = stringLength.apply("Hello World");
		System.out.println(length);
	}
}
```
Ces interfaces fournies par le JDK sont flexibles et puissantes sans pour autant avoir à définir des interfaces personnalisées pour chaque cas d'utilisation