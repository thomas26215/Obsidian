## Commandes Unix et Docker – Liste Complète avec Options

---

### 1. Commandes Unix pour l'isolation et les ressources système

#### 🔐 Isolation via namespaces

- **`chroot <new_root>`**
  - Change la racine du système de fichiers pour le processus courant.

- **`unshare [options] <commande>`**
  - Crée de nouveaux namespaces pour exécuter une commande isolée.
  - **Options utiles :**
    - `--map-root-user` : Mappe l'utilisateur root dans l'espace utilisateur.
    - `--fork` : Fork un processus pour l'exécuter dans le namespace.
    - `--mount-proc` : Monte `/proc` dans un namespace PID.
    - `--pid` : Nouveau PID namespace.
    - `--net` : Nouveau namespace réseau.
    - `--uts` : Nouveau hostname.
    - `--ipc` : Nouveau namespace IPC.
    - `--mount` : Nouveau namespace de montage.
    - `--user` : Nouveau namespace utilisateur.
    - `--cgroup` : Nouveau namespace cgroup.

- **Appels systèmes (niveau C)** :
  - `clone()` : Crée un processus avec des namespaces personnalisés.
  - `setns()` : Attache un processus à un namespace existant.

#### 📊 Gestion des cgroups (control groups)

- **`cgcreate -g <subsys>:<groupe>`** : Crée un nouveau cgroup.
- **`cgdelete [-r] <subsys>:<groupe>`** : Supprime un cgroup.
  - `-r` : Suppression récursive des sous-groupes.
- **`cgget [-r] <subsys>:<groupe>`** : Affiche les paramètres d’un cgroup.
- **`cgset -r <clé>=<valeur> <subsys>:<groupe>`** : Modifie les paramètres d’un cgroup.
- **`cgexec -g <subsys>:<groupe> <commande>`** : Exécute une commande dans un cgroup.

#### 🧰 Utilitaires système

- **`systemd-cgls`** : Affiche l’arborescence des cgroups gérés par systemd.
- **`systemd-cgtop`** : Affiche en temps réel l’utilisation des ressources par cgroup.
- **`mount`** : Liste les systèmes de fichiers montés.
- **`ps aux`** : Affiche tous les processus actifs.
- **`whoami`** : Affiche l’utilisateur courant.
- **`ip addr`** : Affiche les interfaces et adresses IP.

---

### 2. Commandes Docker (conteneurs, images, réseaux, volumes)

#### 🐳 Gestion des images

- **`docker pull <image>[:tag]`** : Télécharge une image.
- **`docker build [options] <chemin>`** : Construit une image.
  - `-t <nom>:<tag>` : Attribue un nom et tag.
  - `--build-arg <clé>=<valeur>` : Argument de build.
- **`docker push <image>[:tag]`** : Envoie une image sur un registre.
- **`docker images`** : Liste les images locales.
- **`docker rmi <image>`** : Supprime une image.

#### 🚀 Exécution de conteneurs

- **`docker run [options] <image> [commande]`** : Démarre un conteneur.
  - `-d` : Mode détaché (background).
  - `-i` : Mode interactif.
  - `-t` : Alloue un pseudo-TTY.
  - `--rm` : Supprime le conteneur à l'arrêt.
  - `--name <nom>` : Nom du conteneur.
  - `-p <hôte>:<conteneur>` : Redirige un port.
  - `-v <hôte>:<conteneur>` : Monte un volume.
  - `-e <clé>=<valeur>` : Variable d’environnement.
  - `--entrypoint <cmd>` : Remplace l’entrée par défaut.
  - `--network <nom>` : Spécifie le réseau.
  - `--hostname <nom>` : Définit le hostname du conteneur.

#### ⚙️ Gestion des conteneurs

- **`docker start <nom|id>`** : Démarre un conteneur arrêté.
- **`docker stop [-t <secondes>] <nom|id>`** : Stoppe un conteneur proprement.
- **`docker kill <nom|id>`** : Stoppe brutalement.
- **`docker restart <nom|id>`** : Redémarre un conteneur.
- **`docker rm [-f] <nom|id>`** : Supprime un conteneur.
- **`docker ps [-a | -q]`** : Liste les conteneurs.
  - `-a` : Tous (même arrêtés).
  - `-q` : Affiche uniquement les IDs.

#### 🛠️ Exécution dans un conteneur

- **`docker exec [options] <nom|id> <commande>`** : Lance une commande dans un conteneur.
  - `-i`, `-t`, `-d`, `-u <utilisateur>`

#### 📋 Inspection & logs

- **`docker logs [options] <nom|id>`** : Affiche les logs.
  - `-f` : Suivi en temps réel.
  - `--tail <nb>` : Limite les lignes.
- **`docker inspect <nom|id>`** : Donne les détails internes.
- **`docker port <nom|id>`** : Affiche le mappage des ports.
- **`docker top <nom|id>`** : Affiche les processus.
- **`docker stats [options] <nom|id>`** : Stats d'utilisation.
  - `--no-stream` : Affiche une seule fois.

#### 📦 Gestion des volumes

- **`docker volume create [-d <driver>] <nom>`** : Crée un volume.
- **`docker volume ls`** : Liste les volumes.
- **`docker volume inspect <nom>`** : Infos détaillées.
- **`docker volume rm <nom>`** : Supprime un volume.

#### 🌐 Gestion réseau Docker

- **`docker network create [-d <driver>] [--subnet <CIDR>] <nom>`**
- **`docker network ls`** : Liste les réseaux.
- **`docker network inspect <nom>`** : Infos détaillées.
- **`docker network connect <réseau> <conteneur>`** : Ajoute le conteneur au réseau.
- **`docker network disconnect <réseau> <conteneur>`** : Retire le conteneur du réseau.
- **`docker network rm <nom>`** : Supprime un réseau.


