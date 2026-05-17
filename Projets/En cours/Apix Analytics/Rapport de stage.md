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


## IV. Réalisation du projet

### 6. Mise en production

La mise en production désigne le processus par lequel une nouvelle version d'un logiciel, développée et testée en environnement local, est installée et rendue opérationnelle sur le serveur réel utilisé par les clients ou par l'entreprise. C'est l'étape finale et critique du cycle de développement : elle mobilise l'ensemble des composants réalisés et exige une coordination précise entre tous les éléments de la PixL Suite. Une erreur à ce stade peut rendre les analyseurs industriels inopérants, ce qui en fait une phase qui demande rigueur et méthode.

#### a. L'environnement de production

Contrairement à l'environnement de développement, qui tourne sur un poste Windows de développeur, le serveur de production est une machine sous **Linux** (distribution Debian). C'est sur cette machine que tournent en permanence tous les services de la PixL Suite, dans des conteneurs Docker isolés. Le développeur n'a pas accès physiquement à cette machine : toute interaction doit se faire à distance, via le réseau.

La structure des fichiers sur ce serveur est organisée sous le répertoire `/usr/bin/apix/`, qui contient l'ensemble des services déployés, leurs fichiers de configuration persistants, leurs journaux d'activité (logs) et leur documentation. Cette organisation centralisée permet de gérer plusieurs versions de la suite sur la même machine et de retrouver facilement les fichiers pertinents lors d'un incident.

#### b. Accès au serveur distant via SSH et MobaXTerm

Pour interagir avec une machine Linux distante depuis Windows, on utilise le protocole **SSH** (Secure Shell). SSH est un protocole réseau chiffré qui permet d'ouvrir un terminal de commande sur une machine distante comme si l'on était physiquement devant elle. Concrètement, une fois connecté en SSH, le développeur tape des commandes Linux qui s'exécutent sur le serveur de production, à plusieurs centaines de kilomètres de son poste.

L'outil utilisé pour cela est **MobaXTerm**, un client SSH graphique pour Windows. Il offre deux fonctionnalités essentielles :

- Un **terminal Linux émulé** : il permet de taper des commandes shell exactement comme sur une machine Linux physique. Le développeur peut naviguer dans l'arborescence des fichiers, lancer des scripts, consulter des logs, redémarrer des services, etc.
- Un **gestionnaire de fichiers par glisser-déposer** : MobaXTerm intègre un navigateur de fichiers qui affiche le contenu du serveur distant en temps réel. Il est possible de faire glisser un fichier depuis le poste Windows directement vers un répertoire du serveur, et inversement. En coulisse, ce transfert utilise le protocole **SCP** (Secure Copy Protocol), qui s'appuie sur SSH pour chiffrer le transfert.

