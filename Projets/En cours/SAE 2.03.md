# Installation de la machine virtuelle
## Préparation de l'image ISO

### Téléchargement et vérification de l'image ISO
- L'image ISO et les fichiers permettant de <mark style="background: #FFB86CA6;">vérifier son intégrité</mark> sont disponibles ici`https://cdimage.debian.org/cdimage/release/current/amd64/iso-cd/`
- Pour noter cas, l'image ISO est déjà téléchargée et trouve dans le répertoire `/usr/local/images-ISO/`. Vérifier son intégrité avec la commande suivante :
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

⇒ Cela étant fait la machine virtuelle se lance. **Il faut maintenant éteindre la machine avant de pourvoir passer à l'étape suivant !** Il faut pour cela se loger sur le compte root (==Identifiant = Hostname et Mdp = Password==) et exécuter la commande `# poweroff` pour éteindre proprement la machine.
 
>[!info]
>A partir de maintenant, c'est cette commande (`# poweroff`) qu'il faut utiliser pour éteindre la machine virtuelle

### Déplacement de l'image disque sur le serveur
- Utiliser la commande suivante pour déplacer l'image disque sur le serveur erebus4. Ce sera utile pour utliiser la machine virtuelle plus facilement
```Shell
S2.03-déplace-image-disque-sur-erebus4
```

## Vérification du serveur Debian
- Il faut maintenant exécuter la commande qui suit pour lancer la machine virtuelle :
```Shell
S2.03-lance-machine-virtuelle
```

>[!warning]
>Attention à bien retenir cette commande car vous l'utiliserez chaque fois que vous voudrez lancer la machine virtuelle


## Redirection des ports et accès par SSH
// Compéter

# Installation de logiciels
## Apache
- Installer Apache2 en lançant les commandes suivantes :
```Shell
apt install apache2
service apache2 start
```
> [!Warning]
> Il faut déjà être **utilisateur root** pour avoir toutes les permissions, notamment celle d'installer un logiciel : `sudo -i` ou `su -i`
- Exécuter la commande suivante pour vérifier que le logiciel est bien installé :
```Shell
systemctl status apache2
```
- Si par malheur Apache n'a pas démarré :
```Shell
systemctl start apache2
```
- Bien qu'il n'est pas possible d'afficher une page Web graphiquement (nous avons installé la machine virtuelle uniquement pour les lignes de commande). Il est cependant possible de se connecter  au serveur Apache avec la commande `telnet` et en entrant la chaîne de charactère `HEAD/HTTP/1.0` suivit de deux retours à la ligne :
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

