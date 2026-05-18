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

### 1. Phase de découverte et prise en main

#### a. Découverte du protocole Modbus

Avant d'écrire la moindre ligne de code, il était indispensable de comprendre le domaine technique au cœur du projet : le protocole Modbus. Un protocole de communication est un ensemble de règles et de conventions qui permettent à deux équipements numériques de s'échanger des informations de manière structurée et fiable — à la manière d'une langue commune que deux interlocuteurs doivent maîtriser pour se comprendre. Modbus est l'un de ces protocoles, spécifiquement conçu pour les environnements industriels.

**Origine et adoption.** Modbus a été conçu en 1979 par la société Modicon pour permettre la communication entre ses automates programmables industriels. Malgré son âge, il reste aujourd'hui l'un des protocoles les plus répandus dans les environnements industriels, en raison de sa simplicité, de sa robustesse, et de la très large base d'équipements qui le supportent. On le retrouve dans les usines, les réseaux de distribution d'énergie, les stations de traitement des eaux, et naturellement dans les systèmes d'analyse de gaz industriels comme ceux d'APIX Analytics.

**Modèle maître / esclave.** Modbus repose sur un modèle de communication dit maître/esclave. Dans ce modèle, un seul équipement — le maître — a le droit d'initier les échanges. Les autres équipements — les esclaves — attendent passivement les requêtes du maître et y répondent. Concrètement, dans le contexte d'APIX, un automate industriel ou un système SCADA joue le rôle de maître : il interroge régulièrement l'analyseur APIX — qui joue le rôle d'esclave Modbus — pour récupérer ses mesures. L'analyseur ne transmet jamais de données de manière spontanée ; il se contente de répondre aux questions qui lui sont posées.

**Les registres Modbus.** L'échange d'informations via Modbus se fait à travers des registres, que l'on peut assimiler à des cases mémoire numérotées situées dans l'esclave. Chaque registre porte un numéro d'adresse unique et contient une valeur numérique. Le maître lit ou écrit dans ces registres en envoyant des requêtes standardisées. Il existe plusieurs types de registres selon la nature de la donnée :

- Les **holding registers** sont les plus courants : ils contiennent des valeurs numériques, accessibles en lecture et en écriture. C'est dans ces registres que l'analyseur APIX expose ses mesures principales — concentrations de composants, valeurs détaillées de chromatographie.
- Les **input registers** fonctionnent de la même manière, mais sont en lecture seule pour le maître. L'analyseur APIX les utilise pour exposer ses alarmes, les états système, les informations de commande et les informations générales.

**Les modes de transport.** Modbus peut fonctionner sur deux types de liaisons physiques. Modbus RTU utilise une liaison série RS-485 : les équipements sont reliés par un câble physique, et les données circulent sous forme de trames binaires compactes. Modbus TCP encapsule ces mêmes trames dans des paquets réseau standard, ce qui permet de faire transiter la communication sur un réseau Ethernet. L'analyseur APIX supporte ces deux modes simultanément, et les paramètres de chacun sont configurables via `network.json`.

**Formats de données et facteur de conversion.** Les registres Modbus de base ne contenant que des entiers 16 bits, il est souvent nécessaire d'utiliser plusieurs registres consécutifs pour représenter des types plus précis. Par exemple, un nombre à virgule flottante au format Float32 (IEEE 754) occupe deux registres de 16 bits consécutifs. De même, des valeurs comme des concentrations en pourcentage peuvent nécessiter un facteur de conversion (`factor`) : une mesure de 12,34 % sera stockée sous la valeur entière 1234 dans le registre, avec un facteur de 0,01 défini dans la configuration. Ces formats (`float32`, `float16`, `sint16`, etc.) et ces facteurs sont consignés pour chaque registre dans `protocol.json`.

#### b. Prise en main de la codebase PixL Expert existante

