



![[Pasted image 20250601140945.png|180]]


**Année Universitaire : 2025-2026**
**RAPPORT DE STAGE OU D’ALTERNANCE**

---


**DÉVELOPPEMENT D'UNE INTERFACE POUR MODIFIER LES PARAMÈTRES MODBUS**

Apix Analytics

![[apix.png|220]]

---
**Présenté par**

Thomas Venouil

**Jury**

IUT : M. X

IUT : Mme. Y

Société : Mme. Baral-Baron



Par la présente, je déclare être le seul auteur de ce rapport et assure qu’aucune autre ressource que celles indiquées n’ont été utilisées pour la réalisation de ce travail. Tout emprunt (citation ou référence) littéral ou non à des documents publiés ou inédits est référencé comme tel et tout usage à un outil doté d’IA a été mentionné et sera de ma responsabilité. 

Je suis informé qu’en cas de flagrant délit de fraude, les sanctions prévues dans le règlement des études en cas de fraude aux examens par application du décret 92-657 du 13 juillet 1992 peuvent s’appliquer. Elles seront décidées par la commission disciplinaire de l’UGA. 

A			 	Le   					 Signature

# Remerciements

Je tiens tout d'abord à remercier l'ensemble de l'équipe d'APIX Analytics pour son accueil chaleureux et la confiance accordée tout au long de ce stage. L'environnement de travail, à la fois bienveillant et stimulant, m'a permis de m'intégrer rapidement et de monter en compétences dans de bonnes conditions.

Je remercie tout particulièrement ma tutrice entreprise, Mme. Baral-Baron, pour sa disponibilité, ses conseils avisés et l'autonomie qu'elle m'a accordée. Son accompagnement a été déterminant dans la réussite du projet de développement d'une interface de modification des paramètres Modbus qui m'a été confié.

Mes remerciements vont également à mon tuteur IUT, M. X, pour son suivi attentif et ses retours constructifs tout au long de cette période de stage.

Enfin, je remercie l'ensemble des collaborateurs avec qui j'ai eu l'occasion d'échanger, pour leur disponibilité et le partage de leur expérience, qui ont largement contribué à enrichir ce stage tant sur le plan technique qu'humain.

```toc
```

# Rapport de stage

## Introduction

Du 23 mars au 27 juin 2026, j'ai réalisé mon stage de fin d'études au sein d'APIX Analytics, une PME (petite et moyenne entreprise) grenobloise spécialisée dans la conception, la fabrication et la commercialisation d'analyseurs de gaz chromatographiques industriels. Déployés sur des sites industriels critiques, ces analyseurs communiquent avec les systèmes de leurs clients via le protocole Modbus (cf. glossaire), un standard de communication industriel. La configuration de cette communication repose sur deux fichiers de paramètres au format JSON, `network.json` et `protocol.json`, qui devaient jusqu'alors être édités manuellement — une opération à la fois longue et propice aux erreurs.

Le sujet de mon stage a consisté à concevoir et développer un outil d'édition de ces paramètres Modbus, intégré à l'interface web PixL Expert, afin de remplacer cette édition manuelle par une interface fiable, guidée et validée. Ce travail, de nature *full-stack*, a mobilisé le développement backend en Python (Django et Django REST Framework), le développement frontend en Vue.js, ainsi que le déploiement de la solution en production.

Ce rapport rend compte de cette expérience et de la démarche suivie pour y parvenir. La première partie présente l'entreprise et son produit. La deuxième précise le contexte et les enjeux du projet. La troisième décrit les méthodes de travail et les outils mobilisés. La quatrième, cœur du rapport, détaille la réalisation technique — de l'architecture logicielle au déploiement en production — puis propose une analyse critique des choix effectués, des difficultés rencontrées et des limites de la solution. La cinquième aborde l'impact environnemental et sociétal du stage et du projet. La conclusion dresse enfin le bilan des compétences acquises et des perspectives d'évolution de l'outil.

## I. Présentation de l'entreprise

### 1. APIX Analytics — contexte et activité


APIX Analytics est une entreprise grenobloise spécialisée dans la conception, la fabrication et la commercialisation d'analyseurs de gaz chromatographiques industriels. Sa particularité tient à une intégration verticale complète : elle maîtrise à la fois le matériel — l'analyseur et son détecteur chromatographique — et le logiciel qui le pilote, l'ensemble de la PixL Suite étant développé en interne. PME à taille humaine (moins de cinq développeurs), elle impose une forte polyvalence : chacun intervient sur toute la pile logicielle, du bas niveau embarqué jusqu'aux interfaces web — une diversité à la fois formatrice et exigeante.

L'activité répond à un besoin précis : déterminer en continu et avec précision la composition d'un mélange gazeux directement sur le terrain. L'application principale est l'analyse du gaz naturel sur les réseaux de transport et de distribution, où la composition détermine la valeur énergétique du gaz (pouvoir calorifique, indice de Wobbe) dont dépend la facturation — une exigence à la fois commerciale et réglementaire. S'y ajoutent le contrôle qualité des gaz renouvelables (biométhane, biogaz) avant injection dans le réseau, porté par la gamme GREENPIX et par la transition énergétique, ainsi que la surveillance de procédés industriels. Dans tous les cas, ces analyseurs équipent des sites industriels critiques, où la fiabilité, la précision et la continuité de service ne sont pas négociables : une erreur de mesure peut avoir des conséquences directes sur la facturation, la sécurité ou la conformité réglementaire.

Sur un marché historiquement occupé par de grands groupes généralistes de l'instrumentation, APIX se positionne comme un acteur spécialisé et agile, dont les facteurs de différenciation sont la maîtrise intégrée du matériel et du logiciel, la réactivité produit et l'investissement sur les gaz renouvelables.

---

### 2. Le produit — les analyseurs APIX et la PixL Suite

Le produit d'APIX Analytics se comprend à trois niveaux complémentaires : les **analyseurs** commercialisés (les gammes de produits), le **chromatographe** qui en constitue le cœur de mesure (le matériel), et la **PixL Suite** qui les pilote (le logiciel).

#### a. Les analyseurs : CHROMPIX et GREENPIX

APIX Analytics décline ses analyseurs en deux gammes, fondées sur la même technologie de mesure mais destinées à des usages distincts :

- **CHROMPIX** est dédié à l'analyse du gaz naturel conventionnel sur les réseaux de transport et de distribution, où il fournit en continu la composition et la valeur énergétique du gaz.
- **GREENPIX** est destiné à l'analyse des gaz renouvelables (biométhane, biogaz), avec les spécificités liées au contrôle qualité avant injection dans le réseau. Cette gamme inscrit directement l'entreprise dans la transition énergétique.

Chaque analyseur est un équipement autonome, conçu pour être installé sur site et fonctionner sans intervention humaine permanente, en dialoguant avec les systèmes industriels environnants.

#### b. Le chromatographe : principe de mesure

Au cœur de chaque analyseur se trouve un chromatographe en phase gazeuse. La **chromatographie en phase gazeuse** est une technique analytique qui détermine précisément la composition d'un mélange gazeux : un échantillon de gaz est injecté puis entraîné à travers une colonne de séparation spécialisée, qui retient plus ou moins longtemps chaque composant selon sa nature. Les composants en ressortent ainsi les uns après les autres et sont mesurés par un **détecteur**, qui produit pour chacun un pic ; la position du pic identifie le composant, et son amplitude permet d'en déduire la concentration.

C'est ce signal brut — la suite des pics — qui alimente la chaîne logicielle : à partir de ces mesures, le logiciel reconstruit la composition du gaz et les grandeurs dérivées (concentrations, valeur énergétique). Les notions de valeur brute, valeur normalisée et réponse du pic, que l'on retrouvera dans `protocol.json`, proviennent directement de cette étape de mesure.

#### c. Le logiciel : la PixL Suite

![[pixl-suite-architecture.png|700]]
*Figure 1 : Architecture de la PixL Suite : PixL Modbus, PixL Core, PixL API et la base PixL DB communiquent entre eux ; **PixL Expert** (en jaune), l'interface Vue.js, constitue le périmètre du stage.*

La **PixL Suite** (voir Figure 1) est un ensemble de logiciels interdépendants qui pilotent intégralement les analyseurs APIX. Elle couvre l'intégralité de la chaîne de traitement, depuis l'acquisition des signaux physiques bruts produits par le détecteur chromatographique, jusqu'à la présentation des résultats aux opérateurs et à la communication avec les systèmes industriels environnants.

L'ensemble de la suite tourne sur un **PC embarqué** dédié, où les composants sont déployés en conteneurs Docker (cf. glossaire) — isolation et mises à jour sans redémarrage complet — avec une base PostgreSQL pour la persistance des mesures et des configurations.

La suite se compose de plusieurs logiciels aux rôles complémentaires :

- **L'orchestrateur général** coordonne l'ensemble des composants embarqués, pilote les cycles d'analyse et gère les états du système.
- **PixL API** est une API REST sécurisée qui sert de passerelle entre le PC embarqué et le monde extérieur. C'est l'interface par laquelle les opérateurs et les systèmes tiers accèdent aux données et aux fonctions de configuration de l'analyseur.
- **Le serveur Modbus** assure la communication avec les automates industriels environnants, selon le protocole standard Modbus (TCP et série). C'est ce module qui lit les fichiers de configuration `network.json` et `protocol.json` pour construire la table des registres qu'il expose.
- **Les interfaces web** permettent aux opérateurs de visualiser les données de mesure en temps réel, configurer l'appareil et diagnostiquer les alarmes depuis un navigateur, sans accès physique à la machine.

