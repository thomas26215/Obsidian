On parle d'optimisation la pratique consistant à améliorer l'efficacité et la clarté du code. Généralement, c'est quand le code s'éxecute plus rapidement, prend moins de place en mémoire, limiter sa consommation de ressources et de consommer moins d'énergie
Il y a certains principes à respecter :
- **Chaque fonction, ligne de code ne doit intervenir qu'une seule fois et répondre à une seule fonction** ⇔ **On devrait oublier les petites optimisation locales. Optimisation prématurée = source maux de tête**. Ainsi, certaines optimisation de bas niveau peuvent éventuellement être effectuées uniquement à la fin de l'écriture du programme. Cependant, garder une certaine rigueur dans l'optimisation permet une meilleur lisibilité du code, ce qui permet aux développeurs de mieux s'y retrouver quand ils doivent reprendre son écriture après des années d'inutilisation.
- **Choisir des algorithmes de complexité mathématiques inférieurs**
- **Utiliser des fonctions / bibliothèques**
- **Utiliser la langage approprié**
	- Utiliser Python s'y beaucoup d'entrées / sorties
	- Si nécessite beaucoup de calculs et d'affectation en mémoire, utiliser C ou C++

Aujourd'hui, les compilateurs réalisent beaucoup d'optimisations automatique, auxquelles le développeur ne penserait pas à premier abord