---
MOOC: "[[Programmation]]"
Langage: Java
Type: Concret
tags:
  - status_finish
  - note_permanent
---
```Java
public class Donnees{
	private String access;
	private int donnee1;

	public void Donnees(String access){
		this.access = access;
	}

	public int getIfAdmin(){
		if(access.contains("Admin")){
			return donnee1;
		}else{
			sout("Vous n'êtes pas admin !")
		}
	}
}

Donnees utilisateur1 = new Donnees("Utilisateur")
```
Ainsi, `utilisateur1` ne pourra pas avoir accès à la donnée 1 car il n'est pas aministrateur. Si la variable `donnee1` était en public, il  y aurait accès sans problèmes et l'accès serait beaucoup moins contrôlé