---
MOOC: "[[Cours]]"
Ressource: "R3.10B : Gestion de projet"
Cours: "Cours 2 : Retour sur l'agilité"
Date: 
tags: 
Complete: false
Learned: false
---

- <mark style="background: #ADCCFFA6;">Les principes du développement</mark> : <mark style="background: #FFB86CA6;">itératif</mark> (développement successif), <mark style="background: #FFB86CA6;">incrémental</mark> (Basés sur un développement par lots ⇒ Ajouter) et <mark style="background: #FFB86CA6;">adaptatif</mark> (Accepter ou non des évolutions, spécifications supplémentaires en cours de projet)
	- → <mark style="background: #FFB86CA6;">Petites itérations et livraisons fréquentes</mark> ⇒ Ancrage temporel fort
	- → <mark style="background: #FFB86CA6;">Centré utilisateur</mark> (user story) ⇒ Mets le focus sur la satisfaction du client != Centré usage (On priorise sur la tâche)
	- → <mark style="background: #FFB86CA6;">Pragmatique</mark> : pas plus de documentation que nécessaire
- <mark style="background: #FFB86CA6;">Piloté par les tests</mark>
- Les grands recueils de besoins, de communication et d'organisation spécifique
- <mark style="background: #ADCCFFA6;">Changement de paradigme</mark> : plus gestion de produit que gestion de projet
>[!info]
>La méthode la plus connue ⇒ SCRUM


<mark style="background: #ADCCFFA6;">SCRUM</mark> :
- Scrum master "Chef de projet"
	- Crée et maintient de bonne conditions de travail
	- Guide l'équipe et résout les problèmes
	- Facilite la communication
- Scrup team "Equipe projet"
	- En charge du dév
	- Agit de manière collaborative
	- Taille réduite
- Business ower "Responsable commercial"
- Product owner "Responsable produit"
	- Etablit les fonctionnalités prioritaires
	- Prend les décisions essentielles
	- Gère les attentes des utilisateurs finaux et le budget

<mark style="background: #ADCCFFA6;">Les temps forts</mark> :
- Planification du sprint → Sélection des éléments du Product backlog
- <mark style="background: #FFB86CA6;">Product backlog</mark> : Liste priorisée des exigences fonctionnelles et non fonctionnelles
- <mark style="background: #FFB86CA6;">Sprint</mark> : Itération scrum, 2 à 4 semaines
- Mélée quotidienne


⇒ 1 = Présenter,  expliquer, 2 = comment mettre en place, 3 = illustrer puis identifier 4 = objectifs avantages et 5 = limites, 6 = outils

<mark style="background: #ADCCFFA6;">Outils de l'agilité</mark> : 
- <mark style="background: #FFB86CA6;">Intégration continue</mark> ⇒ <mark style="background: #FF5582A6;">Lors du développement, détecter rapidement les erreurs. Faire développer les codeurs à coder des testeurs pour réduire boucle de feedback</mark>
	1. Pratique de dév logiciel où les membres d'une équipe  intègrent fréquemment leur travail, généralement plusieurs fois par jour. Chaque intégration vérifiée par compilation automatisée et tests
	2. Configurer serveur d'intégration continue
	   Configurer déclencheurs automatique à chaque commit
	   Mettre en place notif en cas d'échec
	3. Un développeur pousse son code sur le dépôt Git. Le serveur CI détecte le changement, compile le code, exécute les tests unitaires et d'intégration, puis notifie l'équipe du résultat.
	4. Détection rapide des prblms d'intégration, réduction du tps de débogage, amélioration de la qualité du code, livraisons plus fréquentes et fiables
	5. Infrastructure initiale, mauvaise configuratin peut ralentir, peut y avoir des bugs qd mm
	6. GitLab / GitHub
- TDD ⇒ <mark style="background: #FF5582A6;">En cours de développement. Il faut faire de l'intégraction continue pour faire du TDD et inversement</mark>
	1. Les tests sont écrits avant les codes de production
	2. Ecrire test qui échoue, écrire code minimal pour faire passer test, refactoriser le code si nécessaire et répéter le process
	3. Un développeur écrit un test pour une nouvelle fonctionnalité de calcul de TVA. Le test échoue initialement. Le développeur implémente ensuite la fonction de calcul de TVA. Le test passe. Le code est refactorisé pour améliorer sa lisibilité.
	4. Meilleure conception du code, documentation vivante sous forme de tests, réduction des bugs
	5. Courbe d'apprentissage importante, peut ralentir dév initial
	6. Junit
