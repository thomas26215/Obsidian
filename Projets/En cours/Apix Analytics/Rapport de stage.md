![[Pasted image 20250601140945.png]]

# Rapport de stage

## I. Présentation de l'entreprise

### 1. APIX Analytics — contexte et activité

APIX Analytics est une entreprise grenobloise spécialisée dans le développement de logiciels embarqués pour analyseurs de gaz chromatographiques. Elle conçoit et maintient l'ensemble de la suite logicielle **PixL Suite**, qui pilote ses analyseurs industriels — les **CHROMPIX** et **GREENPIX** — depuis la collecte des données brutes jusqu'à la présentation des résultats aux utilisateurs finaux.

Son activité s'inscrit dans un contexte industriel exigeant, où la fiabilité et la précision des mesures sont primordiales : les analyseurs APIX sont utilisés pour mesurer la composition de gaz industriels dans des environnements variés, tels que des réseaux de distribution de gaz naturel, des sites de production industrielle ou des laboratoires d'analyse.

APIX Analytics est une PME à taille humaine, ce qui implique une organisation agile et une forte polyvalence des équipes. Les développeurs sont amenés à intervenir sur l'ensemble de la pile logicielle, du bas niveau embarqué jusqu'aux interfaces utilisateur web.

---

### 2. Le produit — La PixL Suite

La **PixL Suite** est un ensemble de logiciels interdépendants qui pilotent intégralement les analyseurs APIX. Elle couvre l'intégralité de la chaîne, depuis le traitement des signaux électroniques jusqu'à l'interface utilisateur, en passant par la communication avec des systèmes industriels tiers.

La suite se compose de plusieurs logiciels aux rôles complémentaires : un orchestrateur général déployé sur le PC embarqué de l'analyseur, une API REST sécurisée servant de passerelle vers l'extérieur, un module de communication Modbus permettant l'intégration avec des automates et systèmes SCADA, et des interfaces web permettant aux opérateurs de piloter et configurer l'appareil. L'infrastructure repose sur Docker pour la conteneurisation et PostgreSQL comme base de données.

Parmi ces composants figure **PixL Expert**, une interface web nouvelle génération basée sur Vue.js, actuellement en cours de développement pour moderniser et remplacer l'interface existante. C'est dans ce logiciel que s'inscrit directement mon travail de stage.

---

### 3. L'équipe et mon environnement de travail

Mon stage s'est déroulé dans les locaux d'APIX Analytics à Grenoble, au sein d'un openspace partagé avec l'ensemble de l'équipe de développement, mais également avec les personnes en charge de la gestion des chromatographes. Cette configuration favorise la communication spontanée et facilite les échanges techniques au quotidien.

Ma tutrice de stage est **Élodie Baral-Baron**, qui a assuré le suivi de mon travail et m'a accompagné de manière active tout au long du stage. Loin de me laisser seul face aux difficultés, elle a pris le temps de m'expliquer les aspects techniques du projet au fur et à mesure de mon avancement : le fonctionnement du protocole Modbus, la structure des fichiers de configuration, la signification des différents attributs des registres, ou encore les conventions propres à la codebase d'APIX. Cet encadrement m'a permis de monter en compétence efficacement et d'aborder chaque nouvelle tâche avec une bonne compréhension du contexte. J'ai également bénéficié du soutien de **Sébastien Rattier**, développeur au sein de l'équipe, dont l'aide technique a complété cet accompagnement.

L'organisation du stage reflète bien l'esprit de l'équipe : guidé et soutenu quand j'en avais besoin, mais libre dans la manière d'organiser et de mener mon travail au quotidien. Cette autonomie encadrée a été très formatrice.


## II. Contexte et enjeux du projet

### 1. Problématique : la configuration Modbus dans PixL Expert

Le PixlExpert communique avec des systèmes industriels tiers via le protocole **Modbus**, un standard largement répandu dans l'industrie pour l'échange de données entre équipements. Ce protocole, supporté à la fois en mode série et en mode TCP/IP, permet à des automates ou des systèmes SCADA d'interroger l'analyseur et de récupérer ses mesures en temps réel.

La configuration de cette communication repose sur deux fichiers JSON : `network.json`, qui définit les paramètres réseau de la connexion, et `protocol.json`, qui recense l'intégralité des registres Modbus exposés par l'appareil. Ces fichiers peuvent contenir plusieurs centaines d'entrées, chacune décrivant un registre avec ses propres attributs tels que l'adresse, le format, la taille ou encore le facteur de conversion.

Avant mon stage, il n'existait pas d'interface dédiée à l'édition de ces fichiers dans PixL Expert. Les opérateurs et techniciens devaient modifier directement les fichiers JSON à la main, ce qui représentait plusieurs problèmes concrets : risque élevé d'erreurs de saisie, manipulation peu intuitive pour des non-développeurs, et absence de retour visuel permettant de valider les données saisies. Sur un fichier comme `protocol.json`, qui peut recenser plusieurs centaines de registres répartis en de nombreuses catégories, cette approche manuelle devenait particulièrement fastidieuse et risquée.

