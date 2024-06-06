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


- To check and modify Qemu/KVM settings, open the file `S2.03-commun`:
```Shell
nano /users/info/pub/bin/S2.03-commun
```

1. **Image path declaration**:
```ssh
image_locale="/donnees/TP-infobut/Debian-S2.03-$LOGNAME.img"
image_nfs="/users/Stockage-HDD/images-kvm/S2.03/images/Debian-S2.03-$LOGNAME.img"
```
    
2. **Image existence case management**:
    
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

    
3. **Disk configuration for QEMU**:
```ssh
drive="format=raw,file=$image,discard=unmap
```
    
4. **ISO path declaration**:
```ssh
iso=$(ls /usr/local/images-ISO/debian-*-netinst.iso)
```
    
5. **(Commented) Launch of QEMU**:

```ssh
# qemu-system-x86_64 -drive $drive -cdrom $iso -boot d -m 2G
```

The script checks and creates the required disk image, chooses between a local image or one on NFS, configures the disk for QEMU, and prepares the ISO path for launching the virtual machine.

### Follow the standard installation procedure
- Now follow the standard procedure to install the system

>[!Warning]
>You need to install Debian without a graphical interface. **This is the most crucial choice !**. In fact, we won't be using a graphical interface for the whole process, as our aim is to create a virtual machine that runs solely on command lines.


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
>From now on, use this command (`# poweroff`) to shut down the virtual machine

### Déplacement de l'image disque sur le serveur
- Use the following command to move the disk image to the erebus4 server. This will make it easier to use the virtual machine
```Shell
S2.03-déplace-image-disque-sur-erebus4
```
>[!info]
>An ISO image can be transferred to a USB stick, enabling access from any workstation with a USB port. This makes the image portable and usable anywhere. Simply use a tool to make the USB key bootable with the ISO image. You can then boot the computer from the USB key to access the image.
## Vérification du serveur Debian
- The following command must now be executed to start the virtual machine:
```Shell
S2.03-lance-machine-virtuelle
```

>[!warning]
>Make sure you remember this command, as you'll be using it every time you want to launch the virtual machine.
- To check the virtual machine's functionality, you can run the `ip a` command to display the machine's network characteristics. Now we just need to check that the machine is connected to the network
- To check that the machine is connected to the outside world, simply check that it can send packets to other sites using the `ping` command. Here's an example:
```sh
ping google.com
```
- It is also possible to check the presence or absence of Xorg with the command `dpkg -l | grep xorg`. The absence here is essentially due to the fact that we are without a graphical interface, and Xorg provides users with a graphical interface. As a result, this software is of no use to us.


## Redirection des ports et accès par SSH
Some port redirections have been set up in order to access servers running on our virtual machine from clients on our Linux machine:

| Service réseau | Port de la VM | Port sur la station Linux | Exemple d'utilisation depuis la station Linux |
| -------------- | ------------- | ------------------------- | --------------------------------------------- |
| SSH            | 22            | 2222                      | $ ssh toto@localhost -p 2222                  |
| HTTP           | 80            | 8080                      | URL: http://localhost:8080/                   |
| HTTPS          | 443           | 4443                      | URL: https://localhost:4443/                  |
| PostgreSQL     | 5432          | 5432                      | $ psql -h localhost -U postgres postgres      |
- To test whether everything is working, you need to access the virtual machine's simple user account via SSH. Then switch to the root account (`su` and with the root password) and install a Debian package, e.g. micro:
```sh
apt-get update
apt-get install micro
```



- Before proceeding, it may be worthwhile to examine information about file systems and storage devices, including their locations, mount points in the file tree, mount options, and other parameters. The command is:
```ssh
/etc/fstab
```
![[Pasted image 20240606105709.png]]

Before proceeding with software installation, display the current status of the `ssh` service:
```ssh
systemctl status ssh
```
![[Pasted image 20240606110456.png]]
# Installation de logiciels
>[!warning] Root privileges
>Most of the commands below require full root privileges, especially for software installation. To become root, execute the command: `su`. For commands not requiring root privileges, a `$` will be placed in front of the command.

⇒ By the way, vous avez besoin d'avoir votre machine virtuelle de lancée (**Recall command to start virtual machine:** `S2-03-lance-machine-virtuelle)
## Apache
- Install Apache2 with the following commands:
```Shell
apt install apache2
service apache2 start
```
- Run the following command to check that the software has been installed correctly:
```Shell
systemctl status apache2
```
- If by chance Apache has not started:
```Shell
systemctl start apache2
```
- It's not possible to display a Web page graphically (we've installed the virtual machine for command-line use only). However, it is possible to connect to the Apache server with the command `telnet` and enter the string `HEAD/HTTP/1.0` followed by two carriage returns:
```Shell
$ telnet localhost 80 #Il faut taper
Trying ::1...
Connected to localhost.
Escape character is '^]'.
$ HEAD / HTTP/1.0 #Il faut taper

HTTP/1.1 200 OK
[...]
```