Une fois le contexte technique assimilé, la deuxième étape a consisté à explorer et comprendre le code existant. Cette phase est toujours délicate dans un stage : il faut naviguer dans un ensemble de fichiers écrits par d'autres personnes, souvent sans documentation exhaustive, et comprendre non seulement ce que fait le code, mais aussi pourquoi il est structuré ainsi. Pour cette partie du stage, ma tutrice de stage était présente pour m'expliquer les points compliqués dans le code.

**Le dépôt Apix Tools.** Ce dépôt constitue le socle partagé du projet. Il contient les classes Python communes utilisées par l'ensemble des composants de la PixL Suite : les modèles de données, les utilitaires de sérialisation et notamment le système ModelMother. Apix Tools est distribué sous forme de wheel Python — un format d'empaquetage standard qui permet d'installer une bibliothèque Python comme n'importe quel paquet tiers, via la commande `pip install`. Chaque autre dépôt du projet le déclare comme dépendance dans son fichier `requirements.txt`.

**Le dépôt PixL Api.** Ce dépôt contient l'API REST du projet, développée avec le framework Django et son extension Django REST Framework. Une API REST (Representational State Transfer) est une interface de communication entre applications, qui expose des données et des opérations via des URLs standardisées — appelées routes ou endpoints — interrogeables en HTTP. Par exemple, une route `GET /api/modbus/networks` retourne les paramètres réseau Modbus actuels, et une route `POST /api/modbus/networks` permet de les modifier. C'est via ces routes que le frontend Vue.js communique avec le backend Python.

Django impose une organisation précise du code : les applications métier sont regroupées en apps, chacune contenant ses propres vues (`views.py`) — qui contiennent la logique de traitement des requêtes — et son propre fichier de routes (`urls.py`) qui associe chaque URL à une vue.

**Le dépôt PixL Console.** Ce dépôt héberge le projet Vue.js de PixL Expert, l'interface web sur laquelle j'allais travailler. Vue.js est un framework JavaScript progressif orienté composants : l'interface est découpée en blocs autonomes appelés composants, chacun encapsulant sa structure HTML, sa logique JavaScript et ses styles CSS dans un unique fichier `.vue`. Ces composants sont assemblés pour former des vues — les pages de l'application — et communiquent entre eux selon des conventions bien définies.

#### c. Compréhension des fichiers de configuration JSON

Les deux fichiers de configuration JSON ont fait l'objet d'une analyse approfondie dès les premiers jours du stage. JSON (JavaScript Object Notation) est un format textuel d'échange de données, extrêmement répandu en développement web et dans les API REST. Il représente les données sous forme de paires clé/valeur, de listes ordonnées et de structures imbriquées.

Cette analyse n'était pas purement technique : ma tutrice m'a expliqué la signification métier de chaque champ et les règles de cohérence à respecter. Ces règles, absentes des fichiers eux-mêmes, étaient indispensables pour concevoir une interface qui guide l'utilisateur sans lui permettre de saisir des données incohérentes — deux registres ne peuvent par exemple pas partager la même adresse, et le format d'un registre détermine strictement le nombre de cases mémoire qu'il occupe (`size`), ce qui conditionne à son tour l'adressage de tous les registres suivants.

---

### 2. Architecture backend — ModelMother

#### a. Le problème que résout ModelMother

Pour comprendre le rôle de ModelMother, il faut d'abord comprendre le problème qu'il résout.

Le backend Python manipule les données de configuration sous forme d'objets — des structures en mémoire qui regroupent des données et des comportements, selon le paradigme de la programmation orientée objet. Par exemple, un objet `ProtocolParameters` contient un objet `HoldingRegisterParameters`, qui contient lui-même des collections d'`ElementParameters` et d'`AlarmEntryParameters`. Ces objets sont pratiques à manipuler en Python, mais ils ne peuvent pas être directement stockés dans un fichier ou transmis via une API : ils n'existent que le temps où le programme tourne en mémoire.

Pour les stocker ou les transmettre, il faut les **sérialiser** : convertir l'objet en une représentation textuelle standard — ici, du JSON. Et pour les recharger depuis le fichier, il faut les **désérialiser** : reconstruire l'objet Python à partir du dictionnaire JSON lu. Ces deux opérations constituent le cœur du problème de persistance des données.

