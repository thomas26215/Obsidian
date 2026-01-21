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


## Partie 4 — Compte rendu détaillé (avec emplacements des captures)

Cette partie consiste à configurer Kibana pour exploiter l’index `sample_flights_venouilt` : création d’un **Space**, création d’une **Data View** (avec champ temps), paramétrage des formats de champs, vérification dans **Discover**, puis création de **2 dashboards** avec Lens. Les Spaces servent à organiser les objets (dashboards/visualisations/data views) de manière séparée par projet.[elastic+1](https://www.elastic.co/docs/deploy-manage/manage-spaces)

---

## 4.1 Accès à Kibana + vérification initiale

**Où : Navigateur**  
Aller sur : `http://localhost:5601`.

Vérifier que Kibana charge correctement l’interface et que le menu latéral (Analytics / Management / etc.) est accessible.

**Capture à ajouter (Capture 4.1)**

- Capture de la page d’accueil Kibana (ou page principale) montrant l’URL `localhost:5601` et le menu visible.
    

---

## 4.2 Création du Space “Prénom NOM”

**Objectif :** isoler tous les objets Kibana du TP (data views, recherches Discover, visualisations, dashboards) dans un espace dédié. Les Spaces sont gérés dans Stack Management et Kibana demande/autorise de changer d’espace via le menu supérieur.[[elastic](https://www.elastic.co/docs/deploy-manage/manage-spaces)]​

**Étapes**

1. **Où : Kibana → menu (≡) → Stack Management**
    
2. Dans la page Stack Management, aller sur **Spaces**.[[elastic](https://www.elastic.co/docs/deploy-manage/manage-spaces)]​
    
3. Cliquer **Create space**.[[elastic](https://www.elastic.co/docs/deploy-manage/manage-spaces)]​
    
4. Remplir :
    

- **Name** : `Prénom NOM`
    
- (Optionnel) **ID / URL identifier** : généré automatiquement (laisser par défaut)
    
- (Optionnel) icône/couleur
    

5. (Si ton sujet demande de limiter les fonctionnalités) dans **Feature controls**, ne garder que ce qui est nécessaire (souvent _Analytics_ + _Stack Management_).[[elastic](https://www.elastic.co/docs/deploy-manage/manage-spaces)]​
    
6. Valider avec **Create space**.[[elastic](https://www.elastic.co/docs/deploy-manage/manage-spaces)]​
    
7. Basculer dans ce Space (sélecteur d’espace en haut, ou redirection proposée).
    

**Capture à ajouter (Capture 4.2)**

- Capture de la page “Spaces” montrant ton Space `Prénom NOM` dans la liste, ou l’écran de création juste avant validation (nom visible).[[elastic](https://www.elastic.co/docs/deploy-manage/manage-spaces)]​
    

---

## 4.3 Création de la Data View (index pattern) dans le Space

**Objectif :** permettre à Kibana d’explorer l’index `sample_flights_venouilt` et d’activer le filtre temporel via le champ `timestamp`. Une Data View est l’objet Kibana qui relie l’UI Kibana à un ou plusieurs indices.[[elastic](https://www.elastic.co/docs/explore-analyze/find-and-organize/data-views)]​

**Étapes**

1. **Où : Kibana (dans ton Space) → Stack Management → Data Views**
    
2. Cliquer **Create data view**.[[elastic](https://www.elastic.co/docs/explore-analyze/find-and-organize/data-views)]​
    
3. Renseigner :
    

- **Name** : `FLIGHTS_XX` (ou le nom demandé par l’énoncé)
    
- **Index pattern** : `sample_flights_venouilt`
    
- **Timestamp field** : sélectionner `timestamp` (très important, sinon pas de time picker exploitable).[nxlog+1](https://docs.nxlog.co/integrations/db/elasticsearch-kibana.html)
    

4. Valider avec **Create data view**.
    

**Capture à ajouter (Capture 4.3)**

- Capture de l’écran “Create data view” avec `sample_flights_venouilt` saisi et `timestamp` sélectionné, ou capture de la Data View créée (nom visible).[[elastic](https://www.elastic.co/docs/explore-analyze/find-and-organize/data-views)]​
    

---

## 4.4 Paramétrage des formats de champs (Field formatters)

**Objectif :** rendre l’affichage plus lisible dans Discover et dans les visualisations (prix en euros, durées, arrondis, dates).

**Étapes**

1. **Où : Stack Management → Data Views → `FLIGHTS_XX` → Fields**
    
2. Pour chaque champ, cliquer dessus puis **Edit** (ou “pencil”) et choisir un format.[[elastic](https://www.elastic.co/docs/explore-analyze/find-and-organize/data-views)]​  
    Exemples typiques (à adapter à ton sujet) :
    

- `timestamp` : format date/heure lisible (FR)
    
- `AvgTicketPrice` : format “Currency (EUR)”
    
- `DistanceKilometers` : format “Number” avec arrondi (ex. 1 ou 2 décimales)
    
- `FlightTimeMin` et `FlightDelayMin` : format “Duration” (si disponible/pertinent)
    

3. Sauvegarder à chaque champ modifié.
    

**Capture à ajouter (Capture 4.4)**

- Capture de l’onglet **Fields** montrant plusieurs champs et leurs formats configurés (ou capture d’un champ édité, ex. `AvgTicketPrice` en currency).
    

---

## 4.5 Vérification dans Discover (affichage + colonnes)

**Objectif :** vérifier que Kibana voit bien les documents, que la Data View est correcte, et préparer une vue tabulaire avec les champs demandés.

**Étapes**

1. **Où : Kibana → Analytics → Discover**
    
2. En haut à gauche, sélectionner la Data View `FLIGHTS_XX`.[[elastic](https://www.elastic.co/docs/explore-analyze/find-and-organize/data-views)]​
    
3. Ajuster la période via le **time filter** (en haut à droite) : si tu ne vois rien, élargir (ex. “Last 2 years” ou “Absolute”) car Discover dépend du champ temps sélectionné.[[alibabacloud](https://www.alibabacloud.com/help/en/es/use-cases/use-kibana-discover-to-display-data-in-chronological-order)]​
    
4. Ajouter des colonnes :
    

- Dans la colonne de gauche “Available fields”, survoler un champ puis cliquer **+** pour l’ajouter en colonne (ex. `FlightNum`, `Carrier`, `OriginCountry`, `DestCountry`, `timestamp`, etc.).[[youtube](https://www.youtube.com/watch?v=b4Edz_ybA_8)]​
    

5. (Optionnel mais utile pour le rendu) Sauvegarder la recherche Discover (session) : bouton **Save** dans la barre d’outils.[[elastic](https://www.elastic.co/docs/explore-analyze/discover/save-open-search)]​
    

**Capture à ajouter (Capture 4.5)**

- Capture de Discover montrant :
    
    - la Data View sélectionnée,
        
    - la plage de temps,
        
    - et les colonnes visibles dans le tableau (FlightNum, Carrier, OriginCountry, DestCountry, timestamp, …).[[youtube](https://www.youtube.com/watch?v=b4Edz_ybA_8)]​[[elastic](https://www.elastic.co/docs/explore-analyze/discover/save-open-search)]​
        

---

## 4.6 Création des dashboards (2 dashboards + visualisations Lens)

**Objectif :** construire 2 dashboards Kibana à partir de visualisations (Lens), les sauvegarder et les présenter.

## Dashboard 1 — “Synthèse des données”

**Étapes**

1. **Où : Analytics → Dashboard → Create dashboard**
    
2. Cliquer **Create visualization** (Lens).
    
3. Créer au moins 4 visualisations (exemples possibles) :
    

- Metric : nombre total de vols (Count).
    
- Bar chart : Top compagnies (`Carrier`) par nombre de vols.
    
- Bar chart : Top pays de destination (`DestCountry`) par nombre de vols.
    
- Line chart : nombre de vols dans le temps (Date histogram sur `timestamp`).
    

4. Pour chaque visuel : **Save and return** puis l’ajouter au dashboard.[[elastic](https://www.elastic.co/blog/building-kibana-dashboards-more-efficiently)]​
    
5. Sauvegarder le dashboard (bouton **Save**) avec le nom demandé.
    

**Capture à ajouter (Capture 4.6-A)**

- Capture du dashboard “Synthèse des données” affiché avec ses panneaux (le nom du Space visible si possible).
    

## Dashboard 2 — “Analyse des retards”

**Étapes**

1. **Où : Analytics → Dashboard → Create dashboard**
    
2. Ajouter au moins 4 visualisations autour des retards, par exemple :
    

- Donut/Pie : répartition par `FlightDelayType`.
    
- Bar chart : retard moyen (`Average FlightDelayMin`) par `Carrier`.
    
- Histogram : distribution de `FlightDelayMin`.
    
- Série temporelle : moyenne/compte des retards par jour (`timestamp`).
    

3. Sauvegarder les visualisations et le dashboard.[[elastic](https://www.elastic.co/blog/building-kibana-dashboards-more-efficiently)]​
    

**Capture à ajouter (Capture 4.6-B)**

- Capture du dashboard “Analyse des retards” avec ses panneaux.
    

---

## Checklist “captures” (récap)

- **Capture 4.1** : Kibana accessible (menu visible).
    
- **Capture 4.2** : création / liste du Space “Prénom NOM”.[[elastic](https://www.elastic.co/docs/deploy-manage/manage-spaces)]​
    
- **Capture 4.3** : Data View `FLIGHTS_XX` avec `timestamp` comme champ temps.[[elastic](https://www.elastic.co/docs/explore-analyze/find-and-organize/data-views)]​
    
- **Capture 4.4** : formats des champs (fields formatters) visibles.
    
- **Capture 4.5** : Discover avec colonnes + période.
    
- **Capture 4.6-A** : Dashboard 1.
    
- **Capture 4.6-B** : Dashboard 2.
    

Si tu me dis exactement ce que ton énoncé exige comme visuels (titres / nombre / types), je te rédige aussi les descriptions “panel par panel” (X, Y, agrégation, filtres) pour que ton compte rendu colle parfaitement.