Parmi ces interfaces figure **PixL Expert**, application web nouvelle génération en Vue.js, en développement actif pour remplacer l'interface existante (développée entièrement en Django, avec rendu des pages côté serveur). Cette transition vise à découpler l'interface du backend, améliorer l'ergonomie et faciliter les évolutions. C'est dans ce logiciel que s'inscrit mon travail de stage.

---

### 3. L'équipe et mon environnement de travail

Mon stage s'est déroulé de fin mars à fin juin 2026 dans les locaux d'APIX Analytics à Grenoble, au sein d'un espace de travail partagé avec l'ensemble de l'équipe de développement, mais également avec les personnes en charge de la configuration analytique des chromatographes. Cette proximité entre développeurs et utilisateurs métier est caractéristique d'une petite structure : elle favorise les échanges directs, permet de comprendre rapidement les besoins concrets des utilisateurs, et évite les malentendus qui surviennent souvent quand les équipes techniques et fonctionnelles sont trop éloignées.

L'équipe compte notamment un alternant qui travaille en parallèle sur le nouveau PixL Expert. Chaque membre y porte une responsabilité large, et la communication est continue et directe.

Ma tutrice de stage, **Mme Baral-Baron**, a assuré un suivi actif tout au long du stage. Plutôt que de me laisser seul face aux difficultés, elle m'a expliqué au fil de l'eau les aspects techniques du projet : le protocole Modbus, la structure des fichiers de configuration, la signification des attributs des registres, les conventions de la base de code d'APIX, et surtout les règles de cohérence métier — absentes de toute documentation formelle mais indispensables pour concevoir une interface correcte. J'ai également bénéficié du soutien du **chef de produit**, notamment pour comprendre les besoins fonctionnels et les attentes des utilisateurs.

L'organisation du stage reflète bien l'esprit de l'équipe : guidé et soutenu quand j'en avais besoin, mais libre dans la manière d'organiser et de mener mon travail au quotidien. Cette autonomie encadrée, dans un environnement où il est facile de poser une question à la personne assise en face, s'est révélée particulièrement formatrice.


## II. Contexte et enjeux du projet

### 1. Problématique : la configuration Modbus dans PixL Expert


PixL Expert communique avec des systèmes industriels tiers via le protocole **Modbus**, un standard largement répandu dans l'industrie pour l'échange de données entre équipements. Ce protocole, supporté à la fois en mode série et en mode TCP/IP (Transmission Control Protocol / Internet Protocol, la pile de protocoles standard des réseaux), permet à des automates ou des systèmes industriels tiers d'interroger l'analyseur et de récupérer ses mesures en temps réel.

La configuration de cette communication repose sur deux fichiers JSON : `network.json`, qui définit les paramètres réseau de la connexion, et `protocol.json`, qui recense l'intégralité des registres Modbus exposés par l'appareil. Pour chaque registre, le `protocol.json` décrit ses caractéristiques techniques (adresse, format, taille, facteur de conversion), ainsi que la nature de l'information concrète remontée par ce registre — nom du composant mesuré, type de valeur, catégorie d'alarme. C'est donc ce fichier qui fait le lien entre les adresses Modbus abstraites et les données métier de l'analyseur.

Avant mon stage, PixL Expert ne proposait aucune interface dédiée à l'édition de ces fichiers : opérateurs et techniciens devaient modifier le JSON à la main. Cette approche posait deux problèmes. D'une part, un **risque d'erreurs élevé** : une faute de frappe dans une adresse, un mauvais format ou un facteur erroné peut rendre un registre illisible sans qu'aucun message ne le signale. D'autre part, une **perte de temps** : un fichier comme `protocol.json` peut recenser plusieurs centaines de registres imbriqués sur plusieurs niveaux, si bien que retrouver une entrée précise, l'éditer sans rompre la structure, puis vérifier la cohérence de l'ensemble s'avère long et laborieux, même pour un développeur expérimenté. Construire une interface dédiée visait donc à la fois à fiabiliser les modifications et à accélérer la configuration d'un protocole.

### 2. Objectifs du stage


L'objectif de mon stage était de concevoir et développer un outil d'édition des paramètres Modbus intégré directement dans l'interface web PixL Expert. Cet outil devait permettre à un utilisateur de visualiser, modifier et sauvegarder les paramètres contenus dans les fichiers `network.json` et `protocol.json` sans avoir à manipuler ces fichiers directement.

Concrètement, le travail attendu couvrait à la fois le développement backend en Python — pour exposer les données des fichiers JSON via des routes API — et le développement frontend en Vue.js pour construire les interfaces d'édition correspondantes. Ces deux aspects étaient indissociables et ont été développés conjointement tout au long du stage.

Le projet s'est construit de manière itérative, sans cahier des charges formel : les objectifs ont été précisés progressivement au fil des échanges avec ma tutrice, en fonction de l'avancement du développement et des retours obtenus à chaque étape. Cette approche agile m'a demandé une bonne capacité d'adaptation et de communication.

### 3. Contraintes techniques

Le développement de cet outil impliquait plusieurs contraintes techniques importantes.

**Intégration dans la base de code existante.** PixL Expert disposait déjà d'une architecture Vue.js établie, avec ses composants réutilisables et ses conventions ; il fallait s'y conformer, en réutilisant les composants et routes API existants ou en créant de nouveaux dans le même esprit.

**Maîtrise du système de modèles Python.** Le backend repose sur un système de sérialisation/désérialisation (cf. glossaire) interne, `ModelMother`, qui convertit automatiquement les objets Python en JSON et inversement ; le maîtriser était indispensable pour développer des routes cohérentes avec le reste du projet (détaillé en partie IV).

**Complexité des données.** Le fichier `protocol.json` est particulièrement volumineux et hiérarchisé, avec plusieurs niveaux d'imbrication et des centaines d'entrées. Concevoir une interface claire et utilisable pour naviguer et éditer ces données sans surcharger l'utilisateur a représenté un véritable enjeu de conception.

**Validation des données.** L'interface devait intégrer un certain niveau de validation des saisies utilisateur, afin d'éviter d'enregistrer des valeurs incohérentes dans les fichiers de configuration. Ces règles de validation s'appuyaient en partie sur des contraintes métier liées au protocole Modbus lui-même.



## III. Méthodes de travail et outils

### 1. Stack technique

Le projet reposait sur deux environnements techniques distincts et complémentaires, dont la maîtrise simultanée constituait l'une des exigences principales du stage.

Côté **backend**, le développement s'est fait en **Python**, avec le framework **Django** et son extension **Django REST Framework** (DRF, cf. glossaire). Django est l'un des frameworks web Python les plus répandus : il fournit une structure d'application claire, un système de routage des requêtes HTTP (HyperText Transfer Protocol, le protocole d'échange de données du web), et de nombreux outils prêts à l'emploi pour la gestion des données et des utilisateurs. Django REST Framework complète Django pour la construction d'API REST, en simplifiant la sérialisation des données et la gestion des formats de réponse. Les modifications portaient sur trois dépôts distincts : **Apix Tools**, qui contient les modèles de données et utilitaires partagés, **PixL API**, qui expose les routes REST consommées par le frontend, et **PixL Expert**, qui héberge le projet Vue.js de la nouvelle interface web.