MobaXTerm permet également de sauvegarder les paramètres de connexion (adresse IP, utilisateur, clé d'authentification) sous forme de sessions, ce qui évite de les ressaisir à chaque connexion.

#### c. Les artefacts à déployer

Avant de lancer un déploiement, il faut préparer les fichiers à transférer, appelés **artefacts**. Ces artefacts sont produits en amont par les pipelines de build de chaque dépôt GitLab, et regroupent tout ce dont le serveur a besoin pour faire tourner la nouvelle version.

Pour une mise à jour de PixL API et de PixL Console, les artefacts à récupérer sont les suivants :

- **Les archives ZIP produites par le pipeline CI/CD** : chaque service est empaqueté par son pipeline GitLab dans une archive ZIP structurée. Pour PixL API, l'archive contient le projet Django, ses dépendances Python pré-installées, et **la wheel apix-tools déjà intégrée** — c'est le pipeline qui se charge de la récupérer et de l'inclure dans le paquet final, de sorte que la wheel n'a jamais besoin d'être transférée séparément sur le serveur. Pour PixL Console, l'archive contient le backend Django minimal ainsi que le build du frontend Vue.js, c'est-à-dire les fichiers HTML, JavaScript et CSS produits par `npm run build`, prêts à être servis.

- **Les scripts de mise à jour** (`script_upgrade_pixl_api.sh`, `script_upgrade_pixl_console.sh`) : ce sont des scripts shell Bash qui automatisent toutes les opérations de déploiement pour chaque service. Leur rôle est détaillé dans la section suivante.

#### d. Le processus de déploiement pas à pas

Le déploiement d'une nouvelle version se déroule en plusieurs étapes successives et ordonnées. Chaque étape doit être validée avant de passer à la suivante, car une erreur non détectée peut se propager et rendre le diagnostic plus difficile.

**Étape 1 — Transfert des fichiers vers le serveur.** À l'aide du gestionnaire de fichiers intégré de MobaXTerm, les artefacts préparés sont glissés-déposés depuis le poste Windows vers un répertoire temporaire sur le serveur, typiquement un sous-répertoire dédié aux mises à jour sous `/usr/bin/apix/`. Cette opération utilise SCP en arrière-plan et chiffre les fichiers pendant le transfert, ce qui garantit qu'ils ne peuvent pas être interceptés ou altérés sur le réseau.

**Étape 2 — Attribution des droits d'exécution aux scripts.** Sous Linux, un fichier n'est pas exécutable par défaut : il faut explicitement lui accorder ce droit. Or, lors d'un transfert SCP depuis Windows, les permissions Linux des fichiers ne sont pas toujours préservées correctement. Il est donc nécessaire d'exécuter manuellement la commande suivante dans le terminal SSH pour rendre les scripts exécutables :

```bash
chmod 755 script_upgrade_*.sh
```

La commande `chmod` (pour *change mode*) modifie les permissions d'un fichier sous Linux. La valeur `755` est une notation octale qui signifie : lecture, écriture et exécution pour le propriétaire du fichier (`7`), et lecture et exécution uniquement pour les autres utilisateurs (`5`). Sans cette étape, Linux refuserait de lancer les scripts avec une erreur *Permission denied*.

**Étape 3 — Exécution des scripts de mise à jour.** Une fois les permissions correctement définies, les scripts de mise à jour sont exécutés dans le terminal SSH. Chaque script prend en argument l'archive ZIP récupérée depuis le pipeline CI/CD :

```bash
/scripts/script_upgrade_pixl_api.sh     pixl-api-x.y.z.zip
/scripts/script_upgrade_pixl_console.sh poc-console-x.y.z.zip
```

Le script reçoit l'archive en paramètre afin de savoir quelle version déployer : c'est ce fichier ZIP, produit et versionné par le pipeline GitLab, qui fait office de source de vérité pour le déploiement. Cette conception permet de rejouer un déploiement pour n'importe quelle version passée en fournissant l'archive correspondante, sans modifier le script lui-même.

Ces scripts automatisent un enchaînement d'opérations qui seraient longues et risquées à réaliser à la main : arrêt du conteneur Docker en cours d'exécution, extraction de l'archive ZIP de la nouvelle version, remplacement des anciens fichiers, mise à jour du fichier de variables d'environnement `.env` avec le nouveau numéro de version, reconstruction de l'image Docker, et redémarrage du conteneur. L'utilisation de scripts garantit la reproductibilité du déploiement : chaque mise à jour suit exactement la même séquence d'opérations, ce qui réduit le risque d'erreur humaine et facilite le diagnostic en cas de problème.

**Étape 4 — Vérification de l'état des services.** Une fois les scripts exécutés, il est indispensable de vérifier que chaque service a bien démarré et fonctionne correctement. Cette vérification se fait via des commandes Docker dans le terminal SSH :

```bash
docker ps -a
```

Cette commande liste tous les conteneurs Docker présents sur la machine, qu'ils soient en cours d'exécution ou arrêtés, avec leur état, leur nom, et les ports réseau qu'ils exposent. Un conteneur dont le statut affiche `Up` est en fonctionnement normal ; un statut `Exited` ou `Restarting` indique un problème qui nécessite d'aller consulter les logs du conteneur concerné.

#### e. Architecture Docker et orchestration des services

Il est important de comprendre comment les différents services de la PixL Suite coexistent sur le même serveur, car cela conditionne directement la façon dont le déploiement est géré.

Chaque composant de la suite — PixL API, PixL Console et le serveur Modbus — tourne dans un **conteneur Docker** séparé. Un conteneur Docker est un environnement d'exécution isolé qui embarque le code de l'application, son interpréteur Python (ou tout autre runtime), ses bibliothèques et ses fichiers de configuration, de manière totalement indépendante du système hôte. L'analogie courante est celle d'un appartement dans un immeuble : chaque conteneur dispose de son propre espace, de ses propres ressources, et les défaillances d'un conteneur n'affectent pas directement les autres.

Ces conteneurs sont orchestrés par **Docker Compose**, un outil qui permet de définir et de gérer plusieurs conteneurs comme un ensemble cohérent à l'aide d'un unique fichier de configuration : `docker-compose.yml`. Ce fichier décrit pour chaque service l'image Docker à utiliser, les ports réseau à exposer, les volumes de données à monter (pour que les fichiers de configuration persistent entre les redémarrages), et les dépendances entre services (par exemple, PixL Console dépend de PixL API pour fonctionner).

Un fichier annexe, `.env`, centralise les variables d'environnement partagées par tous les services, dont en particulier les numéros de version de chaque image Docker. Ce découplage entre la définition de l'architecture (`docker-compose.yml`) et les valeurs concrètes (`.env`) permet de mettre à jour une version sans toucher à la structure du déploiement.

#### f. Difficultés rencontrées

La mise en production a mis en lumière plusieurs catégories de problèmes qui ne se manifestent pas en développement local et qui sont caractéristiques des environnements de production industriels.

**Gestion des permissions Linux.** Linux dispose d'un système de permissions granulaire qui définit, pour chaque fichier et répertoire, qui peut le lire, le modifier ou l'exécuter. Les fichiers transférés depuis Windows par SCP héritaient parfois de permissions inadaptées au contexte de production : des scripts non exécutables bloquaient le déploiement, des répertoires de logs étaient inaccessibles en écriture par les processus applicatifs, ou des fichiers de configuration étaient lisibles par des utilisateurs non autorisés. Il a fallu définir rigoureusement les droits selon la nature de chaque fichier. Les répertoires recevaient la valeur `2750` : la lecture et l'exécution pour le groupe (mais pas l'écriture), et le bit SGID (le chiffre `2`) qui force les nouveaux fichiers créés dans le répertoire à hériter automatiquement du groupe parent. Les fichiers de configuration recevaient `0640` (lecture-écriture pour le propriétaire, lecture seule pour le groupe, aucun droit pour les autres), et les scripts `0755`.

