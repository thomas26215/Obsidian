# 🧠 Features IA — Vue d'ensemble

Index central pour toutes les features d'analyse IA de LiftConnect.

## 📊 Analyse d'entraînement
Analyses automatisées pour évaluer la qualité des programmes et séances.

→ [[📊 Analyse d'entraînement/INDEX|Accéder au dossier Analyse d'entraînement]]

**Features :**
- Radar Chart Musculaire
- Analyse Comparative
- Historique des Analyses
- Analyse Cross-Semaine
- Fatigue Estimée

---

## 💬 Système de Prompts
Questions personnalisées à l'IA avec contexte riche et préprompts.

→ [[💬 Système de Prompts/INDEX|Accéder au dossier Système de Prompts]]

**Features :**
- Prompts IA Avancés (préprompts + libre combinés)
- Mécanisme de fonctionnement

---

## 💰 Système de crédits IA
Monétisation par crédits avec abonnements flexibles et accumulation bonus.

→ [[💰 Système de crédits/INDEX|Accéder au dossier Système de crédits]]

**Architecture :**
- [[💰 Système de crédits/📋 Abonnements & Pricing|📋 Abonnements & Pricing]] (6 abonnements, 0,99€-5€/mois)
- [[💰 Système de crédits/🔧 Modèle de crédits|🔧 Modèle de crédits]] (tokens = consommation réelle)
- [[💰 Système de crédits/💳 Accumulation & Auto-achat|💳 Accumulation & Auto-achat]] (bonus persistants)
- [[💰 Système de crédits/📊 Dashboard utilisateur|📊 Dashboard utilisateur]] (UI de gestion)

**Préprompts inclus :**
- [[💰 Système de crédits/💬 Préprompt Analyse|💬 Analyse séances]]
- [[💰 Système de crédits/🔄 Préprompt Substitution|🔄 Substitution d'exos]]
- [[💰 Système de crédits/🎯 Préprompt Objectifs adaptatifs|🎯 Objectifs adaptatifs]]
- [[💰 Système de crédits/📝 Préprompt Feedback post-séance|📝 Feedback post-séance]]
- [[💰 Système de crédits/💬 Préprompt Conseils live|💬 Conseils live]]
- [[💰 Système de crédits/🤖 Préprompt Génération|🤖 Génération de programmes]]

---

## 🔄 Flux complet utilisateur

```
1. Utilisateur lance l'app
   ↓
2. Voit une Analyse basique (Radar + Score global)
   ↓
3. Peut creuser plus profond :
   ├─ Historique (voir progression dans le temps)
   ├─ Comparative (vs template de référence)
   ├─ Cross-semaine (équilibre global du split)
   └─ Prompts avancés (questions personnalisées)
   ↓
4. Chaque résultat peut être sauvegardé
```

---

## 📈 Roadmap par priorité

### Phase 1 : Core features IA
1. **Radar Chart + Analyse de base** (quick win, impact visuel)
2. **Historique des analyses** (infrastructure Firestore simple)

### Phase 2 : Monétisation + Features avancées
3. **Système de crédits** (backend + dashboard)
4. **Préprompts + Crédits transversaux** (Analyse, Feedback, Substitution, etc.)
5. **Génération de programmes** (premium feature)

### Phase 3 : Advanced analytics
6. **Analyse comparative** (besoin des templates d'abord)
7. **Analyse cross-semaine + Fatigue** (avancé, après les bases)

---

## 🔗 Liens utiles
- [[../../🚀 Vue d'ensemble LiftConnect|Retour à la vue d'ensemble globale]]
- [[Analyse IA d'un programme]] — Concept de base partagée
- [[Architecture Firebase]] — Stockage des données