Côté **frontend**, l'interface a été développée en **Vue.js 3** (API Composition). Vue.js est un framework JavaScript orienté composants : l'interface est découpée en blocs réutilisables encapsulant chacun sa logique, son template HTML et ses styles — un découpage qui facilite la maintenance, précieux pour un projet appelé à s'enrichir continuellement. L'état partagé entre composants était géré par **Pinia** (le gestionnaire d'état officiel de Vue.js 3) et les appels HTTP vers l'API par **Axios**.

### 2. Outils de développement

**Éditeurs de code.** J'ai utilisé **VS Code** pour le frontend Vue.js (extension Volar) et **PyCharm** pour le backend Python (autocomplétion, débogage et inspection de code avancés), chacun étant le mieux adapté à son langage.

**Versionnage et intégration continue.** Le code était versionné avec **Git** sur un **GitLab** interne, chaque dépôt étant développé sur une branche dédiée. GitLab héberge aussi les pipelines de **CI/CD** (intégration et déploiement continus ; cf. glossaire) : à chaque push, le pipeline compile le projet et exécute les tests, mais la production des artefacts livrables (wheels Python, archives ZIP) n'est déclenchée que par la pose d'un **tag** de version sur un commit. Cette automatisation garantit des artefacts toujours cohérents avec le code et sa version.

**Prise de notes.** J'ai utilisé **Obsidian** pour organiser mes notes tout au long du stage (concepts appris, suivi des tâches, mémos techniques), ce qui m'a aidé à reprendre facilement un sujet laissé en suspens d'une semaine à l'autre.

### 3. Organisation et suivi du projet

Le suivi s'est organisé autour d'une **réunion hebdomadaire le lundi** avec ma tutrice. Ces points faisaient le bilan de la semaine écoulée, identifiaient les blocages et fixaient les objectifs suivants. Cette cadence évitait de s'engager trop longtemps dans une mauvaise direction : une approche inadaptée était corrigée dès le lundi suivant plutôt que de se prolonger sur plusieurs semaines.

Le projet n'ayant pas de cahier des charges formalisé, les fonctionnalités ont été définies progressivement, par itérations : chaque livraison faisait l'objet d'une démonstration dont les retours alimentaient les objectifs suivants. Cette approche itérative, proche des méthodes agiles, est bien adaptée à une petite équipe où les besoins se précisent à mesure que l'outil prend forme.

Entre les réunions, le travail s'organisait de manière autonome, avec des échanges informels dans l'espace de travail partagé dès qu'une question ou un blocage surgissait. La proximité de l'équipe rendait ces échanges rapides, sans formalisme. Ce mélange de cadre régulier et de flexibilité quotidienne s'est révélé bien adapté au rythme du stage.


## IV. Réalisation du projet

### 1. Architecture de PixL Suite

#### a. Le protocole Modbus

![[Pasted image 20260324100959.png]]
*Figure 2 : Architecture Modbus TCP chez APIX : le serveur APIX (esclave) répond aux requêtes du client automate (maître). Les Input Registers sont en lecture seule, les Holding Registers en lecture/écriture ; une valeur `float32` occupe deux registres consécutifs.*

Avant de développer, il était essentiel de maîtriser le socle technique du projet. Le protocole Modbus, conçu en 1979 par Modicon pour ses automates programmables, reste l'un des standards de communication industriels les plus répandus, pour sa simplicité et sa robustesse.

**Modèle maître / esclave.** Modbus repose sur un modèle maître/esclave (voir Figure 8, en annexe A) : seul le maître initie les échanges, les esclaves se contentant de répondre à ses requêtes. Dans le contexte d'APIX, un automate industriel joue le rôle de maître et interroge régulièrement l'analyseur — l'esclave — pour récupérer ses mesures ; l'analyseur ne transmet jamais de données de façon spontanée.

**Les registres Modbus.** Les échanges se font à travers des registres, des cases mémoire numérotées situées dans l'esclave, chacune identifiée par une adresse unique et contenant une valeur numérique (voir Figure 2). On en distingue deux types selon la donnée (cf. glossaire) :

- Les **holding registers**, accessibles en lecture et en écriture : l'analyseur APIX y expose ses mesures principales (concentrations, valeurs détaillées de chromatographie) ainsi que les commandes.
- Les **input registers**, en lecture seule : ils portent les alarmes, les états système, les informations de commande et les informations générales.

**Supports de communication.** Modbus fonctionne sur deux types de liaisons : Modbus RTU (Remote Terminal Unit, liaison série sur bus RS-485 — une norme de transmission série différentielle —, trames binaires compactes) et Modbus TCP (mêmes trames encapsulées dans des paquets réseau Ethernet). L'analyseur APIX supporte les deux simultanément, chacun étant configurable via `network.json`.

**Formats de données et facteur de conversion.** Un registre étant encodé sur 16 bits, représenter des types plus précis impose d'en utiliser plusieurs consécutifs : un flottant Float32 (norme IEEE 754, le standard de représentation des nombres à virgule flottante) occupe ainsi deux registres. Certaines valeurs nécessitent par ailleurs un facteur de conversion (`factor`) : une concentration de 12,34 % est stockée sous la valeur entière 1234, avec un facteur de 0,01. Ces formats (`float32`, `float16`, `sint16`, etc.) et ces facteurs sont consignés pour chaque registre dans `protocol.json`.

#### b. Prise en main de la base de code PixL Expert existante

Une fois le contexte technique assimilé, l'étape suivante a consisté à explorer le code existant — un exercice délicat : naviguer dans des fichiers écrits par d'autres, souvent peu documentés, et comprendre non seulement ce que fait le code, mais pourquoi il est ainsi structuré. Ma tutrice m'a accompagné sur les points les plus complexes.

**La bibliothèque Apix Tools.** Ce module constitue le socle partagé du projet. Il contient les classes Python communes utilisées par l'ensemble des composants de la PixL Suite : les modèles de données, les utilitaires de sérialisation et notamment le système ModelMother. Apix Tools est distribué sous forme de wheel Python (cf. glossaire) — un format d'empaquetage standard qui permet d'installer une bibliothèque Python comme n'importe quel paquet tiers, via la commande `pip install`. Chaque autre dépôt du projet le déclare comme dépendance dans son fichier `requirements.txt`.

**L'application PixL API.** Ce composant contient l'API REST (Representational State Transfer) du projet, développée avec Django et Django REST Framework. Une API REST expose données et opérations via des URLs standardisées — les routes (ou *endpoints*) — interrogeables en HTTP : par exemple, `GET /api/modbus/networks` retourne les paramètres réseau, `POST` les modifie. C'est par ces routes que le frontend communique avec le backend. Django impose une organisation en *apps*, chacune avec ses vues (`views.py`, logique de traitement) et son fichier de routes (`urls.py`, qui associe chaque URL à une vue).

**L'application PixL Expert.** Ce dépôt héberge le projet Vue.js de la nouvelle interface, destinée à remplacer l'ancienne (développée en Python/Django). Comme indiqué en III.1, l'interface y est découpée en composants — fichiers `.vue` encapsulant structure HTML, logique JavaScript et styles CSS — assemblés en vues, les pages de l'application.

#### c. Compréhension des fichiers de configuration JSON

Le comportement Modbus de l'analyseur est entièrement piloté par deux fichiers de configuration au format JSON (JavaScript Object Notation, cf. glossaire) : `network.json`, qui définit les paramètres réseau des liaisons RTU et TCP, et `protocol.json`, qui décrit l'ensemble des registres exposés (adresse, type, format, facteur de conversion). Ces deux fichiers ont été analysés en profondeur dès les premiers jours, car ils constituent le point central autour duquel s'articule toute l'interface à développer.

Cette analyse n'était pas purement technique : ma tutrice m'a expliqué la signification métier de chaque champ et les règles de cohérence à respecter. Ces règles, absentes des fichiers eux-mêmes, étaient indispensables pour concevoir une interface qui guide l'utilisateur sans lui permettre de saisir des données incohérentes — deux registres ne peuvent par exemple pas partager la même adresse, et le format d'un registre détermine strictement le nombre de cases mémoire qu'il occupe (`size`), ce qui conditionne à son tour l'adressage de tous les registres suivants.

---

### 2. Architecture backend — ModelMother

#### a. Le problème que résout ModelMother

Le backend Python manipule les données de configuration sous forme d'objets : un `ProtocolParameters` contient un `HoldingRegisterParameters`, lui-même composé de collections d'`ElementParameters` et d'`AlarmEntryParameters`. Pratiques à manipuler, ces objets n'existent qu'en mémoire et ne peuvent pas être directement stockés dans un fichier ou transmis via une API.

Pour les conserver, il faut les **sérialiser** (convertir l'objet en JSON) puis les **désérialiser** (reconstruire l'objet Python à partir du JSON lu). Sans mécanisme commun, chaque nouvelle classe devrait réécrire cette logique de conversion, au risque d'introduire des inconsistances dans le projet. ModelMother évite cela en centralisant le mécanisme.

#### b. Principe et rôle de la classe de base


ModelMother (cf. glossaire) est la classe de base, définie dans `apix_tools/apix_framework/model/model_mother.py`, dont toutes les sous-classes héritent les comportements de conversion. Elle expose deux méthodes fondamentales :

- `get_attributes_as_dict()` (sérialisation) parcourt les attributs de l'objet et les convertit en dictionnaire Python en adaptant la conversion à chaque type : valeur simple copiée directement, objet héritant de ModelMother sérialisé récursivement, liste parcourue élément par élément, énumération convertie en sa valeur textuelle. Un mécanisme d'attributs exclus (`excluded_attributes`) ignore les attributs utiles en mémoire mais non pertinents dans le fichier — par exemple les états temps réel d'une alarme (`level`, `metrological`, `critical`), présents dans la classe Python mais absents du JSON.
- `set_attributes_from_dict()` (désérialisation) remplit récursivement les attributs à partir d'un dictionnaire : pour chaque clé, elle identifie le type de l'attribut et effectue la conversion inverse, instanciant et récursant sur les objets ModelMother imbriqués. Elle contrôle aussi la validité des données au chargement (valeurs d'énumération autorisées) et peut déclencher une validation métier propre à chaque classe, `model_sanity_check()`, surchargeable par les sous-classes.

Grâce à cette récursivité, une seule instruction charge l'intégralité d'un fichier JSON hiérarchisé en un arbre d'objets Python typés, quelle que soit la profondeur d'imbrication.

#### c. La problématique du dictionnaire dans le dictionnaire : ModelDictToListMother


C'est ici qu'intervient une limitation rencontrée concrètement lors du développement, que ma tutrice a résolue en étendant le framework.

Dans `protocol.json`, certaines sections stockent leurs éléments non pas dans une liste JSON, mais dans un dictionnaire dont les clés sont les noms des éléments. Par exemple, la section `elements_detailed` du holding register ressemble à ceci :

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

Ce format — un dictionnaire de dictionnaires — permet d'accéder directement à un élément par son nom, mais complique la manipulation en Python : pour parcourir, trier, ajouter ou supprimer des éléments, une liste est bien plus naturelle. Or ModelMother, dans sa version d'origine, ne gérait pas la conversion entre ces deux formes.

Ma tutrice a donc créé la classe `ModelDictToListMother`, accompagnée de deux fonctions récursives assurant la conversion bidirectionnelle :

- `dictToList` convertit le dictionnaire JSON indexé par nom en liste Python d'objets, en attachant la clé comme attribut. Ainsi, `"CAL-C2H4": { ... }` devient un objet `ElementDetailParameters` dont l'attribut `name` vaut `"CAL-C2H4"`.
- `fromDictToList` effectue l'opération inverse à la sérialisation : elle reconstruit le dictionnaire indexé par nom à partir de l'attribut `name` de chaque objet.

La récursivité est indispensable car la structure peut être profondément imbriquée : un élément détaillé contient lui-même plusieurs propriétés (`raw_value`, `normalized_value`, `response`…), elles-mêmes des objets. Ces deux fonctions traversent tous les niveaux sans que le code appelant ait à s'en préoccuper.

Cette extension a été intégrée à ModelMother de sorte que `get_attributes_as_dict()` applique automatiquement `fromDictToList` aux objets `ModelDictToListMother`, et `set_attributes_from_dict()` leur applique `dictToList`. L'ajout était transparent pour le reste du code : les classes de modèles n'ont eu qu'à déclarer leurs attributs de ce type pour en bénéficier.

#### d. Hiérarchie des classes de modèles

![[modelmother-hierarchie.png|700]]
*Figure 3 : Hiérarchie des classes de modèles : `ModelMother` est la classe de base dont héritent `NetworkParameters` (`network.json`) et `ProtocolParameters` (`protocol.json`), elles-mêmes décomposées en sous-objets typés.*

La hiérarchie des classes (voir Figure 3) reflète directement la structure des fichiers JSON, organisée autour de trois classes de conteneurs :

- `ModelMother` : classe de base pour tous les objets sérialisables atomiques.
- `ModelListMother` : conteneur pour les listes JSON simples (listes de ports série dans `network.json`).
- `ModelDictToListMother` : conteneur pour les dictionnaires JSON indexés par nom, convertis en listes Python (`elements_detailed`, `elements`, `alarm`).

La hiérarchie concrète des classes du projet est détaillée, sous forme d'arbre, en annexe B (voir Annexe B) : chaque feuille y correspond à un champ concret du JSON (adresse, format, facteur) et hérite de ModelMother, bénéficiant automatiquement des mécanismes de sérialisation.

---

### 3. Éditeur de configuration réseau — network.json

#### a. Analyse de la structure du fichier

Le fichier `network.json` décrit comment l'analyseur APIX expose son interface Modbus sur les différents supports de communication disponibles. Sa structure se divise en quatre sections.

**L'identifiant d'esclave (`slave_id`).** C'est un entier compris entre 1 et 247 qui identifie de manière unique l'analyseur sur le bus Modbus. Lorsque plusieurs esclaves coexistent sur le même réseau RS-485, le maître utilise cet identifiant pour s'adresser à un équipement précis.

**La configuration TCP (`tcp`).** Un drapeau `enabled` (activant le mode Modbus TCP) et un numéro de port réseau (0–65535) ; le port standard de Modbus TCP est 502.

**Les ports série (`serial`).** Contrairement aux sections précédentes, c'est une liste : l'analyseur peut exposer son interface sur plusieurs liaisons série simultanément. Chaque entrée décrit un port physique et ses paramètres : chemin du périphérique (ex. `/dev/ttyS0`), vitesse en bauds, bits de données, parité (N/E/O), bits de stop, mode (`rtu`) et délai d'attente (timeout). Ces paramètres doivent être identiques sur tous les équipements du même bus RS-485.

**La configuration ZMQ.** ZMQ (ZeroMQ) est un protocole de messagerie interne entre composants de la PixL Suite sur la même machine. Trois paramètres sont configurés : un port de données (`zmq_data_port`, 5556), un port de commande (`zmq_command_port`, 5557) et l'adresse IP locale (`zmq_ip`).

Un exemple complet illustrant ces quatre sections est fourni en annexe C (voir Annexe C).

#### b. Développement côté backend

Deux routes ont été créées dans le module `metro_api/settings/modbus/` de PixL API.

La route `GET /metrological/settings/modbus/networks` charge le fichier `network.json` via la méthode `load_network()` de `NetworkParameters`, qui utilise `set_attributes_from_dict()` pour désérialiser le JSON en objet Python, puis retourne les données sérialisées via `get_attributes_as_dict()`. Cette double conversion garantit que les données retournées sont bien conformes au modèle attendu.

La route `POST /metrological/settings/modbus/networks` reçoit les données modifiées par le frontend, effectue des contrôles de validation, puis sauvegarde le fichier. Les validations implémentées portent sur : la plage du port TCP (0–65535), la plage du port ZMQ (0–65535), le délai d'attente des ports série (entre 0,1 et 5 secondes), et la conformité des valeurs énumérées (vitesse de transmission, parité, méthode) aux valeurs supportées par le serveur Modbus. En cas d'erreur de validation, la route retourne un code HTTP 400 (Bad Request) avec un message explicatif, sans modifier le fichier.

#### c. Développement côté frontend — ModbusPart.vue

![[network-editeur-formulaire.png|650]]
*Figure 4 : Éditeur `network.json` (`ModbusPart.vue`) : configuration du port TCP et des ports série, chaque port série étant géré dans un onglet dynamique (baud rate, bits de données, parité, bits de stop, méthode RTU/ASCII, timeout).*

L'interface d'édition de `network.json` a été développée dans le composant `ModbusPart.vue` (voir Figure 4), intégré dans la section Remote Access des paramètres généraux de PixL Expert.

**Chargement des données et route d'énumérations générique.** Au montage du composant (`onMounted`), deux appels API sont effectués : un premier pour charger la configuration actuelle du réseau, et un second pour charger les énumérations disponibles — les listes de valeurs autorisées pour chaque champ à choix multiples (vitesses de transmission, parités, méthodes, etc.).

Plutôt qu'une route dédiée par énumération, j'ai développé une route générique réutilisable, `GET /settings/enums/<enum_name>/` : elle reçoit le nom d'un module d'enum en paramètre d'URL, l'importe dynamiquement depuis Apix Tools via `importlib` (import d'un module à l'exécution à partir de son nom), puis retourne ses valeurs sous forme de paires `value`/`displayName`. `ModbusPart.vue` l'appelle ainsi pour chacune de ses listes déroulantes (vitesses, parités, méthodes…), sans route spécifique à créer.

**Gestion des ports série.** La liste variable de ports série, partie la plus complexe de l'interface, est gérée par un système d'onglets dynamiques : un onglet par port, avec des boutons d'ajout et de suppression. Chaque onglet présente le formulaire du port (chemin, vitesse, bits de données, parité, bits de stop, méthode — chacun en liste déroulante alimentée par la route d'énumérations — et délai d'attente avec validation).

**Sauvegarde.** À la soumission, les données de l'état local Vue.js sont structurées et envoyées via un POST à la route `/metrological/settings/modbus/networks`. Un retour visuel confirme la sauvegarde ou signale les erreurs retournées par le backend.

---

### 4. Éditeur de configuration protocole — protocol.json

#### a. Analyse de la structure du fichier

Le fichier `protocol.json` est structurellement bien plus complexe que `network.json`. Son contenu s'organise autour de deux types de registres Modbus — le `holding_register` et l'`input_register`.

Le point déterminant pour l'éditeur est que ces deux registres ne diffèrent pas par leur contenu mais par leur type Modbus (le holding register en lecture/écriture, l'input register en lecture seule) : ils partagent le même schéma et regroupent leurs entrées dans les mêmes sous-sections — `measure` (mesures), `alarm` (alarmes), `information` (infos appareil), `system` (état système) et `command` (commandes). Une même sous-section peut donc apparaître dans l'un ou l'autre registre.

Au sein de la sous-section `measure`, deux niveaux de représentation coexistent :

- Les **mesures simples**, déclarées chacune par une entrée unique (ex. `data_validity`, `injection_time`), avec une adresse, un format et une taille en registres (`size`).
- Les **éléments détaillés**, regroupés sous `elements_detailed` : un dictionnaire indexé par le nom du composant (ex. `"CAL-C2H4"`, `"H2S"`), typiquement les composants mesurés par chromatographie. Chaque composant porte jusqu'à cinq propriétés — `raw_value` (valeur brute du détecteur), `normalized_value` (valeur normalisée), `response` (réponse du pic), `peak_start` (début du pic) et `peak_end` (fin du pic) — chacune occupant ses propres registres, toujours au format `float32` (2 registres), avec un facteur de conversion.

Les autres sous-sections suivent la même logique de dictionnaire indexé par nom. Dans `alarm`, chaque entrée décrit l'adresse de son registre de statut et son format (toujours `sint16`, 1 registre). Dans `information`, les entrées mélangent des formats variés : `str` de taille variable pour les versions de firmware et les sommes de contrôle, `sint16`/`sint32` pour les états et les dates.

La combinaison de cette imbrication à plusieurs niveaux, du partage du même schéma entre registres et du grand nombre d'entrées possibles représentait le principal défi de conception de l'éditeur.

#### b. La route GET /protocol/formats — configuration dynamique de l'interface

Un point architectural notable est une troisième route, `GET …/protocol/formats`, qui ne retourne pas de données de configuration mais une description de l'interface elle-même. Cette approche, dite *configuration-driven UI* (interface pilotée par la configuration), permet au backend de dicter au frontend son comportement sans que celui-ci connaisse en dur les règles métier Modbus. Elle était nécessaire car une partie des options à afficher — notamment les noms d'alarmes disponibles — dépend du `protocol.json` chargé sur le serveur, qui varie d'une installation à l'autre, et ne pouvait donc pas passer par la route générique d'énumérations utilisée dans `ModbusPart.vue`.

Cette route retourne notamment :

- La liste des formats de données disponibles (`float32`, `float16`, `sint16`, etc.) avec pour chacun son nom d'affichage, si sa taille en registres est fixe ou flexible, et la taille attendue.
- Les formats acceptés par sous-section : par exemple, les alarmes n'acceptent que `sint16`, les éléments détaillés n'acceptent que `float32`, tandis que les éléments simples acceptent plusieurs formats. Ces règles sont vérifiées à la fois côté frontend (pour guider l'utilisateur) et côté backend (comme garde-fou).
- La configuration des champs à afficher par sous-section : quels champs montrer, sous quel type de contrôle (champ texte, liste déroulante), avec quelles options.
- Les colonnes du tableau de l'interface et les options des listes déroulantes d'énumération — en particulier les noms des alarmes, extraits dynamiquement du fichier `protocol.json` courant.

Cette architecture présente un avantage significatif : lorsque les règles métier évoluent — par exemple si un nouveau format de données est supporté — seul le backend doit être mis à jour, sans modifier le code frontend.

#### c. Développement côté backend

Les deux routes principales du protocole ont des responsabilités distinctes.

La route `GET /metrological/settings/modbus/protocol` lit le fichier `protocol.json` et retourne son contenu. Contrairement à la route réseau, elle retourne ici la structure JSON directement, sans passer par une désérialisation complète via ModelMother : cela permet de conserver la structure telle qu'elle est dans le fichier, que le frontend réorganise ensuite pour l'affichage.

La route `POST /metrological/settings/modbus/protocol` reçoit la nouvelle version du protocole modifiée par le frontend et la réécrit dans le fichier. Elle invoque une méthode de vérification de cohérence, `_check_protocol_coherence()`, qui parcourt l'ensemble des entrées du protocole et vérifie la cohérence entre le format déclaré et la taille en registres (`size`) associée — car chaque format impose une taille fixe (un `float32` occupe toujours 2 registres, un `sint16` en occupe toujours 1). Les incohérences détectées sont retournées sous forme d'avertissements, permettant à l'interface de les signaler à l'utilisateur sans bloquer la sauvegarde.

#### d. Développement côté frontend — RegisterMapPart.vue

![[protocole-editeur-tableau.png|650]]
*Figure 5 : Éditeur `protocol.json` (`RegisterMapPart.vue`) : tableau AG Grid listant les registres (type HR/IR, adresse, source, nom, format, facteur), avec tri, filtres et réordonnancement par glisser-déposer.*

![[protocole-editeur-modale.png|450]]
*Figure 6 : Fenêtre modale d'ajout/édition d'un registre : le formulaire s'adapte dynamiquement à la sous-section choisie (ici un `Measure` → `Elements Detailed`), avec un aperçu en direct du nom généré.*

L'interface d'édition de `protocol.json` a été développée dans le composant `RegisterMapPart.vue` (voir Figure 5). La complexité de ce composant est significativement plus élevée que `ModbusPart.vue`, en raison de la richesse de la structure de données à manipuler.

**Chargement et initialisation.** Au montage, trois appels API successifs récupèrent la configuration des formats et champs (`/protocol/formats`), le protocole actuel (`/protocol`) et la configuration du registre map. Ils servent à construire l'état interne : une liste plate d'entrées (`registerMap.entries`), plus simple à afficher et à trier qu'une hiérarchie imbriquée.

**La grille AG Grid.** Le cœur de l'interface est un tableau interactif réalisé avec AG Grid (cf. glossaire), une bibliothèque JavaScript spécialisée dans les tableaux de données complexes. Chaque ligne du tableau représente un registre ou un groupe de registres, avec les colonnes suivantes : le type de registre (Register : holding ou input), l'adresse (Address), la source (Source : la sous-section `measure`, `alarm`, etc.), le nom (Name), le format (Format), et le facteur de conversion (Factor).

AG Grid a été retenu pour ses fonctionnalités avancées, notamment le glisser-déposer des lignes pour réordonner intuitivement les entrées quand le tableau est trié par adresse. La bibliothèque était déjà présente dans le projet : un collègue l'avait intégrée ailleurs et avait développé un utilitaire centralisant la configuration commune des tableaux, ce qui m'a permis de l'utiliser sans en maîtriser tous les détails d'initialisation.

**Le formulaire d'ajout et d'édition.** L'ajout d'une nouvelle entrée ou la modification d'une entrée existante (via un bouton Edit en fin de ligne) ouvre une fenêtre modale contenant un formulaire dynamique (voir Figure 6). Ce formulaire est dit dynamique car son contenu varie selon la sous-section sélectionnée par l'utilisateur, pilotée par la configuration retournée par la route `/protocol/formats` :

- Pour la sous-section `alarm` : le formulaire présente uniquement un sélecteur de nom d'alarme (parmi les alarmes disponibles dans le système, fournies sous forme d'énumération). Le format est imposé à `sint16` et non modifiable, car toutes les alarmes Modbus ont le même format.
- Pour la sous-section `elements` : le formulaire présente un sélecteur de nom d'élément et un champ de facteur de conversion. Le format peut être choisi parmi les formats acceptés pour cette sous-section.
- Pour la sous-section `elements_detailed` : le formulaire présente un sélecteur de nom d'élément, un sélecteur de type de propriété (`raw_value`, `normalized_value`, `response`, `peak_start`, `peak_end`), et un champ de facteur. Le format est imposé à `float32`.

**La détection de conflits d'adresses.** Comme chaque format occupe un nombre précis de registres consécutifs (un `float32` occupe N et N+1, un `float16` le seul registre N), deux entrées peuvent se chevaucher. L'éditeur calcule la plage occupée par chaque entrée et signale visuellement toute collision dans le tableau.

**La sauvegarde.** À la sauvegarde, le composant reconstruit la structure hiérarchique de `protocol.json` à partir de la liste plate : regroupement par section (`holding_register`/`input_register`), sous-section puis sous-sous-section (`elements`, `elements_detailed`), et reconstruction des dictionnaires indexés par nom attendus par le backend, avant l'envoi via `POST …/protocol`.

---

### 5. Tests et validation

La phase de test a été conduite de manière continue et itérative tout au long du développement, selon le principe qu'une fonctionnalité n'est pas terminée tant qu'elle n'a pas été testée dans ses cas nominaux et ses cas limites.

#### a. Tests manuels en cours de développement

À chaque nouvelle fonctionnalité implémentée, des tests manuels étaient effectués directement dans le navigateur sur l'environnement local. Ces tests couvraient systématiquement deux familles de scénarios.

Les **cas nominaux** : saisie de valeurs valides, sauvegarde, rechargement de la page pour vérifier la persistance dans le fichier JSON, puis vérification du fichier résultant dans l'éditeur de code pour s'assurer de la conformité de la structure générée. Cette étape de vérification directe du fichier était systématique : une interface peut sembler correcte visuellement tout en produisant un JSON mal structuré, qui ne sera détecté comme invalide que lors du démarrage du serveur Modbus.

Les **cas limites et cas d'erreur** : port TCP hors plage, timeout série inférieur à 0,1 s, deux registres portant la même adresse, format incompatible avec la sous-section, sous-section d'alarme avec un format autre que `sint16`. Pour chacun, le comportement attendu était une validation explicite bloquant la sauvegarde, avec un message clair indiquant à l'utilisateur la source du problème.

#### b. Vérification de la cohérence des fichiers générés

Après chaque sauvegarde, les fichiers JSON étaient inspectés dans l'éditeur de code : présence de toutes les clés attendues, absence de clés parasites ou dupliquées, exactitude des types (en JSON, la chaîne `"1"` et l'entier `1` diffèrent, et la confusion peut perturber le serveur Modbus) et conformité de la structure imbriquée.