Sans mécanisme commun, chaque développeur qui crée une nouvelle classe devrait réécrire manuellement cette logique de conversion, au risque d'introduire des inconsistances entre les différentes parties du projet. C'est ce que ModelMother évite en centralisant ce mécanisme.

#### b. Principe et rôle de la classe de base

ModelMother est une classe de base définie dans le module `apix_tools/apix_framework/model/model_mother.py`. En programmation orientée objet, une classe de base est une classe dont d'autres classes héritent : elle définit des comportements communs que toutes ses sous-classes partagent automatiquement, sans avoir à les réécrire.

ModelMother expose deux méthodes fondamentales :
- `get_attributes_as_dict()` est la méthode de sérialisation. Elle parcourt l'ensemble des attributs de l'objet et les convertit en un dictionnaire Python — une structure native équivalente au JSON. Pour chaque attribut, elle adapte la conversion à son type : une valeur simple (entier, flottant, chaîne de caractères, booléen) est copiée directement ; un objet héritant lui-même de ModelMother est sérialisé récursivement en appelant sa propre méthode `get_attributes_as_dict()` ; une liste est parcourue élément par élément ; une énumération est convertie en sa valeur textuelle. ModelMother gère également un mécanisme d'attributs exclus (`excluded_attributes`) : certains attributs de l'objet, utiles en mémoire pour le fonctionnement interne mais non pertinents dans le fichier de configuration, sont déclarés dans cette liste et ignorés lors de la sérialisation. Par exemple, les attributs d'état temps réel d'une alarme (`level`, `metrological`, `critical`) sont présents dans la classe Python mais absents du JSON persisté.
- `set_attributes_from_dict()` est la méthode de désérialisation. Elle prend un dictionnaire en entrée et remplit les attributs de l'objet de manière récursive : pour chaque clé du dictionnaire, elle identifie le type de l'attribut correspondant dans la classe Python et effectue la conversion inverse. Si l'attribut est lui-même un objet ModelMother, la méthode l'instancie et appelle récursivement `set_attributes_from_dict()` sur lui. Elle effectue également des contrôles de validité lors du chargement — par exemple, elle vérifie que les valeurs d'énumération présentes dans le JSON appartiennent bien aux valeurs autorisées — et peut déclencher une méthode de validation métier spécifique à chaque classe, `model_sanity_check()`, que les sous-classes peuvent surcharger.

Grâce à cette récursivité, une seule instruction suffit à charger l'intégralité d'un fichier JSON hiérarchisé en un arbre d'objets Python parfaitement typés, quelle que soit la profondeur d'imbrication.

#### c. La problématique du dictionnaire dans le dictionnaire : ModelDictToListMother

C'est ici qu'intervient une limitation que j'ai rencontrée concrètement lors du développement, et que ma tutrice a résolue en étendant le framework.

Dans `protocol.json`, certaines sections présentent une structure particulière : au lieu d'une liste JSON classique, les éléments y sont stockés sous forme d'un dictionnaire dont les clés sont les noms des éléments. Par exemple, la section `elements_detailed` du holding register ressemble à ceci :

```json
"elements_detailed": {
    "CAL-C2H4": {
        "raw_value":        { "address": 100, "format": "float32", "size": 2, "factor": 1.0 },
        "normalized_value": { "address": 102, "format": "float32", "size": 2, "factor": 1.0 },
        "response":         { "address": 104, "format": "float32", "size": 2, "factor": 1.0 }
    },
    "CAL-C2H6": { "..." },
    "H2S":      { "..." }
}
```

Ce format — un dictionnaire de dictionnaires — est courant dans les fichiers de configuration car il permet d'accéder directement à un élément par son nom. Mais il pose un problème lors de la manipulation en Python : pour parcourir tous les éléments, les trier, en ajouter ou en supprimer, une liste est bien plus pratique et naturelle qu'un dictionnaire. Or, ModelMother dans sa version d'origine ne gérait pas la conversion entre ces deux formes.

