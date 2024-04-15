---
MOOC: "[[Cours]]"
Ressource: "R2.06 : SQL"
Cours: Résumé
Date: 
tags: 
Complete: false
Learned: false
---
# Jointures
> [!example] **Jointure externe**
> Jointure externe complète : retourne les tuples dont la condition est vraie dans au moins une des deux tables
>`SELECT * FROM T1 FULL JOIN T2 ON T1.a = T2.b*`
>Jointure externe retournant tous les tuples de la table de gauche
>`SELECT * FROM T1 LEFT JOIN T2 ON T1.a = T2.b*`
>Jointure externe retournant tous les tuples de la table de droite
>`SELECT * FROM T1 RIGHT JOIN T2 ON T1.a = T2.b*`
>> [!tip]
>> Retourne toutes les lignes des tables concernées, ainsi que les lignes correspondantes dans l'autre table, s'il y en a

> [!example] **Jointure interne**
>
> Permet de faire la jointure entre deux tables, uniquement s'il y a des colonnes du même nom et du même type dans les deux tables
>`SELECT * FROM T1 NATURAL JOIN T2*`
>Jointure naturelle, mais rajoute en plus les données de la table de gauche
>`SELECT * FROM T1 NATURAL LEFT JOIN T2`
>Jointure naturelle, mais rajoute en plus les données de la table de droite
>`SELECT * FROM T1 NATURAL RIGHT JOIN T2`
> >[!tip]
>>Retourne uniquement les lignes des tables qui ont des valeurs correspondantes dans les deux tables
>>⇒ Jointure entre les deux tables (jointure naturelle)

# Tout sur les tables
**Créer une table :** `CREATE TABLE nom{colonne1, type1, colonne2, type2`
**Ajouter une colonne :** `ALTER TABLE nom ADD nom_colonne type_donnee`
**Supprimer une colonne :** `ALTER TABLE nom DROP nom_colonne`
**Modifier une colonne :** `ALTER TABLE nom_table ALTER COLUMN nom_colonne TYPE type_donnees`

# Tables temporaires et vues
**Table temporaire :** `CREATE TEMP TABLE AS SELECT ... FROM ...`
**Vue :** `CREATE VIEW nom AS ..`

# Triggers
```SQL
/* Crée la fonction qui sera appelée par le trigger (Fonction) */

CREATE OR REPLACE FUNCTION name_function()
RETURNS TRIGGER AS $$
BEGIN
	/*CODE*/
	RETURN {OLD/NEW};
END;
$$ LANGUAGE plpgsql;


/* Crée le trigger qui déclenchera la fonction une fois qu'il sera appelé (Trigger) */

CREATE OR REPLACE TRIGGER
name_trigger
{BEFORE/AFTER} action
{FOR EACH ROW / COLUMN}
EXECUTE FUNCTION name_function();
```

[[Création d'un trigger SQL]]
[[SQL augmenté - Triggers]]