---
MOOC: "[[Cours]]"
Ressource: "R2.06 : SQL"
Cours: "TD2 : Objets définis par requête"
Date: 2024-02-13
tags: 
Complete: false
Learned: false
---
# 2. Visualisation

# 3. Table, table temporaire et vue
1. .
```SQL
select soiree_demandee, num_salon, parrain, reponse
from demandes
where guest="user"
```
2. Il est utile de créer une vue
3. Cela doit être une temporaire
```SQL
CREATE OR REPLACE temporaire
SELECT *
FROM demandes  d NATURAL JOIN salon
WHERE localisation = 'N'
AND soiree_demandee > current_date
```
4. Ca doit être une temporaire
```SQL
CREATE OR REPLACE temporaire
SELECT idm, prenom, nom, count(d.*) as nb_soirees
FROM membre m JOIN demandes d ON jdm = parrain
where extract('year' from source.demande) = '2021'
group by parrain
having reponse = true
```

5. c
```SQL
CREATE TEMP TABLE demandes_2021
AS
	SELECT parrain, reponse
	FROM demandes
	WHERE extract(...);
```

6. .
```SQL
CREATE TABLE Bilan_2021_full
AS
	SELECT idm, nom, prenom,
	(SELECT count(reponses) as source_ok
	FROM demandes_2021
	WHERE reponse AND parrain = idm),
	
	SELECT idm, nom, prenom,
	(SELECT count(reponses) as source_ok
	FROM demandes_2021
	WHERE not reponse AND parrain = idm),

	SELECT idm, nom, prenom,
	(SELECT count(reponses) as source_ok
	FROM demandes_2021),
FROM membre;
	
```