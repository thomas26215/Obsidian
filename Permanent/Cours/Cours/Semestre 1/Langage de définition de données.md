---
MOOC: "[[Cours]]"
Ressource: "R1.05 : Introduction aux systèmes d'exploitation\ret à leur fonctionnement"
Cours: "Cours 4 : Implémentation du schéma relationnel - CREATE"
Date: 
tags: 
Complete: false
Learned: false
---
Pour créer un table en SQL, il faut utiliser la clause `CREATE`. Il faut savoir qu'un attribut est définit par son nom, son type et les éventuelles contraintes qui portent sur ses valeurs. La forme générale de création de table est :

```SQL
CREATE TABLE REL
	({définition_attribut | contrainte_de_relation}
	[, ...])
```

Ainsi, les différentes contraintes qui peuvent exister sont :
- `primary key`
- `UNIQUE`
- `NOT NULL`
- `DEFAULT`
- `CHECK`
- `foreign key`
**Voici un exemple concret de la création de table SQL :**

```SQL
CREATE humain(
	num_secu_sociale INTEGER PRIMARY KEY AUTOINCREMENT,
	prenom TEXT NOT NULL,
	nom TEXT NOT NULL,
	age INT CHECK(age > 0 and age < 120),
	travaille TEXT FOREIGN KEY travail.nom	
)
```


Il est également possible de supprimer des relations. Pour cela, il suffit d'utiliser la clause `DROP`. Sur cette clause, il est possible d'utiliser `IF EXISTS` qui permet de vérifier que la bse de données est présente avant de la supprimer et  `CASCADE` qui permet de contourner les contraintes référentielles en supprimant récursivement  les keys étrangère ou clés primaires associés à un attribut de cette relation.
Voici la forme générale :
```SQL
DROP TABLE [IF EXISTS] liste_relatinos [CASCADE];
```
En utilisant `DROP`, cela va donc supprimer tous les objets qui dépendent de ces tables de manière récursive


La clause `ALTER` permet la modification du schéma d'une relation. Voici la forme générale :
```SQL
ALTER TABLE [IF EXISTS] REL action[,...];
```

Avec une action qui peut être :
- `ADD [COLUMN] nom_att type_att [contraintes];`
- `DROP [COLUMN] nom_att;`
- `ADD PRIMARY KEY(liste_att_de_REL);`
- `ADD CONTRAINT nom_contrainte def_contrainte;`
- `DROP CONSTRAINT nom_contrainte`
- `ALTER [COLUMN] nom_att TYPE nom_type`
- ...

Pour ajouter des n-uplets dans une table, il faut utiliser la clause `INSERT`. Voici sa forme :
```SQL
INSERT INTO REL[(liste_att)] VALUES (liste_val1) [,(liste_val2) [,...]];
```
Voici la forme la plus simple. Maintenant, on peut ajouter des n-uplets à partir d'une autre relation :
```SQL
INSERT INTO REL[liste_att)]
SELECT ... FROM...[WHERE ...];
```

Pour modifier des n-uplets dans une relation, il faut utiliser la clause `UPDATE`. La forme générale est :
```SQL
UPDATE REL SET att = [,...] = [WHERE ...];
```
Voici un exemple :
```SQL
UPDATE GENERAL SET PrenomGeneral = 'Pierre'
WHERE NomGeneral = 'Cambronne';
```
⇒ Cela va donc  modifier toutes les valeurs qui ont pour attribut PrenomGenerak dans la table GENERAL **UNIQUEMENT SI** dans le n-uplet correspondant, l'attribut NomGeneral est égal à "Carbonne" 


Pour supprimer un n-uplet dans une relation, il faut utiliser la clause `DELETE` :
```SQL
DELETE FROM REL [WHERE condition];
```

---
**Questions :**
1. Quelle est la clause qui permet une relation ? Donner la forme générale.
2. Par quoi est définit un attribut ?
3. Quelle est la contrainte qui ?
	1. Définit la clé primaire
	2. Indique qu'une valeur est unique
	3. Oblige l'attribution d'une valeur
	4. Permet une valeur par défaut
	5. Vérifier parmis de valeurs
	6. Clé étrangère
4. Quelle est la relation pour supprimer une relation ? Donner la forme générale
5. Quelle est la clause pour modifier le schéma d'une relation ? Donner la forme générale
6. Donner l'action qui peut
	1. ajouter une colonne avec des éventuelles contraintes
	2. supprimer une colonne
	3. ajouter une clé primaire sur une ou plusieurs colonnes
	4. ajouter une contrainte
	5. supprimer une contrainte
7. Quelle est la relation qui permet d'ajouter des valeurs dans une table ? Donner la forme générale. Donner un exemple
8. Quelle est la relation qui permet de supprimer une relation ? Donner la forme générale

---
**Links :**
[[BD CIRQUE]]