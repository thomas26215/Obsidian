---
MOOC: "[[Cours]]"
Ressource: "R2.06 : SQL"
Cours: "Cours 7 : Administration de premier niveau - droits"
Date: 2024-03-26
tags: 
Complete: false
Learned: false
---
**Insérer dans un groupe :**
```SQL
CREATE ROLE nom_role IN ROLE nom_groupe; /*A la création du groupe*/
GRANT nom_groupe TO nom_role; /*Après la création du rôle*/
GRANT nom_groupe To nom_role WITH ADMIN OPTION;
```
**Qui ?**
- `superuser`
- `createrole`
- Un membre inclus `WITH ADMIN OPTION`

# Droits
## Sur base

**Accorder :**
```SQL
GRANT CONNECT ON DATABASE nom_base
TO (role | PUBLIC) [,...];
```
**Retirer**
```SQL
REVOKE CONNECT ON DATABASE nom_base
FROM {role | PUBLIC} [,...]
```

# Résumé
- Différence entre authentification et droits
- Par défaut, une base est *ouverte* à PUBLIC, les tables sont *fermées*
- Un rôle est un ensemble de privilèges ; définir des droits ⇒ définir de rôles + attribuer ces rôles à des users
- Droits d'un utilisateur = {ceux attribués directement en son nom} U {Ceux attribués aux rôles auquel il appartient directement ou indirectement} U {Ceux attribués à tout le monde}
- Qui a le droit de créer ou d'attribuer un rôle {createrole, superviseur {WITH ADMIN OPTION}}
- Qui a le droit de donner un privilège sur {base, table, vue} : {propriétaire, superviseur [WITH GRANT OPTION]}