La vérification était particulièrement minutieuse pour `protocol.json` : la reconstruction de la structure hiérarchique depuis la liste plate du frontend comportait plusieurs étapes susceptibles d'introduire des erreurs (groupement incorrect des entrées, perte d'une sous-section vide, confusion entre `holding_register` et `input_register`).

#### c. Tests unitaires automatisés sur Apix Tools

Au-delà des tests manuels, j'ai écrit une série de **tests unitaires automatisés** sur Apix Tools avec le framework **pytest**, qui rejoue d'une seule commande un ensemble de vérifications et signale immédiatement tout échec.

J'ai concentré cet effort sur Apix Tools car cette bibliothèque est le **socle partagé** de toute la PixL Suite (modèles, ModelMother, sérialisation) : une régression à ce niveau se propagerait à tous les services qui en dépendent, et c'est la couche qui porte la logique la plus délicate — la conversion JSON ↔ objets Python. Les tests portent sur les deux modèles concernés par mon travail, `NetworkParameters` et `ProtocolParameters`.

Le principe de ces tests repose sur des **fichiers JSON de référence** versionnés aux côtés du code : pour chaque modèle, un fichier valide contenant un jeu de paramètres corrects (`network_valid.json`, et son équivalent pour le protocole) et un fichier volontairement erroné contenant des valeurs invalides (`network_invalid.json`). Les tests chargent ces fichiers via les modèles d'Apix Tools et confrontent le résultat aux valeurs attendues. Ils couvrent quatre familles de vérifications :