### 2. Objectifs du stage

L'objectif de mon stage était de concevoir et développer un outil d'édition des paramètres Modbus intégré directement dans l'interface web PixL Expert. Cet outil devait permettre à un utilisateur de visualiser, modifier et sauvegarder les paramètres contenus dans les fichiers `network.json` et `protocol.json` sans avoir à manipuler ces fichiers directement.

Concrètement, le travail attendu couvrait à la fois le développement backend en Python — pour exposer les données des fichiers JSON via des routes API — et le développement frontend en Vue.js pour construire les interfaces d'édition correspondantes. Ces deux aspects étaient indissociables et ont été développés conjointement tout au long du stage.

Le projet s'est construit de manière itérative, sans cahier des charges formel : les objectifs ont été précisés progressivement au fil des échanges avec ma tutrice, en fonction de l'avancement du développement et des retours obtenus à chaque étape. Cette approche agile m'a demandé une bonne capacité d'adaptation et de communication.

### 3. Contraintes techniques

Le développement de cet outil impliquait plusieurs contraintes techniques importantes.

**Intégration dans la codebase existante.** PixL Expert disposait déjà d'une architecture Vue.js établie, avec des composants réutilisables et des conventions de développement propres au projet. Il fallait s'y conformer : certains composants existants ont pu être réutilisés, d'autres ont dû être créés de toutes pièces en respectant les mêmes patterns. De même côté backend, certaines routes API étaient déjà en place et ont pu être exploitées, tandis que d'autres ont dû être développées spécifiquement pour les besoins du projet.

**Maîtrise du système de modèles Python.** Le backend repose sur un système de sérialisation/désérialisation maison appelé `ModelMother`, qui permet de convertir automatiquement les objets Python en JSON et inversement. Comprendre et utiliser correctement ce mécanisme était indispensable pour développer les routes backend de manière cohérente avec le reste du projet. Ce système sera détaillé dans la partie IV.

**Complexité des données.** Le fichier `protocol.json` est particulièrement volumineux et hiérarchisé, avec plusieurs niveaux d'imbrication et des centaines d'entrées. Concevoir une interface claire et utilisable pour naviguer et éditer ces données sans surcharger l'utilisateur a représenté un véritable enjeu de conception.

**Validation des données.** L'interface devait intégrer un certain niveau de validation des saisies utilisateur, afin d'éviter d'enregistrer des valeurs incohérentes dans les fichiers de configuration. Ces règles de validation s'appuyaient en partie sur des contraintes métier liées au protocole Modbus lui-même.



## III. Méthodes de travail et outils

### 1. Stack technique

Le projet reposait sur deux environnements techniques distincts et complémentaires.

Côté **backend**, le développement s'est fait en **Python**, en s'appuyant sur la codebase existante d'APIX Analytics. Les modifications portaient principalement sur trois dépôts : **Apix Tools**, qui contient les modèles de données partagés, **PixL Api**, qui expose les routes REST consommées par le frontend, et **PixL Console** (POC), qui héberge les bases de PixL Expert.

Côté **frontend**, l'interface a été développée en **Vue.js**, dans le cadre du projet PixL Expert. Vue.js est un framework JavaScript progressif orienté composants, particulièrement adapté à la construction d'interfaces web dynamiques et réactives.

### 2. Outils de développement

**Éditeurs de code.** J'ai utilisé **VS Code** pour le développement frontend Vue.js, et **PyCharm** pour le développement backend Python. Ce choix reflète les points forts de chaque éditeur : PyCharm offre un support avancé pour Python (autocomplétion, débogage, inspection de code), tandis que VS Code est particulièrement adapté au développement web.

**Versionnage.** Le code était versionné avec **Git**, hébergé sur un **GitLab** interne à APIX Analytics. Pour chacun des trois dépôts du projet (Apix Tools, PixL Api, POC Console), j'ai travaillé sur une branche personnelle dédiée, ce qui m'a permis de développer et tester mes modifications sans impacter le code principal.

**Prise de notes.** J'ai utilisé **Obsidian** pour organiser mes notes personnelles tout au long du stage : documentation des concepts appris, suivi des tâches en cours, mémos techniques et points à clarifier. Cet outil m'a permis de garder une trace structurée de mon avancement et de retrouver facilement les informations importantes.

### 3. Organisation et suivi du projet

Le suivi du projet s'est organisé autour d'une **réunion hebdomadaire le lundi** avec ma tutrice Élodie Baral-Baron. Ces points réguliers permettaient de faire le bilan de la semaine écoulée, de clarifier les objectifs de la semaine à venir, et d'échanger sur les éventuels blocages techniques rencontrés.

Entre ces réunions, le travail s'organisait de manière autonome, avec des échanges informels au fil de l'eau dans l'openspace lorsqu'une question ou un problème se présentait. Cette organisation, combinant un cadre régulier et une flexibilité quotidienne, s'est révélée bien adaptée au rythme itératif du projet.