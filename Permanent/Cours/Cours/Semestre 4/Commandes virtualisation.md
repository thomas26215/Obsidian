D'accord, en me basant sur le document que tu as fourni, voici une liste des commandes mentionnées, classées par catégorie, **avec leurs paramètres courants** :

## Commandes Unix et Docker Mentionnées dans le Cours

### 1. Commandes d'Isolation et de Gestion des Ressources (Unix)

*   **`chroot `**: Change la racine du système de fichiers pour le processus actuel.
*   **`unshare [options]`**: Crée de nouveaux namespaces.
    *   `--map-root-user`: Mappe l'utilisateur root dans le namespace.
    *   `-r`: Crée un nouveau mount namespace.
    *   `--pid`: Crée un nouveau PID namespace.
    *   `--fork`: Fork le processus après la création du namespace.
    *   `--mount-proc`: Monte le système de fichiers /proc dans le namespace.
    *   `--net`: Crée un nouveau network namespace.
*   **`clone()`**: (Appel système, généralement utilisé dans les programmes C) Crée un nouveau processus enfant avec des namespaces isolés. Nécessite des paramètres de configuration complexes (non détaillés ici).
*   **`setns()`**: (Appel système, généralement utilisé dans les programmes C) Associe un processus à un namespace existant. Nécessite des paramètres de configuration complexes (non détaillés ici).
*   **`cgcreate -g :`**: Crée un nouveau control group (cgroup).
*   **`cgdelete [-r] `**: Supprime un cgroup existant.
    *   `-r`: Supprime récursivement tous les sous-groupes.
*   **`cgget [-r] `**: Affiche les paramètres d'un cgroup.
    *   `-r`: Affiche récursivement les paramètres de tous les sous-groupes.
*   **`cgset -r = `**: Modifie les paramètres d'un cgroup.
    *   `-r`: Applique récursivement les paramètres à tous les sous-groupes.
*   **`cgexec -g : `**: Exécute une commande dans un cgroup.
*   **`systemd-cgls`**: Affiche les cgroups gérés par systemd.
*   **`systemd-cgtop`**: Affiche l'utilisation des ressources par cgroup.
*   **`mount`**: Affiche les systèmes de fichiers montés.
*   **`ps aux`**: Affiche les processus en cours d'exécution.
    *   `a`: Affiche les processus de tous les utilisateurs.
    *   `u`: Affiche l'utilisateur et d'autres informations détaillées.
    *   `x`: Affiche les processus sans terminal de contrôle.
*   **`whoami`**: Affiche le nom d'utilisateur courant.
*   **`ip addr`**: Affiche les adresses IP.

### 2. Commandes Docker (Gestion des Images, Conteneurs, Volumes, Réseaux)

*   **`docker`** (commande principale pour interagir avec Docker)
*   **`docker pull [:]`**: Télécharge une image depuis un registre.
*   **`docker build [options] `**: Construit une image à partir d'un Dockerfile.
    *   `-t [:]`: Attribue un nom et un tag à l'image.
    *   `--build-arg `: Définit un argument de construction.
*   **`docker push [:]`**: Envoie une image vers un registre.
*   **`docker images`**: Liste les images disponibles localement.
*   **`docker rmi |`**: Supprime une image.
*   **`docker run [options] [:] [commande] [arguments]`**: Crée et démarre un conteneur à partir d'une image.
    *   `-d`: Démarre le conteneur en mode détaché (en arrière-plan).
    *   `-i`: Maintient l'entrée standard ouverte (interactif).
    *   `-t`: Alloue un pseudo-TTY (terminal).
    *   `--name `: Attribue un nom au conteneur.
    *   `-p :`: Publie un port du conteneur sur l'hôte.
    *   `-v :`: Monte un volume.
    *   `-e `: Définit une variable d'environnement.
        *   `--rm` : Supprime automatiquement le conteneur lorsqu'il s'arrête
*   **`docker start |`**: Démarre un conteneur arrêté.
*   **`docker stop [options] |`**: Arrête un conteneur en douceur.
    *   `-t `: Temps d'attente avant de forcer l'arrêt.
*   **`docker kill |`**: Force l'arrêt d'un conteneur.
*   **`docker restart |`**: Redémarre un conteneur.
*   **`docker rm [options] |`**: Supprime un conteneur arrêté.
    *   `-f`: Force la suppression du conteneur s'il est en cours d'exécution.
*   **`docker ps [options]`**: Liste les conteneurs en cours d'exécution.
    *   `-a`: Affiche tous les conteneurs (en cours d'exécution et arrêtés).
    *   `-q`: Affiche uniquement les IDs des conteneurs.
*   **`docker exec [options] | `**: Exécute une commande dans un conteneur en cours d'exécution.
    *   `-i`: Maintient l'entrée standard ouverte (interactif).
    *   `-t`: Alloue un pseudo-TTY (terminal).
    *   `-d`: Exécute la commande en arrière-plan.
    *   `-u `: Exécute la commande en tant qu'un utilisateur spécifique.
*   **`docker logs [options] |`**: Affiche les journaux d'un conteneur.
    *   `-f`: Suit les journaux en temps réel.
    *   `--tail `: Affiche les dernières lignes du journal.
*   **`docker inspect |||`**: Affiche des informations détaillées sur un conteneur, une image, etc.
*   **`docker port |`**: Affiche le mapping de ports pour un conteneur.
*   **`docker top |`**: Affiche les processus en cours d'exécution dans un conteneur.
*   **`docker stats [options] |`**: Affiche les statistiques d'utilisation des ressources d'un conteneur.
    *   `--no-stream`: Affiche les statistiques une seule fois sans actualisation.
*   **`docker volume create [options] `**: Crée un volume.
    *   `-d `: Spécifie le driver de volume à utiliser.
*   **`docker volume ls`**: Liste les volumes.
*   **`docker volume inspect `**: Affiche des informations sur un volume.
*   **`docker volume rm `**: Supprime un volume.
*   **`docker network create [options] `**: Crée un réseau.
    *   `-d `: Spécifie le driver de réseau à utiliser.
        `--subnet `: Spécifie la sous-réseau.
*   **`docker network ls`**: Liste les réseaux.
*   **`docker network inspect `**: Affiche des informations sur un réseau.
*   **`docker network connect  |`**: Connecte un conteneur à un réseau.
*   **`docker network disconnect  |`**: Déconnecte un conteneur d'un réseau.
*   **`docker network rm `**: Supprime un réseau.