- You can also display the Web page on the host machine.To do this, redirect a port on the host machine (e.g. `8080`) to port 80 (the default port for Web servers) on the virtual machine. Now simply connect to the following URL on the host machine:
```Link
http://localhost:8080
```
- Before proceeding to the next step, display the current service status:
```ssh
systemctl status apache2
```
![[Pasted image 20240606110112.png]]
## PostgreSql
- Install PostgreSql by running the command :
```Shell
apt install postgresql
```
- To check that the software has been installed, connect to the postgres account:
```Shell
su - postgres
```
- To display the default databases, run the command :
```Shell
psql -l
```

It is now possible to perform a few simple tasks, by connecting locally to the postgreSQL server (Command `psql`) :
1. **Create a user with your login name:** `CREATE USER your_login WITH password = 'xxx'`.
2. **Create a database whose owner is your user:**
```SQL
CREATE DATABASE ma_base WITH OWNER = votre_nom_uga;
```
3. **To create a simple table in my database, I need to place myself in that database:**
```SQL
\c ma_base
```
4. **Create a table:**
```SQL
CREATE TABLE ma_table (
    id SERIAL PRIMARY KEY,
    nom VARCHAR(100),
    age INT
);
```
5. **Insert a few lines:**
```SQL
INSERT INTO ma_table (nom, age) VALUES ('Alice', 30);
INSERT INTO ma_table (nom, age) VALUES ('Bob', 25);
INSERT INTO ma_table (nom, age) VALUES ('Charlie', 35);
```

- Run a query to check that uplets have been added soon
![[Interrogation SQL depuis machine virtuelle.png]]

- We now need to modify certain files so that this PostgreSQL database can be accessed by a Linux machine. To do this :
	1. **Edit ` postgresql.conf` :**
	   ⇒ Search in the category *CONNECTIONS AND AUTHENTICATION* and uncomment the line `listen_addresses = '*'`.
	2. **Edit `nano /etc/postgresql/15/main/pg_hba.conf` :**
	   ⇒ In the *#IPv4 remote connections:* category, add the following rule: `host all all 0.0.0.0/0 scram-sha-256`.
	3. Now you need to switch back to **root** and restart the server:
```sh
service postgresql restart
```

- We can now connect to the SQL database from the Linux station hosting the virtual machine:
```sh
psql -h localhost ma_base -U votre_nom_UGA
```

- In the virtual machine, display the list of databases again:
```SQL
psql -l
```
![[liste bases.png]]

- We can now list the contents of the `pg_shadow` table to check that the passwords are indeed hashed with **SHA-256**. To do this, on the virtual machine, connect to postgres and run the following command:
```SQL
SELECT * FROM pg_shadow;
```
![[pg_shadow.png]]
- Before proceeding to the next step, display the current service status:
```ssh
systemctl status postgres
```
![[Pasted image 20240606110319.png]]
## Installer PHP
- Install PHP by executing the following commands while `root`.
```sh
apt install php-common libapache2-mod-php php-cli
/etc/init.d/apache2 start
```
>[!info] `/etc/init.d/apache2 start` is used to start Apache when it is installed, and `/etc/init.d/apache2 stop` is used to stop it.

- To test the installation, place an `info.php` file in the `var/www/html/` directory (Command `touch` possible ⇒ `touch var/www/html/info.php`) then enter the following code:
```PHP
<?php
phpinfo();
phpinfo(INFO_MODULES);
?>
```
- Now return to your host machine and, in your web browser, enter the following link: `http://localhost:8080/info.php`. Normally, a page containing the main features of your PHP installation should appear

![[Pasted image 20240606135933.png]]
## Installer PhpPgAdmin
-  Install PhpPgAdmin by executing the following command while `root` :
```sh
apt -y install phppgadmin php-pgsql
```
- Some files now need to be modified:
1. **Edit `etc/apache2/conf-enabled/phppgadmin.conf`**.
   ⇒ In the *Only allow connections from localhost* category, remove `Require local` and replace with `Require all granted`.
2. **Edit `/usr/share/phppgadmin/classes/database/Connections.php` :**
   ⇒ On line 79, *add PostgresSQL 15*: `case '15': return 'Postgres':break;` replacing line `case '14': return 'Postgres':break;`
- Restart Apache2 to apply changes:
```sh
systemctl reload apache2
```
- Open a web page and enter the link `http://localhost/phppgadmin/`.
- Once you're on the page, log in with the credentials you created for your user (created in the PostgresSQL installation section), then display the tables for `my_base` :
![[phppgadmin.png]]

# Transférer un fichier de la machine hôte à la machine virtuelle
- Sur votre machine virtuelle, effectuer les commandes suivantes :
```ssh
/sbin/blkid
scp -Crp loginUGA@transit.iut2.univ-grenoble-alpes.fr:/users/info/etu1a/loginUGA/Downloads/page_sae_S2.03.php /var/www/html
```

⇒ Cela permet de transférer un fichier dpuis votre machine hôte vers votre machine virtuelle

![[Pasted image 20240606144416.png]]