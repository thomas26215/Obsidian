---
MOOC: "[[Cours]]"
Ressource: "R2.06 : SQL"
Cours: Cours 1 :BD relationnelle et SQL simple
Date: 
tags: 
Complete: false
Learned: false
---
# 1 - Rappels
> [!tip] Base de données relationnelles
**Donnée** = 1 tuple (1 ligne de données)
**Attribut** = Définit une info élémentaire (un nom + domaine). Ex : localisation, nom ..
**Schéma** d'une relation : ensemble d'attributs en relation
**Relation** = ensemble de données (Alias table, tableau)

> [!tip] Avantages
- Structure = même quelle que soit app
- Description logique
- Permet interrogation performante
- Bien adaptée pour cohérence statique et dynamique

## Répartir l'information entre tables
On utilise plusieurs tables. Dépendances fonctionnelles entre les attributs. Des attributs qualifient naturellement un même objet. Cela permet également de réduire la redondance  d'information :
- Gain de place physique
- Facilite maintenance de la cohérence des informations
⇒ Une relation est un ensemble de tuples

## La jointure pour réunir des informations
**Contrainte référentielle** = Un attribut fait référence à la clé primaire d'une autre relation
**Contrainte de clé primaire + référentielles** = Modéliser la base par un schéma entité-association

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



