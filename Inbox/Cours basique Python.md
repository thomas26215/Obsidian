# Bases
## Classes
- Dans une classe, qui est définie par `class nom_class` contient des attributs et des objets
	- Les **attributs** sont les caractéristiques de l'objet (Exemple pour un humain : taille, poids, age, Prenom ...)
	- Les **Fonctions** sont des actions que peut réaliser un objet (Exemple pour un humain : une humaine peut marcher tout droit ; fonction marcher, un humain peut tourner à gauche, fonction tourner_gauche)
- Les attributs d'un objet sont définits au début de la classe. Pour appeler un attribut d'un objet, je doit le précéder par `self` (exemple : `self.prenom`). Si je souhaite appeler un attribut dans une fonction de la classe, je doit rajouter en paramètre de fonction `self` (exemple : `def marcher(self, attribut1, ...)`)

## Liste
- Se définit par `nom_liste[1,2,3,4,5]` ou par `nom_liste[0]*20*`
- Pour l'indice, c'est toujours un inférieur à celui qu'on veut (le deuxième élément est l'indice 1)
- `liste.get[indice]` = Récupérer
- `liste.append(donnee)` Ajouter la donnée à la fin de la liste