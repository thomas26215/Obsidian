#### 2. Le produit — La PixL Suite

Le cœur du savoir-faire d'APIX Analytics réside dans sa **PixL Suite**, un ensemble de logiciels interdépendants qui pilotent intégralement l'analyseur. Chaque composant a un rôle bien défini.

**PixL Core** est l'orchestrateur général de l'analyseur. Déployé directement sur le PC embarqué sous Debian, il gère la communication avec les cartes électroniques, pilote le traitement des chromatogrammes et assure la coordination entre tous les modules internes.

**PixL Console** est l'interface web complète destinée aux utilisateurs avancés. Accessible depuis un navigateur local ou distant, elle donne accès aux commandes, configurations et résultats de l'analyseur, et permet notamment la calibration semi-automatique et la visualisation des chromatogrammes. Elle est disponible en français, anglais et polonais.

**PixL Expert** est le successeur de PixL Console, actuellement en cours de développement. C'est une interface web nouvelle génération basée sur Vue.js, conçue pour moderniser et remplacer progressivement PixL Console. C'est dans ce logiciel que s'inscrit directement mon travail de stage.

**PixL Api** est une API REST sécurisée en HTTPS, accessible aussi bien en interne par les autres logiciels APIX qu'en externe par les clients. Elle sert de passerelle entre PixL Core et les applications tierces, et est documentée via Swagger.

**PixL Modbus** expose les données de l'analyseur via le protocole Modbus (série et TCP/IP simultanément), permettant l'intégration avec des systèmes industriels tiers tels que des automates ou des systèmes SCADA. Il est déployé dans un conteneur Docker.

Plusieurs logiciels de la suite partagent des librairies communes pour éviter la duplication de code : **Apix Tools**, qui regroupe le code utilitaire partagé entre tous les composants, et **Apix Database**, dédiée à la gestion des modèles de base de données entre PixL Api et PixL Console. L'infrastructure repose sur Docker pour la conteneurisation, PostgreSQL comme base de données, et une signature logicielle SHA-256 pour tous les composants de la suite.