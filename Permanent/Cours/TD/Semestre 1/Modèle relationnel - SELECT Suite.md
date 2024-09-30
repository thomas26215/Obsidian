---
MOOC: "[[Cours]]"
Ressource: "R1.05 : Introduction aux bases de données et SQL"
Cours: "TD 2 : Modèle relationnel - SELECT Suite"
Date: 2023-09-25
tags: 
Lien: "[[Introduction aux bases de données - SELECT]]"
---
# Question 1
## 1
```SQL
SELECT NomAct
FROM acteur
GROUP BY NomAct
HAVING count(*) >= 2
```

## 2
```SQL
SELECT NomCine, count(*)
AS nb_seances FROM SEANCE
GROUP BY NomCine;
```

## 3
```SQL
SELECT NomCine, Adresse
FROM CINE, SEANCE
WHERE SEANCE.NomCine = CINE.NomCine
GROUP BY SEANCE.NomCine
HAVING count(*) > 3;
```

## 4
```SQL
SELECT min(Heure), max(Heure)
FROM SEANCE
```

## 5
```SQL
SELECT round(avg(Prix), 2) AS moy_prix
FROM SALLE
GROUP BY nomcine
```

## 6
```SQL
SELECT(SELECT count(*)
FROM SEANCE
WHERE Heure < 12) AS nb_seances_avant_midi
SELECT(SELECT count(*) 
FROM SEANCE
WHERE Heure > 12h) AS nb_seances_apres_midi
```

## 7
Avec sous requête
```SQL
SELECT s.nomCine, adresse
FROM Cine c
WHERE EXISTS(SELECT heure FROM Seance s WHERE c.nomcine = nomcine AND heure < 19:30)
FROM Seance s
```

```SQL
SELECT NomCine, Adresse FROM Cine
WHERE nomCine IN (SELECT DISTINCT NomCine FROM Seance WHERE Heure > 19:30);
```

## 8
```SQL
SELECT titre FROM Film
WHERE Titre NOT IN (SELECT titre FROM Salle);
```

```SQL
SELECT Titre
FROM Film
EXEPT (SELECT Titre FROM Salle;)
```

## 9
```SQL
SELECT f.titre(SELECT count(Distinct NomCine))
AS 
```

## 11
```SQL
SELECT NomCine, 
```