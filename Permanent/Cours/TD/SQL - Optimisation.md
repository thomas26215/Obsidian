---
MOOC: "[[Cours]]"
Ressource: "R3.07 : SQL"
Cours: "TP 2 : Optimisation"
Date: 
tags: 
Complete: false
Learned: false
---
# Exercice 1
**Question 1 :**
>- `pg_class` est un catalogue système de PostGreSQL contenant des informations sur les tables, index, vues et autres objets de la base de données. Il stocke les métadonnées essentielles pour chaque objet, comme son nom, son propriétaire et diverses statistiques
>- `relpages` représente le nombre de pages disque occupées par l'objet. C'est une estimation de la taille physique de l'objet, mesurées en pages (généralement 8 ko chacune)
>- `reltuples`contient une estimation du nombre de lignes dans l'objet. Pour les tables, c'est une approximation du nombre de lignes vivantes. Cette valeur est utilisée par le planificateur de requêtes pour estimer la cardinalité des résultats

>[!info]
>- Caractéristiques mise à jour en temps réel
>- `reltuples`= estimation, pas exact

**Question 2 :**
>La commande `EXPLAIN`premet à l'optimiseur de générer des plans d'exécution plus efficaces. En sidposant de statistiques à jour, l'optimiseur peut prendre des décisions plus éclairées sur la meilleure façon d'exécuter les requêtes


# Exercice 2
**Question 1 :**
>`EXPLAIN SELECT * FROM TOWNS ;`
>1. Cela indique que pour accéder au premier élément, ça se fait instantanément (`0`) alors que pour accéder au dernier, ça prend `617.84` ⇒ `cost=0.00..617.84`
>2. PostgreSQL a choisit un scan séquentiel, suggérant qu'il n'y a pas d'indice utile pour cette requête ou que la table est suffisamment petite pour que le scan séquentiel soit plus efficace ⇒ `Seq Scan on towns`
>
>En faisant `EXPLAIN ANALYZE SELECT * FROM TOWNS ;`, nous avons le temps plannifié et le temps d'exécution en plus ⇒ `Planning Time: 0.119 ms  Execution Time: 12.204 ms`

**Question 2 :**
>1. `explain analyze SELECT code, name FROM towns;`


```text
Seq Scan on towns  (cost=0.00..617.84 rows=36684 width=15) (actual time=0.018..8.525 rows=36684 loops=1)  
Planning Time: 0.391 ms  
Execution Time: 11.216 ms  
(3 rows)
```
- Utiliser un **scan séquentiel**
- Coût estimé relativement élevé

> 2. `EXPLAIN ANALYZE SELECT v.name, d.name AS departement, r.name AS region FROM towns v JOIN departments d ON v.department = d.code JOIN regions r ON d.region = r.code;`

```text
                                                         QUERY PLAN                                                             
------------------------------------------------------------------------------------------------------------------------------  
Hash Join  (cost=4.83..835.05 rows=36684 width=34) (actual time=0.199..22.329 rows=36684 loops=1)  
  Hash Cond: ((d.region)::text = (r.code)::text)  
  ->  Hash Join  (cost=3.25..721.47 rows=36684 width=25) (actual time=0.143..13.938 rows=36684 loops=1)  
        Hash Cond: ((v.department)::text = (d.code)::text)  
        ->  Seq Scan on towns v  (cost=0.00..617.84 rows=36684 width=15) (actual time=0.011..2.960 rows=36684 loops=1)  
        ->  Hash  (cost=2.00..2.00 rows=100 width=16) (actual time=0.120..0.120 rows=100 loops=1)  
              Buckets: 1024  Batches: 1  Memory Usage: 13kB  
              ->  Seq Scan on departments d  (cost=0.00..2.00 rows=100 width=16) (actual time=0.031..0.064 rows=100 loops=1)  
  ->  Hash  (cost=1.26..1.26 rows=26 width=15) (actual time=0.045..0.046 rows=26 loops=1)  
        Buckets: 1024  Batches: 1  Memory Usage: 10kB  
        ->  Seq Scan on regions r  (cost=0.00..1.26 rows=26 width=15) (actual time=0.016..0.025 rows=26 loops=1)  
Planning Time: 1.501 ms  
Execution Time: 23.841 ms  
(13 rows)
```