Ma tutrice a donc créé une nouvelle classe, `ModelDictToListMother`, accompagnée de deux fonctions récursives : `dictToList` et `fromDictToList`. Ces deux fonctions assurent la conversion bidirectionnelle entre les deux représentations :

- `dictToList` parcourt le dictionnaire JSON keyed par noms et le convertit en une liste Python d'objets, en attachant le nom de la clé comme attribut de chaque objet. Ainsi, `"CAL-C2H4": { ... }` devient un objet `ElementDetailParameters` dont l'attribut `name` vaut `"CAL-C2H4"`.
- `fromDictToList` effectue l'opération inverse lors de la sérialisation : elle reparcourt la liste Python et reconstruit le dictionnaire JSON keyed by name à partir de l'attribut `name` de chaque objet.

La récursivité de ces fonctions est indispensable car la structure peut être profondément imbriquée : un élément détaillé contient lui-même plusieurs propriétés (`raw_value`, `normalized_value`, `response`, etc.), qui sont elles-mêmes des objets. `dictToList` et `fromDictToList` traversent tous ces niveaux sans que le code appelant ait à s'en préoccuper.

Cette extension a été intégrée dans le framework ModelMother de sorte que la méthode `get_attributes_as_dict()` reconnaisse automatiquement les objets `ModelDictToListMother` et leur applique `fromDictToList`, et que `set_attributes_from_dict()` leur applique `dictToList`. L'ajout de ce mécanisme était transparent pour le reste du code : les classes de modèles n'ont eu qu'à déclarer leurs attributs de type `ModelDictToListMother` pour bénéficier automatiquement de cette conversion.

#### d. Hiérarchie des classes de modèles

La hiérarchie des classes reflète directement la structure des fichiers JSON, organisée autour de trois classes de conteneurs :

- `ModelMother` : classe de base pour tous les objets sérialisables atomiques.
- `ModelListMother` : conteneur pour les listes JSON simples (listes de ports série dans `network.json`).
- `ModelDictToListMother` : conteneur pour les dictionnaires JSON keyed by name, convertis en listes Python (`elements_detailed`, `elements`, `alarm`).

Voici la hiérarchie concrète des classes de modèles du projet :

```
ModelMother
├── NetworkParameters          ← paramètres réseau complets (network.json)
│   ├── TcpParameters          ← port TCP, flag enabled
│   └── SerialParametersList   ← liste de ports série (ModelListMother)
│       └── SerialParameters   ← un port série (bauds, parité, bits de stop…)
└── ProtocolParameters         ← protocole complet (protocol.json)
    ├── HoldingRegisterParameters
    │   └── MeasureParameters
    │       ├── ElementsDetailedList  (ModelDictToListMother)
    │       │   └── ElementDetailParameters  ← un élément détaillé
    │       │       └── ElementPropertyParameters  ← raw_value, normalized_value…
    │       └── ElementList           (ModelDictToListMother)
    │           └── ElementParameters ← un élément simple
    └── InputRegisterParameters
        ├── AlarmParametersList       (ModelDictToListMother)
        │   └── AlarmEntryParameters  ← une alarme
        ├── MeasureParameters
        ├── InformationParameters
        ├── SystemParameters
        └── CommandParameters
```

Chaque feuille de cet arbre correspond à un champ concret du JSON — une adresse de registre, un format, un facteur de conversion — et hérite de ModelMother, bénéficiant ainsi automatiquement des mécanismes de sérialisation.

---

### 3. Éditeur de configuration réseau — network.json

#### a. Analyse de la structure du fichier

Le fichier `network.json` décrit comment l'analyseur APIX expose son interface Modbus sur les différents supports de communication disponibles. Sa structure se divise en quatre sections.

