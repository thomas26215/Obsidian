# Héritage
En règle générale, une classe A héritant d'une classe B récupère tous ses attributs et toutes ses méthodes. On utilise pour cela `public class A extends B{}`

Ainsi, si j'ai un classe Etudiant qui hérite de Personne, j'aurai toutes les méthodes et tous les attributs de la classe Personne dans la classe Etudiant. Il reste cependant possible d'ajouter des méthodes dans la classe Etudiant.

Pour redéfinir une méthode, il faut utilliser `@Override`

Pour récupérer un attribut de la classe Parent, il faut utiliser `super.attribut` ou `super.fonction()`

# Classe abstraite
Permet de créer des classes filles par héritage, mais jamais instanciées.
Possibilité de créer des méthodes abstraites à l'intérieures, qui devront être implémentées par les classes filles

**Exemple :**
```Java
public abstract class Personne {
private String login;
private String nom;
...
	public Personne(String login, String nom, String prenom{
		setLogin(login);
	}
	 public abstract String getEmail(); //A instancier dans classes filles
```