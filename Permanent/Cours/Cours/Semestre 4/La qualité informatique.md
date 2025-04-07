R3.09

Définition de qualité est un concept polysémique : il est définit de différentes manières selon le contexte. La qualité désigne l'aptitude d'un produit, d'une service, d'un processus ou d'une organsiation à satisfaire les besoins et les attentes des utiliateurs en fonction des utilisateurs ou des clients

Les dimensions de la qualité :
- **La qualité intrasèque**
- **La qualité attendue**
- **La qualité réalisée**
- **La qualité perçue**

La notion de qualité permet de réduire les coûts. En effet, il est moisn coûteux de dépenser en production plutôt qu'en post-production. Cela permet également une meilleure interface utilisateur.

Les coûts de conformité sont :
- Les coûts de conformité
    - Coûts de prévention
        - Formation
        - Processus documentaires
        - Equipement
        - Délai approprié
    - Coûts d'évaluation
        - Tests
        - Perte lié à des tests destructifs
        - Inspections
- Coûts de non-conformité
    - Coûts de défaillances externe (constatés par le projet)
        - Responsabilité
        - Travail sous graranties
        - Affaire perdue
    - Coûts de défaillences internes (constatés par le projet)
        - Reprise
        - Déchets


Les acteurs de la qualité sont :
- Le chef de projet (Responsable qualité globale du projet et définition + mise en place des mesures techniques et organisationnelles nécessaires)
- L'équipe de dév (Chargée de respecter normes de qualité et réaliser tests)
- L'équipe de tests (Resonsable de la validation du logiciel et de la détectino des anomalies)
- Le client

La qualité consiste à la mise en place de procédures et des méthodes pour savoir quoi et comment évaluer. L'évaluation repose sur la mise en place et le respect de bonnes pratiques et sur la mise en place de procédures de vérification et tests


Les domaines de la qualité :
- Qualité des produits
- Qualité des services
- Qualité des processus
- Qualité de vie
- Qualité environnementale

ISO 25000 : Cadre pour l'évaludation de la qualité des logiciels
CMMI : Définit les niveaux de ...
ISO 9126 : Caractéristiques de qualité d'un logiciel

Absolument ! Voici une version complète et homogénéisée du texte, intégrant tous les éléments fournis et structurée de manière cohérente :

# Normes ISO 25000 : Qualité Logicielle

**Objectifs :**

- Spécifier les exigences de qualité des logiciels
    
- Évaluer la qualité des logiciels
    
- Améliorer la qualité des logiciels
    

## 1. Capacité Fonctionnelle

La capacité fonctionnelle d'une application se réfère à sa capacité à exécuter les tâches pour lesquelles elle a été conçue.

## 1.1 Aptitude

- **Définition :** Capacité du système à répondre aux besoins essentiels et aux exigences de l'utilisateur. Le système doit traiter correctement les données et fournir les résultats attendus.
    
- **Compétences à mobiliser :** Modélisation, recueil des besoins, diagramme des cas d’utilisation.
    
- **Évaluation :** Test fonctionnel en boîte noire (avec les pré et post conditions) ou automatisation des tests.
    

## 1.2 Exactitude

- **Définition :** Les informations doivent être traitées avec précision pour éviter les imprécisions et les erreurs. Cela est nécessaire pour éviter des informations erronées, des données mal enregistrées, ce qui pourrait entraîner des incohérences ou faire buguer l'application.
    
- **Compétences à mobiliser :** Qualité de code (nommage des variables…). Avec un référentiel de bonnes pratiques.
    
- **Évaluation :** Le taux de couverture du code (80 % Loi de pareto) par les tests unitaires en boîte blanche.
    

## 1.3 Interopérabilité

- **Définition :** Capacité du système à fonctionner avec d'autres appareils, permettant une transition fluide et efficace avec d'autres applications et systèmes.
    
- **Compétences à mobiliser :** Développement : responsive des vues, le langage correspond aux systèmes que l’on cible.
    
- **Évaluation :** Test d’intégration avec une couverture de code de 80 % (loi de Pareto).
    

## 1.4 Conformité

- **Définition :** Le respect par le système des normes, réglementations et standards applicables. Cela inclut la conformité aux exigences légales, aux normes de sécurité et aux standards de l'industrie.
    
- **Compétences à mobiliser :** Prise en compte dans la modélisation, dans la modélisation de la base de données par exemple.
    
