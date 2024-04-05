---
MOOC: "[[Cours]]"
Ressource: "R2.06 : SQL"
Cours: "Cours 2 : SQL pour explorer et analyser"
Date: 
tags: 
Complete: false
Learned: false
---
# Table définie par une requête
Il est possible de définir une table à partir d'une table déjà existante. Nous pouvons y rajouter des contraintes. C'est le même principe que pour faire une requête avec un `SELECT` sauf qu'au lieu que la requête s'affiche directement, c'est une nouvelle table qui est crée avec le résultat de la requête

**Exemple :** Créer une table à partir d'une table salariés qui récupère tous les salariés qui ont un salaire > 5000$
```SQL
CREATE TABLE bien_payé AS    /*Créer la table*/
SELECT * FROM salaries       /*Y insère les éléments de la table salariés*/
WHERE salaire > 5000;        /*Contrainte de > 5000$*/
```

# Table définie par une vue
Une vue peut être utile afin d'analyser des informations. Celle-ci se supprimera automatiquement quand la session expire. La création de celle-ci se base sur le même principe que pour créer une table par une requête :

**Exemple :** Créer une table temporaire à partir d'une table salariés qui récupère tous les salariés qui ont un salaire > 5000$
```SQL
CREATE TEMP TABLE bien_payé AS    /*Créer la table temporaire*/
SELECT * FROM salaries       /*Y insère les éléments de la table salariés*/
WHERE salaire > 5000         /*Contrainte de > 5000$*/
```