---
MOOC: "[[Programmation]]"
Langage: Git
Type: 
tags:
---
## Visualisation de l'historique des commits

Pour voir les changements apportés à un fichier spécifique au fil du temps, on peut utiliserr la commande suivante :

`git log --oneline -p <fichier>`

Cette commande affiche l'historique des commits avec les différences (diffs) pour le fichier spécifié.

## Revenir à un ancien commit

Pour revenir à un ancien commit en mode "spectateur" (sans modifier le code), il faut utiliser :

`git checkout <clé_commit>`

Cela vous permet de voir le code tel qu'il était à ce moment-là. Notez que vous êtes dans un état **detached HEAD**, ce qui signifie que vous ne pouvez pas faire de commits sur cette version sans créer une nouvelle branche.

## Récupérer des modifications

Si vous souhaitez faire des modifications sur un ancien commit, il est préférable de créer une nouvelle branche à partir de celui-ci :
`git checkout -b <nouvelle_branche> <clé_commit>`
Cela vous permet de travailler sur cette version sans perdre l'historique.
## Restauration d'un fichier spécifique
Pour restaurer une ancienne version d'un seul fichier, utilisez :
`git checkout <clé_commit> -- <nom_fichier>`
Cela ramènera le fichier à son état dans le commit spécifié. Vous pourrez ensuite faire un commit normal pour enregistrer cette modification.

## Commandes pour annuler des commits

- **Annuler un commit spécifique** :
    `git revert <clé_commit>`
    Cela crée un nouveau commit qui annule les changements du commit spécifié. C'est une méthode sécurisée pour revenir en arrière sans supprimer l'historique.
- **Revenir à un ancien état du dépôt** :
    `git reset <clé_commit>`
    Cette commande supprime tous les commits effectués après le commit spécifié. Utilisez-la avec précaution, car elle peut entraîner la perte de données si ces commits n'ont pas été sauvegardés ailleurs.
- **Retirer un fichier de la staging area** :
    `git reset HEAD <nom_fichier>`
    Cela retire le fichier ajouté précédemment avec `git add` avant le commit.
- **Vider la staging area** :
    `git reset`

## Options avancées de reset

- **Revenir au dernier commit et supprimer les modifications** :
    `git reset --hard`
    Cette commande supprime toutes les modifications non commitées et revient au dernier commit.
- **Revenir au dernier commit tout en gardant les modifications** :
    `git reset HEAD^ --mixed`
    Cela vous permet de revenir au dernier commit tout en conservant vos modifications dans votre répertoire de travail sans les ajouter à la staging area