- Utiliser des **hash joins** pour joindre les tables
- **hash cond** = indique la condition utilisée pour construire et sonder la table de hachage
- **hash joins** = Efficace pour de grandes tables sans index appropriées

> 3. `EXPLAIN ANALYZE SELECT COUNT(*) FROM towns;`

```text
                                                 QUERY PLAN                                                      
---------------------------------------------------------------------------------------------------------------  
Aggregate  (cost=709.55..709.56 rows=1 width=8) (actual time=10.989..10.990 rows=1 loops=1)  
  ->  Seq Scan on towns  (cost=0.00..617.84 rows=36684 width=0) (actual time=0.014..6.423 rows=36684 loops=1)  
Planning Time: 0.298 ms  
Execution Time: 11.032 ms  
(4 rows)
```

- Comme requête 1, mais avec agrégation supplémentaire

> 1. `EXPLAIN ANALYZE SELECT count(name), department FROM towns GROUP BY department;`

```text
                                                  QUERY PLAN                                                      
----------------------------------------------------------------------------------------------------------------  
HashAggregate  (cost=801.26..802.26 rows=100 width=11) (actual time=16.689..16.702 rows=100 loops=1)  
  Group Key: department  
  Batches: 1  Memory Usage: 32kB  
  ->  Seq Scan on towns  (cost=0.00..617.84 rows=36684 width=15) (actual time=0.020..3.775 rows=36684 loops=1)  
Planning Time: 0.148 ms  
Execution Time: 16.764 ms  
(6 rows)
```

- Utilise un HashAggregate pour le groupement
- Efficace pour les opérations GROUP BY sur de grands ensembles de données
- 101 lignes de résultat attendues, correspondant probablement au nombre de départements

> `EXPLAIN ANALYZE SELECT count(*) FROM departments`

```text
                                                 QUERY PLAN                                                      
---------------------------------------------------------------------------------------------------------------  
Aggregate  (cost=2.25..2.26 rows=1 width=8) (actual time=0.065..0.066 rows=1 loops=1)  
  ->  Seq Scan on departments  (cost=0.00..2.00 rows=100 width=0) (actual time=0.022..0.041 rows=100 loops=1)  
Planning Time: 0.154 ms  
Execution Time: 0.112 ms  
(4 rows)
```

- On utiliser une fonction d'agrégation (`count`)

> 6. `EXPLAIN ANALYZE SELECT count(*) as nb, region FROM regions r, departments d WHERE r.code = d.region GROUP BY region HAVING count(*) > 5;`

```text
HashAggregate  (cost=4.39..4.72 rows=9 width=11) (actual time=0.133..0.139 rows=5 loops=1)  
  Group Key: d.region  
  Filter: (count(*) > 5)  
  Batches: 1  Memory Usage: 24kB  
  Rows Removed by Filter: 21  
  ->  Hash Join  (cost=1.58..3.89 rows=100 width=3) (actual time=0.041..0.092 rows=100 loops=1)  
        Hash Cond: ((d.region)::text = (r.code)::text)  
        ->  Seq Scan on departments d  (cost=0.00..2.00 rows=100 width=3) (actual time=0.011..0.021 rows=100 loops=1)  
        ->  Hash  (cost=1.26..1.26 rows=26 width=3) (actual time=0.021..0.021 rows=26 loops=1)  
              Buckets: 1024  Batches: 1  Memory Usage: 9kB  
              ->  Seq Scan on regions r  (cost=0.00..1.26 rows=26 width=3) (actual time=0.006..0.011 rows=26 loops=1)  
Planning Time: 0.291 ms  
Execution Time: 0.188 ms  
(13 rows)
```

