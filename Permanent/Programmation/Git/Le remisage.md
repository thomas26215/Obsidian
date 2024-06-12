---
MOOC: "[[Programmation]]"
Langage: 
Type: 
tags:
---
Le remisage sert à stocker les modifications effectueés afin de les réappliquer plus tard. Utile notemment pour changer de branches sans perdre ses modifications ou si l'on souhaite commit une petite feature alors qu'on est en train de travailler sur une grosse feature.

Pour pouvoir effectuer le remisage, li faut exécuter la commande `git stash`. Ca va prendre toutes les modifs effectuées depuis le dernier commit et ça va les stocker en mémoire. Ainsi, on voit que toutes les modifications effectuées depuis le dernier commit ont été supprimées. Maintenant, je peux travailler sans avoir à me soucier de ce commit. Maintenant, je peux continuer ma vie en faisant d'autres commits. Pour remettre toutes les modifications stockées en mémoire, je fais `git stash apply`. Attention, cela ne vide pas la liste en mémoire, la liste reste inchangée

- `git stash -u` : Inclut les fichiers non trackés (fichiers crées, supprimés ..)
- `git stash save nom` : Ajout d'une sauvegarde en stash avec un nom
- `git stash list` : voir les éléments sauvegardées en mémoire
- `git stash apply` : appliquer les changements en mémoire du dernier élément stash
- `git stash apply nom` : appliquer les changement d'un élément stash en particulier
- `git stash drop` : supprimer le dernier élément stocké dans le stash
  `git stash pop` : Applique les changement d'un élément stash puis le supprime par derrière
- `git stash show stash@(numero)` : Affiche les informations d'une sauvegarde

Il se peut également que je souhaite passer d'une branche à  l'autre ([[Les branches]]). Si j'ai des fichiers qui sont modifiés sur une branche (avant commit), et que je souhaite passer sur une autre branche, je ne peux pas simplement faire une `git checkout branche` car cela me dira que j'ai déjà des informations modifiée sur cette branche. Ainsi, le stash me permet de régler ce problème. Pour cela, je mets les modifications dans un stash (`git stash add`), je vais ensuite sur mon autre branche, je fais mes modifications et mes commits (je peux même ajouter les informations de mon ancienne branche sur celle-ci en faisant un `git stash apply`) puis une fois cela fait, je peux retourner sur ma première branche pour reprendre là om j'en était en faisant `git stash apply`
⇒ Je peux de la même manière créer une branche à partir de modifications que j'ai déjà fait sur ma branche actuelle