- **Évaluation :** Vérification dans les textes de lois, revue de code (audit), revue de code en boîte blanche.
    

## 1.5 Sécurité

- **Définition :** La protection du système contre les accès non sécurisés et par les piratages ou les pertes de données. Cela garantit la mise en place de mesures garantissant la confidentialité, l'intégrité et la disponibilité des serveurs, contre tout accès non autorisé.
    
- **Compétences à mobiliser :** Qualité de développement (que des prepare SQL par exemple), mises à jour fréquentes.
    
- **Évaluation :** Test de sécurité des applications statiques (SAST) boite blanche, test destructif, test de stress, test fonctionnel.
    

## 2. Fiabilité

## 2.1 Maturité

- **Définition :** Le niveau de développement et de test du système, reflétant sa stabilité et sa robustesse.
    
- **Compétences à mobiliser :** Gestion des processus de tests (unitaires, d'intégration, de performance), développement logiciel selon des méthodologies éprouvées (ex. : Agile, DevOps), analyse des risques et gestion des anomalies, expertise en assurance qualité (QA).
    
- **Évaluation :** Tests unitaires et d'intégration (boîte blanche), tests de performance et de charge, analyse des métriques de stabilité (taux d'erreurs, plantages), revues de code pour identifier les failles potentielles.
    

## 2.2 Tolérance aux Fautes

- **Définition :** La capacité du système à continuer de fonctionner, y compris de manière dégradée, même en cas de défaillances partielles ou d'erreurs internes.
    
- **Compétences à mobiliser :** Conception logicielle résiliente (ex. : gestion des exceptions), mise en œuvre de mécanismes redondants, expertise en architecture distribuée ou tolérante aux pannes, surveillance proactive des systèmes.
    
- **Évaluation :** Tests de simulation d'erreurs (injection de fautes), vérification des mécanismes de redondance, analyse des logs pour identifier la gestion des erreurs, scénarios de tests en conditions défavorables (boîte noire), tests de stress.
    

## 2.3 Capacité de Récupération (PRA)

- **Définition :** La capacité du système à revenir à un état opérationnel après une panne ou un incident.
    
- **Compétences à mobiliser :** Mise en place de stratégies de reprise après sinistre (Disaster Recovery Plan), gestion des sauvegardes et restaurations (important), expertise en gestion des bases de données et systèmes distribués, connaissances en sécurité informatique pour éviter les interruptions prolongées.
    
- **Évaluation :** Tests réguliers des procédures de reprise après sinistre, simulation d'incidents pour évaluer les temps de récupération, mesure du RTO (Recovery Time Objective) et du RPO (Recovery Point Objective), vérification des sauvegardes automatiques et manuelles.
    

## 3. Facilité d’Usage

- **Exploitabilité :** Indispensable pour les projets nécessitant une maintenance ou une gestion continue, comme par exemple les infrastructures ou les systèmes logiciels. Cela permet d’assurer une meilleure durabilité et un fonctionnement optimal, en raccord avec les objectifs de responsabilité sociétales (Réduction de ressources nécessaires, …)
    
- **Facilité d’apprentissage :** Nécessaire lors de la création d’un logiciel grand public. Les jeunes étant moins affutés, et les personnes plus âgées plus rigides avec la technologie. Essentiel pour les projets éducatifs, technologiques ou d'intégration de nouvelles solutions. Cela permet de réduire le temps d’adaptation par les utilisateurs et améliore leur productivité.
    
- **Facilité de compréhension :** La facilité de compréhension est la facilité de l’utilisateur à comprendre ce qui lui est présenté. Nécessaire dans des projets impliquant des interfaces utilisateur ou des documents techniques. Cela permet une meilleure communication entre les parties prenantes et assure une prise de décision éclairée.
    

## 3.1 Exploitabilité

- **Définition :** Capacité d'un système informatique à être maintenu et géré efficacement sur le long terme, en assurant sa durabilité et son fonctionnement optimal, tout en respectant les principes de responsabilité sociétale.
    
- **Compétences à mobiliser :** Gestion de projet à long terme, maintenance préventive et corrective, optimisation des ressources, connaissance des normes environnementales et sociales.
    
- **Évaluation :** Tests de charge et de performance, audits réguliers du système, analyse de la consommation des ressources, évaluation de l'impact environnemental (boîte noire).
    

## 3.2 Facilité d'Apprentissage

