# Installation de la machine virtuelle
## Préparation de l'image ISO

### Téléchargement et vérification de l'image ISO
- The ISO image and files for <mark style="background: #FFB86CA6;">verifying its integrity</mark> are available here `https://cdimage.debian.org/cdimage/release/current/amd64/iso-cd/`
- In our case, the ISO image has already been downloaded and is located in the `/usr/local/images-ISO/` directory. Check its integrity with the following command, visually comparing the two traces (they must be the same):

```Shell
sha512sum /usr/local/images-ISO/image-iso.iso
```

## Installation de Debian
### Lancer l'installation de Debian
- Boot the virtual machine on the installation ISO image:
```Shell
S2.03-lance-installation
```
### Paramètres de lancements


- To check and modify Qemu/KVM settings, open the file `S2.03-commun` :
```Shell
nano /users/info/pub/bin/S2.03-commun
```

1. **Image path declaration** :
```ssh
image_locale="/donnees/TP-infobut/Debian-S2.03-$LOGNAME.img"
image_nfs="/users/Stockage-HDD/images-kvm/S2.03/images/Debian-S2.03-$LOGNAME.img"
```
    
2. **Image existence case management** :
    
	- If both images exist (local and NFS), the script displays an error message and stops.
	- If no image exists, it creates a new 4 GB local image.
	- If an image exists on the NFS server, it is used.
	- If an image exists locally, it is used.

```ssh
if [ -e "$image_nfs" ] && [ -e "$image_locale" ]; then
	echo "Situation anormale: Vous avez une image locale et une autre sur erebus4"
	exit
elif [ ! -e "$image_nfs" ] && [ ! -e "$image_locale" ]; then
	echo "Création d'une image disque locale ..."
	qemu-img create "$image_locale" 4G
	sync
	echo "Fini."
fi
if [ -e "$image_nfs" ]; then
	image="$image_nfs"
elif [ -e "$image_locale" ]; then
	image="$image_locale"
fi
```

    
3. **Disk configuration for QEMU** :
```ssh
drive="format=raw,file=$image,discard=unmap
```
    
4. **ISO path declaration** :
```ssh
iso=$(ls /usr/local/images-ISO/debian-*-netinst.iso)
```
    
5. **(Commented) Launch of QEMU** :

```ssh
# qemu-system-x86_64 -drive $drive -cdrom $iso -boot d -m 2G
```

The script checks and creates the required disk image, chooses between a local image or one on NFS, configures the disk for QEMU, and prepares the ISO path for launching the virtual machine.

### Follow the standard installation procedure
- Now follow the standard procedure to install the system

>[!Warning]
>You need to install Debian without a graphical interface. **This is the most crucial choice !**


- Here are the steps to follow [If nothing is specified, leave it as is]:

	- _Language_ : English
	- _Location_ : other/Europe/France
	- _Locales_ : United States, en_US.UTF-8
	- _Keyboard_ : French
	- **Hostname**: use server-"VOTRE_LOGIN_UGA
	- **Root Password**: a simple password is recommended, e.g. “root”. In this context, this poses no security problem. Check the “Show Password” box to be sure that the password you enter is the one you want.
	- _User Account_ - **Full Name**: your full name, e.g. “Jean Toto”.
	- **User Name**: enter your UGA login name.

![[Capture2.png]]
- 
	- **User Password** : enter a simple password, e.g. “etu”. Check the “Show Password” box to make sure you've entered the right password.
	- _Partition disks_ : Guided - use entire disk
	- _Partition disks_ : All files in one partition
	- _Partition disks_ : Yes
	- _Software Selection_ : check that “Debian desktop” is unchecked and that “ssh server” is checked

![[Capture3.png]]
- 
	- _Install GRUB_ : Yes
	- _Device for boot loader_ : `/dev/sda`  

⇒ The virtual machine is now launched. **Now it's time to shut down the machine before moving on to the next step!** To do this, log on to the root account and run the command `# poweroff` to shut down the machine cleanly.
 
