---
MOOC: "[[Programmation]]"
Langage: SQL
Type: SEA - SLR
tags:
---
Lors de la construction du schéma relationnel (et donc pour passer d'une SAE à une SRL), il convient d'appliquer les règles dans leur ordre de numérotation. 

La première règle est que chaque entité correspond à une relation, avec sa clé primaire représentée par l'identifiant de l'entrée, et les autres attributs représentant les propriétés de cette entrée. 

Si une association a une cardinalité de 1,1, il suffit d'ajouter les identifiants des autres entités qui participent à cette relation en tant que clés étrangères à la relation qui contient cette cardinalité, et cette association n'a plus besoin d'être traitée davantage. 

Si une association a une cardinalité de 0,1 et n'a pas été traitée, elle doit être traitée comme une nouvelle relation, avec sa clé primaire représentant l'identifiant de l'entité associée à cette association. Les autres attributs sont les identifiants des autres entités participant à cette association (comme clés étrangères) ainsi que les propriétés propres de cette association. 

Enfin, si une association a une cardinalité de x,n et n'a pas été traitée, elle doit également être traitée comme une nouvelle relation. Sa clé primaire est l'ensemble des identifiants des entités associées, ses autres attributs sont les propriétés propres de l'association, et les identifiants de chaque entité sont les clés étrangères de l'association.