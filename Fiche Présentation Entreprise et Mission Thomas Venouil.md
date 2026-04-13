# Présentation Entreprise & Mission — Stage S6

**Venouil Thomas** | IUT2 Grenoble — BUT Informatique | Stage du 23 mars au 26 juin 2026  
**Tuteur IUT :** Élodie Baral-Baron

---

## Partie I — Présentation de l'entreprise

### L'entreprise APIX Analytics

Fondée en 2014 par Pierre Puget et Éric Colinet, Apix Analytics est une PME grenobloise spécialisée dans la commercialisation d'analyseurs de gaz basés sur la **chromatographie en phase gazeuse**, une méthode d'analyse permettant de détecter et quantifier les différents composants d'un gaz. L'entreprise dispose d'une filiale en Chine (NCX) ainsi que d'un site de production situé à Garlin (Pau).

Les analyseurs d'Apix sont des appareils industriels *in situ*, directement branchés sur les lignes de production, qui fonctionnent en continu (24h/24, 7j/7). Les deux marchés principaux sont :

- **La pétrochimie**, pour l'analyse de gaz dérivés du pétrole (clients : TotalEnergies, Aristot, Regas… ; concurrents : ABB, Siemens, Agilent) ;
- **Le biogaz**, pour l'analyse du biogaz et du gaz naturel (clients : MECI/GRDF, Integrotech… ; concurrents : Inficon, Emerson, Agilent).

Les clients visés sont principalement des intégrateurs (Regas, Integrotech, MECI) ainsi que des acteurs majeurs de l'industrie gazière (Engie, TotalEnergies, Air Liquide). Le modèle économique repose sur la vente d'équipements et de licences logicielles, complétée par des prestations de service après-vente.

### L'équipe d'accueil

Apix Analytics compte **15 employés**, répartis en plusieurs équipes :

- Une équipe commerciale (3 personnes) ;
- Une équipe administrative (4 personnes) ;
- Une équipe **développement produit** (4 personnes), au sein de laquelle j'effectue mon stage.

L'équipe de développement produit possède une connaissance globale et approfondie de l'architecture logicielle des systèmes Apix. Elle est supervisée par **Sébastien Rattier**.

**Tuteur professionnel :** Élodie Baral-Baron, qui encadre les stagiaires et alternants au sein de l'équipe technique. Elle assure le suivi de l'avancement des missions, valide les choix d'implémentation et accompagne l'intégration dans l'environnement de travail de l'entreprise.

### Environnement de travail

L'architecture logicielle des systèmes Apix s'articule autour d'un ordinateur embarqué tournant sous **Debian 12 (Bookworm)**, sur lequel sont déployés plusieurs composants :

- **PixlCore** : orchestrateur principal gérant la communication avec les cartes électroniques ;
- **Pixl API** : API REST (Python/Django) exposant les données et services aux interfaces ;
- **PixlExpert** : web application (Vue.js) constituant l'interface utilisateur de contrôle de l'analyseur ;
- **ApixTools** : bibliothèque interne Python fournissant des utilitaires (logger, audit…) ;
- **ApixCommunication** : bibliothèque interne gérant la communication bas-niveau avec les équipements (TCP/IP, RS232, Modbus).

Le développement suit une organisation **semi-agile** avec des sprints hebdomadaires, des points d'avancement réguliers, et un versioning Git avec des conventions de commits explicites (`ADD/FIX/REMOVE : description`).

---

## Partie II — Présentation de la mission

### Objectif général

Les systèmes Apix sont pilotés par un ensemble de **fichiers de configuration JSON**, chacun correspondant à un module fonctionnel du système (paramètres réseau, registres Modbus, etc.). Jusqu'à présent, toute modification de ces paramètres nécessitait d'**éditer manuellement les fichiers JSON** directement sur le système, ce qui implique un accès technique au serveur et présente des risques d'erreurs pour des utilisateurs non développeurs.

Ma mission consiste à **concevoir et intégrer dans PixlExpert une interface graphique permettant de visualiser et modifier ces paramètres de configuration**, en s'appuyant sur l'API existante, sans jamais exposer directement les fichiers JSON à l'utilisateur. L'interface doit couvrir progressivement plusieurs modules de configuration, en commençant par les **paramètres réseau** (configuration du port TCP, de l'identifiant Modbus, des ports ZMQ…), puis en s'étendant à d'autres modules comme la **configuration des registres Modbus**.

### Utilisateurs cibles

L'outil est destiné aux **techniciens de mise en service et ingénieurs** utilisant PixlExpert pour configurer et superviser les analyseurs Apix. Ces utilisateurs ont des connaissances métier en instrumentation industrielle, mais ne sont pas nécessairement développeurs — la modification directe de fichiers JSON n'est donc pas envisageable pour eux en conditions réelles.

### Existant

Les paramètres de configuration des systèmes Apix sont stockés sous forme de **fichiers JSON versionnés** (avec un hash d'intégrité), accessibles via la Pixl API. Il n'existe actuellement **aucune interface graphique** permettant de les consulter ou modifier depuis PixlExpert. Toute intervention sur ces paramètres nécessite donc un accès direct au système de fichiers du serveur embarqué.

### Fonctionnalités à implémenter

- Pages et composants Vue.js pour l'édition des différents modules de configuration JSON ;
- Interface de **paramétrage réseau** (premier livrable) : configuration du port TCP, de l'identifiant esclave Modbus, des ports et adresse ZMQ ;
- Extension progressive vers d'autres modules, notamment la **configuration des registres Modbus** (register map) ;
- Endpoints API Python (Pixl API) pour lire et écrire les configurations, en garantissant l'intégrité des données (validation, gestion du hash) ;
- Validation côté interface des valeurs saisies (types, plages autorisées) avant envoi à l'API.

### Technologies utilisées

| Couche | Technologie |
|--------|-------------|
| Frontend | Vue.js 3 (Composition API, Pinia) |
| Backend | Python 3 (API REST Django) |
| Format de configuration | JSON (avec hash d'intégrité) |
| Maquettes | Figma |
| Versioning | Git |

Les choix technologiques sont imposés par l'existant de PixlExpert. Les marges de décision portent sur l'organisation interne des composants Vue.js et la structuration des endpoints API, arbitrées avec la tutrice selon des critères de maintenabilité et de cohérence avec le code existant.

### Spécification de la mission

La mission a été spécifiée à partir d'échanges avec la tutrice et d'une analyse du code et des fichiers de configuration existants. Des maquettes Figma sont réalisées avant chaque nouvelle fonctionnalité pour valider l'interface. Une documentation technique sera produite en fin de stage.

### Processus de développement

Le développement est organisé de façon itérative : chaque module de configuration fait l'objet d'un cycle complet analyse → maquette → backend → tests → frontend → intégration, avec un point hebdomadaire permettant de valider chaque livrable avant de passer au suivant.

### Suivi et évaluation

- **Points hebdomadaires** avec la tutrice pour faire le bilan du sprint et planifier la semaine suivante ;
- **Revues de code** sur Git avant intégration dans la branche principale ;
- **Tests manuels** de l'interface et des endpoints API ;
- Rédaction d'un **rapport de stage** et soutenance orale en fin de période.