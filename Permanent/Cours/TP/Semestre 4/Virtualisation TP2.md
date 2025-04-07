 .
 parititons : `/dev/sda1`, `/dev/sda2`, `/dev/sda5`

# TP4

`docker run -dti --name conteneur1 debian`
`docker exec -ti conteneur1 bash`

---

```bash
apt update
apt install iproute2
ip addr
apt install iputils-ping
```

**Adresses IP :**
- Conteneur 1 : `172.17.0.4/16`
- Conteneur 2 : `172.17.0.5`

Il est possible de faire un ping entre les conteneurs et également de conteneur vers machine mais également de machine vers conteneur

`docker rm -f conteneur1 conteneur2`

---



`docker run -dti --name conteneur1 --network=none alpine`
`docker exec -it conteneur1 sh`

---

Créer un fichier `Dockerfile` avec le contenu :
```text
FROM debian:latest
RUN apt-get update && apt-get install -y iputils-ping iproute2
```

Mesurer la taille : `sudo du -sh /var/lib/docker/`: 1.7Go avant, 1.7Go après

Construire l'image  : `docker build -t debian-net .`

Construire des conteneurs avec l'image :
```shell
docker run -dti --name container1 debian-net
docker run -dti --name container2 debian-net
```