>[!info]
>A partir de maintenant, c'est cette commande (`# poweroff`) qu'il faut utiliser pour éteindre la machine virtuelle

### Déplacement de l'image disque sur le serveur
- Utiliser la commande suivante pour déplacer l'image disque sur le serveur erebus4. Ce sera utile pour utliiser la machine virtuelle plus facilement
```Shell
S2.03-déplace-image-disque-sur-erebus4
```
>[!info]
>Il est possible de transférer une image ISO sur une clé USB, ce qui permet d'y accéder depuis n'importe quelle station équipée d'un port USB. Cela rend l'image portable et utilisable partout. Il suffit d'utiliser un outil pour rendre la clé USB bootable avec l'image ISO. Vous pouvez ensuite démarrer l'ordinateur depuis la clé USB pour accéder à l'image.
## Vérification du serveur Debian
- Il faut maintenant exécuter la commande qui suit pour lancer la machine virtuelle :
```Shell
S2.03-lance-machine-virtuelle
```

>[!warning]
>Attention à bien retenir cette commande car vous l'utiliserez chaque fois que vous voudrez lancer la machine virtuelle
- Pour vérifier que la fonctionnalité de la machine virtuelle, on peut exécuter la commande `ip a` ou `ip config` pour afficher les caractéristiques réseaux de la machine. Il suffit maintenant de vérifier que la machine est connectée au réseau
- Pour vérifier si la machine est connecté à l'extérieur, il sufft de vérifier qu'elle peut envoyer des paquets vers d'autres sites en utilisant la commande `ping`. Voici un exemple :
```sh
ping google.com
```
- Il est également possible de vérifier la présence ou l'abscence de Xorg avec la commande `dpkg -l | grep xorg`. L'abscence ici est essentiellement dût au fait que nous sommes sans interface graphique et que Xorg permet justement aux utilisateurs de disposer d'une interface graphique. Ainsi, ce logiciel ne nous est d'aucune utilité


## Redirection des ports et accès par SSH
Certaines redirections de port ont été mises en place afin de pouvoir accéder aux serveurs tournant sur notre machine virtuelle depuis des clients sur notre machine Linux :

| Service réseau | Port de la VM | Port sur la station Linux | Exemple d'utilisation depuis la station Linux |
| -------------- | ------------- | ------------------------- | --------------------------------------------- |
| SSH            | 22            | 2222                      | $ ssh toto@localhost -p 2222                  |
| HTTP           | 80            | 8080                      | URL: http://localhost:8080/                   |
| HTTPS          | 443           | 4443                      | URL: https://localhost:4443/                  |
| PostgreSQL     | 5432          | 5432                      | $ psql -h localhost -U postgres postgres      |
- Pour tester si tout fonctionne, il faut accéder au compte utilisateur simple de la machine virtuelle par SSH. Ensuite, il faut passer au compte root (`su` et avec comme mot de passe le mot de passe root) puis installer un paquet Debian, par exemple, micro :
```sh
apt-get update
apt-get install micro
```



- Avant de continuer, il peut être intéressant d'examiner les informations concernant les systèmes de fichiers et les périphériques de stockage, y compris leurs emplacements, leurs points de montage dans l'arborescence de fichiers, leurs options de montage, et d'autres paramètres. La commande est :
```ssh
/etc/fstab
```
![[Pasted image 20240606105709.png]]

Avant de passer à l'installation des logiciels,  afficher l'état actuel du service `ssh` :
```ssh
systemctl status ssh
```
![[Pasted image 20240606110456.png]]
# Installation de logiciels
>[!warning] Privilèges root
>Pour la majorité des commandes qui suivent, il est nécessaire d'avoir tous les droits, notamment pour l'installation de logiciels. Pour pouvoir passer en root, exécuter la commande : `su`. Pour les commandes ne nécessitant pas de privilèges root, un `$` sera placé devant la commande
## Apache
- Installer Apache2 en lançant les commandes suivantes :
```Shell
apt install apache2
service apache2 start
```
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
$ telnet localhost 80 #Il faut taper
Trying ::1...
Connected to localhost.
Escape character is '^]'.
$ HEAD / HTTP/1.0 #Il faut taper

