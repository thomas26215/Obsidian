Bien que les fichiers ne soient pas mappés dans l'espace mémoire du processus, les données accédées transitent souvent par la RAM. Cela permet de garder en cache les dernières données utilisées pour améliorer l'efficacité lors d'un futur accès.Les éléments copiés incluent :

- Les derniers datablocks
- Les i-nœuds des fichiers et répertoires accédés
- Une table contenant des informations sur la partition (superblock)