**L'identifiant d'esclave (`slave_id`).** C'est un entier compris entre 1 et 247 qui identifie de manière unique l'analyseur sur le bus Modbus. Lorsque plusieurs esclaves coexistent sur le même réseau RS-485, le maître utilise cet identifiant pour s'adresser à un équipement précis.

**La configuration TCP (`tcp`).** Elle contient un flag `enabled` (booléen activant ou désactivant le mode Modbus TCP) et un numéro de port réseau. Un port est un numéro entre 0 et 65535 qui identifie un service sur une machine réseau — à la manière d'un numéro d'appartement dans un immeuble. Le port standard de Modbus TCP est 502.

**La configuration des ports série (`serial`).** Contrairement aux deux sections précédentes, celle-ci est une liste : l'analyseur peut exposer son interface Modbus sur plusieurs liaisons série simultanément. Chaque entrée de la liste correspond à un port physique et possède ses propres paramètres : le chemin du périphérique sous Linux (`/dev/ttyS0`), la vitesse de transmission en bauds (baud rate), le nombre de bits de données (data bits, typiquement 8), la parité (parity : N pour aucune, E pour paire, O pour impaire), le nombre de bits de stop (stop bits, 1 ou 2), le mode de communication (`rtu`), et un délai d'attente de réponse (timeout). Tous ces paramètres doivent être identiques sur l'ensemble des équipements connectés au même bus RS-485 pour que la communication fonctionne.

**La configuration ZMQ.** ZMQ (ZeroMQ) est un protocole de messagerie interne utilisé par les différents composants de la PixL Suite pour communiquer entre eux sur la même machine, en dehors du protocole Modbus. Deux ports ZMQ sont configurés : un port de données (`zmq_data_port`, par défaut 5556) et un port de commande (`zmq_command_port`, par défaut 5557), ainsi que l'adresse IP locale (`zmq_ip`).

```json
{
    "data": {
        "slave_id": 1,
        "tcp": { "enabled": true, "port": 502 },
        "serial": [
            {
                "port": "/dev/ttyS0", "bauds": 9600, "bits": 8,
                "parity": "N", "stops": 1, "method": "rtu",
                "timeout": 0.15, "enabled": false
            }
        ],
        "zmq_command_port": 5557,
        "zmq_data_port": 5556,
        "zmq_ip": "localhost"
    }
}
```

#### b. Développement côté backend

Deux routes ont été créées dans le module `metro_api/settings/modbus/` de PixL Api.

La route `GET /metrological/settings/modbus/networks` charge le fichier `network.json` via la méthode `load_network()` de `NetworkParameters`, qui utilise `set_attributes_from_dict()` pour désérialiser le JSON en objet Python, puis retourne les données sérialisées via `get_attributes_as_dict()`. Cette double conversion garantit que les données retournées sont bien conformes au modèle attendu.

La route `POST /metrological/settings/modbus/networks` reçoit les données modifiées par le frontend, effectue des contrôles de validation, puis sauvegarde le fichier. Les validations implémentées portent sur : la plage du port TCP (0–65535), la plage du port ZMQ (0–65535), le délai d'attente des ports série (entre 0,1 et 5 secondes), et la conformité des valeurs énumérées (vitesse de transmission, parité, méthode) aux valeurs supportées par le serveur Modbus. En cas d'erreur de validation, la route retourne un code HTTP 400 (Bad Request) avec un message explicatif, sans modifier le fichier.

#### c. Développement côté frontend — ModbusPart.vue

L'interface d'édition de `network.json` a été développée dans le composant `ModbusPart.vue`, intégré dans la section Remote Access des paramètres généraux de PixL Expert.

**Chargement des données.** Au montage du composant (`onMounted`), deux appels API sont effectués en parallèle : un premier pour charger les énumérations disponibles (valeurs autorisées pour les vitesses de transmission, parités, méthodes, etc.) et un second pour charger la configuration actuelle du réseau. Les énumérations, fournies par le backend, garantissent que les listes déroulantes du formulaire reflètent exactement les valeurs acceptées par le serveur Modbus — sans duplication de cette logique côté frontend.