- Pair programming ⇒ <mark style="background: #FF5582A6;">Majoritairement en développement mais aussi interface entre recueil besoins et dév</mark>
	1. Deux programmeurs travaillent ensemble sur le même projet
	2. Former binôme de dév, alterner les rôles pilote et navigateur et changer régulièrement de partenaire
	3. Alice et Bob travaillent ensemble sur une nouvelle fonctionnalité. Alice code pendant que Bob examine chaque ligne, suggère des améliorations et réfléchit à la structure globale. Ils échangent leurs rôles toutes les 30 minutes.
	4. Partager les connaissances, réductino des erreurs, amélioration de la qualité du code, renforcement cohésion d'équipe
	5. Moins productif à court terme et bonne compatibilité entre les devs
- Planner poker ⇒ <mark style="background: #FF5582A6;">Durant les spécifications</mark>
	1. technique d'estimation consensuelle, principalement utilisée pour estimer l'effort ou la taille relative des tâches dans le développement logiciel
	2. Présenter une user story ou une tâche à l'équipe, chaque membre estime secrètement la complécité, tous révèlent simultanément leurs estimations et disputent des écarts et atteignent un consensus
	3. L'équipe doit estimer la complexité d'une nouvelle fonctionnalité de recherche. Chaque membre choisit une carte (1, 2, 3, 5, 8, 13). Après discussion sur les différentes estimations, l'équipe s'accorde sur un 8
	4. Estimation plus précise grace à l'intelligence collective, favoriser participation de tous les membres de l'équipe, réduire l'influence des personnalités dominantes
	5. Prends du tps
	6. <mark style="background: #FF5582A6;">Méthode d'estimation de charges. Basé sur la suite de Fibonnacci jusqu'à 13 puis 20, 40, 100, ?, +infini</mark>
- Timeboxing ⇒ <mark style="background: #FF5582A6;">Tout le temps</mark>
	- <mark style="background: #FF5582A6;">Allocation par avance du temsp fixe pour une tâche ou le développement d'un user stories afin d'éviter les effets loi de Parkinson et la procrastination. Peut découler d'un séancer de planning poker et attribution de plages horaires spécifiques et définies pour la résalisation de tâches dédiées. A compléter avec la matrice d'Eisenhower consistant à classer tâche en focntion de leur urgence et de leur importance ce qui permet de prioriser et / ou avec la méthode KANBAN</mark>
- User stories ⇒ <mark style="background: #FF5582A6;">Spécifications. Centré utilisateur</mark>
- Réussinage de code ⇒ <mark style="background: #FF5582A6;">Après le développement</mark>
	- Restructurer le code existant sans modifier les fonctionnalités
	- Améliorer qualité du code et sa réutilisabilité
	- Gain de temps sur le long terme
	- Ne pas confondre avec maintenabilité ⇒ Maintenabilité se concentre sur facilité de gestion à long terme du code alors que réusinage se concentre sur favoriser réutilisation du code déjà existant
- Kanban de tâches ⇒ <mark style="background: #FF5582A6;">Durant les spécifications</mark>
	- <mark style="background: #FF5582A6;">Système visuel de gestion des tâches permettant d'optimiser productivité en limitant nombre de tâches en cours et en évitant surmenage</mark>

- <mark style="background: #FF5582A6;">Non-régression : L'ajout de nouveau code ne nuie pas au précédant code précédemment réalisé</mark>


- Recueil des besoins et spécifications
	- User stories
- Réalisation
	- Intégration continue
	- TDD
	- Pair programming
- Amélioration continue
	- Réussinage du code
- Gestion du temps
	- Planning poket
	- Timeboxing
	- Kanban des tâches


Dans le user story, plusieurs Epic (macro-user story) spécifiés regroupant plusieurs {En tant que $x$ je veux $y$ pour $z$ ⇒ User story} et qui peut être décomposé en tâches

---
Questions :
1. Donner les 7 critères de l'agilité
2. SCRUM → Quelle organisation et quels temps forts ?
3. Outils
