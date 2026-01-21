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
docker compose up -d
docker compose ps
```

Vérification rapide (optionnelle) :

```shell
curl http://localhost:9200
curl "http://localhost:9200/_cluster/health?pretty"
```

## 1.3 Preuve de fonctionnement (Elasticvue)

![[Pasted image 20260121141916.png]]



## Partie 2 — Initialisation Elasticsearch (commandes)

## 2.1 Vérifications préalables (cluster up)

**Où : Terminal**


```bash
curl -s "http://localhost:9200" | head
curl -s "http://localhost:9200/_cluster/health?pretty"
```

(Optionnel) voir les nœuds :

```bash
curl -s "http://localhost:9200/_cat/nodes?v"
```

## 2.2 Vérifier le format du fichier d’import (NDJSON)

**Où : Terminal**


```bash
ls -lh sample_flights_data.json
head -n 4 sample_flights_data.json
```

On doit voir des lignes alternées `{"index":{...}}` puis `{...document...}`, ce qui correspond au bulk NDJSON.

​

## 2.3 Créer l’index `sample_flights_venouilt`




```shell
curl -X PUT "http://localhost:9200/sample_flights_venouilt" \
  -H "Content-Type: application/json" \
  -d '{
    "settings": {
      "number_of_shards": 4,
      "number_of_replicas": 0
    },
    "mappings": {
      "properties": {
        "timestamp": { "type": "date" },

        "FlightNum": { "type": "keyword" },
        "Carrier": { "type": "keyword" },

        "Cancelled": { "type": "boolean" },
        "FlightDelay": { "type": "boolean" },
        "FlightDelayType": { "type": "keyword" },

        "OriginCountry": { "type": "keyword" },
        "OriginCityName": { "type": "text" },
        "Origin": { "type": "text" },
        "OriginAirportID": { "type": "keyword" },
        "OriginRegion": { "type": "keyword" },
        "OriginWeather": { "type": "keyword" },
        "OriginLocation": { "type": "geo_point" },

        "DestCountry": { "type": "keyword" },
        "DestCityName": { "type": "text" },
        "Dest": { "type": "text" },
        "DestAirportID": { "type": "keyword" },
        "DestRegion": { "type": "keyword" },
        "DestWeather": { "type": "keyword" },
        "DestLocation": { "type": "geo_point" },

        "DistanceKilometers": { "type": "float" },
        "FlightTimeMin": { "type": "float" },
        "FlightDelayMin": { "type": "float" },
        "AvgTicketPrice": { "type": "float" }
      }
    }
  }'

```

Créer un index avec `number_of_shards` / `number_of_replicas` se fait via `PUT /{index}` + `settings`, comme dans la doc officielle “Create an index”.

​  
Le type `geo_point` est le type prévu pour stocker des coordonnées géographiques.

​

## 2.4 Vérifier que l’index est créé + mapping


```shell
curl -s "http://localhost:9200/_cat/indices?v" | grep sample_flights_venouilt
curl -s "http://localhost:9200/sample_flights_venouilt/_mapping?pretty" | head -n 120
```

## 2.5 Importer les données (Bulk)


```
curl -s -H "Content-Type: application/x-ndjson" \
  -X POST "http://localhost:9200/sample_flights_venouilt/_bulk" \
  --data-binary "@sample_flights_data.json" \
  | head -n 40
```

La doc Bulk précise l’usage du format NDJSON et recommande `application/x-ndjson` (ou `application/json`) comme `Content-Type`.

​

## 2.6 Vérifier que l’import est OK (13014 documents)



```shell
curl -s "http://localhost:9200/sample_flights_venouilt/_count?pretty"

