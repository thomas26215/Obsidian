# Trame oral de stage — Éditeur de configuration Modbus pour PixL Expert

> Format visé : ~15-20 min de présentation + questions
> Minutages indicatifs à ajuster selon le temps imposé
> Voir le [[Rapport de stage]] pour le détail de chaque point
> 🖼️ = éléments visuels à mettre sur la slide

---

## Slide 1 — Page de titre *(~30 s)*
- Titre : *Développement d'un outil d'édition des paramètres Modbus dans l'interface web PixL Expert*
- Nom, formation, dates du stage (fin mars → fin juin 2026)
- APIX Analytics — tutrice : Élodie Baral-Baron
- 🖼️ **Logo APIX** en grand + éventuellement photo d'un analyseur CHROMPIX/GREENPIX en fond ou en coin
- 🖼️ Logo de l'école/formation

## Slide 2 — Plan *(~30 s)*
Annoncer les 4 temps : l'entreprise → le besoin → la réalisation → bilan.
- 🖼️ **Sommaire visuel** : 4 blocs/icônes numérotés (entreprise 🏢 / besoin ❓ / réalisation 🛠️ / bilan ✅)

---

## 1. Présentation de l'entreprise et du contexte *(~2-3 min)*

### Slide 3 — APIX Analytics
- PME grenobloise, < 5 personnes en dev → polyvalence, organisation agile
- Métier : analyseurs de gaz chromatographiques industriels (CHROMPIX / GREENPIX)
- En une phrase : à quoi sert la chromatographie en phase gazeuse (analyse de la composition du gaz naturel → enjeu de facturation, sécurité, conformité)
- Logiciel **+** matériel développés en interne → forte intégration
- 🖼️ **Photo d'un analyseur APIX** (produit physique)
- 🖼️ **Carte/pin de Grenoble** ou photo des locaux (optionnel)
- 🖼️ Petit **schéma chromatographie** : mélange gazeux → colonne → composants séparés → concentrations (très simplifié)

### Slide 4 — La PixL Suite
- **PixL Expert** (Vue.js) qui remplace l'ancienne interface full Django → périmètre du stage
- 🖼️ **Schéma d'architecture** : PC embarqué (cadre) contenant des conteneurs Docker → orchestrateur / PixL API / module Modbus / interfaces web + base PostgreSQL
- 🖼️ Mettre en surbrillance/encadrer **PixL Expert** pour montrer où se situe le travail réalisé

---

## 2. Le besoin et les objectifs *(~2-3 min)*

### Slide 5 — La problématique
- Avant : configuration Modbus éditée **à la main** dans `network.json` et `protocol.json`
- Deux problèmes : **risque d'erreurs** (silencieuses) + **perte de temps** (centaines de registres imbriqués)
- 🖼️ **Capture d'un extrait brut de `protocol.json`** (volumineux, imbriqué) → effet « illisible » qui justifie le projet
- 🖼️ Deux **icônes/pictos** : ⚠️ risque d'erreur + ⏱️ perte de temps

### Slide 6 — Objectifs du stage
- Concevoir une interface d'édition intégrée à PixL Expert (visualiser / modifier / sauvegarder)
- Travail **full-stack** : backend Python (routes API) + frontend Vue.js
- Projet **itératif, sans cahier des charges formel** → point de méthode à souligner
- 🖼️ **Schéma avant → après** : JSON brut à gauche → interface graphique à droite (flèche entre les deux)

---

## 3. Réalisation *(~7-9 min — le cœur de l'oral)*

### Slide 7 — Le protocole Modbus (le socle)
- Modèle maître/esclave, notion de registres (holding / input)
- Formats de données et facteur de conversion (un `float32` = 2 registres) → cette règle reviendra dans la validation
- 🖼️ **Schéma maître/esclave** : SCADA/automate (maître) ⇄ analyseur APIX (esclave), flèche requête/réponse
- 🖼️ **Schéma des registres** : cases mémoire numérotées avec adresses, montrer un `float32` qui occupe 2 cases (N et N+1)

### Slide 8 — Stack technique & organisation
- Backend : Python / Django / DRF — 3 dépôts (Apix Tools, PixL Api, PixL Console)
- Frontend : Vue.js 3, Pinia, Axios, AG Grid
- Git/GitLab + CI/CD, réunion hebdo du lundi, méthode agile
- 🖼️ **Logos** des technologies organisés en 2 colonnes (backend / frontend)

