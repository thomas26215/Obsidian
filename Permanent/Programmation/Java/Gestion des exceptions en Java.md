---
MOOC: "[[Programmation]]"
Langage: Java
Type: Exceptions
tags:
---
Bloc `try-catch` :
```java
public main()throws Exception{
try{
	fonction();
}catch(Exception e){
	System.out.println(e);
	}
}
```

Fonction renvoyant l'erreur
```Java
public void fonction()throws Exception{
	if(false){
		throws new Exception();
	}else{
		System.out.println("Vrai");
	}
}
```

Il est aussi possible de faire remonter une exception en ayant [[Création de ses propres exceptions|appelé une exception que l'on a crée soit-même]]