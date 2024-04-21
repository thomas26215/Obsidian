---
MOOC: "[[Programmation]]"
Langage: Git
Type: 
tags:
---
travailler en collaboration nécessite souvent l'utilisation d'un dépôt distant, ou "remote", pour centraliser les sauvegardes. Avec Git, cette démarche est universelle et fonctionne de manière uniforme sur tous les systèmes. Par exemple, un dossier accessible via SSH peut servir de dépôt Git, et les données peuvent être stockées localement, sur une clé USB, ou sur des plateformes comme GitHub et GitLab.

Pour illustrer cela, prenons l'exemple d'un dépôt local que nous appellerons `depot-remote`, situé à `C:\Users\venou\OneDrive\Bureau`

Après avoir créé ce dossier, il faut ouvrir un terminal et naviguer jusqu'à ce dossier. Je vais ensuite exécuter le commande `git init --barre`. 
Il va ensuite falloir informer notre répertoire de travail que c'est un dépôt distant, je vais ainsi exécuter la commande `git remote add nom_remote chemin-absolu`en me plaçant dans mon répertoire de travail. Dans notre cas, nous choisirons comme nom de remote `origin`, signifiant que c'est le dépôt originel (convention de nom) ⇒ `git remote add origin C:\Users\venou\OneDrive\Bureau\depot-remote`.

Pour envoyer mes modifications, je peux utiliser la commande `git push nom_depot nom_branche`. Nous entrons donc la commande `git push origin master` ce qui envoie les changements de la branche master sur le dépôt origin.
⇒ **Push permet donc d'envoyer mes modifications au dépôt**

Afin de récupérer des informations, je peux effectuer la commande `git pull origin master` afin de récupérer les derniers commits qui ont été faits.
⇒ **Push permet donc de récupérer les modifications faites sur les modification par les autres utilisateurs**
Cela peut être plus propre de faire un rebase, car ca met d'abord le commit du dépôt distant puis le mien. Les gens préfèrent cette manière car cela évite d'avoir des dizaines de commits se nommant `merge`. Pour que cela le fasse automatiquement, je peux éxecuter la commande `git congif --global branch.autosetuprebase always`

>[!tip] Pull puis push
>Si des modifications ont déjà été faites sur le dépôt distant, et qu'il est donc *en avance* par rapport à ce que j'ai fait, je doit d'abord faire **pull** et ensuite je peux faire le **push**. Sinon, cela ma génèrera une erreur



La commande `git clone` permet à une personne externe de récupérer le dépôt. Il faut donc faire `git clone chemin_absolu dossier_projet`, dans notre cas, notre troisième utilisateur doit exécuter la commande `git clone C:\Users\venou\OneDrive\Bureau\depot-remote clone-git` si notre utilisateur veut récupérer le dépôt dans un dossier nommé `clone-git`

- `git remote -v` : Affiche la liste des dépôts
- `git remote rename ancien-nom nouveau-nom` : Renommer un dépôt
- `git branch -r` : Afficher la liste des branches