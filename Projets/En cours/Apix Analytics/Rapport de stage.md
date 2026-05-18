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

La structure des fichiers sur ce serveur est organisée sous le répertoire apix, qui contient l'ensemble des services déployés, leurs fichiers de configuration persistants (notamment `custom.json` qui contrôle le choix du fichier de protocole), leurs journaux d'activité (logs) et leur documentation. Cette organisation centralisée permet de gérer plusieurs versions de la suite sur la même machine et de retrouver facilement les fichiers pertinents lors d'un incident.

#### b. Accès au serveur distant via SSH et MobaXTerm

Pour interagir avec une machine Linux distante depuis Windows, on utilise le protocole **SSH** (Secure Shell). SSH est un protocole réseau chiffré qui permet d'ouvrir un terminal de commande sur une machine distante comme si l'on était physiquement devant elle. Concrètement, une fois connecté en SSH, le développeur tape des commandes Linux qui s'exécutent sur le serveur de production, à plusieurs centaines de kilomètres de son poste.

L'outil utilisé pour cela est **MobaXTerm**, un client SSH graphique pour Windows. Il offre deux fonctionnalités essentielles :

- Un **terminal Linux émulé** : il permet de taper des commandes shell exactement comme sur une machine Linux physique. Le développeur peut naviguer dans l'arborescence des fichiers, lancer des scripts, consulter des logs, redémarrer des services, etc.
- Un **gestionnaire de fichiers par glisser-déposer** : MobaXTerm intègre un navigateur de fichiers qui affiche le contenu du serveur distant en temps réel. Il est possible de faire glisser un fichier depuis le poste Windows directement vers un répertoire du serveur, et inversement. En coulisse, ce transfert utilise le protocole **SCP** (Secure Copy Protocol), qui s'appuie sur SSH pour chiffrer le transfert.

