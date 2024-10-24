---
MOOC: "[[Cours]]"
Ressource: R3.01
Cours: ETL
Date: 
tags: 
Complete: false
Learned: false
---
Une données est la résultat direct d'une mesure collectée par une personne ou un outil de supervision. Elle ne sert à rien s'il n'y a pas de traitement ultérieur. Elle doit être qualitative (nom, ville ...) soit quantitative.
Une donnée n'a pas de contexte. C'est seulement une donnée que l'on enregistre

Il existe différents supports de données :
- Fichiers
- BD
- Bd propriétaire
Les données sont stockées à différents endroits. Cependant, cela est potentiellement redondant ou incohérent (Exemple : Gestion de clients et Gestion des commandes = deux fois la même information)
[[ERP - PGI - Etude de cas]] ⇒ Définition

On peut vouloir la synchronisation (gestion des commandes - gestion des stocks), la migration ou l'intégration

Exemple simple d'intégration de 2 fichiers :
Etats des Etats-Unis + Clients des Etats-Unis ⇒ Table des clients (Comme une jointure en BDD)

On va donc faire un process [[ETL - Extract, Transform and Load]]. 
On peut aussi faire [[ELT - Extract, Load and Transform]]. 

| ETL                                                  | ELT                                                                  |
| ---------------------------------------------------- | -------------------------------------------------------------------- |
| <mark style="background: #BBFABBA6;">+ rapide</mark> | <mark style="background: #BBFABBA6;">+ gros volume de données</mark> |
| Flux de transformation explicite mais dans un langage souvent propriétaire | Besoin de plus d'espace disque                                  |
| Difficultés pour traitements paralèlles                                    | Nécessite un système cible plus puissant                        |
| Pas d'opérations sur des ensembles de données                              | Transformation dans le langage du système cible                 |

[[ETL - Extract, Transform and Load]]
- Extraction
	- Identifier, collecter et extraire les données de sources ayant subi une modification depuis la dernière exécution
	- Opérations *manuelles*
		- Localiser sources
		- Sélectionner données pertinentes
		- Identifier le format des données
		- Identifier structuration des données
	- Questions pour la sélection des données
		- Quelles sont les données utiles ?
		- Quel est le bon niveau de granularité ? Exemple STMicroelectronics
		- Quelle est la disponibilité des sources
	- Collecte et traitement des données
		- Définir les stratégies de chargement
			- Total ou incrémental
			- Mode Push ou Pull
	- Collecte et traitement des données
		- Opérations *automatiques*
			- Traiter les différents formats
			- Gérer les connexions aux sources
			- Extraire le format des données
			- Extraire le format des données
			- Détecter les données qui ont été modifiées
			- Ajouter des contrôles
			- Stocker les règles d'extraction
- Transformation
	- Appliquer diverses transformations aux données pour les vérifier, les nettoyer, les intégrer, les agréger
	- Objectifs
		- Vérifier les données (pas de `null`)
		- Les unifier
		- Les nettoyer
		- Les transformer
- Chargement
	- Insérer les données et gérer les changements aux données existantes