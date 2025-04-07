![[Pasted image 20241206153158.png]]

Etude de faisabilité de git sur les serveur apache des vm

installé git sur le serveur

créé un token sur github afin de pouvoir clone, pour cela se rendre sur 
https://github.com/settings/tokens
cocher toutes les cases dans repo
Cliquez sur Generate new token.
Donnez un nom au token (par exemple, "Git clone").
Cochez les autorisations nécessaires : comme repo pour accéder aux dépôts privés et workflow pour intéragir avec GitHub Actions.
BIEN COPIER LE TOKEN (limite le mettre dans votre stockeur de mot de passe)

root@debian:/var/www/html# git clone https://github.com/QuentinPeg/portfolio.git
Mettre votre user github
METTRE LE TOKEN

et tout est bon !

Nous avons testé avec un projet html/css basique, puis nou l'avons testé avec un projet php sans rencontrer de souci

---

En haut, nous voyons écrit "La chute", texte issu de la BDD de données dans la table Histoire à la colonne titre

Les deux personnages sont issus de la BDD
Le nom du personnage "Jean" est issu de la BDD venant de la table personnages dans la colonne prenom

Le dialogue est issu de la BDD venant de la table DIALOGUES dans la colonne contenu. On récupère ce dialogue grâçe à id_dialog