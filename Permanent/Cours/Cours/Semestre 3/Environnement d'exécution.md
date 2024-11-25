---
MOOC: "[[Cours]]"
Ressource: "R3.01 : Développement Web"
Cours: "Cours 6 : Environnement d'exécution"
Date: 
tags: 
Complete: false
Learned: false
---
L'interpréteur PHP exécute un seul fichier à la fois, mais le fichier peut être modifié par **l'instruction** `include`. Ainsi, tout ce qui est exécuté est fait par rapport au fichier principale
Les chemins relatifs (`PATH`) sont par rapport à la disposition sur le disque et de cet unique fichierPour les codes de grande taille, cela permet de regrouper des codes dans des fichiers qui sont inclus au moment de l'éxecution.

>[!warning]
>Dans les langages compilés comme ADA, C, C++ ... l'inclusion de fichier se fait à la compilation donc **avant** l'exécution

Il ne faut jamais mettre de chemin absolu dans le projet (ou `__DIR__`) mais plutôt des fichiers relatifs (ou `__DIR__`) car il est comme ça plus facile de relocaliser le projet

Il y a d'autres constantes *magiques* qui sont évaluées au moment de l'interprétation :
- Utiles pour les débogage :
	- `__LINE__` : Le numéro de la ligne
	- `__FUNCTION__`
	- `__METHOD__`
	- `__CLASS__`

On peut créer un fichier de configuration
- Pas besoin de `$` pour [[Permanent/Programmation/PHP/Les variables|Les variables]]
- Les valeurs ne sont que des strings
- délimiteur optionnels
- Pas d'interprétation des charactères spéciaux

Exemple :
```shell
chemin = ./data
valeur_limite = 100
```

```shell
$config = parse_ini_file("exemple-config.init");

array(5){
["chemin"]=> string(6) "./data"
["valeur_limite"]=> string(3) "100"
["tab"]=> array(3){
	[0]=> string(2) "10" [1]=> string(2) "20"
	["animal"]=> string(15) "chien du voisin"}
}
}

```
La fonction d'analyse produit un tableau
Méthode :
- Aucune constante importante dans un programme PHP
- Utiliser un fichier de configuration

---
Il est possible de découper le code trop long en utilisant :
- `include()` : Le fichier appelé n'est pas obligé d'exister et cela ne provoquera pas d'erreur
- `require()` : Le fichier appelé doit exister sinon cela provoque une erreur