- **Définition :** Aptitude d'un logiciel à être rapidement compris et utilisé par ses utilisateurs cibles, en favorisant l'inclusion et en réduisant les inégalités d'adaptation technologique. Facilité pour l’utilisateur à prendre en main l’application.
    
- **Compétences à mobiliser :** Conception d'interfaces utilisateur intuitives, développement de tutoriels et d'aides contextuelles, compréhension des besoins des différents groupes d'utilisateurs, techniques de formation et d'accompagnement, contrôle explicite, tutoriels, FAQ.
    
- **Évaluation :** Tests utilisateurs (boîte noire), mesure du temps d'apprentissage, enquêtes de satisfaction auprès des utilisateurs, analyse des taux d'adoption et d'utilisation.
    

## 3.3 Facilité de Compréhension

- **Définition :** Capacité d'un projet informatique à présenter des informations claires et accessibles pour toutes les parties prenantes, favorisant la transparence et la prise de décision éclairée.
    
- **Compétences à mobiliser :** Communication technique claire, conception de documentation utilisateur, visualisation de données, gestion des parties prenantes.
    
- **Évaluation :** Revues de documentation (boîte blanche), tests de compréhension auprès des utilisateurs, évaluation de la qualité de la documentation technique, feedback des parties prenantes sur la clarté des informations.
    

## 4. Efficacité

## 4.1 Efficacité des Ressources Employées

- **Définition :** Ce critère évalue l'utilisation efficace des ressources matérielles et logicielles disponibles par le logiciel.
    
- **Conséquence pratique :** Organisation (formation des développeurs aux bonnes pratiques d'optimisation), conception (choix judicieux des algorithmes et structures de données), développement (monitoring et optimisation de l'utilisation des ressources), évaluation (mesures précises de la consommation de ressources (monitoring)).
    
- **Cadre de projet pertinent :** Applications mobiles, systèmes embarqués, logiciels cloud avec facturation à l'usage.
    

## 4.2 Efficacité des Temps de Réalisation

- **Définition :** Ce critère mesure la capacité du logiciel à répondre aux exigences de temps spécifiées pour ses opérations et fonctionnalités.
    
- **Cadres de projet pertinents :** Applications interactives, systèmes de contrôle industriel, logiciels de trading financier.
    
