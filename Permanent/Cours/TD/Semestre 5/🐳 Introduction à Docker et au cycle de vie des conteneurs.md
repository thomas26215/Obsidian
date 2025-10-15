---
MOOC: "[[Cours]]"
Ressource: "R5.09 : 🐳 Virtualisation"
Cours: "TP 1 : Docker run"
Date:
tags:
Complete: false
Learned: false
---
## 1. Introduction à la conteneurisation

La conteneurisation est une technologie de virtualisation légère permettant d’exécuter des applications dans des environnements isolés appelés **conteneurs**.  
Contrairement aux machines virtuelles, les conteneurs partagent le **noyau du système hôte**, mais disposent de leur propre système de fichiers, réseau et espace de processus.  
L’outil le plus populaire pour la conteneurisation est **Docker**.

Un conteneur est donc un environnement portable, reproductible et rapide à lancer. Il repose sur des **images**, qui servent de modèles pour créer des instances de conteneurs.

---

## 2. Installation et fonctionnement de Docker

L’installation de Docker se fait à l’aide du gestionnaire de paquets du système (par exemple `apt` sur Debian/Ubuntu).  
Une fois installé, il est recommandé d’ajouter l’utilisateur courant au groupe `docker` afin d’exécuter les commandes sans avoir recours à `sudo`.

Deux commandes permettent de vérifier la bonne installation :

- `docker --version` : indique la version du moteur Docker ;
    
- `docker info` : fournit des détails sur le moteur, les conteneurs, les réseaux, le stockage, et la configuration du système.
    

Docker fonctionne selon une architecture client-serveur :

- le **client Docker** interprète les commandes de l’utilisateur ;
    
- le **daemon Docker** (dockerd) exécute les conteneurs et gère les ressources.
    

---

## 3. Cycle de vie d’un conteneur

### 3.1 Création et exécution

Un conteneur se crée à partir d’une **image** :

```bash
docker run --rm -it debian bash
```

Cette commande :

- télécharge l’image Debian (si absente localement) ;
    
- crée un conteneur temporaire (`--rm`) ;
    
- ouvre une session interactive (`-it`) avec le shell `bash`.
    

À l’intérieur, le conteneur se comporte comme un système Debian minimal.  
On peut y installer des paquets via `apt`, naviguer dans l’arborescence, et exécuter des programmes.

### 3.2 Éphémérité

Une caractéristique essentielle des conteneurs est leur **éphémérité**.  
Lorsqu’un conteneur est supprimé, toutes les modifications internes (fichiers, paquets installés, etc.) sont perdues, sauf si elles sont stockées dans un volume externe.  
Ainsi, installer un éditeur (comme `vim`) puis relancer un nouveau conteneur ne conserve pas l’installation précédente.

### 3.3 Observation et gestion

Pendant l’exécution, on peut observer les conteneurs actifs via :

```bash
docker ps
```

Lorsqu’un conteneur est arrêté ou supprimé, il disparaît de cette liste.

---

## 4. Isolation réseau des conteneurs

Chaque conteneur Docker est isolé dans son propre **espace réseau**, mais peut être relié à d’autres conteneurs via des **réseaux Docker**.

### 4.1 Réseau par défaut

Par défaut, Docker connecte tous les conteneurs au réseau `bridge`.  
Ce réseau attribue une adresse IP interne à chaque conteneur.  
L’installation des paquets `iputils-ping` et `iproute2` permet de tester la connectivité :

```bash
apt update
apt install -y iputils-ping iproute2
ip addr
ping <adresse_IP_autre_conteneur>
```

Les conteneurs du même réseau `bridge` peuvent communiquer entre eux.

### 4.2 Réseaux personnalisés

Docker permet également de créer des réseaux dédiés :

```bash
docker network create --driver bridge test
```

En lançant un conteneur avec `--network test`, celui-ci sera isolé des conteneurs du réseau par défaut.  
Seuls les conteneurs rattachés au même réseau peuvent s’échanger des paquets.  
Cela illustre l’un des grands avantages de Docker : une **isolation réseau fine et maîtrisée**.

---

## 5. Gestion des données avec les volumes

Par défaut, les fichiers créés à l’intérieur d’un conteneur disparaissent à sa suppression.  
Pour conserver les données, Docker propose les **volumes**, qui permettent de lier un dossier de l’hôte à un dossier du conteneur.

Exemple :

```bash
docker run -v "/tmp/toto:/home/toto" --rm -it debian bash
```

Le dossier `/tmp/toto` de l’hôte est alors monté dans `/home/toto` du conteneur.  
Toute modification dans ce répertoire est immédiatement visible des deux côtés.  
Ainsi, les volumes permettent de **partager et de persister** les données au-delà de la durée de vie d’un conteneur.

---

## 6. Nommage et gestion des conteneurs

Il est possible d’attribuer un **nom explicite** à un conteneur :

```bash
docker run --name apache php:apache
```

Le nom facilite la gestion :

- `docker stop apache` : arrête le conteneur ;
    
- `docker start apache` : le redémarre ;
    
- `docker rm apache` : le supprime.
    

Pour les conteneurs non nommés, il faut utiliser leur **identifiant** (`docker ps -a`).

Les conteneurs peuvent aussi exécuter automatiquement des services (ici Apache), sans interface interactive.

---

## 7. Exposition de ports

Pour rendre un service accessible depuis l’extérieur, Docker propose une **redirection de ports** :

```bash
docker run --name apache -p 8000:80 php:apache
```

Le port `80` du conteneur (port standard du serveur web Apache) est redirigé vers le port `8000` de l’hôte.  
Ainsi, le service est consultable via `http://localhost:8000`.  
Cette redirection permet d’exposer des applications web, des API ou des bases de données à l’extérieur du conteneur, tout en gardant une séparation nette entre l’hôte et le service.

---

## 8. Variables d’environnement

Docker permet de configurer dynamiquement les conteneurs grâce aux **variables d’environnement** :

```bash
docker run -e TOTO=salut --rm -it debian bash
```

Dans le conteneur :

```bash
echo $TOTO
env
```

Ces variables servent à paramétrer les services sans modifier le code ou l’image.  
Elles sont très utiles pour la configuration d’applications (par exemple, indiquer un mot de passe, un port ou un mode de déploiement).

---

## 9. Exemple d’application : mini site PHP

Pour illustrer l’utilisation combinée des volumes et des variables d’environnement, on peut créer un petit site PHP affichant un message personnalisé :

**index.php :**

```php
Bonjour
<?php
echo $_ENV['NOM'];
?>
```

**Commande de lancement :**

```bash
docker run -e NOM=Marie -p 8080:80 -v "$PWD:/var/www/html" php:apache
```

Ce conteneur exécute Apache et PHP, affiche la page à l’adresse [http://localhost:8080](http://localhost:8080), et récupère la variable d’environnement `NOM` passée au lancement.  
Le résultat visible est :

```
Bonjour Marie
```

Cet exemple illustre parfaitement l’intérêt de Docker pour le **déploiement rapide d’applications web isolées et configurables**.

---

## 10. Conclusion

Ce TP a permis de comprendre les fondements de Docker et le fonctionnement des conteneurs :

- un conteneur est une **instance d’une image** ;
    
- il est **léger, isolé et éphémère** ;
    
- la persistance se fait via les **volumes** ;
    
- la communication se gère par les **réseaux Docker** ;
    
- la configuration se fait par les **variables d’environnement**.
    

Docker simplifie grandement la mise en place, le déploiement et la maintenance des environnements logiciels.  
Il constitue aujourd’hui un outil incontournable pour les développeurs, les administrateurs systèmes et les ingénieurs DevOps.