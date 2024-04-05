---
MOOC: "[[Cours]]"
Ressource: "R2.06 : SQL"
Cours: "TD 4 : Triggers et vues"
Date: 2024-03-05
tags: 
Complete: false
Learned: false
---
# 2 - Triggers sur vues
1)
```SQL
CREATE OR REPLACE FUNCTION f_mesDemandes() RETURNS trigger
AS $$
BEGIN
	INSERT INTO demandes
	VALUES(null, user, new.parrain, new.salon, new.soiree_demandee, null),
	Return new;
END $$ language plpgsql;

CREATE trigger t_mesDemandes
INSTEAD OF insert on mesdemandes
FOR EACH ROW
EXECUTE FUNCTION f_mesDemandes();
```

# 5
1. Réponses :
	- **Table tarif :** Elle est définie par la création de la table avec le not null et "c_montant" CHECK (montant >= 0::doubleprecision)
	  ⇒ Pas besoin de trigger
	- **Table adhérant :**
		- Values
		- skipper not null
		- Contrainte 4 non indiquée dans table. Il faut le coder avec un trigger *Cas 1*
	- **Table Cotisation :**
		- On ne sait pas si seulement la cotisation peut être modifiée *Cas 1*
		- Rien indique qu'on ne peut pas régler une année précédante que actuelle *Cas 2 et ce n'est pas une contrainte d'unicité toute simple*
		- Rien indique que la modification d'une cotisation indique true *Cas 3*
		  ⇒ Paiement complet → Croiser données avec table tarif
	- **Table Bateau :**
		- integer
		- Oui contrainte check nbplaces >= 5
	- **Course**
		- numcourse integer
		- CHECK datedebut <= datefin
		- 2e contrainte UNIQ CONSTRAINT
		- Il faut créer un trigger car aucune indication. *Cas 2*
	- **Chef de bord :**
		- Oui on a pour chacun un FOREIGN KEY pour sa propre table
		- Pas de précisions concernant l'agrément skipper. *Cas 3*
		- UNIQ CONSTRAINT (numcourse, numadh)
		- PRIMARY KEY numcourse, numadh
		- Aucune indication *Cas 3*
	- **Equipier :**
		- Foreign key (derniere)
		- Primary key
		- Pas de contraintes *cas 3*
		- Aucun conratines *cas 3*
	- **Régate :**
		- Primary key
		- Aucune indication donc *cas 2*
	- **Résultat :**
		- Clé étrangère
		- *Cas 1* Contrainte complexe
		- *Cas 3*
		- *Cas 2*

**Triggers**
```SQL

```