**Gestion des ports série.** La partie la plus complexe de l'interface concerne la liste variable de ports série. Comme le fichier peut en contenir plusieurs, l'interface présente un système d'onglets dynamiques : chaque port série dispose de son propre onglet, et des boutons permettent d'en ajouter de nouveaux ou de supprimer l'onglet courant. Chaque onglet présente un formulaire avec les champs du port correspondant : chemin du périphérique (liste déroulante `port_enum`), vitesse de transmission (`baud_rate_enum`), bits de données (`data_bits_enum`), parité (`serial_parity_enum`), bits de stop (`stop_bits_enum`), méthode (`serial_method_enum`), et délai d'attente (champ numérique avec validation).

**Sauvegarde.** À la soumission, les données de l'état local Vue.js sont structurées et envoyées via un POST à la route backend. Un retour visuel confirme la sauvegarde ou signale les erreurs retournées par le backend.

---

### 4. Éditeur de configuration protocole — protocol.json

#### a. Analyse de la structure du fichier

Le fichier `protocol.json` est structurellement bien plus complexe que `network.json`. Il s'organise en deux grandes branches correspondant aux deux types de registres Modbus utilisés.

**Le holding register** expose les mesures principales de l'analyseur. Il contient une section `measure`, elle-même divisée en deux sous-sections :

- `elements_detailed` : les éléments avec mesures détaillées, typiquement les composants mesurés par chromatographie. Chaque entrée est un dictionnaire keyed par le nom du composant (ex. `"CAL-C2H4"`, `"H2S"`). Elle peut contenir jusqu'à cinq types de propriétés, chacune occupant un ou plusieurs registres consécutifs : `raw_value` (valeur brute du détecteur), `normalized_value` (valeur normalisée), `response` (réponse du pic), `peak_start` (début du pic en temps), `peak_end` (fin du pic). Chaque propriété précise son adresse de registre, son format de données (toujours `float32` pour les éléments détaillés, occupant 2 registres), et son facteur de conversion.
- `elements` : les éléments simples, représentant une mesure unique par un seul groupe de registres. Chaque entrée possède une adresse, un format (`float16`, `float32`, etc.), une taille en registres (`size`), et un facteur de conversion.

**L'input register** regroupe les données en lecture seule, organisées en cinq sous-sections : `alarm` (les alarmes), `measure` (mesures supplémentaires), `information` (informations générales sur l'appareil), `system` (état du système), et `command` (registres de commande). La sous-section `alarm` est structurée de la même manière que les éléments : un dictionnaire keyed par nom d'alarme, chaque entrée décrivant l'adresse du registre de statut, son format (toujours `sint16` pour les alarmes, occupant 1 registre), ainsi que des codes de catégorie et de code d'erreur utilisés par le système de gestion des alarmes.

La combinaison de cette imbrication à plusieurs niveaux et du grand nombre d'entrées possibles représentait le principal défi de conception de l'éditeur.

#### b. La route GET /protocol/formats — configuration dynamique de l'interface

Un point architectural notable du projet est l'existence d'une troisième route, `GET /metrological/settings/modbus/protocol/formats`, qui ne retourne pas de données de configuration mais une description de l'interface elle-même. Cette approche, appelée parfois *configuration-driven UI* (interface pilotée par la configuration), permet au backend de dicter au frontend comment se comporter sans que le frontend ait à connaître en dur les règles métier du protocole Modbus.

Cette route retourne notamment :

