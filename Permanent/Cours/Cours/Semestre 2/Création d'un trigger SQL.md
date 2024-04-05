---
MOOC: "[[Cours]]"
Ressource: "R2.06 : SQL"
Cours: "Cours 3 : Création d'un tigger SQL"
Date: 
tags: 
Complete: false
Learned: false
---
# Trigger simple
Un trigger permet d'automatiser des actions en réponse à certains évènements sur une table (`INSERT`, `DELETE` ...). Cela permet de maintenir une certaines intégrité des données et la propagation d'une modification sur d'autres tables (peut être pratique si il y a des clé étrangères avec des `NOT NULL`)

Il faut créer une fonction qui fera les actions quand le trigger est activé et créer le trigger qui déclenchera la fonction en fonction de ce qui est modifié sur la table

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
# Trigger
## Utilisation de `ROW` et de `STATEMENT`
→ `FOR EACH ROW` ⇒ L'action doit se produire à chaque opération
→ `FOR EACH STATEMENT` ⇒ L'action doit se produire à la fin de l'opération sur toutes les lignes
## Déclenchement
- `BEFORE`
	- `STATEMENT` ⇒ Avant l'ensemble des opérations
	- `ROW` ⇒ Avant chaque opération
- `AFTER`
	- `STATEMENT` ⇒ Après l'ensemble des opérations
	- `ROW` ⇒ Après chaque opération
# Fonction
La fonction sera appelée dès que le trigger correspondant est actionné. Cela exécutera le code à l'intérieur, entre les balises `BEGIN` et `END`. La fonction reste la même dans tous les cas.
### New et Old
- Il est possible de récupérer la valeur d'une colonne d'une ligne qui est supprimée en utilisant `OLD.colonne`. Exemple : une ligne de la table personnages est supprimée. Je veux récupérer son prénom. J'utilise `OLD.prenom`
- Il est possible de récupérer la valeur d'une colonne d'une ligne qui est crée en utilisant `NEW.colonne`. Par exemple : une ligne de la table personnage est ajoutée. Je veux récupérer son prénom. J'utilise `NEW.prenom`
### Que retourner ?
- **FOR EACH ROW** :
	- `FOR EACH ROW` + `BEFORE`
		- `DELETE` ⇒ `RETURN OLD;`
		- `INSERT` ⇒ `RETURN NEW;`
		- `UPDATE` ⇒ `RETURN NEW;`
	- `FOR EACH ROW` + `AFTER` ⇒ `RETURN NULL`
	- `FOR EACH STATEMENT` ⇒ `RETURN NULL`
- **FOR EACH STATEMENT**
# Commande psql utiles
## Les variables caractérisant un trigger
- `TG_WHEN` ⇒ BEFORE ou AFTER
- `TG_LEVEL` ⇒ ROW, STATEMENT
- `TG_OP` ⇒ INSERT, UPDATE, DELETE
- `TG_TABLE_NAME` ⇒ Le nom de la table associée
- `TG_NAME` ⇒ Nom du trigger
## Retrouver un trigger
Liste des fonctions trigger :
-  Liste des fonctions : `\dft`
- Code d'une fonction : `sf nom_fonc`
Liste des triggers :
- Définition des triggers sur une table : `\d nom_table`
# Informations supplémentaires
## Comment  faire pour qu'un trigger ne se déclenche que quand c'est nécessaire ?
```SQL
CREATE TRIGGER nom_trigger
{ BEFORE | AFTER } { INSERT | UPDATE | DELETE [ OR ... ] }
ON nom_table FOR EACH ROW
WHEN (condition) /*La condition est ici*/
EXECUTE FUNCTION nom_fonc();
```
