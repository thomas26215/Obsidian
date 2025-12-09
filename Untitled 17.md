# **Compte rendu de la réunion du mardi 9 décembre 20…**

_(De 8h00 à 10h00)_

**Ordre du jour :** Comment éviter de reproduire une suppression de base de données ?  
_(Rappel du thème : identifier les solutions techniques et organisationnelles pour éviter la suppression involontaire d’une BDD.)_

---

## **Étaient présents :**

M.Mathias – M.Valentin – M.Maxime – M.Mathis – M.Adam – M.Corentin _(doublon dans les notes)_

## **Étaient absents :**

Aucun absent signalé.

---

Après un bref tour de table, la séance débute officiellement à **8h12**.

---

# **I – Analyse des solutions techniques concernant la BDD**

La réunion s’ouvre par une présentation des premières pistes pour renforcer la sécurité de la base de données.  
L’équipe étudie d’abord **Ruteck**, une bibliothèque Python permettant d’encadrer les opérations sensibles et d’automatiser certains contrôles. L’intérêt principal réside dans sa capacité à limiter les manipulations dangereuses et à structurer davantage les interactions avec la BDD.

Vient ensuite l’idée d’ajouter des **triggers**, destinés à bloquer ou vérifier certaines requêtes critiques. Ces mécanismes permettraient de prévenir directement toute suppression accidentelle de données.

La question des **backups** est abordée : une commande dédiée permettrait d’automatiser les sauvegardes, mais le choix des serveurs externes reste à définir. L’équipe évoque aussi brièvement le **PCA** (Plan de Continuité d’Activité) qui pourrait compléter les dispositifs de sécurité.

Il est souligné que des **tests unitaires et d’intégration** devront être mis en place afin de vérifier systématiquement que les développements backend ne provoquent pas de suppressions non souhaitées. À **8h17**, M.Noah propose de s’inspirer des **normes ISO**, notamment pour encadrer les bonnes pratiques.

<div style="page-break-before: always;"></div>


# **II – Réflexions sur l’interface et la sécurité applicative**

À partir de 8h19, la discussion se déplace sur le Frontend. M.Mathis estime dans un premier temps qu’aucune action particulière n’est nécessaire de ce côté-là. M.Adam nuance cette position en expliquant qu’un utilisateur peut toujours commettre une erreur involontaire, ce qui justifie selon lui la mise en place de garde-fous comme une double confirmation lors des opérations sensibles. À 8h21, M.Mathias revient sur la nécessité de mieux configurer les rôles utilisateurs et de renforcer la protection contre les injections, ce qui contribuerait à sécuriser davantage l’application.

Peu après, M.Noah propose de mettre en place un système de logs pour suivre les actions importantes. M.Mathias exprime certaines réserves à ce sujet, estimant qu’un dashboard centralisé offrant une vision globale de l’activité serait plus utile qu’un simple historique de logs. À 8h24, M.Corentin insiste sur la séparation des environnements — test, production et éventuellement un environnement supplémentaire — afin de réduire les risques d’erreurs humaines. M.Adam propose ensuite un mode bac à sable permettant aux utilisateurs de s’entraîner sans danger. À 8h26, M.Valentin et M.Corentin échangent brièvement sur l’amélioration du système d’authentification.

---

# **III – Priorisation des actions et estimation des charges**

À partir de 8h28, la discussion s’oriente vers l’ordre de priorité des actions à mener. La mise en place d’un système de backup fiable est considérée comme la priorité principale. La confirmation de suppression, déjà en partie implémentée, pourrait selon M.Valentin être finalisée en une demi-journée seulement. À 8h29, M.Maxime précise qu’un fichier de sauvegarde existe déjà et qu’il faudrait environ deux jours pour le rendre pleinement opérationnel.

Vers 8h31, M.Valentin présente l’idée de mettre en place un serveur dédié à l’environnement de test, distinct de celui de la production. Il estime également cette tâche à environ deux jours de travail. M.Maxime ajoute que l’intégration de Ruteck ne représenterait pas une charge de travail importante tout en apportant une réelle valeur ajoutée. À 8h34, M.Valentin réaffirme l’intérêt d’un serveur de test séparé, et quelques minutes plus tard, à 8h35, l’ensemble de l’équipe semble s’accorder sur le fait que les différentes améliorations à mettre en place restent relativement rapides à réaliser.

<div style="page-break-before: always;"></div>


# **IV – Point sur le recrutement**

En fin de réunion, M.Noah interroge l’équipe sur l’état du recrutement. M.Mathias indique qu’aucun curriculum vitae n’a encore été reçu, mais confirme qu’un renfort serait utile compte tenu de la charge de travail actuelle.

---

### **Clôture de la réunion**

La séance est levée à **8h37**.  
La date de la prochaine réunion n’est pas encore fixée.

_(Date de rédaction du compte rendu : 9 Décembre 2025 / Rédacteur : Thomas Venouil)_