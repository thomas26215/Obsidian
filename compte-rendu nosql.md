# Introduction

Ce mini‑projet consiste à mettre en place en local, via Docker Compose, un cluster Elasticsearch (2 nœuds) et un serveur Kibana afin d’analyser un jeu de données factices de vols d’avions de ligne sur la période décembre 2023 – janvier 2024.  
Elasticsearch est pertinent pour indexer et interroger rapidement des documents JSON (filtres, tris, agrégations), et Kibana permet de créer des visualisations et tableaux de bord interactifs à partir de ces index.  
Les objectifs sont : déployer une stack fonctionnelle, créer un index shardé correctement, définir un mapping adapté, importer 13 014 documents, écrire des requêtes (dont agrégations et géo‑requêtes), puis produire 2 dashboards Kibana.

# Partie 1 — Mise en place de la stack en local

## 1.1 docker-compose.yml

Le fichier suivant crée 3 services : `es001`, `es002` et `kibana000`, avec persistance via volumes Docker et sécurité désactivée.  
Le cluster est formé grâce aux paramètres de découverte `discovery.seed_hosts` et de bootstrap `cluster.initial_master_nodes`

  
Le démarrage de Kibana est ordonné après Elasticsearch avec `depends_on` (ordre de création/démarrage).

​
```shell
services:
  es001:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.19.8
    container_name: conteneur_es001
    environment:
      - node.name=node_es001
      - cluster.name=cluster_$LOGIN$
      - discovery.seed_hosts=es002
      - cluster.initial_master_nodes=node_es001,node_es002
      - xpack.security.enabled=false
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ports:
      - "9200:9200"
    volumes:
      - esdata01:/usr/share/elasticsearch/data

  es002:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.19.8
    container_name: conteneur_es002
    environment:
      - node.name=node_es002
      - cluster.name=cluster_$LOGIN$
      - discovery.seed_hosts=es001
      - cluster.initial_master_nodes=node_es001,node_es002
      - xpack.security.enabled=false
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ports:
      - "9201:9200"
    volumes:
      - esdata02:/usr/share/elasticsearch/data

  kibana000:
    image: docker.elastic.co/kibana/kibana:8.19.8
    container_name: conteneur_kibana000
    depends_on:
      - es001
      - es002
    environment:
      - SERVER_NAME=kibana_local
      - ELASTICSEARCH_HOSTS=http://es001:9200
      - xpack.security.enabled=false
    ports:
      - "5601:5601"

volumes:
  esdata01:
  esdata02:

```

## 1.2 Commandes d’exécution


```shell
docker compose up -d docker compose ps
```

Vérification rapide (optionnelle) :

```shell
curl http://localhost:9200 curl "http://localhost:9200/_cluster/health?pretty"
```

## 1.3 Preuve de fonctionnement (Elasticvue)

![[Pasted image 20260121141916.png]]


