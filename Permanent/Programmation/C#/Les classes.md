Voici comment créer une classe :
```Csharp
class Livre{
	private string titre;
	private string auteur;
	const private string AUTEUR = "OC";
	
	public int NombrePages { get; set; };

	// Constructeur
	public Livre(string titre, string auteur, int nombrePages){
		this.titre = titre;
		this.auteur = auteur;
		this.nombrePages = nombrePages;
	}

	//Propriétés avec accesseurs personnalisés
	public string Titre{
		get{return titre;}
		set{titre = value;}
	}
	public string auteur{
		get{return auteur;}
		private set{auteur = value;} // Setter privé
	}

	//Méthode statique
	public static bool ComparerNombrePages(Livre livre1, Livre livre2){
		return livre1.NombrePages == livre2.NombrePages;
	}


	//Méthode virtuelle (peut être surchargée dans les classes dérivées)
	public virtual string ObtenirInformations(){
		return $"Titre: {titre}, Auteur: {auteur}, Pages: {NombrePages}";
	}
	
}
```

**Voici les éléments clés d'une classe :**

1. **Attributs privés** :
    - `titre` et `auteur` sont des attributs privés, accessibles uniquement à l'intérieur de la classe.
    - Ils sont protégés contre l'accès direct depuis l'extérieur de la classe.
2. **Constante** :
    - `EDITEUR` est une constante privée, sa valeur ne peut pas être modifiée.
3. **Propriété publique** :
    - `NombrePages` est une propriété auto-implémentée, accessible et modifiable de l'extérieur.
4. **Constructeur** :
    - Méthode spéciale appelée lors de la création d'un objet.
    - Initialise les attributs de l'objet.
5. **Propriétés avec accesseurs personnalisés** :
    - `Titre` et `Auteur` sont des propriétés qui contrôlent l'accès aux attributs privés.
    - `Auteur` a un setter privé, ce qui signifie qu'il ne peut être modifié qu'à l'intérieur de la classe.
6. **Méthode statique** :
    - `ComparerNombrePages` est une méthode de classe, pas d'instance.
    - Peut être appelée sans créer d'objet Livre.
7. **Méthode virtuelle** :
    - `ObtenirInformations` peut être surchargée dans les classes dérivées.

**Maitenant, voici comment créer un objet à partir de cette classe :**
```Csharp
Livre monLivre = new Livre("1984", "George Orwell", 328); Console.WriteLine(monLivre.Titre); // Accès via la propriété
monLivre.NombrePages = 330; // Modification via la propriété
Console.WriteLine(monLivre.ObtenirInformations());

Livre autreLivre = new Livre("Brave New World", "Aldous Huxley", 311);
bool memeNombrePages = Livre.ComparerNombrePages(monLivre, autreLivre);
```