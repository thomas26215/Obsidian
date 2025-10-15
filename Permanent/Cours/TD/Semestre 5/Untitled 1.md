
## 🧩 1. Construction d’une première image

### 1.1. Création d’une image de base

Le TP débute par la création d’un premier répertoire (`etape-base`) contenant un simple fichier texte nommé `test` avec le contenu `Hello world`.

Le **Dockerfile** correspondant spécifie :

- une **image de base** : `debian:stable` ;
    
- la **copie du fichier test** dans le conteneur (`COPY`) ;
    
- l’**installation d’un paquet** (ici `vim`) à l’aide de `RUN apt install -y vim`.
    

Une fois ce fichier rédigé, la commande suivante permet de construire l’image :

```bash
docker build -t monimage .
```

L’option `-t monimage` permet d’attribuer un **tag** à l’image, facilitant son identification et son exécution ultérieure.

Lorsqu’un conteneur est lancé à partir de cette image avec `--rm`, on peut observer que les modifications effectuées à l’intérieur (par exemple une édition du fichier `test`) ne persistent pas après l’arrêt du conteneur, car celui-ci est éphémère.

---

### 1.2. Compréhension du cache de build

Docker construit une image en **empilant des couches** (layers) correspondant à chaque instruction du Dockerfile (`FROM`, `COPY`, `RUN`, etc.).  
Ces couches sont **mises en cache** afin d’accélérer les reconstructions.

Lors d’une recompilation :

- si seule l’instruction `RUN apt install` change (ex. passage de `vim` à `emacs`), **les couches précédentes sont réutilisées** ;
    
- si le contenu copié (via `COPY`) est modifié, la couche correspondante **et toutes les suivantes** sont reconstruites.
    

Ce mécanisme permet d’optimiser considérablement le temps de build et l’utilisation des ressources.

---

## ⚙️ 2. L’instruction ENTRYPOINT

### 2.1. Comportement par défaut

Dans un nouveau répertoire (`etape-entrypoint`), un Dockerfile installe le paquet **netcat** (`nc`) et définit comme **entrypoint** la commande :

```dockerfile
ENTRYPOINT ["nc", "-l", "-p", "1337"]
```

Cette commande crée un **serveur TCP** écoutant sur le port 1337.  
Après avoir construit et lancé le conteneur en exposant ce port (`-p 1337:1337`), on peut s’y connecter depuis l’hôte via :

```bash
nc localhost 1337
```

Le terminal de l’hôte et celui du conteneur deviennent alors interconnectés.

---

### 2.2. Utilisation de variables d’environnement

Pour rendre le port configurable, on introduit une **variable d’environnement** `PORT`.  
Cependant, la commande `ENTRYPOINT` ne peut pas interpréter directement une variable.  
Il est donc nécessaire d’écrire un **script intermédiaire** (par exemple `start.sh`) :

```bash
#!/bin/bash
nc -l -p ${PORT:-1337}
```

Ce script est copié dans l’image et défini comme nouvel entrypoint :

```dockerfile
ENTRYPOINT ["/start.sh"]
```

Ainsi, le port d’écoute peut être personnalisé au lancement :

```bash
docker run -e PORT=8080 monimage
```

Si la variable n’est pas définie, le script utilise la valeur par défaut (1337).

---

## 💾 3. Gestion des volumes

### 3.1. Définition d’un volume

Dans un nouveau répertoire (`etape-volumes`), le Dockerfile utilise l’instruction :

```dockerfile
VOLUME ["/data"]
```

Cette directive indique à Docker que `/data` sera un **point de montage persistant**.  
Les fichiers créés dans ce répertoire ne sont **pas enregistrés dans l’image** ; ils sont stockés dans un volume externe.

Ainsi, après le build, un fichier placé dans `/data` n’apparaît pas dans un conteneur lancé depuis l’image, car Docker isole ce répertoire pour la persistance.

### 3.2. Option `-v`

Même sans l’instruction `VOLUME`, il est possible de monter un dossier externe lors de l’exécution :

```bash
docker run -v /mon/dossier/local:/data monimage
```

Cela permet d’échanger facilement des fichiers entre l’hôte et le conteneur.

---

## 🌐 4. Exposition des ports

### 4.1. L’instruction EXPOSE

En reprenant l’image de l’étape précédente, on ajoute :

```dockerfile
EXPOSE 1337
```

Cette instruction **documente** le port utilisé par le service, mais **n’ouvre pas réellement le port**.  
Il reste nécessaire d’utiliser l’option `-p` lors du `docker run` :

```bash
docker run -p 1337:1337 monimage
```

`EXPOSE` sert donc principalement à des fins **informative et de standardisation**, notamment lors de l’orchestration de conteneurs (ex. : Docker Compose).

---

## 🧠 5. Choix de l’image de base

Selon le type d’application, différents choix d’images s’imposent :

|Cas d’usage|Image de base recommandée|Justification|
|---|---|---|
|Serveur SQL|`mysql:latest` ou `postgres:latest`|Image officielle optimisée et maintenue|
|Serveur web|`nginx:stable` ou `apache:latest`|Configurations prêtes à l’emploi|
|Application Python|`python:3.12-slim`|Environnement léger et adapté à l’exécution de scripts|
|Scripts Shell personnalisés|`alpine:latest` ou `debian:stable-slim`|Images minimalistes contenant les outils standards|

Le choix d’une image de base doit équilibrer **légèreté, compatibilité et sécurité**.

---

## 🧾 Conclusion

Ce TP a permis d’explorer en profondeur la **construction d’images Docker** :

- comprendre la **structure d’un Dockerfile** ;
    
- manipuler le **cache de build** et les **couches** d’une image ;
    
- configurer un **entrypoint** et des **variables d’environnement** ;
    
- gérer la **persistance des données** via les **volumes** ;
    
- et exposer des **ports** pour les services en réseau.
    

Ces notions constituent la base indispensable pour concevoir des conteneurs **efficaces, modulaires et reproductibles** dans un contexte professionnel de déploiement d’applications.