- **Valeurs par défaut** : à l'instanciation d'un `NetworkParameters` neuf, les valeurs par défaut attendues (port TCP 502, ports ZMQ 5556/5557, identifiant d'esclave 1, liste série vide).
- **Désérialisation** : après chargement du fichier valide, reconstruction correcte de l'arbre jusqu'aux niveaux imbriqués (ports série et leurs énumérations pour `network.json` ; sous-sections indexées par nom transformées en listes typées pour `protocol.json`), validant à la fois ModelMother et `ModelDictToListMother` (cf. IV.2.c).
- **Sérialisation (round-trip)** : `get_attributes_as_dict()` doit reproduire fidèlement le fichier d'origine (énumérations reconverties en valeur brute, listes Python re-converties en dictionnaires indexés par nom) — garantie qu'un fichier chargé puis resauvegardé reste identique.
- **Cas d'erreur** : dossier inexistant, chemin non renseigné, fichier introuvable, valeurs d'énumération invalides ; le chargement doit échouer proprement (statut d'échec et message explicite, comparé au texte attendu via `LogErrorMessages`) plutôt que de lever une exception non maîtrisée.

Cette automatisation présente un double intérêt par rapport aux tests manuels : elle est **rapide** (l'ensemble des cas est rejoué en quelques secondes) et surtout **non régressive** — toute modification ultérieure d'Apix Tools qui casserait la sérialisation serait immédiatement détectée, sans avoir à reproduire les scénarios à la main.


---

### 6. Mise en production

La mise en production consiste à installer et rendre opérationnelle, sur le serveur réel, une version développée et testée en local. C'est l'étape finale et critique du cycle : elle mobilise l'ensemble des composants et exige une coordination précise, car une erreur peut rendre les analyseurs inopérants.

#### a. L'environnement de production

Contrairement à l'environnement de développement (poste Windows), le serveur de production est une machine **Linux** (Debian) sur laquelle tournent en permanence tous les services de la PixL Suite, dans des conteneurs Docker isolés. Le développeur n'y a pas accès physique : toute interaction se fait à distance. Les fichiers y sont organisés sous le répertoire `apix`, qui regroupe les services déployés, leurs configurations persistantes (notamment `custom.json`, qui contrôle le choix du fichier de protocole), leurs journaux (logs) et leur documentation — une organisation centralisée qui permet de gérer plusieurs versions sur la même machine.

#### b. Accès au serveur distant via SSH et MobaXTerm

L'accès distant repose sur le protocole **SSH** (Secure Shell ; SSH et SCP, cf. glossaire), qui ouvre un terminal de commande chiffré sur la machine distante. L'outil utilisé est **MobaXTerm**, un client SSH graphique pour Windows offrant deux fonctions clés : un terminal Linux émulé (navigation, scripts, consultation des logs, redémarrage de services) et un gestionnaire de fichiers par glisser-déposer, qui transfère les fichiers entre le poste et le serveur via **SCP** (Secure Copy Protocol, chiffré sur SSH).

#### c. Les artefacts à déployer et le flux de la wheel apix-tools

Avant un déploiement, il faut préparer les fichiers à transférer, appelés **artefacts**, produits par les pipelines de build des dépôts GitLab. La wheel apix-tools suit un flux particulier : compilée par l'alternant (versions Windows et Linux) et stockée dans un dépôt partagé, elle est automatiquement récupérée par le pipeline CI/CD de PixL API d'après le numéro de version de `requirements.txt`, puis intégrée à l'archive ZIP finale — elle est donc déjà présente dans le répertoire `whl/` à l'extraction, sans transfert séparé.

Les artefacts à récupérer pour une mise à jour sont :

- **Les archives ZIP** produites par le pipeline : `pixl-api-x.y.z.zip` (projet Django, dépendances Python et wheel apix-tools intégrée dans `whl/`) et `pixl-expert-x.y.z.zip` (backend Django minimal et build du frontend Vue.js, soit les fichiers HTML/JS/CSS produits par `npm run build`).
- **Les scripts de mise à jour** (`script_upgrade_pixl_api.sh`, `script_upgrade_pixl_expert-vue-js.sh`), scripts Bash qui automatisent le déploiement de chaque service.

#### d. Le processus de déploiement pas à pas

![[flux-deploiement.png|700]]
*Figure 7 : Flux de déploiement : depuis le poste Windows, le code et les fichiers de déploiement sont transférés par SCP/SSH (MobaXTerm) vers le serveur Linux/Debian, puis `docker compose up` démarre l'ensemble des conteneurs (orchestrateur, PixLAPI, module Modbus, interface web, PostgreSQL).*

Le déploiement se déroule en étapes ordonnées (voir Figure 7), chacune validée avant la suivante.

**Étape 1 — Transfert des fichiers.** Les artefacts sont glissés-déposés depuis Windows vers un répertoire temporaire du serveur (`/usr/bin/apix/updates/`) ; MobaXTerm utilise SCP, qui chiffre le transfert.

**Étape 2 — Droits d'exécution.** Sous Linux, un fichier transféré n'est pas exécutable par défaut, et SCP ne préserve pas toujours les permissions ; il faut donc les accorder :

```bash
chmod 755 script_upgrade_*.sh
```

**Étape 3 — Exécution des scripts.** Chaque script prend en argument l'archive à déployer :

```bash
bash script_upgrade_pixl_api.sh     pixl-api-1.0.0.zip
bash script_upgrade_pixl_expert-vue-js.sh pixl-expert-1.0.0.zip
```

L'archive ZIP, versionnée par le pipeline, fait office de source de vérité : on peut rejouer n'importe quelle version sans modifier le script. Ces scripts enchaînent automatiquement des opérations longues et risquées à la main — arrêt du conteneur, extraction de l'archive, remplacement des fichiers, mise à jour des numéros de version dans `.env`, reconstruction de l'image Docker et redémarrage — ce qui garantit la reproductibilité et réduit le risque d'erreur humaine.

**Étape 4 — Vérification des services.** On contrôle enfin que chaque service a démarré :

```bash
docker ps -a
docker-compose logs pixl-api
docker-compose logs pixl-expert
```

`docker ps -a` liste les conteneurs et leur état : `Up` (fonctionnement normal) ou `Exited`/`Restarting` (problème, à diagnostiquer via les logs).

#### e. Architecture Docker et orchestration des services

Chaque composant de la suite — PixL API, PixL Expert et le serveur Modbus — tourne dans un **conteneur Docker** séparé (cf. glossaire). Ces conteneurs sont orchestrés par **Docker Compose** (cf. glossaire) via un unique fichier `docker-compose.yml`, qui décrit pour chaque service son image, ses ports, ses volumes (pour que `custom.json` persiste entre les redémarrages) et ses dépendances (PixL Expert dépend ainsi de PixL API). Un fichier annexe `.env` centralise les variables d'environnement partagées :

```
PIXL_API_VERSION=1.0.0
PIXL_EXPERT_VERSION=1.0.0
APIX_TOOLS_VERSION=3.1.0
```

Ce découplage entre la définition de l'architecture (`docker-compose.yml`) et les valeurs concrètes (`.env`) permet de mettre à jour une version sans toucher à la structure du déploiement. Les scripts de mise à jour modifient automatiquement ces variables dans le fichier `.env` pour refléter les nouvelles versions déployées.

#### f. Difficultés rencontrées

La mise en production a mis en lumière plusieurs problèmes qui ne se manifestent pas en développement local.

**Erreur de version en cascade dans `.env`.** La principale difficulté fut une incohérence entre les versions déclarées dans `.env` et les archives réellement déployées : lors du déploiement de PixL Expert, le script avait mis à jour `PIXL_EXPERT_VERSION` mais pas `APIX_TOOLS_VERSION`. Au démarrage, PixL API cherchait donc la wheel apix-tools à l'ancien numéro de version, ne la trouvait pas et échouait sur `ModuleNotFoundError: No module named 'apix_tools'` — alors que la wheel était bien présente, mais sous un autre numéro. Le diagnostic a consisté à lire les logs (`docker-compose logs pixl-api`), comparer `APIX_TOOLS_VERSION=3.0.0` à la wheel réelle (`apix_tools-3.1.0-…whl`), corriger `.env` et redémarrer le conteneur. Ce bug est sournois : le script s'exécute sans erreur, mais le message pointe vers la wheel manquante plutôt que vers la vraie cause, l'oubli de mise à jour de `.env`.

**Migrations Django incohérentes.** Dans Django, les migrations décrivent l'évolution du schéma de base de données et sont jouées automatiquement au démarrage du conteneur. Le refactoring de PixL Expert (passage d'un backend Django monolithique à une API REST couplée à un frontend Vue.js) avait rendu certaines anciennes migrations inapplicables, créant un état incohérent qui bloquait le démarrage. Il a fallu identifier les migrations fautives dans les logs, corriger leur état et vérifier la cohérence avec la base.

#### g. Résultats et apports

Après ces corrections, l'ensemble de la PixL Suite fonctionnait correctement en production : le serveur Modbus répondait aux équipements connectés, l'API REST exposait ses routes avec la wheel correctement intégrée (lecture/écriture des protocoles définis dans `custom.json`), et PixL Expert servait l'interface Vue.js en dialoguant avec l'API.

---

### 7. Analyse critique : contribution, choix et limites

Au-delà de la description des solutions développées, il me paraît important de prendre du recul sur la démarche suivie : ce qui relève précisément de mon travail, les arbitrages effectués et les limites de l'outil livré.

#### a. Distinguer ma contribution de la base existante

Le projet s'est inscrit dans une base de code déjà conséquente, dont je n'ai écrit qu'une partie. L'architecture générale de la PixL Suite, le framework de sérialisation ModelMother, le socle de configuration commun d'AG Grid et les conventions Vue.js du projet préexistaient à mon arrivée ; l'extension `ModelDictToListMother` (cf. IV.2.c) a par ailleurs été réalisée par ma tutrice pour débloquer une limitation que j'avais rencontrée. Mon apport personnel a porté sur l'ensemble suivant : la conception et le développement des deux éditeurs (`ModbusPart.vue` et `RegisterMapPart.vue`), les routes backend de chargement, de validation et de sauvegarde des deux fichiers, la route générique d'énumérations, la logique de détection des conflits d'adresses, la reconstruction de la structure hiérarchique de `protocol.json` à partir de la liste plate manipulée par le frontend, ainsi que les tests unitaires sur Apix Tools. J'ai donc avant tout construit des fonctionnalités autonomes et identifiables en m'appuyant sur des fondations existantes — un exercice qui m'a demandé de comprendre du code écrit par d'autres avant de pouvoir m'y greffer sans en rompre la cohérence.

#### b. Retour sur les principaux choix techniques

Plusieurs décisions de conception résultaient d'un arbitrage, et non d'une évidence ; elles méritent d'être explicitées au regard des alternatives possibles.

- **Une route d'énumérations générique plutôt que des routes dédiées.** Pour alimenter les listes déroulantes, j'aurais pu créer une route par énumération (vitesses, parités, méthodes…). J'ai préféré une route unique paramétrée par le nom de l'enum, importé dynamiquement via `importlib`. Cette approche évite la multiplication de routes quasi identiques et reste réutilisable pour de futurs éditeurs ; en contrepartie, elle repose sur un import dynamique, légèrement moins explicite et qu'il faut sécuriser pour n'autoriser que les modules d'énumération attendus.
- **Une liste plate plutôt que la hiérarchie native pour le tableau.** Le `protocol.json` est profondément imbriqué, mais un tableau se manipule bien plus naturellement à partir d'une liste plate. J'ai donc choisi d'« aplatir » la structure au chargement puis de la reconstruire à la sauvegarde. Ce choix simplifie nettement l'affichage et le tri, au prix d'une étape de reconstruction délicate (regroupement par section et sous-section) qui a concentré une part importante de l'effort de test (cf. IV.5.b).
- **Une interface pilotée par la configuration (*configuration-driven UI*).** Plutôt que de coder en dur les règles métier du protocole dans le frontend, la route `/protocol/formats` les fait dicter par le backend (cf. IV.4.b). L'alternative — figer ces règles côté Vue.js — aurait été plus rapide à écrire, mais aurait imposé de modifier le frontend à chaque évolution métier. Le choix retenu est plus coûteux initialement mais bien plus évolutif.
- **Un effort de test concentré sur Apix Tools.** Plutôt que de répartir les tests automatisés sur l'ensemble des couches, je les ai concentrés sur la bibliothèque partagée, qui porte la logique la plus critique et la plus réutilisée (cf. IV.5.c). C'est un compromis assumé : il maximise la valeur des tests à coût limité, mais laisse le frontend couvert uniquement par des tests manuels.

#### c. Limites de la solution actuelle

L'outil livré remplit son objectif, mais présente plusieurs limites qu'il est honnête de reconnaître. La validation des saisies, bien que présente, reste partielle : elle couvre les contraintes principales (plages de valeurs, cohérence format/taille, formats autorisés par sous-section) mais pas l'intégralité des règles métier envisageables. La détection des conflits d'adresses *signale* les chevauchements sans proposer de correction automatique. Côté qualité, le frontend n'est couvert que par des tests manuels, faute de tests automatisés d'interface (end-to-end). Enfin, le déploiement, bien qu'outillé par des scripts, reste déclenché manuellement : l'incident de version dans le fichier `.env` (cf. IV.6.f) a montré la fragilité d'une synchronisation encore partiellement manuelle entre composants.

---

## V. Impact environnemental et sociétal

### 1. Impact environnemental de mes déplacements

Les déplacements constituent l'un des principaux postes d'émission de gaz à effet de serre associés à une activité professionnelle. Durant ce stage, qui s'est déroulé du **23 mars au 27 juin 2026** (environ 14 semaines), j'ai effectué l'intégralité de mes trajets domicile-travail en **tramway**, sur une distance d'environ **16 km aller-retour**, à raison de **5 jours par semaine**. En tenant compte des jours fériés, cela représente près de **65 jours travaillés**, soit environ **1 040 km** parcourus sur l'ensemble de la période.

Le tramway étant un transport en commun électrique, il s'agit de l'un des modes de déplacement les moins émetteurs en milieu urbain. À l'aide de l'outil d'estimation mis à disposition par l'ADEME [8], ces trajets représentent une émission estimée à environ **4 kg équivalent CO₂** sur toute la période — un impact très faible comparé aux quelque **225 kg CO₂** qu'aurait générés le même trajet en voiture individuelle, soit un rapport d'environ 1 à 55. Ce choix de transport a ainsi permis d'éviter l'émission de près de **220 kg de CO₂** sur la durée du stage.

Le stage n'a par ailleurs occasionné **aucun déplacement professionnel**, l'activité ayant été réalisée intégralement sur site, ce qui a limité d'autant l'empreinte carbone liée à la mobilité.

### 2. Démarche environnementale et sociale de l'entreprise

La démarche d'APIX en matière écologique et sociale mérite aussi d'être considérée. Son cœur de métier s'inscrit déjà dans une logique environnementale : la gamme **GREENPIX**, dédiée aux gaz renouvelables (biométhane, biogaz), accompagne directement la transition énergétique en permettant le contrôle qualité nécessaire à l'injection de gaz « verts » dans les réseaux.

Sur le plan des pratiques internes, plusieurs éléments témoignent d'une démarche responsable : la petite taille favorise la sobriété (échanges oraux et numériques plutôt que papier, outils dématérialisés), le tri des déchets est en place, et l'implantation en centre-ville de Grenoble, bien desservie, facilite les mobilités douces.

Sur le plan social, l'organisation en petite équipe offre des conditions de travail favorables : communication directe et bienveillante, accompagnement des nouveaux arrivants, autonomie réelle et entraide favorisée par la proximité dans l'espace de travail partagé. Une politique de télétravail partiel apporte en outre de la flexibilité et réduit les déplacements. Cet environnement, exigeant techniquement et humainement accueillant, contribue au bien-être et à la montée en compétence de l'équipe.

### 3. Impact sociétal du projet

Le projet a aussi des retombées sociétales, liées à l'usage de l'outil. En remplaçant l'édition manuelle de `network.json` et `protocol.json` par une interface guidée et validée, il réduit nettement le risque d'erreur humaine lors du paramétrage Modbus, améliore les conditions de travail des techniciens et intégrateurs — qui manipulent une interface claire plutôt qu'un JSON brut — et limite les interventions correctives.

Plus largement, l'outil s'intègre à la PixL Suite, qui pilote des analyseurs de gaz industriels. En contribuant à la fiabilité de ces analyseurs — notamment ceux dédiés au contrôle des gaz renouvelables — le projet participe indirectement à un système ayant un impact environnemental positif : un paramétrage correct et sûr des équipements est une condition de la qualité des mesures sur lesquelles reposent la surveillance des procédés industriels et le suivi des émissions.

---

## VI. Conclusion

Ce stage avait pour objectif de concevoir et développer un outil d'édition des paramètres Modbus intégré à l'interface web PixL Expert, afin de remplacer la modification manuelle des fichiers `network.json` et `protocol.json` par une interface fiable et guidée. Cet objectif a été atteint : l'outil livré permet de visualiser, modifier, valider et sauvegarder ces configurations sans manipuler directement le JSON, et il a été déployé en production au sein de la PixL Suite.

Le projet a couvert l'ensemble de la chaîne de développement, du backend au frontend. Côté Python, il a fallu comprendre et exploiter ModelMother, le système de sérialisation interne du projet, exposer les données de configuration via des routes API, et intégrer des règles de validation issues des contraintes métier du protocole Modbus. Côté Vue.js, il a fallu construire des interfaces d'édition claires pour des données volumineuses et fortement hiérarchisées, tout en respectant l'architecture et les conventions existantes du projet. La phase de mise en production a enfin permis d'aborder des aspects plus opérationnels — déploiement par scripts, conteneurisation Docker, diagnostic d'erreurs en environnement réel — qui ne se rencontrent pas en développement local.

Sur le plan technique, ce stage a été l'occasion de monter en compétence sur une stack complète et largement utilisée en milieu professionnel (Python, Django, Vue.js, Docker, Modbus), et de découvrir les exigences propres au développement logiciel en entreprise : intégration dans une base de code existante, lecture et réutilisation du code d'autrui, validation rigoureuse des données, et diagnostic de problèmes en production. Le travail dans un cadre itératif, sans cahier des charges formel, a par ailleurs renforcé ma capacité d'adaptation, d'autonomie et de communication, les objectifs se précisant au fil des échanges avec ma tutrice.

Ce stage a également prolongé et mis en pratique, dans un contexte professionnel réel, les compétences développées au cours du BUT Informatique. Le développement full-stack de l'outil a directement mobilisé la compétence « Réaliser un développement d'application », tant côté backend que frontend. La manipulation et la validation des fichiers de configuration structurés ont fait appel aux compétences « Gérer des données de l'information » et « Optimiser des applications ». La phase de déploiement par conteneurs sur un serveur Linux distant a prolongé les enseignements de systèmes et réseaux, en lien avec la compétence « Administrer des systèmes informatiques communicants complexes ». Enfin, l'organisation itérative du projet et le travail au sein d'une petite équipe ont concrétisé les compétences « Conduire un projet » et « Travailler dans une équipe informatique ». Ce stage a ainsi constitué une application intégrée de l'ensemble du référentiel de compétences du BUT3.

Au-delà des compétences acquises, ce stage a confirmé mon intérêt pour le développement logiciel appliqué à des problématiques industrielles concrètes, où la fiabilité et la rigueur ne sont pas négociables. L'outil développé constitue une base extensible : il pourra être enrichi de nouveaux types de registres, de validations supplémentaires ou d'une ergonomie affinée à mesure que les besoins des utilisateurs évolueront.

La mise en production, enfin, a été particulièrement formatrice sur la rigueur qu'exige un tel environnement. Des erreurs en apparence anodines — un numéro de version mal synchronisé dans `.env`, des migrations dans un état incohérent — peuvent bloquer un déploiement ou produire un comportement difficile à diagnostiquer. J'en retiens qu'il faut vérifier chaque étape après exécution et ne jamais considérer qu'un script « sans erreur » a forcément produit le résultat attendu : en production, le silence n'est pas synonyme de succès.

---

## Glossaire

- **Modbus** — protocole de communication industriel (1979) reposant sur un modèle maître/esclave, supporté en mode série (RTU/ASCII) et TCP/IP.
- **RTU** *(Remote Terminal Unit)* — mode série de Modbus, transmettant des trames binaires compactes, généralement sur un bus RS-485.
- **RS-485** — norme de transmission série différentielle multipoints, support physique du Modbus série.
- **TCP/IP** *(Transmission Control Protocol / Internet Protocol)* — pile de protocoles standard des réseaux informatiques, support du Modbus TCP.
- **HTTP** *(HyperText Transfer Protocol)* — protocole d'échange de données du web, utilisé par les API REST.
- **IEEE 754** — norme standard de représentation des nombres à virgule flottante en informatique (ici le format `float32`).
- **PME** *(petite et moyenne entreprise)* — entreprise de moins de 250 salariés.
- **Registre (holding / input)** — case mémoire adressable exposée par un équipement Modbus. Les *holding registers* sont accessibles en lecture/écriture, les *input registers* en lecture seule.
- **Sérialisation / désérialisation** — conversion d'un objet en mémoire vers un format textuel persistant (ici JSON), et inversement.
- **JSON** *(JavaScript Object Notation)* — format textuel d'échange de données structuré en paires clé/valeur, listes et objets imbriqués.
- **ModelMother** — classe de base du framework interne d'APIX assurant la sérialisation/désérialisation récursive des modèles Python.
- **Wheel (`.whl`)** — format d'archive de distribution d'un paquet Python prêt à être installé.
- **Conteneur / Docker** — environnement d'exécution isolé embarquant une application et ses dépendances, indépendamment du système hôte.
- **Docker Compose** — outil d'orchestration de plusieurs conteneurs décrits dans un fichier `docker-compose.yml`.
- **CI/CD** — intégration et livraison continues : automatisation du build, des tests et du packaging à chaque modification du code.
- **SSH / SCP** — protocoles d'accès distant sécurisé à un serveur (SSH) et de copie de fichiers chiffrée (SCP).
- **AG Grid** — bibliothèque JavaScript de tableaux de données interactifs (tri, filtres, glisser-déposer) utilisée côté frontend.
- **DRF** *(Django REST Framework)* — extension de Django pour exposer des API REST.

## Références bibliographiques et webographiques

[1] Modbus Organization. *MODBUS Application Protocol Specification V1.1b3* [en ligne]. Disponible sur : https://modbus.org/specs.php (consulté le 08/06/2026)
[2] Vue.js. *Documentation officielle — Guide* [en ligne]. Disponible sur : https://vuejs.org/guide/ (consulté le 08/06/2026)
[3] Django Software Foundation. *Django documentation* [en ligne]. Disponible sur : https://docs.djangoproject.com/ (consulté le 08/06/2026)
[4] Encode. *Django REST Framework* [en ligne]. Disponible sur : https://www.django-rest-framework.org/ (consulté le 08/06/2026)
[5] Docker Inc. *Docker documentation* [en ligne]. Disponible sur : https://docs.docker.com/ (consulté le 08/06/2026)
[6] AG Grid Ltd. *AG Grid — Documentation* [en ligne]. Disponible sur : https://www.ag-grid.com/documentation/ (consulté le 08/06/2026)
[7] Université Grenoble Alpes. *Règlement des études BUT Informatique* [en ligne]. (consulté le 08/06/2026)
[8] ADEME. *Calculateur d'émissions carbone des trajets — Agir pour la transition écologique* [en ligne]. Disponible sur : https://agirpourlatransition.ademe.fr/particuliers/bureau/deplacements/calculer-emissions-carbone-trajets (consulté le 08/06/2026)

## Annexes

### Annexe A — Modèle de communication Modbus maître/esclave

![[modbus-maitre-esclave.png|400]]
*Figure 8 : Modèle de communication Modbus maître/esclave : l'automate maître envoie une requête, l'analyseur APIX (esclave) y répond. L'esclave ne transmet jamais de données spontanément.*

### Annexe B — Hiérarchie complète des classes de modèles

*Arbre complet des classes de modèles du projet, complément de la Figure 3 (cf. IV.2.d). Chaque feuille hérite de `ModelMother` et bénéficie automatiquement des mécanismes de sérialisation.*

```
ModelMother
├── NetworkParameters              ← paramètres réseau complets (network.json)
│   ├── TcpParameters              ← port TCP, flag enabled
│   └── SerialParametersList       ← liste de ports série (ModelListMother)
│       └── SerialParameters       ← un port série (bauds, parité, bits de stop…)
└── ProtocolParameters             ← protocole complet (protocol.json)
    ├── HoldingRegisterParameters
    │   └── MeasureParameters
    │       ├── ElementsDetailedList                (ModelDictToListMother)
    │       │   └── ElementDetailParameters         ← un élément détaillé
    │       │       └── ElementPropertyParameters   ← raw_value, normalized_value…
    │       └── ElementList                         (ModelDictToListMother)
    │           └── ElementParameters               ← un élément simple
    └── InputRegisterParameters
        ├── AlarmParametersList     (ModelDictToListMother)
        │   └── AlarmEntryParameters ← une alarme
        ├── MeasureParameters
        ├── InformationParameters
        ├── SystemParameters
        └── CommandParameters
```

### Annexe C — Structure complète du fichier `network.json`

*Exemple complet illustrant les quatre sections décrites en IV.3.a (identifiant d'esclave, configuration TCP, ports série, configuration ZMQ).*

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

## Résumé

Ce stage, réalisé chez APIX Analytics, fabricant grenoblois d'analyseurs de gaz chromatographiques industriels, a porté sur le développement d'un outil d'édition des paramètres Modbus intégré à l'interface web PixL Expert. Auparavant, la configuration de la communication Modbus de l'analyseur, décrite dans les fichiers `network.json` et `protocol.json`, devait être éditée à la main, au prix d'un risque d'erreurs élevé et d'une perte de temps importante. Le travail réalisé, de nature full-stack, a consisté à exposer ces données via des routes API en Python (Django / DRF) et à construire les interfaces d'édition correspondantes en Vue.js, avec validation des saisies, détection des conflits d'adresses et affichage tabulaire des registres. L'outil a été testé puis déployé en production via Docker. Il fiabilise la configuration des analyseurs et réduit sensiblement le temps nécessaire pour adapter un protocole.

**Mots clés :** Modbus, configuration, full-stack, Vue.js, Python, Django, API REST, Docker

## Abstract

This internship, carried out at APIX Analytics — a Grenoble-based manufacturer of industrial chromatographic gas analysers — focused on developing a Modbus parameter editor integrated into the PixL Expert web interface. Previously, the analyser's Modbus communication settings, stored in the `network.json` and `protocol.json` files, had to be edited by hand, which was error-prone and time-consuming. The full-stack work consisted of exposing this data through Python API endpoints (Django / DRF) and building the matching editing interfaces in Vue.js, with input validation, address-conflict detection and a tabular view of the registers. The tool was tested and deployed to production using Docker. It makes analyser configuration more reliable and significantly reduces the time needed to adapt a protocol.

**Keywords:** Modbus, configuration, full-stack, Vue.js, Python, Django, REST API, Docker