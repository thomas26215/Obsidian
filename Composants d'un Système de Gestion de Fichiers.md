## 1. **Structure de Données**

Les systèmes de fichiers utilisent diverses structures de données pour gérer les fichiers, notamment :

- **Table des fichiers** : Contient des informations sur chaque fichier (nom, taille, emplacement).
- **Inodes** : Structures qui stockent les métadonnées des fichiers, y compris les permissions et l'emplacement sur le disque.

## 2. **Opérations sur les Fichiers**

Les opérations fondamentales qu'un SGF doit gérer comprennent :

- **Création** : Ajouter un nouveau fichier au système.
- **Lecture** : Accéder au contenu d'un fichier.
- **Écriture** : Modifier le contenu d'un fichier existant.
- **Suppression** : Retirer un fichier du système.

## 3. **Gestion de l'Espace**

Le SGF doit également gérer l'espace disque disponible en utilisant des techniques comme :

- **Allocation dynamique** : Allouer de l'espace disque à mesure que les fichiers sont créés ou modifiés.
- **Compression** : Réduire la taille des fichiers pour économiser de l'espace.