HTTP/1.1 200 OK
[...]
```

- On peut également afficher la page Web sur la machine hôte. Pour cela, il faut rediriger un port de la machine hôte (`8080` par exemple) au port 80 (port par défaut des serveurs Web) sur la machine virtuelle. Il suffit maintenant de se connecter à l'URL suivante sur la machine hôte :
```Link
http://localhost:8080
```
- Avant de passer à l'étape suivant, afficher l'état actuel du service :
```ssh
systemctl status apache2
```
![[Pasted image 20240606110112.png]]
## PostgreSql
- Installer PostgreSql en exécutant la commande :
```Shell
apt install postgresql
```
- Pour vérifier l'installation du logiciel, se connecter sur le compte postgres :
```Shell
su - postgres
```
- Pour faire appraître les bases de données par défaut, exécuter la commande :
```Shell
psql -l
```

Il est maintenant possible de faires quelques tâches simples, en se connectant localement au serveur postgreSQL (Commande `psql`) :
1. **Créer un utilisateur avec comme nom votre login :** `CREATE USER votre_login WITH password = 'xxx'`
2. **Créer une base dont le propriétaire est votre utilisateur :**
```SQL
CREATE DATABASE ma_base WITH OWNER = votre_nom_uga;
```
3. **Pour créer une table simple dans ma base de données, il faut que je me place dans cette base :**
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

- Effectuer une requête pour vérifier que les uplets ont bient été ajoutés
![[Interrogation SQL depuis machine virtuelle.png]]

- Il faut maintenant modifier certains fichiers pour que cette base PostgreSQL soit accessible par une machine Linux. Pour se faire :
	1. **Modifier `postgresql.conf` :**
	   ⇒ Rechercher dans la catégorie *CONNECTIONS AND AUTHENTICATION* et décommenter la ligne `listen_addresses = '*'`
	2. **Modifier `nano /etc/postgresql/15/main/pg_hba.conf` :**
	   ⇒ Dans la catégorie *#IPv4 remote connections:*, ajouter la règle suivante : `host  all all 0.0.0.0/0 scram-sha-256`
	3. Il faut maintenant repasser en **root** et relancer le serveur :
```sh
service postgresql restart
```

- On peut maintenant se connecter à la base SQL depuis la station Linux hébergeant la machine virtuelle :
```sh
psql -h localhost ma_base -U votre_nom_UGA
```

- Dans la machine virtuelle, afficher de nouveau la liste des bases :
```SQL
psql -l
```
![[liste bases.png]]

- On peut maintenant lister le contenu de la table `pg_shadow` pour vérifier que les mots de passe sont bien hâches avec **SHA-256**. Pour cela, sur la machine virtuelle, se connecter en postgres et exécuter la commande suivante  :
```SQL
SELECT * FROM pg_shadow;
```
![[pg_shadow.png]]
- Avant de passer à l'étape suivant, afficher l'état actuel du service :
```ssh
systemctl status postgres
```
![[Pasted image 20240606110319.png]]
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
1. **Modifier `etc/apache2/conf-enabled/phppgadmin.conf`**
   ⇒ Dans la catégorie *Only allow connections from localhost*, enlever `Require local` et remplacer par `Require all granted`
2. **Modifier `/usr/share/phppgadmin/classes/database/Connections.php` :**
   ⇒ A la ligne 79, *ajouter PostgresSQL 15* : `cas '15' : return 'Postgres':break;` remplaçant la ligne `cas '14' : return 'Postgres':break;`
- Relancer Apache2 pour appliquer les modifications :
```sh
systemctl reload apache2
```
- Ouvrir une page internet et rentrer le lien `http://localhost/phppgadmin/`
- Une fois sur la page, se connecter avec les identifiants crées pour votre user (Crées dans la partie installation de PostgresSQL) puis afficher la tables pour `ma_base` :
![[phppgadmin.png]]