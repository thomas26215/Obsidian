# 📊 Analyse d'entraînement

Index des features d'analyse automatisée des entraînements.

## Features principales

- [[Analyse IA d'un programme]] — Analyse basique (global score, équilibre, volume)
- [[🎯 Radar Chart Musculaire]] — Visualisation de la couverture musculaire
- [[📊 Analyse Comparative]] — Comparer à un template de référence
- [[📈 Historique des Analyses]] — Suivi de la progression dans le temps
- [[🗓️ Analyse Cross-Semaine]] — Analyse du split global hebdomadaire
- [[😴 Fatigue Estimée]] — Estimation de récupération par muscle

## Flux d'analyse complet

```
Utilisateur → Analyse basique (Radar + Score)
         ↓
    Points faibles détectés
         ↓
    Historique des analyses (suivi dans le temps)
         ↓
    Analyse comparative (vs templates)
         ↓
    Analyse cross-semaine (équilibre global)
         ↓
    Fatigue estimée (récupération par muscle)
```

## Données stockées
Firestore : `users/{uid}/programs/{programId}/analyses/`

## Lié à
- [[💬 Système de Prompts]] — Questions avancées en-dessous des analyses
- [[Analyse IA d'un programme]] — Concept principal
