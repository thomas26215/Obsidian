Les descripteurs de fichiers sont des entités essentielles pour la gestion des fichiers dans un système d'exploitation. Les trois premiers descripteurs sont définis systématiquement :

- **0** : Entrée standard (stdin)
- **1** : Sortie standard (stdout)
- **2** : Erreur standard (stderr)

Un fichier peut être ouvert plusieurs fois par un même processus, et chaque ouverture génère un nouveau descripteur. Le **Process Control Block (PCB)** contient une table des fichiers ouverts, qui associe chaque descripteur à un pointeur vers l'accès.