{
  "count" : 13014,
  "_shards" : {
    "total" : 4,
    "successful" : 4,
    "skipped" : 0,
    "failed" : 0
  }
}
```

L’API `/_count` permet de compter les documents d’un index (avec ou sans query).

![[Pasted image 20260121145454.png]]



## 2.7 Vérifier la santé (shards/replicas)

```shell
curl -s "http://localhost:9200/_cluster/health?pretty"
curl -s "http://localhost:9200/_cat/shards/sample_flights_venouilt?v"
```



---

## Partie 3 — Exploration des données à travers quelques requêtes

## Contexte

Cette partie vise à valider la capacité à interroger Elasticsearch sur des données “brutes” (documents) et des données “agrégées” (statistiques) à l’aide de requêtes REST. Les requêtes ont été exécutées via **Kibana > Dev Tools > Console** (ou Elasticvue REST), sur l’index `sample_flights_venouilt`.

---

## 3.1 Compagnie du vol “U95ZN76”

## Requête (document brut)

```json
GET /sample_flights_venouilt/_search
{
  "_source": ["FlightNum", "Carrier"],
  "query": {
    "term": {
      "FlightNum": "U95ZN76"
    }
  }
}
```

## Résultat (présentation)

- Vol recherché : `U95ZN76`
    
- Compagnie aérienne (`Carrier`) : **Kibana Airlines**
    

---

## 3.2 Vols “Sunny” au départ ET à l’arrivée mais avec retard météo (requête `_count`)

## Requête (compter)

> Remarque : dans les données, le champ `FlightDelayType` contient des valeurs comme “No Delay”, “Weather Delay”, etc. Il faut donc filtrer exactement sur la valeur correspondant au retard météo.​

```json
GET /sample_flights_venouilt/_count
{
  "query": {
    "bool": {
      "must": [
        { "term": { "OriginWeather": "Sunny" } },
        { "term": { "DestWeather": "Sunny" } },
        { "term": { "FlightDelayType": "Weather Delay" } }
      ]
    }
  }
}
```

## Résultat (présentation)

- Nombre de vols avec météo “Sunny” au départ et à l’arrivée **et** un retard météo : **4**
    

---

## 3.3 Numéros des 3 vols France → USA entre le 08/01 et le 10/01/2024 (inclus), triés chronologiquement

## Requête (filtre + tri)

Le tri chronologique se fait via le paramètre `sort` sur le champ `timestamp` en ordre croissant.​

text

```json
GET /sample_flights_venouilt/_search
{
  "_source": ["FlightNum", "timestamp", "OriginCountry", "DestCountry"],
  "query": {
    "bool": {
      "filter": [
        { "term": { "OriginCountry": "FR" } },
        { "term": { "DestCountry": "US" } },
        {
          "range": {
            "timestamp": {
              "gte": "2024-01-08T00:00:00",
              "lte": "2024-01-10T23:59:59"
            }
          }
        }
      ]
    }
  },
  "sort": [
    { "timestamp": "asc" }
  ],
  "size": 3
}

