---
MOOC: "[[Programmation]]"
Langage: Git
Type: 
tags:
---
Il se peut certaines fois que je souhaite envoyer certains fichiers dans un commit mais qu'au lieu de faire un nouveau commit, je souhaite rajouter ces fichiers au commit précédant. Pour cela, il faut tout d'abord que je stage mes fichiers (`git add .`)  et par la suite, au lieu de faire un classique `git commit -m ""`, il faut que je fasse `git commit --amend`. Je vais donc me retrouver avec un éditeur qui va me permettre de changer le message du commit

Quand j'ai plusieurs branches, et que je souhaite merge deux branches de manière simple ([[Les branches]] ⇒ `git merge fichier`), je vais devoir créer un nouveau fichier pour la résolution de conflits, ce qui n'est pas toujours très propre. Je peux dans ce cas-là procéder d'une autre manière : Il faut tout d'abord que je me positionne sur la branche qui va être renvoyée, et non pas sur celle qui fusionne. Dans notre exemple, nous souhaitons fusionner la branche 1 sur notre branche master. Je vais donc me positionner sur la branche 1. Maintenant, je vais exécuter la commande `git rebase nom_branche`, avec `nom_branche` le nom de la branche qui fusionne, dans notre cas master. Cela va tout simplement ajouter les commits de notre branche qui fusionne à notre branche externe depuis le moment où j'ai crée cette fameuse branche (Exemple, si j'ai fait 3 commits sur la branche master depuis le moment où j'ai crée la branche 1, cela va envoyer ces trois commits sur la branche 1). Je peux par la suite faire un simple `git merge branche` afin de rapatrier la banche 2 sur la branche 1 ce qui m'assureras un fast forward.
⇒ **Résumé : Le rebase permet de rapatrier les différents commits sur une branche pour être sûr de pouvoir faire un fast forward et d'avoir un historique clean**

Il est aussi possible de faire un rebase interactif pour mieux analyser les différents commits que l'on rapatrie. Il faut pour cela se positionner sur la branche que l'on rapatrie. Je vais ensuite rebase ce que j'ai fait sur ma branche principale en ajoutant une option : `git rebase-i  branche`. Cela va ouvrir un éditeur de texte

Voila comment se présente le texte :
```git
pick 76ee419 message1
pick 74ff215 message2

#
#
#
```
On peut modifier avec différents mots-clés :
- `pick` : Le commit est inclus
- `reword` : Le commit peut être renommé
- `edit` : Le commit peut être édité
- `squash` : Le commit sera fusionné avec le commit au dessus
- `fixup` : comme squash mais le message du commit ne sera pas modifié
- `exec` : Permet d'effectuer des commandes shell sur le commit
Nous, on va mettre `squash`. Il faut résoudre les conflits s'il y en a, donc modifier les codes, `git add`, `git commit` et enfin `git rebase --continue`. Je résous le conflit en gardant le message que je souhaite conserver pour le commit. Finalement, je retourne sur la branche principale puis je fais `git merge branche`

⇒ **En résumé, rebase nous permet de réorganiser nos commits, en inversant des commits, en fusionnant des commits.**

>[!tip] Partage de fichiers
> Il ne faut surtout pas utiliser ce genre de méthode après publication avec d'autres collaborateurs car ces derniers auraient deux versions différentes de l'historique, à ne plus rien y comprendre. On utiliser généralement ce genre de méthode pour le travail local, pour avoir quelque chose de propre avant publication en ligne

