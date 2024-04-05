---
MOOC: "[[Cours]]"
Ressource: "R1.05 : Introduction aux bases de données et SQL"
Cours: "TD 4 : BD CIRQUE"
Date: 2023-11-14
tags: 
Complete: false
Learned: false
---
# Q1
```SQL
CREATE TABLE ARTISTE(
	Surnom varchar(20) PRIMARY KEY,
	Specialite varchar
);
```

```SQL
CREATE TABLE NUMERO(
	Titre varchar PRIMARY KEY,
	Responsable varchar(20), FOREIGN KEY(Responsable) REFERENCES ARTISTE(Surnom)
)
```

```SQL
CREATE TABLE INTERPRETE(
	Surnom varchar(20) PRIMARY KEY, FOREIGN KEY(Surnom) REFERENCES ARTISTE(Surnom),
	Titre varchar PRIMARY KEY, FOREIGN KEY(Titre) REFERENCES NUMERO(Titre)
)
```

```SQL
CREATE TABLE ACCESSOIRE
```

Voir TP réalisé

# Q2
```SQL
ALTER TABLE ACCESSOIRE ADD CONSTRAINT c-color CHECK(Couleur IN('blue', 'violet', ...))
ALTER TABLE ACCESSOIRE ALTER Couleur SET NOT NULL;
```

# Q3
### a
```SQL
INSERT INTO Numero VALUES ('Des étoiles plein les yeux', 'Starlette');
```

### b
```SQL
INSERT INTO INTERPRETE
SELECT Surnom FROM INTERPRETE i, Artiste a
WHERE i.surnom = a.surnom AND specialite = 'Acrobate'
FOREIGN KEY AND titre = 'Voie lactée'
```

### c
```SQL
UPDATE ACCESSOIRE SET ImmtCamion = 'GB-32S' WHERE tyoe = 'ballon';
```

### d
```SQL
DELETE FROM 
```

# Q4
```SQL
CREATE temp TABLE Greate_Artiste AS
SELECT a.surnom, specialite
FROM Artiste a, Interprete i
WHERE a.surnom = i.surnom
GROUP BY i.surnom
HAVING COUNT(*) >= 3;
```