**Orchestration Docker et conflits d'état.** Un problème récurrent lors des mises à jour consistait en des conflits entre l'ancien et le nouvel état des conteneurs. Si un conteneur de l'ancienne version occupait encore un port réseau au moment où le nouveau tentait de démarrer, ce dernier échouait avec une erreur de conflit de port. La solution est de toujours effectuer un arrêt complet de l'ensemble des services avant de lancer la nouvelle version :

```bash
docker-compose down
```

Cette commande arrête proprement tous les conteneurs définis dans le `docker-compose.yml` et libère les ressources réseau associées, évitant ainsi tout conflit lors du redémarrage. De même, une mise à jour incomplète du fichier `.env` — par exemple, si la version de PixL API était mise à jour mais pas celle de PixL Console — entraînait des incompatibilités entre services, car ils ne partageaient plus les mêmes formats de données ou les mêmes protocoles de communication internes.

**Divergence entre environnement de développement et de production.** Certains problèmes ne se manifestaient qu'en production et étaient absents en développement local. Le cas le plus représentatif concerne les chemins vers les fichiers de configuration. En développement, les fichiers `custom.json` et les fichiers de protocole se trouvaient dans des répertoires relatifs au projet, facilement accessibles. En production, la structure des répertoires est différente : les fichiers de configuration sont dans `/usr/bin/apix/Settings/`, séparés des exécutables. Des chemins codés en dur dans le code source, qui fonctionnaient en local, pointaient vers des emplacements inexistants en production. Ces situations ont mis en évidence l'importance de ne jamais coder en dur des chemins de fichiers dans le code source, et de toujours les rendre configurables via des variables d'environnement ou des paramètres, ce que le mécanisme `CUSTOM_CONFIG_PATH` introduit dans PixL API permettait précisément de faire.


#### g. Résultats et apports

À l'issue des déploiements successifs, l'ensemble des composants de la PixL Suite fonctionnait correctement en production. Le serveur Modbus répondait aux requêtes des équipements industriels connectés ; l'API REST exposait ses routes avec la wheel apix-tools correctement intégrée, permettant la lecture et l'écriture dynamiques des fichiers de protocole ; la console web servait l'interface Vue.js et communiquait correctement avec l'API.

Au-delà du résultat technique, cette phase de mise en production a constitué une expérience particulièrement formatrice. Elle m'a confronté à une réalité de l'ingénierie logicielle souvent sous-estimée en formation : la distance qui sépare un code qui fonctionne en développement local d'un code qui fonctionne de manière fiable et durable en production. Les contraintes sont d'une nature différente — permissions système, isolation des conteneurs, gestion des versions entre services interdépendants, vérification systématique de chaque maillon de la chaîne — et ne peuvent s'appréhender pleinement qu'en les rencontrant concrètement.