- La liste des formats de données disponibles (`float32`, `float16`, `sint16`, etc.) avec pour chacun son nom d'affichage, si sa taille en registres est fixe ou flexible, et la taille attendue.
- Les formats acceptés par sous-section : par exemple, les alarmes n'acceptent que `sint16`, les éléments détaillés n'acceptent que `float32`, tandis que les éléments simples acceptent plusieurs formats. Ces règles sont vérifiées à la fois côté frontend (pour guider l'utilisateur) et côté backend (comme garde-fou).
- La configuration des champs à afficher par sous-section : quels champs montrer, sous quel type de contrôle (champ texte, liste déroulante), avec quelles options de sélection.
- Les colonnes du tableau de l'interface et les options des listes déroulantes d'énumération (noms des alarmes disponibles, noms des éléments disponibles, types de propriétés).

Cette architecture présente un avantage significatif : lorsque les règles métier évoluent — par exemple si un nouveau format de données est supporté — seul le backend doit être mis à jour, sans modifier le code frontend.

#### c. Développement côté backend

Les deux routes principales du protocole ont des responsabilités distinctes.

La route `GET /metrological/settings/modbus/protocol` lit le fichier `protocol.json` et retourne son contenu. Contrairement à la route réseau, elle retourne ici la structure JSON directement, sans passer par une désérialisation complète via ModelMother : cela permet de conserver la structure telle qu'elle est dans le fichier, que le frontend réorganise ensuite pour l'affichage.

La route `POST /metrological/settings/modbus/protocol` reçoit la nouvelle version du protocole modifiée par le frontend et la réécrit dans le fichier. Elle invoque une méthode de vérification de cohérence, `_check_protocol_coherence()`, qui parcourt l'ensemble des entrées du protocole et vérifie la cohérence entre le format déclaré et la taille en registres (`size`) associée — car chaque format impose une taille fixe (un `float32` occupe toujours 2 registres, un `sint16` en occupe toujours 1). Les incohérences détectées sont retournées sous forme d'avertissements, permettant à l'interface de les signaler à l'utilisateur sans bloquer la sauvegarde.

#### d. Développement côté frontend — RegisterMapPart.vue

L'interface d'édition de `protocol.json` a été développée dans le composant `RegisterMapPart.vue`. La complexité de ce composant est significativement plus élevée que `ModbusPart.vue`, en raison de la richesse de la structure de données à manipuler.

**Chargement et initialisation.** Au montage, trois appels API sont effectués successivement : la configuration des formats et champs (`/protocol/formats`), les données du protocole actuel (`/protocol`), et les données de la configuration du registre map. Ces données permettent de construire l'état interne du composant : une liste plate d'entrées de registres (`registerMap.entries`), plus facile à afficher et à manipuler dans un tableau qu'une hiérarchie imbriquée.

**La grille AG Grid.** Le cœur de l'interface est un tableau interactif réalisé avec AG Grid, une bibliothèque JavaScript spécialisée dans les tableaux de données complexes. Chaque ligne du tableau représente un registre ou un groupe de registres, avec les colonnes suivantes : le type de registre (Register : holding ou input), l'adresse (Address), la source (Source : la sous-section `measure`, `alarm`, etc.), le nom (Name), le format (Format), et le facteur de conversion (Factor).

AG Grid a été choisi pour ses fonctionnalités avancées, en particulier le glisser-déposer (drag & drop) des lignes pour réordonner les entrées lorsque le tableau est trié par adresse croissante. Cette fonctionnalité permet à l'utilisateur de visualiser et d'ajuster l'ordre des registres dans la table d'adressage Modbus de manière intuitive. La bibliothèque n'était pas nouvelle dans le projet : un collègue l'avait déjà intégrée dans d'autres parties de PixL Expert et avait développé un fichier utilitaire centralisant la configuration commune des tableaux (définition des options par défaut, gestion des événements récurrents, helpers de formatage). Cela m'a permis d'utiliser AG Grid directement sans avoir à en maîtriser tous les détails d'initialisation, en m'appuyant sur ce socle déjà éprouvé.

**Le formulaire d'ajout et d'édition.** L'ajout d'une nouvelle entrée ou la modification d'une entrée existante (via un bouton Edit en fin de ligne) ouvre une fenêtre modale contenant un formulaire dynamique. Ce formulaire est dit dynamique car son contenu varie selon la sous-section sélectionnée par l'utilisateur, pilotée par la configuration retournée par la route `/protocol/formats` :

- Pour la sous-section `alarm` : le formulaire présente uniquement un sélecteur de nom d'alarme (parmi les alarmes disponibles dans le système, fournies sous forme d'énumération). Le format est imposé à `sint16` et non modifiable, car toutes les alarmes Modbus ont le même format.
- Pour la sous-section `elements` : le formulaire présente un sélecteur de nom d'élément et un champ de facteur de conversion. Le format peut être choisi parmi les formats acceptés pour cette sous-section.
- Pour la sous-section `elements_detailed` : le formulaire présente un sélecteur de nom d'élément, un sélecteur de type de propriété (`raw_value`, `normalized_value`, `response`, `peak_start`, `peak_end`), et un champ de facteur. Le format est imposé à `float32`.

