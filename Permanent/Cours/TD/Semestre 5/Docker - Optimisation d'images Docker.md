## **1. Inspection des images construites**

- **Lister les images locales :**
    

```bash
docker images
```

- **Les couches intermédiaires apparaissent-elles ?**  
    ❌ Non, elles ne sont pas listées par défaut dans `docker images`.
    
- **Afficher toutes les couches d’une image :**
    

```bash
docker history <nom_image>:<tag>
```

- **Supprimer les images inutilisées :**
    

```bash
docker image prune
# ou pour tout supprimer
docker system prune -a
```

---

## **2. Construction en plusieurs étapes**

### 2.1 Travail préparatoire

- **Dockerfile single-stage :**
    

```dockerfile
FROM debian:stable-slim
RUN apt-get update && apt-get install -y default-jdk
WORKDIR /app
COPY HelloWorld.java .
RUN javac HelloWorld.java
CMD ["java", "HelloWorld"]
```

- **Build :**
    

```bash
docker build -t java-hello-world:single-stage .
```

- **Nombre de couches :** 6
    
- **Taille de l’image :** ~800 Mo

```bash
~/Programmation/docker/tp3 % docker images

REPOSITORY         TAG            IMAGE ID       CREATED          SIZE
java-hello-world   single-stage   4d42997bcfc8   30 seconds ago   840MB

~/Programmation/docker/tp3 % docker history java-hello-world:single-stage

IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
4d42997bcfc8   45 seconds ago   CMD ["java" "HelloWorld"]                       0B        buildkit.dockerfile.v0
<missing>      45 seconds ago   RUN /bin/sh -c javac HelloWorld.java # build…   427B      buildkit.dockerfile.v0
<missing>      46 seconds ago   COPY HelloWorld.java . # buildkit               125B      buildkit.dockerfile.v0
<missing>      46 seconds ago   WORKDIR /app                                    0B        buildkit.dockerfile.v0
<missing>      46 seconds ago   RUN /bin/sh -c apt-get update && apt-get ins…   761MB     buildkit.dockerfile.v0
<missing>      2 days ago       # debian.sh --arch 'amd64' out/ 'stable' '@1…   78.6MB    debuerreotype 0.16
```

---

### 2.2 Multi-stage build

- **Principe :** Utiliser une première étape avec JDK pour compiler, puis copier uniquement le `.class` dans l’image finale avec le JRE.
    
- **Dockerfile multi-stage :**
    

```dockerfile
# Étape 1 : Builder
FROM debian:stable-slim AS builder

# Installer le JDK pour compiler
RUN apt-get update && \
    apt-get install -y default-jdk && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY HelloWorld.java .

# Compiler le programme
RUN javac HelloWorld.java

# Étape 2 : Image finale avec JRE
FROM debian:stable-slim

# Installer le JRE pour exécuter le programme
RUN apt-get update && \
    apt-get install -y default-jre && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copier le fichier compilé depuis le builder
COPY --from=builder /app/HelloWorld.class .

# Définir le point d'entrée
CMD ["java", "HelloWorld"]


```

- **Build :**
    

```bash
docker build -t java-hello-world:multi-stage .
```

- **Run** (WebServer) :

```bash
docker run --rm -p 8080:8080 java-hello-world:single-stage
```


    
- **Taille de l’image :** ~680 Mo
    
- **Gestion des dépendances :** Le JDK n’est plus dans l’image finale → taille réduite.
    

---

### 2.3 Images distroless

- **Principe** :
	- Une étape (builder) compile le programme avec toutes les dépendances.
	- Une autre étape (final) ne conserve que le binaire compilé, ce qui réduit drastiquement la taille.
- **Dockerfile distroless :**
    

```dockerfile
# Étape 1 : Builder
FROM debian:stable-slim AS builder

# Installer le JDK pour compiler
RUN apt-get update && \
    apt-get install -y default-jdk && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY HelloWorld.java .

# Compiler le programme
RUN javac HelloWorld.java

# Étape 2 : Image finale avec JRE
FROM debian:stable-slim

# Installer le JRE pour exécuter le programme
RUN apt-get update && \
    apt-get install -y default-jre && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copier le fichier compilé depuis le builder
COPY --from=builder /app/HelloWorld.class .

# Définir le point d'entrée
CMD ["java", "HelloWorld"]


```

- **Build :**
    

```bash
docker build -t java-hello-world:multi-stage .
```

- **Run**

```bash
docker build -t java-hello-world:multi-stage .
```


- **Taille de l’image :** ~695 Mo
    
- **Observation :** Fonctionnelle et minimale, adaptée à la production.
- 

---


## Distorless
Fichier DockerFile :

```Dockerfile
# Étape 1 : Builder
FROM eclipse-temurin:17 AS builder
WORKDIR /app
COPY HelloWorld.java .
RUN javac HelloWorld.java && \
    echo 'Main-Class: HelloWorld' > manifest.txt && \
    jar cfm HelloWorld.jar manifest.txt HelloWorld.class

# Étape 2 : Finale Distroless
FROM gcr.io/distroless/java17
WORKDIR /app
COPY --from=builder /app/HelloWorld.jar .
CMD ["HelloWorld.jar"]
```

Commande build :

```bash
docker run --rm -p 8080:8080 java-hello-world:single-stage
```
