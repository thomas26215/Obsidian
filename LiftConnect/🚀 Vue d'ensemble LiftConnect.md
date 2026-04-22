# 🚀 LiftConnect — Vue d'ensemble du Projet

Documentation complète du projet LiftConnect avec toutes les features et APIs.

## 📁 Dossiers du projet

### 🔌 APIs
L'infrastructure pour ouvrir LiftConnect à des intégrations tierces.

- [[🗺️ Vue d'ensemble API]] — Architecture générale
- [[Authentification API]] — Système d'API Keys et scopes
- [[API Exercices]] — Base de données d'exercices (read-only public)
- [[API Programmes]] — Gestion des programmes d'entraînement
- [[API Stats & Progression]] — Statistiques et progression utilisateur
- [[API Groupes]] — Gestion des groupes et membres

**Roadmap API :**
1. API Exercices (quick win)
2. API Groupes (valeur B2B)
3. API Stats
4. API Programmes

---

### 🧠 Features IA
Analyse intelligente des programmes d'entraînement pour optimiser les workouts.

#### 📊 [[Features IA/📊 Analyse d'entraînement/INDEX|Analyse d'entraînement]]
Analyses automatisées des programmes et séances.

- [[Features IA/📊 Analyse d'entraînement/🎯 Radar Chart Musculaire|🎯 Radar Chart Musculaire]] — Visualisation couverture musculaire
- [[Features IA/📊 Analyse d'entraînement/📊 Analyse Comparative|📊 Analyse Comparative]] — Comparer à template
- [[Features IA/📊 Analyse d'entraînement/📈 Historique des Analyses|📈 Historique des Analyses]] — Suivi progression
- [[Features IA/📊 Analyse d'entraînement/🗓️ Analyse Cross-Semaine|🗓️ Analyse Cross-Semaine]] — Split global
- [[Features IA/📊 Analyse d'entraînement/😴 Fatigue Estimée|😴 Fatigue Estimée]] — Récupération par muscle

#### 💬 [[Features IA/💬 Système de Prompts/INDEX|Système de Prompts]]
Questions personnalisées + préprompts avec contexte injectable.

- [[Features IA/💬 Système de Prompts/💬 Prompts IA Avancés|💬 Prompts IA Avancés]] — Préprompts + texte libre combinés
- [[Features IA/💬 Système de Prompts/🔧 Mécanisme - Préprompts combinés|🔧 Mécanisme]] — Comment ça marche

**Roadmap Features IA :**
1. Radar Chart + Analyse basique (impact visuel fort)
2. Historique des analyses (infrastructure simple)
3. Prompts IA avancés (puissant + flexible)
4. Analyse comparative (templates de référence)
5. Analyse cross-semaine + Fatigue (features avancées)

---

## 🔗 Ressources liées
- [[Architecture Firebase]] — Structure Firestore et authentification
- [[Mise en place d'un endroit personnel pour stocker sessions et exercices]] — Stockage local Flutter
- [[CRUD avec symfony]] — Backend existant (si applicable)

---

## 📝 Notes de travail
- Toutes les notes utilisent les `[[wikilinks]]` pour la navigation
- Utiliser la **Graph View** d'Obsidian pour voir le réseau complet
- Chaque feature/API a un statut (`🟢 Fait`, `🟡 À faire`, `🔴 Bloqué`, `⏸️ En attente`)

---

*Dernière mise à jour : 21 avril 2026*