### Slide 9 — Architecture backend : ModelMother
- Le problème : sérialiser / désérialiser objets Python ↔ JSON
- Mécanisme commun récursif (éviter que chacun réécrive la logique)
- Contribution liée : la limite « dictionnaire de dictionnaires » → `ModelDictToListMother`
- 🖼️ **Schéma de sérialisation** : objet Python ⇄ JSON avec les 2 flèches (`get_attributes_as_dict` / `set_attributes_from_dict`)
- 🖼️ **Arbre de la hiérarchie des classes** (version simplifiée de celui du rapport : ModelMother → NetworkParameters / ProtocolParameters)
- 🖼️ **Schéma dict ⇄ list** : `{"CAL-C2H4": {...}}` → objet avec `name = "CAL-C2H4"`

### Slide 10 — Éditeur `network.json` (ModbusPart.vue)
- Routes GET/POST + validations (ports, timeout, énumérations)
- Idée réutilisable : **route générique d'énumérations** `/settings/enums/<enum_name>/` (importlib)
- Gestion des ports série en onglets dynamiques
- 🖼️ **Capture d'écran de ModbusPart.vue** (le formulaire réseau avec les onglets de ports série)

### Slide 11 — Éditeur `protocol.json` (RegisterMapPart.vue) *(le plus complexe — insister)*
- Structure hiérarchique → liste plate pour l'affichage
- **Configuration-driven UI** : route `/protocol/formats` qui décrit l'interface elle-même
- Tableau **AG Grid** avec drag & drop
- **Détection de conflits d'adresses** (calcul des plages occupées)
- 🖼️ **Capture du tableau AG Grid** (colonnes Register / Address / Source / Name / Format / Factor)
- 🖼️ **Capture de la fenêtre modale** d'ajout/édition (formulaire dynamique selon la sous-section)

### Slide 12 — Démo / captures d'écran
- 🖼️ **Capture avant/après** ou GIF court du drag & drop pour réordonner les registres

### Slide 13 — Tests & mise en production
- Tests manuels : cas nominaux + cas limites, vérification du JSON généré
- Déploiement : serveur Linux/Debian, SSH/MobaXTerm, Docker Compose, `.env`
- **1 difficulté marquante** : bug `ModuleNotFoundError` dû à `APIX_TOOLS_VERSION` non synchronisé dans `.env` → leçon « en production, le silence ≠ succès »
- 🖼️ **Schéma du flux de déploiement** : poste Windows → SCP/SSH → serveur Linux → conteneurs Docker



- 🖼️ **Capture du terminal MobaXTerm** (logs `docker ps -a` ou l'erreur `ModuleNotFoundError`)

---

## 4. Bilan *(~2 min)*

### Slide 14 — Résultats
- Outil fonctionnel en production : fini l'édition JSON à la main, fiabilisation + gain de temps
- Composants livrés : ModbusPart.vue, RegisterMapPart.vue, routes API, contribution au framework
- 🖼️ **Capture finale de l'interface en fonctionnement** (la plus aboutie)
- 🖼️ Petit **récapitulatif visuel** des livrables (2-3 icônes : frontend / backend / framework)

### Slide 15 — Apports personnels
- Techniques : full-stack Python/Vue, Modbus, Docker, déploiement, codebase existante
- Humains/méthode : autonomie encadrée, méthode agile, rigueur de la production
- 🖼️ **Deux colonnes** « compétences techniques » / « compétences humaines » avec pictos

### Slide 16 — Conclusion & ouverture
- Ce que le stage a confirmé sur le projet professionnel
- Évolutions possibles de l'outil
- 🖼️ Visuel sobre (pas surchargé) : une **phrase forte** + éventuellement une flèche « vers la suite »

### Slide 17 — Remerciements / Questions
- 🖼️ **Logo APIX** + « Merci de votre attention »
- 🖼️ **Coordonnées** (mail) en pied de slide

---

## Conseils de présentation
- **Garder l'équilibre** : ne pas passer 10 min sur l'entreprise. Le jury attend surtout **la réalisation** → parties 3 et 4.
- **Privilégier les visuels au texte** : sur chaque slide, une image/schéma vaut mieux qu'un paragraphe. Commenter à l'oral pendant que la slide illustre.
- **Préparer LA démo ou capture** du conflit d'adresses et de l'éditeur protocole : résultat le plus visuel.
- **Anticiper les questions** : pourquoi AG Grid ? pourquoi une liste plate plutôt que l'arbre ? différence holding/input register ? comment valider sans cahier des charges ?
- Viser **~1 min par slide** ; les slides 11 et 13 méritent un peu plus.

