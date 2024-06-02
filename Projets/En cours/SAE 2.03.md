# Installation de la machine virtuelle
## Préparation de l'image ISO

### Téléchargement et vérification de l'image ISO
- L'image ISO et les fichiers permettant de <mark style="background: #FFB86CA6;">vérifier son intégrité</mark> sont disponibles ici `https://cdimage.debian.org/cdimage/release/current/amd64/iso-cd/`
- Dans notre cas, l'image ISO est déjà téléchargée et se trouve dans le répertoire `/usr/local/images-ISO/`. Vérifier son intégrité avec la commande suivante en comparant visuellement les deux traces (elles doivent être les mêmes) :
```Shell
sha512sum /usr/local/images-ISO/image-iso.iso
```

## Installation de Debian
### Lancer l'installation de Debian
    
- Démarrez la machine virtuelle en amorçant sur l'image ISO d'installation :
```Shell
S2.03-lance-installation
```
	
- Pour vérifier et modifier les paramètres de Qemu/KVM, ouvrez le fichier `S2.03-commun` :
```Shell
nano /users/info/pub/bin/S2.03-commun
```
	
Les paramètres nécessaires sont déjà configurés dans ce fichier.
### Suivez la procédure d'installation standard
    
- Il faut maintienant suivre la procédure classique pour installer le système

>[!Warning]
>Il faut installer Debian sans interface graphique. **C'est le choix le plus crucial !**

