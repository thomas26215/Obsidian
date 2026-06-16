# Texte oral de stage — Éditeur de configuration Modbus pour PixL Expert

> Texte à dire slide par slide. Les passages entre *[crochets]* sont des rappels de timing ou de geste.
> Durée visée : 15-20 minutes.
> Principe : du général au particulier — on pose le contexte avant d'entrer dans le sujet.

---

## Slide 1 — Page de titre *(~30 s)*

Bonjour à tous. Je m'appelle Thomas Venouil, je suis en dernière année de BUT Informatique, et j'ai effectué mon stage de fin d'année chez **APIX Analytics**, à Grenoble, de fin mars à fin juin 2026.

Je vais vous présenter le travail que j'y ai réalisé pendant ces trois mois.

---

## Slide 2 — Plan *(~30 s)*

Ma présentation s'organise en quatre parties.

Je commencerai par vous présenter l'entreprise et son contexte. J'expliquerai ensuite le besoin auquel mon stage devait répondre. Je détaillerai la réalisation technique, qui est le cœur de cet exposé. Et je terminerai par un bilan de ce que cette expérience m'a apporté.

---

## 1. Présentation de l'entreprise et du contexte

### Slide 3 — APIX Analytics *(~1 min)*

APIX Analytics est une PME basée à Grenoble, spécialisée dans l'instrumentation industrielle pour l'analyse de gaz.

Ce qui distingue APIX, c'est que l'entreprise développe **à la fois le matériel et le logiciel** en interne. De l'électronique embarquée jusqu'à l'interface web, tout est conçu et maintenu par les mêmes équipes. C'est ce qui leur permet d'avoir une maîtrise complète de leur produit.

### Slide 4 — Le produit : les analyseurs de gaz *(~1 min)*

Le produit phare d'APIX, ce sont les analyseurs de gaz industriels CHROMPIX et GREENPIX. Ce sont des équipements physiques déployés sur le terrain — dans des usines, des réseaux de distribution de gaz, des sites industriels.

