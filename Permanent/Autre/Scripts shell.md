---
MOOC: "[[Autre]]"
Sujet: Systèmes d'exploitation
Type: 
tags:
---
Les scripts shell sont des fichiers contenant une séquence de commandes exécutées séquentiellement de manière automatique. Ils sont utilisés pour automatiser des tâches, effectuer des opérations répétitives ou combiner plusieurs commandes.
Ils peuvent également prendre [[Fournir une variable à un script shell|des paramètres]] depuis la ligne de commande pour personnaliser leur comportement.

Pour créer un script shell :

1. Créez un fichier texte avec un éditeur de texte.
2. Écrivez les commandes du script.
3. Rendez le fichier exécutable avec `chmod +x NOM_DU_SCRIPT`.
4. Exécutez le script avec `./NOM_DU_SCRIPT`.


Il existe des répertoires standards pour stocker les scripts :
- **Pour un utilisateur particulier :** Il faut placer le script dans le répertoire `/.local/bin/`. C'est d'ailleurs le homedir de chaque utilisateur. Ce dernier y met ce qu'il veux
- **Script pour tous les utilisateurs :** Le script doit être placé dans le répertoire `/usr/local/bin` et seul le super-utilisateur y a accès