- Voici les différentes étapes à réalise [Si rien n'est précisé, ne changez rien] :

	- _Language_ : English
	- _Location_ : other/Europe/France
	- _Locales_ : United States, en_US.UTF-8
	- _Keyboard_ : French
	- **Hostname** : utilisez server-"VOTRE_LOGIN_UGA"
	- **Root Password** : un mot de passe simple est conseillé, par exemple "root". Dans ce contexte, cela ne pose pas de problème de sécurité. Cocher la case "Show Password" pour être sûr que le mot de passe saisi est bien celui que vous voulez.
	- _User Account_ - **Full Name** : votre nom complet, par exemple "Jean Toto"
	- **User Name** : saisir votre nom de login UGA
	- **User Password** : saisir un mot de passe simple, par exemple "etu". Cocher la case "Show Password" pour être sûr que le mot de passe saisi est bien celui que vous voulez.
	- _Partition disks_ : Guided - use entire disk
	- _Partition disks_ : All files in one partition
	- _Partition disks_ : Yes
	- _Software Selection_ : vérifier que "Debian desktop" n'est pas coché et que "ssh server" est coché
	- _Install GRUB_ : Yes
	- _Device for boot loader_ : `/dev/sda`  

⇒ Cela étant fait la machine virtuelle se lance. **Il faut maintenant éteindre la machine avant de pourvoir passer à l'étape suivante !** Il faut pour cela se logger sur le compte root (==Identifiant = Hostname et Mdp = Password==) et exécuter la commande `# poweroff` pour éteindre proprement la machine.
 
>[!info]
>A partir de maintenant, c'est cette commande (`# poweroff`) qu'il faut utiliser pour éteindre la machine virtuelle

### Déplacement de l'image disque sur le serveur
- Utiliser la commande suivante pour déplacer l'image disque sur le serveur erebus4. Ce sera utile pour utliiser la machine virtuelle plus facilement
```Shell
S2.03-déplace-image-disque-sur-erebus4
```
>[!info]
>On peut aussi déplacer l'image disque sur une clé USB si l'on souhaite accéder à la machine virtuelle depuis plusieurs machines. Pour cela, il faut directement chercher cette image dans la clé USB
## Vérification du serveur Debian
- Il faut maintenant exécuter la commande qui suit pour lancer la machine virtuelle :
```Shell
S2.03-lance-machine-virtuelle
```

>[!warning]
>Attention à bien retenir cette commande car vous l'utiliserez chaque fois que vous voudrez lancer la machine virtuelle


## Redirection des ports et accès par SSH
Certaines redirections de port ont été mises en place afin de pouvoir accéder aux serveurs tourant sur notre machine Linux depuis des clients sur notre machine Linux :

| Service réseau | Port de la VM | Port sur la station Linux | Exemple d'utilisation depuis la station Linux |
| -------------- | ------------- | ------------------------- | --------------------------------------------- |
| SSH            | 22            | 2222                      | $ ssh toto@localhost -p 2222                  |
| HTTP           | 80            | 8080                      | URL: http://localhost:8080/                   |
| HTTPS          | 443           | 4443                      | URL: https://localhost:4443/                  |
| PostgreSQL     | 5432          | 5432                      | $ psql -h localhost -U postgres postgres      |

# Installation de logiciels
## Apache
- Installer Apache2 en lançant les commandes suivantes :
```Shell
apt install apache2
service apache2 start
```
> [!Warning]
> Il faut déjà être **utilisateur root** pour avoir toutes les permissions, notamment celle d'installer un logiciel : `sudo -i` ou `su`
- Exécuter la commande suivante pour vérifier que le logiciel est bien installé :
```Shell
systemctl status apache2
```
- Si par malheur Apache n'a pas démarré :
```Shell
systemctl start apache2
```
- Il n'est pas possible d'afficher une page Web graphiquement (nous avons installé la machine virtuelle uniquement pour les lignes de commande). Il est cependant possible de se connecter  au serveur Apache avec la commande `telnet` et en entrant la chaîne de charactère `HEAD/HTTP/1.0` suivit de deux retours à la ligne :
```Shell
telnet localhost 80 #Il faut taper
Trying ::1...
Connected to localhost.
Escape character is '^]'.
HEAD / HTTP/1.0 #Il faut taper

HTTP/1.1 200 OK
[...]
```

- On peut également afficher la page Web sur la machine hôte. Pour cela, il faut rediriger un port de la machine hôte (`8080` par exemple) au port 80 (port par défaut des serveurs Web) sur la machine virtuelle. Il suffit maintenant de se connecter à l'URL suivante sur la machine hôte :
```Link
http://localhost:8080
```

## PostgreSql
- Installer PostgreSql en exécutant la commande :
```Shell
apt install postgresql
```
- Pour vérifier l'installation du logiciel, se connecter en `root` et exécuter la commande suivant :
```Shell
su - postgres
```
- Pour faire appraître les bases de données par défaut, exécuter la commande :
```Shell
psql -l
```

Il est maintenant possible de faires quelques tâches simples, en se connectant à la machine virtuelle depuis ce même shell tournant sur la machine virtuelle (Commande `psql`) :
1. **Créer un utilisateur avec comme nom votre login :** `CREATE USER votre_login WITH password = 'xxx'`
2. **Créer une base dont le propriétaire est votre utilisateur :**
```SQL
CREATE DATABASE ma_base WITH OWNER = votre_nom_uga;
```
3. **Créer une table simple dans la base de données :**
```SQL
\c ma_base
```
4. **Créer une table :**
```SQL
CREATE TABLE ma_table (
    id SERIAL PRIMARY KEY,
    nom VARCHAR(100),
    age INT
);
```
5. **Insérer quelques lignes :**
```SQL
INSERT INTO ma_table (nom, age) VALUES ('Alice', 30);
INSERT INTO ma_table (nom, age) VALUES ('Bob', 25);
INSERT INTO ma_table (nom, age) VALUES ('Charlie', 35);
```

- Il faut maintenant modifier certains fichiers pour que cette base PostgreSQL soit accessible par une machine Linux. Pour se faire :
	1. **Modifier `postgresql.conf` :**
	   ⇒ Rechercher dans la catégorie *CONNECTIONS AND AUTHENTICATION* et décommenter la ligne `listen_addresses = '*'`
	2. **Modifier `nano /etc/postgresql/15/main/pg_hba.conf` :**
	   ⇒ Dans la catégorie *#IPv4 remote connections:*, ajouter la règle suivante : `host  all all 0.0.0.0/0 scram-sha-256`
	3. Il faut maintenant repasser en **root** et relancer le serveur :
```sh
service postgresql restart
```

- On peut maintenant lister le contenu de la table `pg_shadow` pour vérifier que les mots de passe sont bien hâches avec **SHA-256** :
```SQL
\c postgres
SELECT usename, passwd FROM pg_shadow;
```

## Installer PHP
- Installer PHP en exécutant les commandes suivantes tout en étant `root`
```sh
apt install php-common libapache2-mod-php php-cli
/etc/init.d/apache2 start
```
>[!info] `/etc/init.d/apache2 start` sert à lancer Apache quand il est installé et `/etc/init.d/apache2 stop` sert à l'arrêter

- Pour tester l'installation, placer un fichier `info.php` dans le répertoire `var/www/html/` (Commande `touch` possible ⇒ `touch var/www/html/info.php`) puis rentrer le code suivant :
```PHP
<?php
phpinfo();
phpinfo(INFO_MODULES);
?>
```
- Maintenant, revener sur votre machine hôte puis, dans votre navigateur Web, rentrez le lien suivant : `http://localhost:8080/info.php`. Normalement, une page contenant les caractéristiques principales de votre installation PHP devrait apparaître

## Installer PhpPgAdmin
-  Installer PhpPgAdmin en exécutant la commande suivante tout en étant `root` :
```sh
apt -y install phppgadmin php-pgsql
```
-  Il faut maintenant modifier certains fichiers :
1. **Modifier `etc/phppgadmin/config.inc.pgp`**
   ⇒ Dans la catégorie *Only allow connections from localhost*, enlever `Require local` et remplacer par `Require all granted`
2. **Modifier `/usr/share/phppgadmin/classes/database/Connections.php` :**
   ⇒ A la ligne 79, *ajouter PostgresSQL 15* : `cas '15' : return 'Postgres':break;` remplaçant la ligne `cas '14' : return 'Postgres':break;`
- Relancer Apache2 pour appliquer les modifications :
```sh
systemctl reload apache2
```
- Ouvrir une page internet et rentrer le lien `http://localhost/phppgadmin/`
