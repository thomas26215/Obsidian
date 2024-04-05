---
MOOC: "[[Programmation]]"
Langage: Java
Type: Concret
---
Il est possible d'intéragir avec l'utilisateur en lui demandant cetaines valeurs afin d'éxecuter certains trucs
La première chose à faire est d'initialiser ce lecteur :
```Java
Scanner lecteur = new Scanner(System.in);
```
Maintenant, il est possible de demander une valeur une valeur à l'utilisateur. Attention, la synthaxe ne sera pas la même en fonction des types de variables. Il faut mettre `variable = lecteur.nextType();` suivit de `lecteur.nextLine();`. Voici le tableau des différentes valeurs
**Exemple** :
```Java
int age;
String name;

System.out.println("Quel est ton âge ?")
age = lecteur.nextInt();
System.out.println("Quel est ton nom ?")
name = lecteur.nextLine();

```
