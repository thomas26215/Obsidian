Pour configurer GTest dans VSCode, il faut :
- Créer un fichier [[CMakeLists.txt]] à la racine du projet
- Aller dans le shell et créer une répertoire `build` dans la racine du projet. S'y diriger
- Générer les fichier de construction : `cmake ..`
- Construire le projet : `make`
- Exécuter les tests : `NomDeLaClasseDeTests`