- **Conséquence pratique :** Organisation (définition claire des objectifs de performance temporelle), conception (mise en place d'architectures asynchrones ou parallèles si nécessaire), développement (optimisation des algorithmes critiques en termes de temps), évaluation (tests de performance avec mesure précise des temps de réponse).
    

## 5. Maintenabilité

- **Définition :** La maintenance d’une application sont les opérations visant à maintenir, rétablir ou améliorer les fonctionnalités d’une application. Pour que cela soit fait efficacement, il y a certains critères de maintenabilité à suivre.
    

## 5.1 Métriques de Code

- **Définition :** Mesures quantitatives de divers aspects du code (taille, complexité, cohésion, couplage, lisibilité, testabilité et documentation).
    
- **Compétences à mobiliser :** Compréhension des différentes métriques, utilisation d'outils d'analyse statique pour calculer ces métriques.
    
- **Évaluation :** Analyse des métriques de code (taille, complexité, cohésion, couplage, lisibilité, testabilité et documentation).
    

## 5.2 Modularité

- **Définition :** Application composée de modules indépendants, pouvant être analysées et développées séparément.
    
- **Compétences à mobiliser :** Conception d'architectures modulaires.
    
- **Évaluation :** Analyse de la structure du code pour vérifier le niveau de modularité.
    

## 5.3 Documentation

- **Définition :** Sert à mieux comprendre la structure du code, les fonctionnalités de l’application et des usages. Pour une meilleure maintenabilité, elle doit être détaillée et régulièrement mise à jour.
    
- **Compétences à mobiliser :** Description de l’architecture du code, description des fonctionnalités, déclaration des formats de données.
    
- **Évaluation :** Description de l’architecture du code, description des fonctionnalités, déclaration des format des données.
    

## 5.4 Tests

- **Définition :** Servent à vérifier le bon fonctionnement de l’application après chaque modification, assurant sa stabilité.
    
- **Compétences à mobiliser :** Tests automatisés, approfondissement des tests, testage régulière.
    
- **Évaluation :** Tests automatisés, approfondissement des tests, testage régulière.
    

## 5.5 Simplicité et Intuitivité

- **Définition :** Bonne qualité de code, plus facile à maintenir et faire évoluer.
    
- **Compétences à mobiliser :** Noms des méthodes claires et descriptifs, code optimisé et concis, Présence de commentaires pour expliquer le code.
    
- **Évaluation :** Noms des méthodes claires et descriptifs, code optimisé et concis, Présence de commentaires pour expliquer le code.
    

Ce critère est pertinent pour toute application qui vise à une évolution. Une application avec une bonne maintenabilité permet une évolution efficace du code, une fois que la prise en main et la compréhension du code est plus rapide. Contrairement, un code qui n’est pas maintenable mène à un plus grand coût et investissement.

## 6. Portabilité

- **Définition :** La portabilité est la capacité d'un logiciel à être transféré d'un environnement à un autre.
    

## 6.1 Facilité d'Installation

- **Cadres de projet pertinent :** Logiciels multiplateforme, applications destinées à des marchés internationaux.
    
- **Conséquence pratique :** Organisation (formation des équipes aux différentes plateformes cibles), conception (architecture modulaire permettant l'adaptation facile), développement (utilisation de frameworks cross-platform et de techniques d'internationalisation), évaluation (tests sur diverses plateformes et configuration).
    

## 6.2 Conformité

- **Cadres de projet pertinent :** Logiciels dans des secteurs réglementés (finance, santé), applications nécessitant des certifications spécifiques.
    
- **Conséquence pratique :** Organisation (désignation d'un responsable de la conformité), conception (intégration des exigences de conformité dès la phase de conception), développement (implémentation de fonctionnalités d'audit et de traçabilité), évaluation (audits réguliers et tests de conformité).
    

## 6.3 Facilité de Migration

- **Cadres de projet pertinent :** Systèmes de gestion de données, applications avec des mises à jour fréquentes.
    
- **Conséquence pratique :** Organisation (planification détaillée des processus de migration), conception (conception de mécanismes de conversion de données et de paramètres), développement (implémentation d'outils de migration automatisés), évaluation (tests de migration avec des jeux de données réels).
    

## 6.4 Adaptabilité

- **Cadres de projet pertinent :** Logiciels multiplateforme, applications destinées à des marchés internationaux.
    
- **Conséquence pratique :** Organisation (formation des équipes aux différentes plateformes cibles), conception (architecture modulaire permettant l'adaptation facile), développement (utilisation de frameworks cross-platform et de techniques d'internationalisation), évaluation (tests sur diverses plateformes et configurations).
    

# Normes ISO 27000
### Répartition des rôles

**Définition :** C'est le processus de définition et d'attribution claire des tâches et des responsabilités liées à la sécurités de l'information. C'est pour assurer une gestion efficace et éviter les chevauchements ou lacunes. Mis en place sur les points stratégique de l'entreprise (pour minimiser le travail).

**Comment on le met en place :** En communiquant efficacement de ces rôles à tous les employés concernés et en utilisant des outils comme la matrice RACI. Documenter clairement les rôles dans la description de poste. faire un organigramme bis pour savoir qui est la personne relais pour faire remonter es incidents. Définir le perimetre du domaine du SI pour appliquer le managment du SI
Les types de domaines d'application : 
Données personnels
Les elt d'avantage concurentiels

**Pourquoi on le met en place :** Pour gérer efficacement de la sécurité informatique de l'information, éviter les chevauchements dans les responsabilités et faciliter la responsabilité et l'audit.

### Séparation des tâches

**Définition :** C'est un principe visant à diviser les tâches sensibles entre plusieurs personnes pour prévenir les abus et erreurs. C'est pour renforcer la sécurité en limitant les pouvoirs individuels. Diviser les taches du meme processus a plusieurs personnes pour eviter les erreurs ou abus

**Comment on le met en place :** Il faut identifier les tâches conflictuelles et les séparer entre différentes personnes. En mettant en place des contrôles compensatoires comme des audits et des approbations de flus de travail et en impliquant les gestionnaires dans les discussions sur les risques liés à la séparation des tâches. principe du moindre privilege pendant la conception

**Pourquoi on le met en place :** Permet d'augmenter l'efficacité au sein de l'entreprise, réduire les risques de fraude ou d'erreurs. eviter les erreurs

### Relations avec les autorités

**Définition :** C'est l'établissement de canaux de communication et de collaboration avec les autorités compétentes en matières de sécurité, l'objectif étant d'assurer la conformité réglementaire et de bénéficier de conseils experts. Gestion des contraintes et analyse des risques

**Comment on le met en place :** Identifier les autorités pertinentes, établir des procédures de contact et de reporting et désigner des responsables pour ces relations. Identifier es autorités de controles qui sont ammener a controler mon activite -> mes obligation, quelle forme prend la relation -> créer les cannaux( mon SI correspond aux attentes (ex: hopitaux 24h pour prévenir l'ensii en cas d'incident donc les cannaux doivent etre preetabli)

**Pourquoi on le met en place :** C'est pour assurer la conformité réglementaire, faciliter la gestion des incidents de sécurité et bénéficier des conseils et ressourecs des autorités compétentes.

### Gestion de projet

**Définition :** C'est l'intégration des considérations de sécurité dans la planification et l'exécution des projets, l'objectif étant de garantir que la sécurité est prise en compte dès le début pour réduire les risques et améliorer la qualité.

**Comment on le met en place :** En intégrant la sécurité de l'information dans la méthodologie de gestion de projet, en formant les chefs de projet aux exigences de sécurité et en incluant des étapes de validation de sécurité dans le cycle de vie du projet. Produire un PIA (Privacy Impact Assecement) -> analyse d'impact de données personnels à montrer a la CNIL en cas de demande

**Pourquoi on le met en place :** C'est pour garantir la prise en compte de la sécurité dès la conception des projets, pour réduire les coûts liés à l'intégration tardive de la sécurité et pour améliorer la qualité et la sécurité des livrables de projet.

### Mobilité et Télétravail

**Définition :** Permettre aux employés de pouvoir travailler à distance et/ou sur leur machine personnel. Ordi portable ou telephone fourni par l'entreprise -> mobilité ou en BIOD (materiel perso de l'employer)

**Comment on le met en place :** "- identifier les risques liés à l'usage d'un poste nomade
- mettre en place les mesures de sécurité complémentaires de l’utilisation des appareils mobiles, et la protection des informations consultées, traités ou stockées 
Donc mettre en place une politique de confidentialité
Il faut définir et communiquer, à chaque salarié en télétravail, les principes de détention et d’utilisation d’un périphérique" Cartografier et identifier l'utilisation des appareils nomade (sur site ou hors site) 
formaliser dans la charte informatique

**Pourquoi on le met en place :** Il faut mettre en place ces meusure pour protéger la confidentialité de l'information et protéger les donées (potentielement confidentiel)

### Responsabilité

**Définition :** C'est de determiner quels informations sont répertorié, quels sont leurs degrès de confidentialité et donc savoir qui doit y avoir accès

**Comment on le met en place :** "Droit d'acces et role déterminer :
Chaque personne a un rôle et un droit d'acces determiné par l'administrateur systeme" Capacité a faire un inventaire des actifs supports d'information physique ou numérique
Déterminer qui a acces, qui est le proprietaire / comment on le MAJ, on le rentre et sort du domaine d'application (cycle de vie), les nivaux de sécurité necessaire (le limiter aux domaine de la sécurité de l'information)
attention a la géographie ex : imprimante mutualisés (ou tous le monde y a acces)

**Pourquoi on le met en place :** C'est pour limiter le risques d'incident (suppression ou fuite de données). Chaque personne n'a acces qu'aux données qui luiu sont utile pour éviter qu'une personne qui n'en a pas besoin ai acces à des données confidentiels

### Manipulation des supports

**Définition :** C'est l'intégration de support interne ou externes qui peuvent nécéssité des procédures particulières en prévention

**Comment on le met en place :** "Mettre en place des procédure en cas d'incidents
Bien séparer le développement et la production
Pas d'utilisation direct de périphérique (comme une cles USB) qui vient de l'exterieur"

**Pourquoi on le met en place :** C'est pour éviterla fuite de données et pour éviter l'intrusion dans le systeme d'un programme malveillant

### Politique de chiffrement

**Définition :** C'est la mise en place dans le système d'information d'algirithme de chiffrement sur les données sensibles. Définit la politique de chiffrement (taille des cles)

**Comment on le met en place :** "dans une base de données ou durant un échange de données : AES (symetrique) / RSA (asymétriqque) ou autre, ou une combinaison de AES et RQA par exemple" Pas la meme politique pour tous le domaine. Il faut spécifier précisement la politique de chiffrement sans deteriore l'activite (ex temps d'attente)