MobaXTerm permet également de sauvegarder les paramètres de connexion (adresse IP, utilisateur, clé d'authentification) sous forme de sessions, ce qui évite de les ressaisir à chaque connexion.

#### c. Les artefacts à déployer et le flux de la wheel apix-tools

Avant de lancer un déploiement, il faut préparer les fichiers à transférer, appelés **artefacts**. Ces artefacts sont produits en amont par les pipelines de build de chaque dépôt GitLab, et regroupent tout ce dont le serveur a besoin pour faire tourner la nouvelle version.

Le flux complet de la wheel apix-tools jusqu'à la production est le suivant : l'alternant compile la wheel apix-tools (versions Windows pour développement et Linux pour production) et la stocke dans un dépôt partagé. Lors du lancement du pipeline CI/CD de PixL API, celui-ci récupère automatiquement la wheel apix-tools spécifiée par son numéro de version dans le fichier `requirements.txt`, et l'intègre directement dans l'archive ZIP finale. De cette façon, lorsque l'archive ZIP est extraite sur le serveur de production, la wheel apix-tools se trouve déjà à l'intérieur (dans le répertoire `whl/` de l'archive), prête à être installée. C'est le pipeline qui gère cette intégration, éliminant le besoin de transférer la wheel séparément.

Pour une mise à jour de PixL API, PixL Console et PixL Modbus, les artefacts à récupérer sont les suivants :

- **Les archives ZIP produites par le pipeline CI/CD** : chaque service est empaqueté par son pipeline GitLab dans une archive ZIP structurée.
  - **PixL API** (`pixl-api-x.y.z.zip`) : contient le projet Django, ses dépendances Python, et **la wheel apix-tools déjà intégrée dans le répertoire `whl/`**. Cette intégration dans le ZIP garantit que tous les éléments nécessaires sont présents lors du déploiement.
  - **PixL Console** (`pixl-console-x.y.z.zip`) : contient le backend Django minimal (API endpoints uniquement), ainsi que le build du frontend Vue.js, c'est-à-dire les fichiers HTML, JavaScript et CSS produits par `npm run build`, prêts à être servis.
  - **PixL Modbus** (fourni sous forme de `.deb` ou `.tgz`) : le serveur Modbus qui dépend également de la wheel apix-tools pour ses fonctionnalités internes.

- **Les scripts de mise à jour** (`script_upgrade_pixl_api.sh`, `script_upgrade_pixl_console.sh`, `script_upgrade_pixl_modbus.sh`) : ce sont des scripts shell Bash qui automatisent toutes les opérations de déploiement pour chaque service. Leur rôle est détaillé dans la section suivante.

#### d. Le processus de déploiement pas à pas

Le déploiement d'une nouvelle version se déroule en plusieurs étapes successives et ordonnées. Chaque étape doit être validée avant de passer à la suivante, car une erreur non détectée peut se propager et rendre le diagnostic plus difficile.

**Étape 1 — Transfert des fichiers vers le serveur.** À l'aide du gestionnaire de fichiers intégré de MobaXTerm, les artefacts préparés sont glissés-déposés depuis le poste Windows vers un répertoire temporaire sur le serveur, typiquement un sous-répertoire dédié aux mises à jour sous `/usr/bin/apix/updates/`. Cette opération utilise SCP en arrière-plan et chiffre les fichiers pendant le transfert, ce qui garantit qu'ils ne peuvent pas être interceptés ou altérés sur le réseau.

**Étape 2 — Attribution des droits d'exécution aux scripts.** Sous Linux, un fichier n'est pas exécutable par défaut : il faut explicitement lui accorder ce droit. Or, lors d'un transfert SCP depuis Windows, les permissions Linux des fichiers ne sont pas toujours préservées correctement. Il est donc nécessaire d'exécuter manuellement la commande suivante dans le terminal SSH pour rendre les scripts exécutables :

```bash
chmod 755 script_upgrade_*.sh
```

La commande `chmod` (pour *change mode*) modifie les permissions d'un fichier sous Linux. La valeur `755` est une notation octale qui signifie : lecture, écriture et exécution pour le propriétaire du fichier (`7`), et lecture et exécution uniquement pour les autres utilisateurs (`5`). Sans cette étape, Linux refuserait de lancer les scripts avec une erreur *Permission denied*.

**Étape 3 — Exécution des scripts de mise à jour.** Une fois les permissions correctement définies, les scripts de mise à jour sont exécutés dans le terminal SSH. Chaque script prend en argument l'archive récupérée depuis le pipeline CI/CD :

```bash
bash script_upgrade_pixl_api.sh     pixl-api-1.0.0.zip
bash script_upgrade_pixl_console.sh pixl-console-1.0.0.zip
bash script_upgrade_pixl_modbus.sh  apix-pixl-modbus-4.4.2.tgz
```

Le script reçoit l'archive en paramètre afin de savoir quelle version déployer : c'est ce fichier ZIP ou TGZ, produit et versionné par le pipeline GitLab, qui fait office de source de vérité pour le déploiement. Cette conception permet de rejouer un déploiement pour n'importe quelle version passée en fournissant l'archive correspondante, sans modifier le script lui-même.

Ces scripts automatisent un enchaînement d'opérations qui seraient longues et risquées à réaliser à la main : arrêt du conteneur Docker en cours d'exécution, extraction de l'archive de la nouvelle version, remplacement des anciens fichiers, mise à jour du fichier de variables d'environnement `.env` avec les nouveaux numéros de version, reconstruction de l'image Docker, et redémarrage du conteneur. L'utilisation de scripts garantit la reproductibilité du déploiement : chaque mise à jour suit exactement la même séquence d'opérations, ce qui réduit le risque d'erreur humaine et facilite le diagnostic en cas de problème.

**Étape 4 — Vérification de l'état des services.** Une fois les scripts exécutés, il est indispensable de vérifier que chaque service a bien démarré et fonctionne correctement. Cette vérification se fait via des commandes Docker dans le terminal SSH :

```bash
docker ps -a
docker-compose logs pixl-api
docker-compose logs pixl-console
```

La commande `docker ps -a` liste tous les conteneurs Docker présents sur la machine, qu'ils soient en cours d'exécution ou arrêtés, avec leur état, leur nom, et les ports réseau qu'ils exposent. Un conteneur dont le statut affiche `Up` est en fonctionnement normal ; un statut `Exited` ou `Restarting` indique un problème qui nécessite d'aller consulter les logs du conteneur via `docker-compose logs [service_name]`.

#### e. Architecture Docker et orchestration des services

Il est important de comprendre comment les différents services de la PixL Suite coexistent sur le même serveur, car cela conditionne directement la façon dont le déploiement est géré.

Chaque composant de la suite — PixL API, PixL Console et le serveur Modbus — tourne dans un **conteneur Docker** séparé. Un conteneur Docker est un environnement d'exécution isolé qui embarque le code de l'application, son interpréteur Python (ou tout autre runtime), ses bibliothèques et ses fichiers de configuration, de manière totalement indépendante du système hôte. L'analogie courante est celle d'un appartement dans un immeuble : chaque conteneur dispose de son propre espace, de ses propres ressources, et les défaillances d'un conteneur n'affectent pas directement les autres.

Ces conteneurs sont orchestrés par **Docker Compose**, un outil qui permet de définir et de gérer plusieurs conteneurs comme un ensemble cohérent à l'aide d'un unique fichier de configuration : `docker-compose.yml`. Ce fichier décrit pour chaque service l'image Docker à utiliser, les ports réseau à exposer, les volumes de données à monter (pour que les fichiers de configuration, notamment `custom.json`, persistent entre les redémarrages), et les dépendances entre services (par exemple, PixL Console dépend de PixL API pour fonctionner).

Un fichier annexe, `.env`, centralise les variables d'environnement partagées par tous les services :

```
PIXL_API_VERSION=1.0.0
PIXL_CONSOLE_VERSION=1.0.0
PIXL_MODBUS_VERSION=4.4.2
APIX_TOOLS_VERSION=3.1.0
```

Ce découplage entre la définition de l'architecture (`docker-compose.yml`) et les valeurs concrètes (`.env`) permet de mettre à jour une version sans toucher à la structure du déploiement. Les scripts de mise à jour modifient automatiquement ces variables dans le fichier `.env` pour refléter les nouvelles versions déployées.

#### f. Difficultés rencontrées

La mise en production a mis en lumière plusieurs problèmes qui ne se manifestent pas en développement local.

**Erreur de version en cascade : mauvaise référence dans le fichier `.env`.** La principale difficulté rencontrée lors de la mise en production était une incohérence entre les numéros de version spécifiés dans le fichier `.env` et les archives réellement déployées. Concrètement, lors du déploiement de PixL Console, le script d'installation avait mis à jour `PIXL_CONSOLE_VERSION` avec le nouveau numéro de version, mais n'avait pas correctement mis à jour `APIX_TOOLS_VERSION` pour refléter la nouvelle version de la wheel apix-tools intégrée dans le ZIP. Résultat : au démarrage du conteneur PixL API, celui-ci tentait de charger la wheel apix-tools en se basant sur le numéro de version spécifié dans `.env` (l'ancienne version), ne la trouvait pas, et échouait avec une erreur `ModuleNotFoundError: No module named 'apix_tools'`. La wheel était bien présente sur le serveur avec le nouveau numéro de version — mais `.env` n'avait pas été mis à jour pour le refléter.

Pour identifier ce bug, nous avons consulté les logs du conteneur via `docker-compose logs pixl-api`, qui affichait l'erreur de module introuvable, puis comparé le numéro de version dans `.env` (`APIX_TOOLS_VERSION=3.0.0`) avec la version réelle du fichier wheel présent dans l'archive (`apix_tools-3.1.0-py3-none-linux_x86_64.whl`). Une fois l'incohérence constatée, il a suffi de corriger manuellement `.env` avec le bon numéro de version et de redémarrer le conteneur via `docker-compose restart pixl-api`.

Ce type de bug est particulièrement difficile à diagnostiquer en production : le script de déploiement s'exécute sans signaler d'erreur explicite, mais le conteneur échoue au démarrage avec un message qui pointe vers la wheel manquante plutôt que vers le véritable problème — l'absence de mise à jour de `.env`.

**Migrations Django dans un état incohérent.** Un deuxième ensemble de problèmes est apparu en raison des migrations Django. Dans Django, les migrations sont des fichiers qui décrivent l'évolution du schéma de la base de données au fil du temps. Lorsqu'un conteneur démarre, Django exécute automatiquement les migrations en attente avant de pouvoir servir des requêtes. En raison du refactoring important de PixL Console — passage d'un backend Django monolithique à une API REST couplée à un frontend Vue.js — certaines migrations anciennement créées n'étaient plus applicables à la nouvelle structure du code, créant un état incohérent qui bloquait le démarrage du conteneur. Il a fallu identifier les migrations problématiques en analysant les logs Django, corriger leur état, et vérifier la cohérence entre la base de données et les migrations restantes.

#### g. Résultats et apports

À l'issue des déploiements successifs et après correction des problèmes identifiés, l'ensemble des composants de la PixL Suite fonctionnait correctement en production. Le serveur Modbus répondait aux requêtes des équipements industriels connectés ; l'API REST exposait ses routes avec la wheel apix-tools correctement intégrée, permettant la lecture et l'écriture dynamiques des fichiers de protocole définis dans `custom.json` ; la console web servait l'interface Vue.js et communiquait correctement avec l'API.

Au-delà du résultat technique, cette phase de mise en production a constitué une expérience formatrice sur la rigueur qu'exige un environnement de production. Des erreurs en apparence anodines — un numéro de version mal synchronisé dans `.env`, des migrations dans un état incohérent — peuvent bloquer complètement un déploiement ou produire un comportement incorrect difficile à diagnostiquer à première vue. Cette expérience m'a appris l'importance de vérifier systématiquement chaque étape après exécution, de valider la cohérence entre les variables d'environnement et les artefacts réellement présents, et de ne pas considérer qu'un script qui « ne produit pas d'erreur » a nécessairement produit le résultat attendu. En production, le silence n'est pas synonyme de succès : il faut toujours valider activement l'état final du système.