*[pointer la photo de l'analyseur]*

Leur rôle est de mesurer précisément la composition d'un gaz : savoir quelle quantité de méthane, d'éthane ou de propane est présente dans un mélange. C'est ce qu'on appelle la **chromatographie en phase gazeuse** — on injecte le gaz dans une colonne et on analyse comment ses composants se séparent.

Ces mesures servent à des enjeux très concrets : la **facturation** de l'énergie, la **sécurité** des installations, et la **conformité réglementaire**. Ce sont des valeurs critiques — une erreur de mesure peut avoir des conséquences directes sur la sécurité ou la facturation d'un réseau entier.

### Slide 5 — La PixL Suite *(~1 min)*

Le logiciel qui pilote ces analyseurs s'appelle la **PixL Suite**. C'est un ensemble de composants qui tournent tous sur un PC embarqué à l'intérieur de l'analyseur, dans des conteneurs Docker.

*[pointer le schéma d'architecture]*

Sans rentrer dans tous les détails, on peut retenir quatre briques principales. **PixL Core** est le chef d'orchestre : il pilote les cartes électroniques et traite les données brutes. **PixL API** est une API REST qui sécurise l'accès à la base de données. **PixL Modbus** gère la communication avec les systèmes industriels externes — j'y reviendrai. Et **PixL Expert** est la nouvelle interface web, développée en Vue.js, qui permet de configurer et surveiller l'analyseur depuis un navigateur.

*[encadrer PixL Expert]*

C'est dans PixL Expert que se situe mon travail. Cette interface est en cours de développement — elle remplace progressivement une ancienne interface écrite en Django — et mon stage a contribué directement à cette migration.

---

## 2. Le besoin et les objectifs

### Slide 6 — La problématique *(~1 min)*

L'analyseur APIX peut être connecté à des systèmes de supervision industriels — automates, SCADA     — via le protocole Modbus. Pour que cette communication fonctionne, il faut configurer précisément quelles données sont exposées, à quelle adresse, et dans quel format.

Avant mon stage, cette configuration se faisait **à la main**, en éditant directement des fichiers JSON.

*[montrer la capture du JSON brut]*

Et c'est là que le problème apparaît. Ces fichiers peuvent contenir des centaines de registres imbriqués sur plusieurs niveaux. Ils sont **illisibles** à l'œil nu et **très longs** à modifier. Pire encore : une erreur de saisie — une mauvaise adresse, un format incorrect — ne génère aucun message d'erreur. Le fichier reste valide, mais le comportement de l'analyseur devient imprévisible. C'est ce qu'on appelle une erreur **silencieuse**, et c'est le pire type d'erreur qu'on puisse avoir en production.

### Slide 7 — Objectifs du stage *(~1 min)*

Mon objectif était donc de concevoir et développer une **interface graphique** intégrée à PixL Expert, qui permette de configurer Modbus sans jamais toucher au JSON — de façon sécurisée et accessible.

Concrètement : visualiser la configuration existante, la modifier, la valider, et la sauvegarder depuis l'interface web.

C'était un projet **full-stack** : j'ai travaillé à la fois sur le backend Python et sur le frontend Vue.js.

Côté méthode, il n'y avait pas de cahier des charges formel. Les fonctionnalités se définissaient de façon itérative, au fil des réunions hebdomadaires du lundi. Ça m'a appris à cadrer moi-même le périmètre de chaque itération et à valider chaque livraison avant de passer à la suite.

---

## 3. Réalisation

### Slide 8 — Éditeur réseau : ModbusPart.vue *(~1 min)*

Le premier éditeur permet de configurer les **paramètres réseau** de Modbus : adresses IP, ports, paramètres des liaisons série.

*[montrer la capture de ModbusPart.vue]*

La partie la plus délicate côté frontend était la gestion des **ports série en onglets dynamiques** : l'utilisateur peut avoir plusieurs ports configurés, chacun dans son propre onglet, créés et supprimés à la volée.

### Slide 9 — Éditeur protocole : RegisterMapPart.vue *(~2 min)*

C'est la partie la plus complexe — et la plus centrale — de mon stage.

*[montrer la capture du tableau AG Grid]*

La carte des registres est affichée sous forme de tableau interactif, avec du **drag & drop** pour réordonner les entrées. L'ajout et la modification se font via une fenêtre modale dont le formulaire s'adapte dynamiquement selon le type de registre concerné.

*[montrer la capture de la modale]*

J'ai également implémenté une **détection de conflits d'adresses** : certains types de données comme le `float32` occupent deux registres consécutifs. Si deux registres se retrouvent sur les mêmes adresses, le comportement de l'analyseur devient imprévisible. L'interface calcule donc les plages occupées et signale tout chevauchement avant la sauvegarde.

### Slide 10 — Architecture backend : ModelMother *(~1 min)*

Maintenant que vous avez vu l'interface, voici ce qui se passe côté backend.

Le backend repose sur un framework interne appelé **ModelMother**, qui gère la conversion entre les objets Python et les fichiers JSON de configuration — dans les deux sens. C'est ce mécanisme qui permet de lire la configuration existante, de la modifier via l'interface, et de la sauvegarder de façon fiable.

J'y ai contribué en ajoutant un mécanisme manquant pour gérer un cas particulier de structure de données, contribution réutilisable dans toute la suite logicielle.

*[pointer le schéma si présent sur la slide]*

### Slide 11 — Démo *(~30 s)*

*[montrer la capture ou le GIF]*

Voici le résultat concret : le tableau des registres avec le drag & drop, et la modale d'édition. À gauche, ce qu'il fallait éditer à la main avant ; à droite, l'interface que j'ai développée.

### Slide 12 — Tests et mise en production *(~1 min 30)*

Pour le déploiement, le processus consistait à transférer les fichiers par SCP vers un serveur Linux distant, puis à relancer les conteneurs Docker.

*[pointer le schéma ou la capture MobaXTerm]*

C'est là que j'ai rencontré ma difficulté la plus marquante. Après un déploiement qui semblait s'être bien passé, l'application refusait de démarrer avec une erreur `ModuleNotFoundError`. Après investigation, la cause était une variable `APIX_TOOLS_VERSION` dans le fichier `.env` qui n'avait pas été mise à jour et pointait vers une version inexistante. Le conteneur démarrait sans se plaindre — mais importait silencieusement une mauvaise version du module.

Ce bug m'a appris une leçon concrète : **en production, l'absence d'erreur n'est pas une garantie de succès.** Il faut toujours vérifier activement que ce qui tourne est bien ce qu'on a déployé.

---

## 4. Bilan

### Slide 13 — Résultats *(~45 s)*

L'outil est aujourd'hui **fonctionnel en production**. La configuration Modbus ne se fait plus à la main : elle passe par l'interface graphique, ce qui supprime le risque d'erreurs silencieuses et réduit le temps de configuration.

Les livrables sont : le composant ModbusPart.vue, le composant RegisterMapPart.vue, les routes API associées, et la contribution au framework ModelMother.

### Slide 14 — Apports personnels *(~45 s)*

Sur le plan technique, ce stage m'a permis de travailler sur une stack full-stack réelle — Python, Vue.js, Docker, déploiement Linux — et de découvrir un protocole industriel que je ne connaissais pas. J'ai aussi appris à me repérer dans une **base de code existante et conséquente**, ce qui est une compétence à part entière.

Sur le plan humain, j'ai développé mon autonomie : avancer sans qu'on me dicte chaque étape, savoir quand chercher seul et quand solliciter de l'aide. La méthode agile m'a aussi appris à communiquer régulièrement sur l'avancement, même quand le travail n'est pas encore terminé.

### Slide 15 — Conclusion et ouverture *(~30 s)*

Ce stage m'a confirmé que le développement full-stack en contexte industriel m'intéresse : la contrainte de production, la rigueur qu'elle impose, et la satisfaction d'un outil réellement utilisé.

En termes d'évolution, l'outil pourrait être étendu pour couvrir d'autres parties de la configuration de PixL Expert, ou enrichi d'une validation temps réel plus poussée.

### Slide 16 — Remerciements *(~15 s)*

Merci de votre attention. Je suis disponible pour répondre à vos questions.

---

## Questions probables à préparer

**Pourquoi AG Grid et pas une solution maison ?**
AG Grid est une bibliothèque éprouvée qui offre nativement le drag & drop, la gestion de grandes listes, et les colonnes configurables. Développer ces fonctionnalités from scratch aurait pris beaucoup de temps pour un résultat moins robuste.

**Pourquoi une liste plate plutôt que l'arbre directement ?**
Un tableau est le format le plus lisible et le plus manipulable pour l'utilisateur final. L'arbre reste en mémoire côté backend — le frontend travaille sur la représentation plate, et la conversion se fait à la sauvegarde.

**Quelle est la différence entre Holding Register et Input Register ?**
Les Input Registers sont en lecture seule et contiennent les mesures de l'analyseur. Les Holding Registers sont en lecture/écriture et permettent d'envoyer des commandes. Dans mon éditeur, les deux types sont configurables mais avec des champs différents.

**Comment valider un projet sans cahier des charges ?**
En procédant par itérations courtes, en définissant chaque semaine ce qui doit être livré et validé, et en impliquant régulièrement la tutrice pour confirmer que le résultat correspond au besoin réel.
