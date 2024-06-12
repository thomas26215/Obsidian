---
MOOC: "[[Programmation]]"
Langage: Git
Type: 
tags:
---
Après des commit, si je souhaite voir le code qui était présent avant, il est possible de faire `git log --oneline -p fichier` afin d'observer les différentes étapes d'un fichier en particulier

Si je souhaite revenir en arrière, il faut que je tape la commande `git checkout clé_commit`. Attention, ici, je ne viens en arrière que comme spectateur. Je ne peux rien toucher, du moins, ca ne me laissera pas revenir au dernier commit. Si je fais des modifications sur un ancien commit, il faut que je fasse un commit. Maintenant, je peux revenir sur ma branche Master (branche principale). Cependant, ce dernier commit ne sera pas sauvegardé. Il sera comme perdu
⇒ **Conclusion :** la commande checkout me permet donc seulement de regarder les anciennes versions du code

Si maintenant, si je souhaite revenir à une ancienne version d'un seul fichier, je peux faire la commande `git checkout clé_commit nom_fichier`. Seulement ce fichier sera revenu à une ancienne version en fonction de la clé de commit. Maintenant, je peux faire un commit normal et ce commit sera ajouté à la liste des autres commits

Quelques commandes :
- Revenir en arrière sur un commit en particulier : `git revert clé_commit` ⇒ Cela permet de défaire un commit en particulier. Je peux aussi défaire ce que j'ai défait
<mark style="background: #BBFABBA6;">Exemple : Je ne veux plus le commit `ajout de la classe Guerrier` : Je peux le supprimer grâce à la commande `git revert clé`</mark>
- **Attention ! cette commande n'est pas sécurisée. Avec cette commande, il est possible de supprimer des choses.** `git reset clé_commit` nous permet de revenir à un ancien commit du code. **Attention :** Tous les commits réalisés entre le dernier commit et le commit du reset vont être supprimés
	- `git reset HEAD nom_fichier` nous permet de retirer un fichier que l'on a ajouté dans le add avant le commit. Cela est utile si on se rend compte que finalement, on ne veut pas commit ce fichier
	- `git reset` : Vider tout ce que j'ai dans le add (staging)
	- `git --hard` : On revient au commit précédent. **Attention : suppression de mon dernier commit donc suppression de fichiers**
	- `git reset HEAD^ --mixed` : Reviens en arrière mais laisse les modifications au niveau du dépôt et ne les stage pas
- 