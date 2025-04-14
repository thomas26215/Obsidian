# Informations générales

## Présentation de TestComplete

TestComplete est un outil d’automatisation des tests développé par SmartBear, conçu pour tester une grande variété d’applications : desktop (Windows), web et mobiles (iOS, Android). Il prend en charge de nombreuses technologies et langages, notamment .NET, WPF, Visual C++, Visual Basic, Delphi, Java, HTML5, et bien d’autres.

## Fonctionnalités principales

- **Automatisation des tests fonctionnels et unitaires** : TestComplete permet de créer des tests pour valider le bon fonctionnement des applications, aussi bien pour des tests de régression quotidiens que pour des tests unitaires ou orientés données.
- **Création de tests sans code ou avec scripts** : Les utilisateurs peuvent enregistrer leurs actions pour générer des tests automatisés ou écrire des scripts dans différents langages (Python, JavaScript, VBScript, C#Script, etc.).
- **Reconnaissance intelligente des objets** : Grâce à l’IA, TestComplete identifie les éléments d’interface, même si leur structure évolue, facilitant la maintenance des tests.
- **Exécution flexible** : Les tests peuvent être lancés localement, sur des machines virtuelles, ou de façon distribuée pour optimiser la couverture et la rapidité des campagnes de tests.
- **Rapports détaillés** : L’outil génère des rapports complets sur les résultats des tests, permettant d’identifier rapidement les anomalies et d’optimiser la qualité logicielle
- **Intégration avec l’écosystème DevOps** : TestComplete s’intègre avec des outils comme Jenkins, Jira, Git, Azure DevOps, Selenium, facilitant l’automatisation dans les pipelines CI/CD.
- **Support multi-plateformes et multi-navigateurs** : Il permet de tester sur différents navigateurs, systèmes d’exploitation et appareils mobiles, avec gestion des tests parallèles.

## Avantages

- **Accessibilité** : Aucune compétence en programmation n’est requise pour débuter, grâce à l’enregistrement des tests et à l’interface intuitive.
- **Polyvalence** : Convient aussi bien aux petites équipes qu’aux grandes entreprises, pour des applications variées (web, desktop, mobile).
- **Réduction du temps de test** : L’automatisation accélère les cycles de développement et de validation, tout en maintenant un haut niveau de qualité.

## Cas d’utilisation

TestComplete est utilisé pour :
- Automatiser les tests de régression et fonctionnels
- Effectuer des tests de performance et d’interface utilisateur
- Gérer des campagnes de tests à grande échelle dans des environnements complexes
- S’intégrer dans des processus DevOps pour des déploiements rapides et fiables.

## Conclusion

TestComplete s’impose comme une solution complète et puissante pour l’automatisation des tests logiciels, adaptée à tous types d’applications et d’environnements. Son interface conviviale, ses capacités avancées de reconnaissance d’objets et son intégration dans les pipelines DevOps en font un choix privilégié pour les équipes souhaitant améliorer la qualité et la fiabilité de leurs applications tout en optimisant leurs processus de test.



# Différents types de tests
Il existe de nombreux types de tests dans TestComplete adaptés à différents besoins et à différents niveaux de complexité. Il existe 2 types majeurs de tests : les tests majeurs et les tests auxiliaires. Les tests majeurs sont des tests qui sont exécutés de manière autonome, tandis que les tests auxiliaires sont des tests qui sont appelés par d'autres tests. Les tests majeurs peuvent être des tests de régression, des tests de performance, des tests de sécurité, etc. Les tests auxiliaires peuvent être des fonctions ou des méthodes qui effectuent des actions spécifiques, comme la connexion à une base de données ou l'envoi d'un e-mail.

## Les tests majeurs

### Les tests de mots clés (Keyword tests)
Un **Keyword test** est constitué d'une suite d'opérations correspondant chacune à une opération utilisateur (clic, saisie, sélection de menu ...). Ils sont faciles à créer et à modifier grâce à une interface visuelle

### Les scripts
Un script est une suite d'instructions écrites dans un langage de programmation (Python, VBScript, C#Script, JScript) qui effectue des actions sur l'application à tester. Les scripts sont plus flexibles et puissants que les tests de mots clés, mais ils nécessitent des compétences en programmation.



## Les tests auxiliaires
### Procédures bas niveau (Low-Level Procedure)
Une **Low-Level Procedure** est une suite d'instructions qui effectue des actions sur l'application à tester. Elles sont utilisées pour effectuer des actions spécifiques qui ne peuvent pas être réalisées avec les tests de mots clés ou les scripts. Les Low-Level Procedures sont généralement utilisées pour effectuer des actions sur des objets d'interface utilisateur qui ne sont pas pris en charge par TestComplete.

### Test unitaires
=> [[Test unitaire]]

# Comment créer un test avec TestComplete
Nous retrouvons deux moyens de créer un test avec TestComplete :
- Enregistrement de l'application
- Écriture de scripts

## Enregistrement de l'application
C'est la méthode la plus simple et la plus rapide pour écrire un test. Pour cela, il suffit de lancer l'application à tester et de cliquer sur le bouton "Enregistrer" dans TestComplete. Ensuite, il faut effectuer les actions que l'on souhaite tester dans l'application. TestComplete va enregistrer ces actions et les convertir en un test automatisé. Il est possible de modifier le test enregistré pour ajouter des assertions ou des vérifications supplémentaires.

### Barre d'enregistrement
Bien sûr ! Voici une explication complète et structurée de toutes les fonctionnalités de la **Recording Toolbar** de TestComplete, en français et en phrases simples :

---

## La barre d’outils d’enregistrement (Recording Toolbar) dans TestComplete

Lorsque vous commencez à enregistrer un test avec TestComplete, une barre d’outils spéciale s’affiche à l’écran. Elle disparaît automatiquement quand l’enregistrement s’arrête. Cette barre vous permet de contrôler l’enregistrement et d’ajouter des actions ou des vérifications à votre test.

### Les boutons principaux de la barre d’outils

- **Record**  
Ce bouton clignote pour montrer que l’enregistrement est en cours. Si vous mettez l’enregistrement en pause, ce bouton permet de le reprendre.

- **Pause**  
Ce bouton met l’enregistrement en pause. Pour continuer, il suffit de cliquer à nouveau sur Record.

- **Stop**  
Ce bouton arrête complètement l’enregistrement.

- **Next Step**  
Ce bouton n’apparaît que si vous enregistrez des étapes de test BDD (Behavior Driven Development). Il permet d’arrêter l’enregistrement du code pour l’étape actuelle et de commencer à enregistrer l’étape suivante qui n’a pas encore de commandes de test.

- **Add Check**  
Ce bouton met l’enregistrement en pause pour ajouter un checkpoint (vérification). Un assistant s’ouvre pour vous aider à choisir le type de checkpoint et à définir ses propriétés. Une fois terminé, TestComplete ajoute automatiquement cette vérification à votre test.

### Les boutons pour lancer des applications

- **Run App**  
Ce bouton permet de lancer une ou plusieurs applications à tester. Vous pouvez choisir l’application dans une liste ou lancer toutes les applications définies dans le projet. Cette action est enregistrée dans le test.

- **Virtual Browser**  
Ce bouton lance un émulateur de navigateur mobile. Vous pouvez choisir le navigateur à émuler. Cette action est aussi enregistrée dans le test. Pour utiliser cette fonction, il faut que Google Chrome soit installé sur votre ordinateur.

### Les boutons pour enrichir le test

- **Add Comment**  
Ce bouton ouvre une fenêtre pour ajouter un commentaire dans le test enregistré. Cela permet d’expliquer certaines étapes ou de donner des indications.

- **Test Type**  
Ce bouton permet de choisir le type de test à enregistrer :
  - Test de mots-clés (Keyword Test)
  - Script
  - Procédure bas niveau (en coordonnées d’écran ou de fenêtre)

- **Custom Action**  
Ce bouton met l’enregistrement en pause et exécute une action personnalisée, comme un checkpoint presse-papiers ou un checkpoint manuel. Ces actions sont ajoutées par des extensions de script.

- **Parent and Object**  
Ce bouton affiche des informations sur l’objet actuellement sous la souris et sur son parent. Cela aide à mieux comprendre la structure de l’interface testée.

### Les options supplémentaires

- **Expand** : Ce bouton permet d’afficher tous les boutons disponibles sur la barre d’outils.
- **Enable Quick Checkpoints** : Ce bouton active ou désactive la création rapide de checkpoints pendant l’enregistrement.
- **Other Options** : Ce bouton ouvre la fenêtre des options d’enregistrement, où vous pouvez configurer tous les paramètres qui influencent l’enregistrement.

## Écriture de scripts
L'écriture de scripts est la méthode la plus puissante et la plus flexible pour écrire des tests. Pour cela, il faut créer un nouveau projet dans TestComplete et écrire le code du test dans le langage de programmation de son choix (Python, VBScript, C#Script, JScript). Il est possible d'utiliser les fonctions et les méthodes de TestComplete pour interagir avec l'application à tester et effectuer des vérifications.

# Plannifier les tests
Pour pouvoir créer efficacement un test automatisé avec TestComplete, il faut :
- **Identifer l'objectif du test** :  Identifier précisément les fonctionnalités à tester. Il faut privilégier des objectifs simples et claires. Une fois que plusieurs tests simple sont crées, on peut les organiser en tests plus complexes.
- **Définir les étapes du test** : Déterminer les actions que doit effectuer le test (Ouverture de l'application, saisie ...). Structurer de manière séquentielle pour garantir la reproductibilité.
- **Planifier les vérifications (checkpoints)** : Choisir les critères de réussite du test. Identifier les changements visuels ou de données à contrôler. Ajouter des points de contrôle (checkpoints) adaptés.
- **Prévoir la consignation du test** : Consigner toutes les actions dans un journal de test. Ajouter des messages ou des images si nécessaire. Exporter, partager ou archiver les résultats. Créer un rapport de bug depuis le journal si besoin.

