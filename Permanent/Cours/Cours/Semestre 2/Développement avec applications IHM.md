---
MOOC: "[[Cours]]"
Ressource: "R2.02 : IHM"
Cours: "Cours 1 : Développement avec applications IHM"
Date: 
tags: 
Complete: false
Learned: false
---
# L'anatomie d'une interface utilisateur
Voici les différents composants d'une interface graphique :
- **Label :** zone de texte statique
- **Bouton :** Formes et apparences variées, plusieurs états
- **Champs de texte :** Zone de texte éditable
- **Champs de texte :** Zone de texte éditable *TextFIeld*
- **Case à cocher :** Bouton avec label *CheckBox*
- **Bouton avec radio :** Bouton avec label *RadioButton*
- **Table :** Section d'items avec plusieurs attributs *TableView*
- **Liste :** Sélection d'items *List*
...

## Création d'une application avec JavaFX
Il y a 3 classes de base :
- **Application :** Classe principale de l'application
	- Hérite de la classe javafx.application.Application
	- Gère tout le cycle de vie de l'application
- **Stage :** La fenêtre principale de l'application
- **Scene :** L'interface qu'il faut associer à la fenêtre composées de nodes

On peut comparer celà à la composition d'une salle de théâtre :
- **Stage :** Fenêtre principale de l'application ⇒ Endroit où se déroule action
- **Scene :** Interface qu'il faut associer à la fenêtre ⇒ Tableau faisant intervenir acteur
- **Node :** (containers, controls) ⇒ acteurs, éléments de scène ...

![[Pasted image 20240601142253.png]]
**Graphe de scène = arbre orienté avec :**
- Racine correspondant à conteneur
- Noeurs étant éléments de l'interface
- Arcs = relations parent-enfant

3 types de noeuds :
- **Formes primitives** (2D ou 3D)
- **Conteneurs** se chargeant de disposition des composants enfants et qui sont comme classe parente Pane
- **Composants**
	- Standards (Controls)
	- Spécialisés dédiés à domaine particulier (lecteur multimédia, nav web ...)

# Programmation évènementielle
C'est un paradigme de programmation fondée sur les évènements
- Programme principalement définit par ses réactions aux différents évènements qui peuvent se produire
- Processus en tâche de fond surveille constamment actions de l'utilisateur susceptible de déclencher évènements qui pourront être ensuite traités par application

⇒ On prépare code à exécuter en associant à évènement que l'on souhaite associer et on attend que processus de surveillance détecte un évènement à traiter