---
MOOC: "[[Cours]]"
Ressource: "R1.05 : Introduction aux bases de données et SQL"
Cours: "TD 3 : Modélisation d'une BD - SEA & SLR"
Date: 
tags:
---
# Exercice 1
## Q2
**SiteArch**(CodeSite, AnneesDecs, Pays, Continent)
**Objet**(CodeObj, AnneeDecs, Type, Description, Date, # CodeSite ⇒ R1)
**Musee**(NomMusee, Ville, Pays, NomConservateur)

**R2 :**
**Expose**(# CodeObject, # CodeMusee)

# Q3
```SQL
SELECT count(*) AS nbObjects FROM Objet
WHERE CodeSite="S1Louxor";
```

```SQL
SELECT AnneeDecs FROM Objet
WHERE CodeSite="S1Louxor"
ORDER BY AnneeDecs
LIMIT 1;
```

```SQL
SELECT NomMusee FROM Musee, Objet
WHERE CodeSite="S1Louxor";
```

```SQL
SELECT Type, CodeObj FROM Objet, Musee
WHERE CodeSite
```

# Exercice 4

**Film**(Titre, MetteurScene)
**Interprète**(NomAct)
**Cine**(NomCine)
**NumeroSalle**(NumSalle)
**Horaire**(Heure)


```sql
Site(id_site(id), ann_decouverte, nom_pays, nom_continent, #id_site)
Musee(id_musee(id), nom, ville, pays, nom_cons, #id_musee)
Objet(id_obj(id), ann_dec, type, descriptif, date_fabrication)
```