**Pourquoi on le met en place :** Pour ne pas avoir acces aux données directement visible (dans la BD ou lors d'un échange de données) pour amélioré leur sécurité

### Gestion des clés

**Définition :** Le chiffrement est utilisé pour protéger les données privées et sensibles lors du stockage, du transit et de l’utilisation. Les clés utilisés pour le déchiffrement doivent être aussi protégées, ce qui s’appelle la gestion des clés. Qui a acces a quelle cles / comment ont les renouvelles / comment on les supprimes/ procedure en cas de perte des cles / sucurisation du stockage et gest des cles

**Comment on le met en place :** "La gestion des clés est faite principalement de deux manières : Gestion du cycle de vie - La génération, l’utilisation, le stockage, la mise à jour, l’archivage et la destruction des clés critiques.
Gestion de l’accès - Seulement les utilisateurs autorisés peuvent utiliser les clés."

**Pourquoi on le met en place :** La qualité d’un chiffrement dépend du degré de protection des clés associés. Il devient inutile de chiffrer les données si l’on ne protège pas aussi les clés. De cette manière, pour garantir que le système de chiffrement soit efficace en faire ce qu’il était prévu, une bonne gestion des clés est essentielle et indispensable.

### Documentation des procédures d'exploitation

**Définition :** La documentation des procédures d’exploitation consiste à formaliser les processus et instructions nécessaires pour gérer les opérations informatiques quotidiennes. Cela inclut également les conduites à tenir en cas d’erreur ou d’incident. a destination de l'équipe IT (admin systeme...) pas pour les utilisateurs

**Comment on le met en place :** Pour une documentation plus efficace, tous les tâches et processus doivent être listées et décrites de forme détaillé, claire et précise. Il est important aussi d’avoir une mise à jour régulière de la documentation, afin de refleter les changements technologiques Wiki de document d'exploitation avec toutes les procédures du cycle de vie de ...

**Pourquoi on le met en place :** Pour standardiser les pratiques, assurant une coherence entre les tâches, et aussi reduction des erreurs, evitant les oublis et mauvaises mamnipulations.

### Séparation des environnements

**Définition :** C'est la pratique d'isoler physiquement ou logiquement les serveurs de développement, de test, de préproduction et de production serveur de dev, qualification (test), préproduction(pour les grande entreprise) et production

**Comment on le met en place :** En utilisant des environnements virtuels ou physiques distincts, mettre en place une identification claire des environnements, pour minimiser les erreurs

**Pourquoi on le met en place :** Proteger l'environnement de production et les données sensibles des risques de changements non autorisées, permetant de tester les changements dans un environnement securisée avant le déploiement 

### Protection contre les malware

**Définition :** C'est les mesures visant à détecter, prévenir et récupérer des attaques de logiciels malveillants pouvant compromettre la confidentialité, l'intégrité ou la disponibilité des systèmes et des données identifier la vulnérabilité du systeme : faire de la veille

**Comment on le met en place :** Logiciels anti-malware mises à jour, isoler et surveiller les réseaux et systèmes, procédures de gestion des changements pour limiter les risques d'introduction de malwares

**Pourquoi on le met en place :** Prévenir la perte des données sensibles (protection de la réputation), maintenir l'integrité des systèmes. Assurer les critères 25000
Serv dev : test unitaire
Serv test : integration, non regresion (+ test boite noir si petite entreprise)
serv préprod : test boite noir

### Sauvegarde

**Définition :** Les sauvegardes sont des procédures essentielles visant à protéger et à préserver les données critiques d'une organisation

**Comment on le met en place :** création régulière de copies des informations importantes, qui sont stockées de manière sécurisée, 3 copies sur 2 lieux/support différents Préconisation 3 sur 2 lieux différents et + c'est sensible, + les nombre de copie et importante et la géographie est différente
différent sur le domaine

**Pourquoi on le met en place :** garantir la disponibilité et l'intégrité des données en cas d'incident Savoir d'ou les erreurs viennent

### Journalisation

**Définition :** La journalisation est le processus d'enregistrement systématique des événements pertinents dans un système d'information

**Comment on le met en place :** Elle consiste à créer des fichiers journaux (log files) qui enregistrent des informations détaillées sur les activités du système, telles que les accès, les modifications de fichiers, les transferts de données et autres événements significatifs

**Pourquoi on le met en place :** "Assurer l'imputabilité et la traçabilité des actions effectuées

    Identifier les auteurs des actions (identification)

    Garder une trace des actions et de leurs auteurs (traçabilité)

    Concrétiser la propriété d'imputabilité, permettant d'attribuer les actions aux personnes, systèmes ou processus qui les ont initiées"

### Cloisonnement des réseaux

**Définition :** Pratique de sécurité qui consiste à séparer et à isoler différents domaines ou segments d'un réseau informatique

**Comment on le met en place :** La séparation des différents domaines de réseau (par exemple, postes de travail, serveurs, DMZ)

    L'utilisation de pare-feu et d'autres dispositifs de contrôle d'accès pour gérer le trafic entre les segments

    La mise en place de politiques de sécurité spécifiques pour chaque segment du réseau Cloisonnement physique ou logique (+vulnérable) :
+ les données sont sensible, on va préférer le cloisonnement physique

**Pourquoi on le met en place :** Cette approche vise à limiter la propagation des menaces et à réduire l'impact potentiel d'une compromission Evite de propager les problemes

### Engagement de confidentialité

**Définition :** Il s'agit d'un accord formel par lequel les employés, les sous-traitants et autres parties prenantes s'engagent à ne pas divulguer ou utiliser de manière inappropriée les informations confidentielles auxquelles ils ont accès dans le cadre de leurs fonctions.

Cet engagement comprend généralement :

Une définition claire de ce qui constitue une information confidentielle

  Les obligations spécifiques de l'individu concernant la protection de ces informations... Les conséquences en cas de violation de la confidentialité

**Comment on le met en place :** Mettre un mdp different
deffinir quels sont les engagent suivant la confidentialité lié a son poste de travail
mis dans le contrat de travail

**Pourquoi on le met en place :** Eviter la fuite d'information !!!!

### Signalement des incidents et des failles

**Définition :** établir un systeme permettant aux employés de signaler rapidement et efficacement les évenements de sécurité observés ou suspectés. (inclut la documentation et l'analyse des oncidents pour prevenir les futures occurences

**Comment on le met en place :** tous les employés doivent savoir qu'ils doivent signaler les incidents et l'organisation doit avoir un point de contact et une procédure simple, accessible et disponible
signaler : controle de securité inefficaces, violation des attentes de confidentialités ou d'intégrités, erreurs humaines, modification non autorisées des systemes et infection par un logiciel malveillant GLPI -> permet de faire de la remonter d'incident

**Pourquoi on le met en place :** detecter les menaces potentielles et minimiser leurs impact

### Recueil des preuves

**Définition :** "ensemble de procédures et de mesures préétablies visant à assurer la poursuite des activités critiques d'une organisation en cas d'incident majeur ou de catastrophe. Il a pour objectif de minimiser les interruptions opérationnelles et de permettre une reprise rapide et efficace des fonctions essentielles.

**Comment on le met en place :** recueillir : documents de politiques de secu, rapports d'audits, registres de formation, logs de securité, evaluation des risques, rapports d'incidents
comment : surveillance continue, revues périodiques, interview et questionnaires

**Pourquoi on le met en place :** demontrer la conformité de l'organisation,, evaluer l'efficacité des mesures de securités, identifier les points d'amelioration du systeme de management de la securité de l'information

### Plan de continuité (PCA)

**Définition :** ensemble de procédures et de mesures préétablies visant à assurer la poursuite des activités critiques d'une organisation en cas d'incident majeur ou de catastrophe. Il a pour objectif de minimiser les interruptions opérationnelles et de permettre une reprise rapide et efficace des fonctions essentielles.

**Comment on le met en place :** analyse des risques, controle des accès, cryptage des données, sauvegardes régulières, planification de la continuité (Recovery Time Objective, Recovery Point Objective), tests et revisions Coute plus chere que le PRA au niveau de la mise en place

**Pourquoi on le met en place :** assurer la continuité des activités et la protections des informations critiques Service de crise et dégradation de l'activité des services essentiels

### PRA

**Définition :** "ensemble de procédures documentées qui permettent à une entreprise de rétablir et de reprendre ses activités après un incident

**Comment on le met en place :** evaluation des risques, controles de securité, planification de la continuité, sensibilisation et formation Au niveau de l'exploitation coute plus chere

**Pourquoi on le met en place :** assurer la continuité des operations Il y a forcément du PRA avec car il faut revenir a la normale apres
