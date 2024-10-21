https://github.com/Mojang/minecraft-editor-extension-starter-kit

Certaines faiblesses dans leur conception, persistant aujourd'hui :
- **Complexité excessive**
	- Projet `DataFixerUpper` :  Transformation de données mais particulièrement complexe
	- Code difficile à maintenanir + à évoluer
	- Risques de bugs
	- Rôle essentiel
		- Priorités de développement : Doit développer de nvlles fonctionnalités
		- Rétrocompatibilité : Large base utilisateurs + mods. Refactoriser pourrait briser comptabilité avec contenu existant
		- Ressources limitées : Demande temps et efforts utilisé ailleurs
		- Compléxité de codebase : Effets de cascade car code devenu complexe. Processus risqué et chronophage
		- Il fonctionne, donc risques d'introduire de nouveaux bugs
- Dette technique
- Manque de standardisation
	- Plusieurs langages utilisés (C, Java, JavaScript, TypeScript)
	- Diversité persiste car besoins spécifiques de différentes parties du jeu et de l'historique du développement

1. Projets en développement précoce :
    - Exemples : bedrock-samples et minecraft-editor
    - Statut : marqués comme étant en développement précoce ou contenant des échantillons
2. Implications du statut :
    - Certaines parties du code pourraient être expérimentales
    - Certaines parties du code pourraient être non optimisées
3. Conséquence potentielle :
    - Accumulation de dette technique
4. Raison de la persistance :
    - Ressources limitées pour refactoriser le code

En conclusion, malgré ces faiblesses potentielles, le code de Minecraft continue d'être utilisé en raison de sa fonctionnalité éprouvée, de la difficulté à effectuer des changements majeurs sur un produit en direct, et de la nécessité de maintenir la compatibilité avec le contenu existant et ancien. La nature évolutive du jeu et sa large base d'utilisateurs rendent complexe toute refonte majeure du code.