---
MOOC: "[[Programmation]]"
Langage: Git
Type: 
tags:
---
Il faut ouvrir powershell pour windows, bash pour linux ... Et se rendre dans le dossier où nous avons notre projet. (Commande `cd repertoire`). Il est possible de créer ce dossier en lignes de commandes (Commande `mkdir nom_dossier`)
Une fois cela fait, il faut que je tape la ligne de commande `git init` qui permet d'initialiser le versionning.

>[!tip]
>A l'intérieur de notre répertoire de projet est créer un dossier caché nommé `.git`
> ⇒ **Il ne faut jamais le toucher, ni le modifier, ni le supprimer !**

Il faut maintenant configurer git. Voici les différentes lignes de commandes de base à rentrer :
```git
git config --global user.email "email@extension.fr"
git config --global user.name "prenom nom"
git config --global color.ui "true"
```

Maintenant que j'ai fait tout cela, il est possible d'ajouter les fichiers à l'historique git.

Tout d'abord, afin de connaître quels fichiers ont été ajoutés, modifiés ou bien supprimés depuis le dernier push il est possible de taper la commandes `git status` qui nous donnera l'avancée de notre travail

Maintenant, pour ajouter les fichiers à notre projet `git`, il faut passer par les étapes suivantes :
- `git add .` - `git add nom_fichier`
  ⇒ Dire a git que les fichiers que l'on veut commit sont ceux spécifiés. Tant que l'on a pas commit, il est possible d'ajouter ou d'enlever des fichiers à ce dernier
- `git commit -m"message"`
  ⇒ Maintenant que mes fichiers sont envoyés et que je suis prêt à envoyer mes modification, je peux commit mes fichiers. Il est important de bien choisir sont message pour retrouver plus facilement les anciennes versions de son code
<mark style="background: #BBFABBA6;">Exemple : Dans mon code, j'ai modifié des codes concernant le personnage principale. J'ai ajouté une fonction de saut et de nage. Mon commit serait semblable à : </mark><mark style="background: #FF5582A6;">"Personnage principale : ajout de la méthode saut et nage"</mark>

La commande `git log` permet de liste tous les derniers commit qui ont été réalisés après le dernier push
`git log --oneline` permet d'afficher les commits sur une seule ligne
`git log -p nomfichier` permet d'afficher tous les commits concernant un fichier