**La détection de conflits d'adresses.** Une fonctionnalité importante de l'éditeur est la détection de chevauchements d'adresses entre registres. Comme chaque format occupe un nombre précis de registres consécutifs (un `float32` occupe les registres à l'adresse N et N+1, un `float16` occupe uniquement le registre N), il est possible que deux entrées se chevauchent si leurs plages d'adresses se recoupent. L'éditeur calcule la plage occupée par chaque entrée à partir de son adresse et de la taille imposée par son format, et signale visuellement dans le tableau toute collision détectée.

**La sauvegarde.** Lors de la sauvegarde, le composant reconstruit la structure hiérarchique de `protocol.json` à partir de la liste plate d'entrées. Cette opération consiste à regrouper les entrées par section (`holding_register` / `input_register`), puis par sous-section (`measure`, `alarm`, etc.), puis par sous-sous-section (`elements`, `elements_detailed`), et enfin à reconstruire les dictionnaires keyed by name attendus par le backend. La structure reconstruite est ensuite envoyée via `POST /metrological/settings/modbus/protocol`.

---

### 5. Tests et validation

La phase de test a été conduite de manière continue et itérative tout au long du développement, selon le principe qu'une fonctionnalité n'est pas terminée tant qu'elle n'a pas été testée dans ses cas nominaux et ses cas limites.

#### a. Tests manuels en cours de développement

À chaque nouvelle fonctionnalité implémentée, des tests manuels étaient effectués directement dans le navigateur sur l'environnement local. Ces tests couvraient systématiquement deux familles de scénarios.

Les **cas nominaux** : saisie de valeurs valides, sauvegarde, rechargement de la page pour vérifier la persistance dans le fichier JSON, puis vérification du fichier résultant dans l'éditeur de code pour s'assurer de la conformité de la structure générée. Cette étape de vérification directe du fichier était systématique : une interface peut sembler correcte visuellement tout en produisant un JSON mal structuré, qui ne sera détecté comme invalide que lors du démarrage du serveur Modbus.

Les **cas limites et cas d'erreur** : port TCP hors plage, timeout série inférieur à 0,1 s, deux registres portant la même adresse, format incompatible avec la sous-section, sous-section d'alarme avec un format autre que `sint16`. Pour chacun, le comportement attendu était une validation explicite bloquant la sauvegarde, avec un message clair indiquant à l'utilisateur la source du problème.

#### b. Vérification de la cohérence des fichiers générés

Après chaque cycle de modification et de sauvegarde, les fichiers JSON résultants étaient inspectés directement dans l'éditeur de code. Les points vérifiés incluaient : la présence de toutes les clés attendues, l'absence de clés parasites ou dupliquées, la correction des types de valeurs (en JSON, `"1"` et `1` sont deux valeurs différentes — l'une est une chaîne de caractères, l'autre un entier — et une confusion entre les deux peut provoquer un comportement inattendu côté serveur Modbus), et la conformité de la structure imbriquée avec le schéma attendu.

La vérification était particulièrement minutieuse pour `protocol.json` : la reconstruction de la structure hiérarchique depuis la liste plate du frontend comportait plusieurs étapes susceptibles d'introduire des erreurs (groupement incorrect des entrées, perte d'une sous-section vide, confusion entre `holding_register` et `input_register`).


---

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