```

## Résultat (présentation)

- Vol 1 : **TLTKOGK** (FlightNum) — **2024-01-08T12:07:55** (timestamp)
    
- Vol 2 : **XN4R38U** (FlightNum) — **2024-01-09T20:38:55** (timestamp)
    
- Vol 3 : **L4B4GPZ** (FlightNum) — **2024-01-10T14:43:04** (timestamp)
    

---

## 3.4 5 vols (compagnies ≠ “Logstash Airways”) France → Canada sur toute la période

## Requête (filtre + exclusion)

text

```json
GET /sample_flights_venouilt/_search
{
  "_source": ["FlightNum", "DestCityName", "Carrier", "OriginCountry", "DestCountry"],
  "query": {
    "bool": {
      "filter": [
        { "term": { "OriginCountry": "FR" } },
        { "term": { "DestCountry": "CA" } }
      ],
      "must_not": [
        { "term": { "Carrier": "Logstash Airways" } }
      ]
    }
  },
  "size": 5
}
```

## Résultat (présentation)

- Vol A : **PYK4TVQ** → destination : **Winnipeg**​
    
- Vol B : **V1TCR2A** → destination : **Edmonton**
    
- Vol C : **MUFJ77J** → destination : **Edmonton**​
    
- Vol D : **XH9H5H3** → destination : **Edmonton**​
    
- Vol E : **0G503MR** → destination : **Edmonton**​
    

---

## 3.5 2 vols partis à moins de 50 km du London Eye le 09/12/2023 entre 9h et 15h

## Requête (geo_distance + range date)

La requête utilise `geo_distance` sur un champ de type `geo_point` (ici `OriginLocation`) et filtre également une plage horaire via `timestamp`.[[elastic](https://www.elastic.co/docs/reference/query-languages/query-dsl/query-dsl-geo-distance-query)]​

text

```json
GET /sample_flights_venouilt/_search
{
  "_source": ["FlightNum", "Origin", "timestamp", "OriginLocation"],
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "timestamp": {
              "gte": "2023-12-09T09:00:00",
              "lte": "2023-12-09T15:00:00"
            }
          }
        },
        {
          "geo_distance": {
            "distance": "50km",
            "OriginLocation": {
              "lat": 51.5034,
              "lon": -0.1195
            }
          }
        }
      ]
    }
  },
  "size": 2
}
```

## Résultat (présentation)

- Vol 1 : **BGW87E2** — aéroport de départ : **London Luton Airport**
    
- Vol 2 : **1A5EKSQ** — aéroport de départ : **London Heathrow Airport**
    

---

## 3.6 Noms des 4 compagnies + nombre de vols par compagnie

## Requête (agrégation terms)

text

```json
GET /sample_flights_venouilt/_search
{
  "size": 0,
  "aggs": {
    "flights_by_carrier": {
      "terms": {
        "field": "Carrier",
        "size": 10
      }
    }
  }
}
```

## Résultat (présentation)

- **Logstash Airways** : **3323** vols
    
- **JetBeats** : **3261** vols
    
- **Kibana Airlines** : **3219** vols
    
- **ES-Air** : **3211** vols  
    Vérification : la somme des 4 valeurs = **13014**.
    

---

## 3.7 4 villes de départ des vols qui décollent depuis l’Allemagne

## Requête (match + terms aggregation)

Le sujet conseille `match` (recherche “texte”) et une agrégation `terms` sur les villes de départ. Pour agréger un champ `text`, on utilise en général le sous‑champ `.keyword` (si présent).[[geeksforgeeks](https://www.geeksforgeeks.org/elasticsearch/bucket-aggregation-in-elasticsearch/)]​

text

```json
GET /sample_flights_venouilt/_search
{
  "size": 0,
  "query": {
    "match": {
      "OriginCountry": "DE"
    }
  },
  "aggs": {
    "origin_cities": {
      "terms": {
        "field": "OriginCityName.keyword",
        "size": 10
      }
    }
  }
}
```

## Résultat (présentation)

- Ville 1 : **Frankfurt am Main**
    
- Ville 2 : **Berlin**
    
- Ville 3 : **Cologne**
    
- Ville 4 : **Munich**
    

---

## 3.8 Nombre de vols par plages de retard (range aggregation)

## Requête (agrégation range)

L’agrégation `range` permet de créer des “buckets” selon des intervalles numériques (ici `FlightDelayMin`). Les bornes `from` et `to` permettent de définir précisément chaque intervalle.​


```json
GET /sample_flights_venouilt/_search
{
  "size": 0,
  "aggs": {
    "delay_ranges": {
      "range": {
        "field": "FlightDelayMin",
        "ranges": [
          { "key": "Aucun retard", "to": 1 },
          { "key": "Retard [1, 60[ min", "from": 1, "to": 60 },
          { "key": "Retard >= 60 min", "from": 60 }
        ]
      }
    }
  }
}
```

## Résultat (présentation)

- Aucun retard : **9744** vols (attendu : 9744)
    
- Retard [1, 60[ min : **412**
    
- Retard ≥ 60 min : **2858**


## Partie 4 — Configuration Kibana

Un **Space** “Prénom NOM” a été créé dans _Stack Management → Spaces_ afin d’isoler tous les objets Kibana du TP (data views, visualisations, dashboards) dans un espace dédié.
Dans ce Space, une **Data View** a été créée dans _Stack Management → Data Views_ en pointant sur l’index `sample_flights_venouilt` et en sélectionnant `timestamp` comme champ temporel (activation du time picker et des analyses temporelles)

![[Pasted image 20260121223553.png]]

Les champs ont ensuite été vérifiés dans _Analytics → Discover_ en sélectionnant la Data View et en adaptant la plage de temps si nécessaire pour faire apparaître les documents.​

![[Pasted image 20260121223837.png]]

## Partie 4 — Dashboards (Lens)

Deux dashboards ont été créés dans _Analytics → Dashboard_ en ajoutant des panneaux via **Create visualization (Lens)**, puis en sauvegardant chaque dashboard. Kibana permet soit d’ajouter un panneau directement, soit de sauvegarder la visualisation dans la bibliothèque avant de l’ajouter

**Captures à insérer (dashboards)**

- Capture 4.4 : dashboard “Synthèse des données” affiché (panneaux visibles).​
    
- Capture 4.5 : dashboard “Analyse des retards” affiché (panneaux visibles).​