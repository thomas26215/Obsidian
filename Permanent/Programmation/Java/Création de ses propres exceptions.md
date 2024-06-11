---
MOOC: "[[Programmation]]"
Langage: Java
Type: Exceptions
tags:
---
Code de base :
```java
public class MonException extends Exception{

}
```

On peut maintenant l'appeler pour faire remonter une exception : [[Gestion des exceptions en Java]]
```java
public void main()throws Exception{
	try{
		fonction()
	}catch(MonException e){
		System.out.println("Erreur")
	}
}
public void fonction()throws Exception{
	if(false){
		throws new MonException();
	}else{
		System.out.println("réussi")
	}
}
```